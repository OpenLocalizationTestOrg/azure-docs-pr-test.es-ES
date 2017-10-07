---
title: "aaaBack las máquinas virtuales de Azure | Documentos de Microsoft"
description: "Detectar, registrar y realizar copias de seguridad de almacén de servicios de recuperación de máquinas virtuales de Azure tooa."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copia de seguridad de máquinas virtuales; hacer copia de seguridad de máquinas virtuales; copia de seguridad y recuperación ante desastres; copia de seguridad de arm"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Máquinas virtuales de Azure de copia de seguridad del almacén de servicios de recuperación de tooa
> [!div class="op_single_selector"]
> * [Copia el almacén de servicios de máquinas virtuales tooRecovery](backup-azure-arm-vms.md)
> * [Realizar copias de las máquinas virtuales tooBackup almacén](backup-azure-vms.md)
>
>

Este artículo detalla cómo almacén tooback seguridad tooa servicios de recuperación de máquinas virtuales de Azure (implementado por el Administrador de recursos e implementado clásico). La mayoría del trabajo de Hola para copia de seguridad de máquinas virtuales es preparación Hola. Para poder realizar una copia o proteger una máquina virtual, debe completar hello [requisitos previos](backup-azure-arm-vms-prepare.md) tooprepare su entorno para proteger las máquinas virtuales. Después de completar los requisitos previos de hello, a continuación, puede iniciar las instantáneas de tootake de hello operación de copia de seguridad de la máquina virtual.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Para obtener más información, vea los artículos de hello en [planear la infraestructura de copia de seguridad de máquina virtual en Azure](backup-azure-vms-introduction.md) y [máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Activación de trabajo de copia de seguridad de Hola
Directiva de copia de seguridad de Hello asociada Hola que del almacén de servicios de recuperación define la frecuencia y cuándo se ejecuta la operación de copia de seguridad de Hola. De forma predeterminada, copia de seguridad programada Hola primer es copia de seguridad inicial de Hola. Hasta que se produzca la copia de seguridad inicial de hello, Hola último estado de copia de seguridad en hello **trabajos de copia de seguridad** hoja se muestra como **advertencia (copia de seguridad inicial pendiente)**.

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A menos que la copia de seguridad inicial vence toobegin pronto, se recomienda que ejecute **realizar una copia de seguridad ahora**. Hello procedimiento siguiente se inicia desde el panel de almacén de Hola. Este procedimiento sirve para ejecutar el trabajo de copia de seguridad inicial de hello después de haber completado todos los requisitos previos. Si ya se ha ejecutado el trabajo de copia de seguridad inicial de hello, este procedimiento no está disponible. Hello directiva de copia de seguridad asociada determina siguiente trabajo de copia de seguridad de Hola.  

toorun Hola trabajo inicial de copia de seguridad:

1. En el panel de almacén de hello, haga clic en número de hello en **elementos de copia de seguridad**, o haga clic en hello **elementos de copia de seguridad** icono. <br/>
  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hola **elementos de copia de seguridad** abre la hoja.

  ![Elementos de copias de seguridad](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. En hello **elementos de copia de seguridad** hoja, elemento de hello select.

  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hola **elementos de copia de seguridad** lista se abre. <br/>

  ![Trabajo de copia de seguridad desencadenado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. En hello **elementos de copia de seguridad** lista, haga clic en el botón de puntos suspensivos hello **...**  menú contextual de tooopen Hola.

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu.png)

  aparece el menú contextual de Hola.

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. En el menú contextual de hello, haga clic en **una copia de seguridad ahora**.

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  se abre la hoja de copia de seguridad ahora Hola.

  ![Muestra la hoja de copia de seguridad ahora Hola](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. En hoja iniciar copia de seguridad de hello, haga clic en el icono de calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.

  ![se conserva el conjunto Hola último día Hola punto de recuperación de copia de seguridad ahora](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Las notificaciones de implementación le permiten saber se ha desencadenado el trabajo de copia de seguridad de Hola y que puede supervisar el progreso de hello del trabajo de hello en la página de trabajos de copia de seguridad de Hola. Según el tamaño de saludo de la máquina virtual, crear copia de seguridad inicial de hello puede tardar unos instantes.

6. estado de hello tooview o el seguimiento de hello copia de seguridad inicial, en panel de almacén de hello, vaya a hello **trabajos de copia de seguridad** icono haga clic en **en curso**.

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  se abre la hoja de trabajos de copia de seguridad de Hola.

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Hola **trabajos de copia de seguridad** hoja, puede ver el estado de Hola de todos los trabajos. Compruebe si el trabajo de copia de seguridad de hello para la máquina virtual aún está en curso, o si se ha terminado. Cuando finaliza un trabajo de copia de seguridad, estado de hello es *completado*.

  > [!NOTE]
  > Como parte de la operación de copia de seguridad de hello, Hola servicio copia de seguridad de Azure emite una extensión de copia de seguridad de toohello de comando en cada tooflush VM todos escribe y tome una instantánea coherente.
  >
  >

## <a name="troubleshooting-errors"></a>Solución de errores
Si surgen problemas durante la copia de seguridad de la máquina virtual, vea hello [artículo de solución de problemas de VM](backup-azure-vms-troubleshoot.md) para obtener ayuda.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha protegido la máquina virtual, vea Hola después toolearn artículos acerca de las tareas de administración de máquinas virtuales y cómo toorestore las máquinas virtuales.

* [Administración y supervisión de las máquinas virtuales](backup-azure-manage-vms.md)
* [Restauración de máquinas virtuales](backup-azure-arm-restore-vms.md)
