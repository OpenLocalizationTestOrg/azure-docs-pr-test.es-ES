---
title: "aaaRun una conmutación por error de prueba para la replicación de máquina virtual de Azure con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de Hola que necesita para ejecutar una prueba de conmutación por error de replicación de máquinas virtuales de Azure tooanother usando de región de Azure hello Azure Site Recovery de servicio."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>Paso 6: Ejecución de una conmutación por error de prueba para la replicación de VM de Azure

Después de habilitar la replicación de la máquina virtual de Azure (VM), siga los pasos de hello en este artículo, conmutación por error de prueba de toorun de tooanother de una región de Azure, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

- Cuando termine de artículo hello, debería ha comprobado que con una conmutación por error de prueba, que al menos una máquina virtual de Azure puede conmutar por error tooyour región secundaria de Azure. 
- Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> La replicación de VM de Azure se encuentra en una versión preliminar en este momento.


## <a name="before-you-start"></a>Antes de comenzar

- Antes de ejecutar una prueba de conmutación por error, se recomienda que compruebe las propiedades de la máquina virtual de Hola y realizar cualquier cambio que necesite. puede tener acceso a propiedades de la máquina virtual de hello en **replican elementos**. Hola **Essentials** hoja muestra información sobre la configuración de máquinas y estado.
- Se recomienda usar una red de máquina virtual de Azure independiente para la conmutación por error de prueba de hello y no en red hello (valor predeterminado o personalizado) que se configuró para conmutación por error de producción.
- Hola prueba de conmutación por error se produce un error sobre máquinas virtuales de Azure (y su almacenamiento) toohello región secundaria de Azure. No se replican aplicaciones o recursos dependientes. Si las aplicaciones que se ejecutan en errores con las máquinas virtuales se depende de otros recursos, como Active Directory o DNS, debe tooreplicate estos demasiado, si no están disponibles en su región secundaria. [Más información](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Si desea tooaccess replicar las máquinas virtuales después de la conmutación por error de un sitio local, necesita demasiado[preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese máquinas virtuales.

## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

1. En **configuración** > **replican elementos**, haga clic en hello VM **+ conmutación por error de prueba** icono. 

2. En **conmutación por error de prueba**, seleccione un toouse de punto de recuperación para hello conmutación por error:

    - **Procesar más reciente**: se produce un error Hola VM en el último punto de recuperación de toohello que se procesó por servicio de Site Recovery Hola. se muestra la marca de tiempo de Hola. Con esta opción, no se empleó tiempo en el procesamiento de datos, por lo que se proporciona un objetivo de tiempo de recuperación (RTO) bajo.
    - **Más reciente coherente con la aplicación**: esta opción se conmuta punto coherente con la aplicación de recuperación de todas las máquinas virtuales toohello más reciente. se muestra la marca de tiempo de Hola. 
    - **Personalizado**: seleccione un punto de recuperación.
 
3. Después de producirse la conmutación por error de hello, se conectará toowhich de red virtual de Azure de destino Hola seleccione máquinas virtuales de Azure en la región secundaria de Hola.
4. toostart Hola conmutación por error, haga clic en **Aceptar**. tootrack de progreso, haga clic en hello VM tooopen sus propiedades. O bien, puede hacer clic en hello **conmutación por error de prueba** trabajo en el nombre del almacén de hello > **configuración** > **trabajos** > **detrabajosderecuperacióndesitio**.
5. Después de hello conmutación por error finaliza, réplica de hello Azure VM aparece en hello portal de Azure > **máquinas virtuales**. Asegúrese de que ese hello VM es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.
6. Hola toodelete las máquinas virtuales que se crearon durante la conmutación por error de prueba hello, haga clic en **conmutación por error de prueba de limpieza** en hello replicar Hola o elemento de plan de recuperación. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. 

[Más información](site-recovery-test-failover-to-azure.md) sobre las conmutaciones por error de prueba.

## <a name="next-steps"></a>Pasos siguientes

Después de realizar la conmutación por error, este tutorial se habrá completado. Ahora, obtenga información sobre la ejecución de conmutaciones por error en producción:

- [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
- Obtenga más información sobre la conmutación por error de varias VM [con un plan de recuperación](site-recovery-create-recovery-plans.md).
- Aprenda sobre el [uso de planes de recuperación](site-recovery-create-recovery-plans.md).
- Más información sobre la [reprotección de máquinas virtuales de Azure](site-recovery-how-to-reprotect.md) después de una conmutación por error.

