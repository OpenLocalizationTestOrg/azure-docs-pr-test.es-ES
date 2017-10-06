---
title: "aaaSet una directiva de replicación para máquinas virtuales de Hyper-V tooAzure de replicación (sin System Center VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset una directiva de replicación al replicar las máquinas virtuales de Hyper-V tooAzure almacenamiento"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Paso 9: Configurar una directiva de replicación para tooAzure de replicación de máquina virtual de Hyper-V

Este artículo se describe cómo tooset una directiva de replicación al replicar máquinas virtuales de Hyper-V tooAzure (sin System Center VMM) mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Acerca de las instantáneas

Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola.
    - Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola.
    - Si habilita las instantáneas coherentes con la aplicación, afectará al rendimiento de Hola de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.

## <a name="set-up-a-replication-policy"></a>Configurar una directiva de replicación

1. toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.

    ![Red](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. En **Crear y asociar directiva**, especifique un nombre de directiva.
3. En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).

    > [!NOTE]
    > No se admite una frecuencia de segundo 30 al replicar toopremium almacenamiento. limitación de Hello viene determinado por el número de Hola de instantáneas por blob (100) compatible con almacenamiento premium. [Más información](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. En **retención de punto de recuperación**, especifique en horas cuánto tiempo es el período de retención de Hola para cada punto de recuperación. Las máquinas virtuales se pueden recuperar tooany punto dentro de una ventana.
5. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación.
6. En **hora de inicio de la replicación inicial**, especifique cuándo toostart Hola la replicación inicial. se produce la replicación de Hello sobre el ancho de banda de internet por lo que conviene tooschedule que fuera de su horario ocupado. y, a continuación, haga clic en **Aceptar**.

    ![Directiva de replicación](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Cuando se crea una nueva directiva, automáticamente tiene asociadas con el sitio de Hyper-V de Hola. Puede asociar un sitio de Hyper-V (hello las máquinas virtuales en ella y) con varias directivas de replicación en **replicación** > nombre de directiva > **asociar el sitio de Hyper-V**.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 10: habilitar la replicación](hyper-v-site-walkthrough-enable-replication.md)
