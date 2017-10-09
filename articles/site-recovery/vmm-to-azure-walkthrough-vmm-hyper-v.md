---
title: "aaaPrepare System Center VMM para Hyper-V replicación tooAzure | Documentos de Microsoft"
description: "Describe cómo servidor de System Center VMM tooprepare para tooAzure de replicación de Hyper-V, con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Paso 6: Preparar servidores VMM y hosts de Hyper-V tooAzure de replicación de Hyper-V

Después de configurar [componentes de Azure](vmm-to-azure-walkthrough-prepare-azure.md) para la implementación de hello, use instrucciones de hello en este servidores VMM locales de artículo tooprepare y toointeract de hosts de Hyper-V con Azure Site Recovery.

Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Preparar los servidores VMM

- Necesita al menos un servidor VMM que cumplen los requisitos de compatibilidad de hello para la replicación de Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Asegúrese de que ha preparado el servidor VMM de Hola para [asignación de red](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Asegúrese de que ese servidor VMM Hola puede tener acceso a estas direcciones URL

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.
- Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).
- Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).

Durante la implementación de Site Recovery, también descarga Hola proveedor de Site Recovery e instalarlo en cada servidor VMM. servidor VMM de Hello está registrado en hello que del almacén de servicios de recuperación.




## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 7: crear un almacén](vmm-to-azure-walkthrough-create-vault.md)

