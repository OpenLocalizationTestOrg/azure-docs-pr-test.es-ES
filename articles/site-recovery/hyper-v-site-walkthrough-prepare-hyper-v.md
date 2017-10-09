---
title: "hospeda aaaPrepare Hyper-V (sin System Center VMM) para la replicación tooAzure | Documentos de Microsoft"
description: "Describe cómo se hospeda tooprepare Hyper-V para tooAzure de replicación mediante Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Paso 6: Preparar los hosts de Hyper-V tooAzure de replicación

Use las instrucciones de hello en este artículo tooprepare toointeract de hosts de Hyper-V con Azure Site Recovery en local.

Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Preparar los hosts

- Asegúrese de que los hosts de Hyper-V de hello cumplen hello [requisitos previos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Asegúrese de que Hola hosts pueden obtener acceso a direcciones URL de hello necesario:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.
- Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).
- Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).

Durante la implementación de Site Recovery, agregar hosts de Hyper-V que contienen máquinas virtuales que desea que el sitio de Hyper-V tooa tooreplicate. Hola proveedor de Site Recovery y el agente de servicios de recuperación se instalan en cada host. sitio de Hello Hyper-V está registrado en hello que del almacén de servicios de recuperación.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 7: crear un almacén](hyper-v-site-walkthrough-create-vault.md)

