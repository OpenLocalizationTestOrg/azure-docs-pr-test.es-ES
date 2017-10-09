---
title: "requisitos previos de hello aaaReview para Hyper-V replicación tooa sitio VMM secundario con Azure Site Recovery | Documentos de Microsoft"
description: "Describe los requisitos previos de hello para la replicación de máquinas virtuales de Hyper-V tooa secundaria sitio de VMM con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Paso 2: Revisar los requisitos previos de Hola y limitaciones para el sitio VMM secundario de tooa de replicación de máquina virtual de Hyper-V


Una vez que haya revisado hello [arquitectura del escenario](vmm-to-vmm-walkthrough-architecture.md), lea este toomake artículo debe comprender los requisitos previos de implementación de hello, al replicar máquinas virtuales de Hyper-V local (máquinas virtuales) administrados en System Center Virtual Machine Manager (VMM) nubes tooa secundaria sitio mediante [Azure Site Recovery](site-recovery-overview.md) Hola portal de Azure.

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones

**Requisito** | **Detalles**
--- | ---
**Las tablas de Azure** | Una suscripción de [Microsoft Azure](http://azure.microsoft.com/).<br/><br/> Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [Más información](https://azure.microsoft.com/pricing/details/site-recovery/) sobre los precios de Site Recovery.<br/><br/> Busque regiones Hola admitida la recuperación del sitio, en disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
**Servidores VMM** | Se recomienda que tener dos servidores VMM, uno en el sitio primario de hello y otro en hello secundaria.<br/><br/> Se admite la replicación entre nubes en un único servidor VMM.<br/><br/> Servidores VMM se deben ejecutar al menos System Center 2012 SP1 con las últimas actualizaciones de Hola.<br/><br/> Los servidores VMM necesitan acceso a Internet.
**Nubes VMM** | Deben tener todos los servidores VMM en una o varias nubes y todas las nubes deben establecerse perfil de capacidad de Hyper-V de Hola. <br/><br/>Las nubes deben incluir uno o más grupos de hosts de VMM.<br/><br/> Si sólo tiene un servidor VMM, necesita al menos dos nubes, tooact como servidor principal y secundaria.
**Hyper-V** | Servidores de Hyper-V deben ejecutar al menos Windows Server 2012 con el rol de Hyper-V de Hola y Hola a las últimas actualizaciones instaladas.<br/><br/> Un servidor de Hyper-V debe contener una o varias máquinas virtuales.<br/><br/>  Servidores de host de Hyper-V deben estar en grupos host en nubes VMM principales y secundarias de Hola.<br/><br/> Si ejecuta Hyper-V en un clúster con Windows Server 2012 R2, instale la [actualización 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si ejecuta Hyper-V en un clúster con Windows Server 2012, el agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Configurar a un agente de clúster Hola manualmente. [Más información](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Los servidores de Hyper-V necesitan acceso a Internet.




## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 3: planear las redes](vmm-to-vmm-walkthrough-network.md).
