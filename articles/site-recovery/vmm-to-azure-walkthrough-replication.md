---
title: "aaaSet una directiva de replicación para tooAzure de replicación de máquina virtual de Hyper-V (con VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooset una directiva de replicación para tooAzure de replicación de máquina virtual de Hyper-V (con VMM) con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Paso 10: Configurar una directiva de replicación de máquina virtual de Hyper-V tooAzure de replicación (con VMM)


Después de configurar [asignación de red](vmm-to-azure-walkthrough-network-mapping.md), use este tooconfigure artículo una directiva de replicación T\tooreplicate máquinas virtuales de Hyper-V administrados en tooAzure de nubes de System Center Virtual Machine Manager (VMM) local, utilizando Hola [ Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Para crear una directiva

1. toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.

    ![Red](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. En **Crear y asociar directiva**, especifique un nombre de directiva.
3. En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).

    > [!NOTE]
    >  No se admite una frecuencia de segundo 30 al replicar toopremium almacenamiento. limitación de Hello viene determinado por el número de Hola de instantáneas por blob (100) compatible con almacenamiento premium. [Más información](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. En **retención de punto de recuperación**, especifique en horas cuánto va un período de retención Hola para cada punto de recuperación. Equipos protegidos pueden ser recuperado tooany punto dentro de una ventana.
5. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola. Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola. Tenga en cuenta que si habilita las instantáneas coherentes con la aplicación, afectará Hola rendimiento de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.
6. En **hora de inicio de la replicación inicial**, indicar al toostart Hola la replicación inicial. se produce la replicación de Hello sobre el ancho de banda de internet por lo que conviene tooschedule que fuera de su horario ocupado.
7. En **cifrar los datos almacenados en Azure**, especifique si tooencrypt datos de rest de almacenamiento de Azure. y, a continuación, haga clic en **Aceptar**.

    ![Directiva de replicación](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Cuando se crea una nueva directiva automáticamente tiene asociadas con hello nube de VMM. Haga clic en **Aceptar**. Puede asociar más nubes de VMM (hello y máquinas virtuales en ellos) con esta directiva de replicación en **replicación** > nombre de directiva > **asociar la nube de VMM**.

    ![Directiva de replicación](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 11: habilitar la replicación](vmm-to-azure-walkthrough-enable-replication.md)
