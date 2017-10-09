---
title: "trabajos de copia de seguridad de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento tooview y administrar trabajos de copia de seguridad programados, actualmente en ejecución y completados."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>Use el Administrador de instantáneas StorSimple tooview y administrar los trabajos de copia de seguridad

## <a name="overview"></a>Información general
Hola **trabajos** nodo Hola **ámbito** panel muestra hello **programada**, **últimas 24 horas**, y **ejecutando**copia de seguridad de las tareas que inició interactivamente o mediante una directiva configurada. 

Este tutorial le explica cómo puede usar hello **trabajos** información del nodo toodisplay acerca de los trabajos de copia de seguridad programadas, recientes y que se está ejecutando. (lista de Hola de trabajos e información correspondiente aparece en hello **resultados** panel.) Además, puede es posible hacer clic en un trabajo de la lista y ver un menú contextual que enumera las acciones disponibles.

## <a name="view-scheduled-jobs"></a>Visualización de los trabajos programados
Hola uso siguiendo el procedimiento tooview programa trabajos de copia de seguridad.

#### <a name="tooview-scheduled-jobs"></a>tooview programar trabajos
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple. 
2. Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **programada**. Hello siguiente información aparece en hello **resultados** panel:
   
   * **Nombre** : hello nombre de instantánea programada Hola
   * **A continuación ejecute** : Hola fecha y hora de la siguiente instantánea programada de Hola
   * **Última ejecución** : Hola fecha y hora de instantánea programada más reciente de Hola
     
     > [!NOTE]
     > Para las instantáneas sola una sola vez, Hola **siguiente ejecución** y **última ejecución** será Hola igual.
     
     ![Trabajos de copia de seguridad programados](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. tooperform acciones adicionales en un trabajo específico, haga clic en el nombre del trabajo Hola Hola **resultados** panel y seleccione Hola opciones del menú.

## <a name="view-recent-jobs"></a>Visualización de los trabajos recientes
Usar hello después de la copia de seguridad de procedimiento tooview y restaura los trabajos que se completaron en hello últimas 24 horas.

#### <a name="tooview-recent-jobs"></a>trabajos recientes tooview
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **últimas 24 horas**. Hola **resultados** panel muestra los trabajos de copia de seguridad para hello últimas 24 horas (tooa máximo de 64 trabajos). Hello siguiente información aparece en hello **resultados** panel, dependiendo de hello **vista** opciones especificadas:
   
   * **Nombre** : hello nombre de instantánea programada Hola.
   * **Iniciar** : Hola fecha y la hora de inicio de instantánea de Hola.
   * **Detenido** : Hola fecha y la hora cuando instantánea Hola se finalizó o canceló.
   * **Transcurrido** : Hola período de tiempo entre hello **iniciado** y **detenido** veces.
   * **Estado** : Hola estado de hello completado recientemente trabajo. **Éxito** indica que copia de seguridad de Hola se creó correctamente. **No se pudo** indica que el trabajo de hello no se ha ejecutado correctamente.
   * **Información** : Hola motivo Hola error.
   * **Bytes procesados (MB)** : cantidad de Hola de datos del grupo de volúmenes de Hola que se procesó (en MB). 
     
     ![Trabajos ejecutados en hello últimas 24 horas](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. tooperform acciones adicionales en un trabajo específico, haga clic en el nombre del trabajo Hola Hola **resultados** panel y seleccione Hola opciones del menú.
   
    ![Eliminación de un trabajo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Visualización de los trabajos en ejecución
Usar hello después de los trabajos de tooview de procedimiento que se están ejecutando actualmente.

#### <a name="tooview-currently-running-jobs"></a>tooview trabajos en ejecución
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **ejecutando**. Función hello **vista** opciones que se especifiquen, Hola siguiente información aparece en hello **resultados** panel:
   
   * **Nombre** : hello nombre de instantánea programada Hola.
   * **Iniciar** : Hola fecha y la hora de inicio de instantánea de Hola.
   * **Punto de comprobación** : Hola acción actual de copia de seguridad de Hola.
   * **Estado** : Hola porcentaje de finalización.
   * **Transcurrido** : cantidad de Hola de tiempo que ha transcurrido desde que comenzó la copia de seguridad de Hola. 
   * **Rendimiento medio (MB)** : proporción del total de bytes de datos procesados toothat de tiempo total de procesamiento (MB).
   * **Bytes procesados (MB)** : total de bytes de los datos procesados (en MB).
   * **Bytes escritos (MB)** : total de bytes de los datos escritos (en MB). Incluye datos de hello así como los metadatos de hello y, por lo que es normalmente mayor que Hola Bytes procesados.
     
     ![Trabajos en ejecución](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. tooperform acciones adicionales en un trabajo específico, haga clic en el nombre del trabajo Hola Hola **resultados** panel y seleccione Hola opciones del menú.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga información acerca de cómo demasiado[usar el catálogo de copia de seguridad de administrador de instantáneas StorSimple toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md).

