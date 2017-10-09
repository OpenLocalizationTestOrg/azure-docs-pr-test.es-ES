---
title: "arquitectura de hello aaaReview para tooa de sitio secundario con Azure Site Recovery para la replicación Hyper-V | Documentos de Microsoft"
description: "Este artículo proporciona información general sobre la arquitectura de hello para la replicación de máquinas virtuales de Hyper-V tooa secundaria System Center VMM sitio local con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Paso 1: Revisar la arquitectura de hello para el sitio secundario de tooa de replicación de Hyper-V

Este artículo describen los componentes de Hola y procesos que tienen lugar al replicar máquinas virtuales de Hyper-V (VM) en nubes de System Center Virtual Machine Manager (VMM), sitio VMM secundario tooa con hello local [Azure Site Recovery](site-recovery-overview.md)servicio Hola portal de Azure.

Registrar cualquier comentario a la parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componentes de la arquitectura

Aquí es lo que necesita para la replicación de máquinas virtuales de Hyper-V tooa sitio secundario de VMM.

**Componente** | **Ubicación** | **Detalles**
--- | --- | ---
**Las tablas de Azure** | Suscripción de Azure. | Cree un almacén de servicios de recuperación en hello suscripción de Azure, tooorchestrate y administrar la replicación entre ubicaciones de VMM.
**Servidor VMM** | Necesita una ubicación principal de VMM y otra secundaria. | Se recomienda un servidor VMM en el sitio primario de hello y otro en el sitio secundario de Hola 
**Servidor de Hyper-V** |  Uno o varios servidores Hyper-V host Hola principales y secundarias en nubes de VMM. | Datos se replican entre Hola principales y secundarios Hyper-V host servidores a través de LAN de Hola o VPN, con la autenticación Kerberos o certificados.  
**Máquinas virtuales de Hyper-V** | En el servidor de host de Hyper-V. | servidor de host de origen de Hello debe tener al menos una máquina virtual que desea tooreplicate.

## <a name="replication-process"></a>Proceso de replicación

1. Configurar la cuenta de Azure hello, cree un almacén de servicios de recuperación y especifique qué desea tooreplicate.
2. Configurar Hola origen y destino configuración de replicación, que incluye la instalación de hello Azure Site Recovery Provider en servidores VMM y el agente de servicios de recuperación de Microsoft Azure de hello en cada host de Hyper-V.
3. Crear una directiva de replicación para el origen de hello nube de VMM. Directiva de Hello es aplicado tooall máquinas virtuales ubicadas en hosts en la nube de Hola.
4. Habilitar la replicación para cada VMM y se produce la replicación inicial de una máquina virtual de acuerdo con la configuración de Hola que elija.
5. Después de la replicación inicial, empieza la de los cambios diferenciales. Las marcas de revisión de un elemento se conservan en un archivo .hrl.


![Local tooon-local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Proceso de conmutación por error y conmutación por recuperación

1. Puede ejecutar una [conmutación por error](site-recovery-failover.md), planeada o no, entre sitios locales. Si se ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan tooensure sin pérdida de datos.
2. Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md) tooorchestrate conmutación por error de varias máquinas.
4. Si lleva a cabo un sitio secundario de conmutación por error imprevista tooa, después de máquinas de conmutación por error de hello en la ubicación secundaria hello no están habilitadas para protección o la replicación. Si ha ejecutado una conmutación por error planeada, después de la conmutación por error de hello, máquinas en la ubicación secundaria Hola están protegidas.
5. A continuación, confirmar Hola conmutación por error toostart acceso a Hola cargas de trabajo de VM de réplica de Hola.
6. Cuando el sitio primario vuelve a estar disponible, iniciar la replicación inversa tooreplicate de toohello de sitio secundario de hello principal. La replicación inversa pone hello las máquinas virtuales en un estado protegido, pero Hola centro de datos secundaria sigue siendo ubicación activa Hola.
7. sitio primario de hello toomake en ubicación activa Hola de nuevo, que se inicie una conmutación por error planeada de tooprimary secundaria, seguido por otra replicación inversa.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 2: revisar los requisitos previos de Hola y limitaciones](vmm-to-vmm-walkthrough-prerequisites.md).
