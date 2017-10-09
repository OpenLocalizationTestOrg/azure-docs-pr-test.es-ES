---
title: "aaaSet una directiva de replicación para tooAzure de replicación de VM de VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset una directiva de replicación al replicar máquinas virtuales VMware tooAzure almacenamiento"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>Paso 9: Configurar una directiva de replicación para tooAzure de replicación de VM de VMware


Este artículo se describe cómo tooset una directiva de replicación al replicar tooAzure de máquinas virtuales VMware con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configuración de una directiva

Vea un vídeo introductorio rápido antes de empezar:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate una nueva directiva de replicación, haga clic en **infraestructura de Site Recovery** > **directivas de replicación** > **+ directiva de replicación**.
2. En **Crear directiva de replicación**, especifique un nombre de directiva.
3. En **umbral de RPO**, especifique el límite RPO de Hola. Este valor especifica la frecuencia con que se crean puntos de recuperación de datos. Se genera una alerta cuando la replicación continua supera este límite.
4. En **retención de punto de recuperación**, especifique cuánto tiempo (en horas) es el período de retención de Hola para cada punto de recuperación. Máquinas virtuales replicadas se pueden recuperar tooany punto en una ventana. Seguridad too24 retención de horas es compatible con máquinas replicadas toopremium almacenamiento y 72 horas para el almacenamiento estándar.
5. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Haga clic en **Aceptar** toocreate directiva de Hola.

    ![Directiva de replicación](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Cuando se crea una nueva directiva automáticamente está asociada con el servidor de configuración de Hola. De forma predeterminada, se crea automáticamente una directiva correspondiente para la conmutación por recuperación. Por ejemplo, si hello directiva de replicación es **rep-policy** será la directiva de conmutación por recuperación de hello **rep-directiva de conmutación por recuperación**. Esta directiva no se usa hasta que se inicie una conmutación por recuperación desde Azure.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 10: instalar el servicio de movilidad de Hola](vmware-walkthrough-install-mobility.md)
