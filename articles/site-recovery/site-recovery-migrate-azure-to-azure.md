---
title: "aaaMigrate las máquinas virtuales de IaaS de Azure entre regiones de Azure | Documentos de Microsoft"
description: "Use máquinas de virtuales de Azure Site Recovery toomigrate IaaS de Azure de tooanother de una región de Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Migración de máquinas virtuales de IaaS de Azure entre regiones de Azure con Azure Site Recovery
## <a name="overview"></a>Información general
Bienvenido tooAzure Site Recovery. Use este artículo si desea toomigrate máquinas virtuales de Azure entre regiones de Azure. Antes de comenzar, tenga en cuenta lo siguiente:

* Azure tiene dos modelos de implementación diferentes para crear y utilizar recursos: Azure Resource Manager y el portal clásico. Azure también tiene dos portales: Hola portal de Azure clásico que admite el modelo de implementación clásica de Hola y Hola portal de Azure con compatibilidad para dos modelos de implementación. pasos básicos de Hello para la migración son Hola mismo si va a configurar la recuperación del sitio en el Administrador de recursos o en clásico. Sin embargo Hola instrucciones de la interfaz de usuario y capturas de pantalla en este artículo son relevantes para hello portal de Azure.
* **Actualmente sólo se pueden migrar desde una región tooanother. Puede conmutar las máquinas virtuales de tooanother de una región de Azure, pero no puede realizar conmutación por recuperación ellos nuevo.**

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Requisitos previos
Requisitos para realizar esta implementación:

* **Máquinas virtuales de IaaS**: Hola máquinas virtuales que desee toomigrate. Migrará estas máquinas virtuales tratándolas como máquinas físicas.

## <a name="deployment-steps"></a>Pasos de implementación
Esta sección describen los pasos de implementación de hello en el nuevo portal de Azure Hola.

1. [Cree un almacén](site-recovery-vmware-to-azure.md).
2. [Habilite la replicación](site-recovery-vmware-to-azure.md). Habilitar la replicación de hello las máquinas virtuales que desee toomigrate y elija Azure como origen. 
3. [ Ejecute una conmutación por error no planeada](site-recovery-failover.md). Una vez completada la replicación inicial, puede ejecutar una conmutación por error no planeada desde tooanother de una región de Azure. Si lo desea, puede crear un plan de recuperación y ejecutar varias máquinas virtuales de un error no planeadas, toomigrate entre regiones. [Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre otros escenarios de replicación en [¿Qué es Site Recovery?](site-recovery-overview.md)
