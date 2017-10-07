---
title: "aaaRun una conmutación por error de prueba para el sitio secundario tooa de máquina virtual de Hyper-V replicación con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo toorun una conmutación por error de prueba para la máquina virtual de Hyper-V replicación tooa sitio de System Center VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Paso 10: Ejecutar una prueba de conmutación por error para el sitio secundario de tooa de replicación de Hyper-V


Después de habilitar la replicación de máquinas virtuales de Hyper-V (VM) con [Azure Site Recovery](site-recovery-overview.md), use este toorun artículo una conmutación por error de prueba. Una conmutación por error de prueba comprueba que la replicación funciona, sin afectar a su entorno de producción. 


Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

- Cuando está desencadenan una conmutación por error de prueba, puede especificar réplica Hola red toowhich Hola prueba que se conectarán las máquinas virtuales. [Obtener más información](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) acerca de las opciones de red de Hola.
- Le recomendamos que no seleccione una red que haya seleccionado durante la asignación de red.
- las instrucciones de Hello en este artículo se describe cómo toofail a través de una sola máquina virtual. Obtenga información sobre [crear planes de recuperación](site-recovery-create-recovery-plans.md) si desea toofail a varias máquinas virtuales juntas.
- Obtenga información sobre las [limitaciones para las conmutaciones por error de prueba](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- dirección IP dada tooa VM durante la conmutación por error de prueba Hello es hello misma dirección IP que Hola VM recibiría una planeada o no planeada conmutación por error (suponiendo que la dirección IP de hello está disponible en la red de conmutación por error de prueba de hello). Si la dirección IP de hello no está disponible en la red de conmutación por error de prueba de hello, Hola VM recibe otra dirección IP que está disponible en la red de conmutación por error de prueba de Hola.
- Si desea toodo una conmutación por error de prueba en la red de producción, para la validación completa de la máquina de conectividad de red de extremo a extremo, tenga en cuenta que:
    - Hola que máquina virtual principal se debe cerrar cuando está realizando la conmutación por error de prueba de Hola. En caso contrario, dos máquinas virtuales con hello misma identidad se ejecutará en hello misma red hello en el mismo tiempo. 
    - Si realiza cambios tootest las máquinas virtuales, estos cambios se perderán al limpiar Hola probar conmutación por error. Estos cambios no replicado toohello back-VM principal.
    - Pruebas de una red de producción conduce toodowntime para las cargas de trabajo de producción. Pedir a los usuarios no toouse aplicación de hello cuando detalles de recuperación ante desastres de hello está en curso.  


## <a name="run-a-test-failover-for-a-vm"></a>Ejecutar una prueba de conmutación por error para una máquina virtual

1. toofail a través de una sola máquina virtual, en **replican elementos**, haga clic en hello VM > **conmutación por error de prueba**.
2. En **probar conmutación por error**, especificar cómo prueba máquinas virtuales estarán conectados toonetworks después de la conmutación por error de prueba de Hola. 
3. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Realizar un seguimiento del progreso en hello **trabajos** ficha.
5. Una vez completada la conmutación por error, compruebe que inicio de máquinas virtuales de la prueba de hello correctamente.
6. Cuando haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación.
7. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Este paso elimina hello las máquinas virtuales y redes que se crearon durante la conmutación por error de prueba.


## <a name="next-steps"></a>Pasos siguientes

Después de haberlo probado implementación hello, obtener más información sobre otros tipos de [conmutación por error](site-recovery-failover.md).
