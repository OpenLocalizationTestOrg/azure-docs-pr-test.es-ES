---
title: "requisitos previos de hello aaaReview para la replicación de tooAzure de Hyper-V (sin System Center VMM) mediante Azure Site Recovery | Documentos de Microsoft"
description: "Describe los requisitos previos de Hola para configurar la replicación, la conmutación por error y la recuperación de tooAzure de máquinas virtuales de Hyper-V local con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Paso 2: Revisar los requisitos previos de hello para la replicación de Hyper-V (sin WMM) tooAzure

requisitos previos de Hola se resumen en la tabla de Hola.


**Requisito previo** | **Detalles** 
--- | --- 
**Las tablas de Azure** | Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidores locales** | [Obtener más información](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre los requisitos para hosts de Hyper-V de hello en local.
**Máquinas virtuales de Hyper-V locales** | Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Direcciones URL de Azure** | Hosts de Hyper-V necesitan tener acceso a direcciones URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.<br/></br> Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).<br/></br> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).



## <a name="next-steps"></a>Pasos siguientes

- Si está realizando una implementación completa, vaya demasiado[paso 3: planear la capacidad](hyper-v-site-walkthrough-capacity.md)
- Si está realizando una implementación de prueba simple, vaya demasiado[paso 4: planear las redes](hyper-v-site-walkthrough-network.md).
