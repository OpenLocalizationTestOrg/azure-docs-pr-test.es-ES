---
title: "directivas de copia de seguridad de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento toocreate y administrar directivas de copia de seguridad de Hola que controlan las copias de seguridad programadas."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>Use el Administrador de instantáneas StorSimple toocreate y administrar las directivas de copia de seguridad
## <a name="overview"></a>Información general
Una directiva de copia de seguridad crea una programación de copia de seguridad de datos del volumen localmente o en la nube de Hola. Cuando crea una directiva de copia de seguridad, también puede especificar una directiva de retención. (Puede retener un máximo de 64 instantáneas). Para obtener más información sobre las directivas de copia de seguridad, consulte [Tipos de copia de seguridad](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) en [Serie StorSimple 8000: una solución de almacenamiento en la nube híbrida](storsimple-overview.md).

Este tutorial explica cómo realizar lo siguiente:

* Creación de una directiva de copia de seguridad
* Edición de una directiva de copia de seguridad
* Eliminación de una directiva de copia de seguridad

## <a name="create-a-backup-policy"></a>Creación de una directiva de copia de seguridad
Usar hello siguiendo el procedimiento toocreate una nueva directiva de copia de seguridad.

#### <a name="toocreate-a-backup-policy"></a>toocreate una directiva de copia de seguridad
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **directivas de copia de seguridad**y haga clic en **Crear directiva de copia de seguridad**.

    ![Creación de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Hola **crear una directiva** aparece el cuadro de diálogo.

    ![Creación de una directiva - pestaña General](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. En hello **General** ficha, Hola completo siguiente información:

   1. Hola **nombre** cuadro de texto, escriba un nombre para la directiva de Hola.
   2. Hola **grupo de volúmenes** cuadro de texto, escriba un nombre de grupo de volúmenes de hello asociado con la directiva de hello como Hola.
   3. Seleccione **Instantánea local** o **Instantánea de nube**.
   4. Seleccione el número de Hola de tooretain de instantáneas. Si selecciona **todos los**, se conservarán 64 instantáneas (Hola máximo).
4. Haga clic en hello **programación** ficha.

    ![Creación de una directiva - pestaña Programación](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. En hello **programación** ficha, Hola completo siguiente información:

   1. Haga clic en hello **habilitar** casilla de verificación tooschedule Hola siguiente copia de seguridad.
   2. En **Configuración**, seleccione **Una vez**, **Diario**, **Semanal** o **Mensual**.
   3. Hola **iniciar** cuadro de texto, haga clic en el icono del calendario de Hola y seleccione una fecha de inicio.
   4. En **Configuración avanzada**, puede establecer programaciones de repetición opcionales y una fecha de finalización.
   5. Haga clic en **Aceptar**.

Después de crear una directiva de copia de seguridad, Hola siguiente información aparece en hello **resultados** panel:

* **Nombre** : hello nombre de directiva de copia de seguridad.
* **Tipo** : instantánea local o instantánea de nube.
* **Grupo de volúmenes** : hello grupo de volúmenes asociado con la directiva de Hola.
* **Retención** : hello conserva el número de instantáneas; Hola máximo es 64.
* **Crear** : fecha de Hola que se creó esta directiva.
* **Habilitado** : indica si la directiva de hello está actualmente en vigor: **True** indica que está en vigor; **False** indica que no está en vigor.

## <a name="edit-a-backup-policy"></a>Edición de una directiva de copia de seguridad
Usar hello siguiendo el procedimiento tooedit una directiva de copia de seguridad existente.

#### <a name="tooedit-a-backup-policy"></a>tooedit una directiva de copia de seguridad
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en hello **directivas de copia de seguridad** nodo. Todas las directivas de copia de seguridad de hello aparecen en hello **resultados** panel.
3. Haga clic en directiva de Hola que desee tooedit y, a continuación, haga clic en **editar**.

    ![Edición de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Cuando Hola **crear una directiva de** ventana aparece, escriba los cambios y, a continuación, haga clic en **Aceptar**.

## <a name="delete-a-backup-policy"></a>Eliminación de una directiva de copia de seguridad
Usar hello siguiendo el procedimiento toodelete una directiva de copia de seguridad.

#### <a name="toodelete-a-backup-policy"></a>toodelete una directiva de copia de seguridad
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en hello **directivas de copia de seguridad** nodo. Todas las directivas de copia de seguridad de hello aparecen en hello **resultados** panel.
3. Haga clic en directiva de copia de seguridad de Hola que desee toodelete y, a continuación, haga clic en **eliminar**.
4. Cuando aparezca el mensaje de bienvenida de confirmación, haga clic en **Sí**.

    ![Eliminación de la confirmación de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooview y administrar los trabajos de copia de seguridad](storsimple-snapshot-manager-manage-backup-jobs.md).
