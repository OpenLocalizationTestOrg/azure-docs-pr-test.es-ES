---
title: "grupos de volúmenes del Administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento toocreate y administrar grupos de volúmenes."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>Use el Administrador de instantáneas StorSimple toocreate y administrar grupos de volúmenes
## <a name="overview"></a>Información general
Puede usar hello **grupos de volúmenes** nodo hello **ámbito** grupos toovolume del panel tooassign volúmenes, ver información acerca de un grupo de volúmenes, programar copias de seguridad y editar grupos de volúmenes.

Grupos de volúmenes son conjuntos de tooensure de volúmenes relacionados que se usa que las copias de seguridad son coherentes con la aplicación. Para obtener más información, consulte [Volúmenes y grupos de volúmenes](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) e [Integración con el Servicio de instantáneas de volumen de Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Todos los volúmenes de un grupo de volúmenes deben provenir de un solo proveedor de servicios en la nube.
> * Al configurar grupos de volúmenes, no combine volúmenes compartidos de clúster (CSV) y no csv en hello mismo grupo de volúmenes. Administrador de instantáneas de StorSimple no admite la combinación de CSV y no csv en Hola misma instantánea.

![Nodo Grupos de volúmenes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Ilustración 1: Nodo de grupos de volúmenes de Administrador de instantáneas StorSimple** 

Este tutorial explica cómo puede usar Administrador de instantáneas StorSimple para:

* Visualizar información acerca de los grupos de volúmenes
* Crear un grupo de volúmenes
* Realizar una copia de seguridad de un grupo de volúmenes
* Editar un grupo de volúmenes
* Eliminar un grupo de volúmenes

Todas estas acciones también están disponibles en hello **acciones** panel.

## <a name="view-volume-groups"></a>Visualización de grupos de volúmenes
Si hace clic en hello **grupos de volúmenes** nodo, hello **resultados** panel muestra hello después de obtener información acerca de cada grupo de volúmenes, según las selecciones de columna de Hola que realice. (Hola columnas Hola **resultados** panel son configurables. Menú contextual hello **volúmenes** nodo, seleccione **vista**y, a continuación, seleccione **agregar o quitar columnas**.)

| Columna Resultados | Descripción |
|:--- |:--- |
| Nombre |Hola **nombre** columna contiene el nombre de hello del grupo de volúmenes de Hola. |
| Application |Hola **aplicaciones** columna muestra el número de Hola de escritores VSS instalados actualmente y ejecuta en Hola host de Windows. |
| Seleccionado |Hola **seleccionados** columna muestra el número de Hola de volúmenes que se encuentran en el grupo de volúmenes de Hola. Un cero (0) indica que no haya ninguna aplicación está asociada a volúmenes de hello en el grupo de volúmenes de Hola. |
| Importado |Hola **importada** columna muestra el número de Hola de volúmenes importados. Cuando se establece demasiado**True**, esta columna indica que un grupo de volúmenes se importó desde Hola portal de Azure y no se creó en el Administrador de instantáneas de StorSimple. |

> [!NOTE]
> Grupos de volúmenes del Administrador de instantáneas StorSimple también se muestran en hello **directivas de copia de seguridad** ficha Hola portal de Azure.
> 
> 

## <a name="create-a-volume-group"></a>Crear un grupo de volúmenes
Usar hello siguiendo el procedimiento toocreate un grupo de volúmenes.

#### <a name="toocreate-a-volume-group"></a>toocreate un grupo de volúmenes
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **grupos de volúmenes**y, a continuación, haga clic en **crear grupo de volúmenes**.
   
    ![Crear grupo de volúmenes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Hola **crear un grupo de volúmenes** aparecerá el cuadro de diálogo.
   
    ![Cuadro de diálogo Crear un grupo de volúmenes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Escriba Hola siguiente información:
   
   1. Hola **nombre** , escriba un nombre único para el nuevo grupo de volúmenes Hola.
   2. Hola **aplicaciones** cuadro, seleccione las aplicaciones asociadas con los volúmenes de Hola que vas a agregar grupo de volúmenes de toohello.
      
       Hola **aplicaciones** cuadro enumera sólo las aplicaciones que usan volúmenes de StorSimple y tienen VSS writers habilitadas para ellos. Un escritor VSS está habilitado sólo si todos los volúmenes de Hola ese sistema de escritura de hello es consciente de los volúmenes de StorSimple. Si Hola aplicaciones cuadro está vacío, se instala ninguna aplicación que usa volúmenes de StorSimple de Azure y escritores de VSS, ha admitido. (Actualmente, Azure StorSimple admite Microsoft Exchange y SQL Server). Para obtener más información acerca de los escritores VSS, consulte [Integración con el Servicio de instantáneas de volumen de Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Si selecciona una aplicación, se seleccionan automáticamente todos los volúmenes asociados a ella. Por el contrario, si selecciona volúmenes asociados a una aplicación específica, aplicación hello se selecciona automáticamente en hello **aplicaciones** cuadro. 
   3. Hola **volúmenes** , seleccione el grupo de volúmenes de StorSimple volúmenes tooadd toohello. 
      
      * Puede incluir volúmenes con una o varias particiones. (Los volúmenes de varias particiones pueden ser discos dinámicos o discos básicos con varias particiones.) Un volumen que contiene varias particiones se trata como una sola unidad. Por lo tanto, si agrega solo una de grupo de volúmenes tooa Hola particiones, Hola todas las otras particiones se toothat agregadas automáticamente volumen grupo Hola mismo tiempo. Después de agregar un grupo de volúmenes tooa de varias particiones volumen, hello volumen de varias particiones continúa toobe tratada como una sola unidad.
      * Puede crear grupos de volúmenes vacíos si no asigna ningún toothem de volúmenes. 
      * No combine volúmenes compartidos de clúster (CSV) y no csv en hello mismo grupo de volúmenes. Administrador de instantáneas de StorSimple no admite la combinación de volúmenes CSV y los volúmenes no CSV en Hola misma instantánea.
4. Haga clic en **Aceptar** grupo de volúmenes de toosave Hola.

## <a name="back-up-a-volume-group"></a>Realizar una copia de seguridad de un grupo de volúmenes
Usar hello siguiendo el procedimiento tooback un grupo de volumen.

#### <a name="tooback-up-a-volume-group"></a>tooback un grupo de volumen
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **grupos de volúmenes** nodo, haga clic en un nombre de grupo de volúmenes y, a continuación, haga clic en **hacer copia de seguridad**.
   
    ![Copia de seguridad de un grupo de volúmenes de forma inmediata](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. Hola **hacer copia de seguridad** cuadro de diálogo, seleccione **instantánea Local** o **instantánea en la nube**y, a continuación, haga clic en **crear**.
   
    ![Cuadro de diálogo Realizar copia de seguridad](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. se está ejecutando tooconfirm que Hola copia de seguridad, expanda hello **trabajos** nodo y, a continuación, haga clic en **ejecutando**. debe aparecer la copia de seguridad de Hola.
5. Hola tooview completado instantánea, expanda hello **catálogo de copia de seguridad** nodo, expanda el nombre del grupo de volúmenes de hello y, a continuación, haga clic en **instantánea Local** o **instantánea en la nube**. copia de seguridad de Hola se mostrarán si finalizó correctamente.

## <a name="edit-a-volume-group"></a>Editar un grupo de volúmenes
Usar hello siguiendo el procedimiento tooedit un grupo de volúmenes.

#### <a name="tooedit-a-volume-group"></a>tooedit un grupo de volúmenes
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **grupos de volúmenes** nodo, haga clic en un nombre de grupo de volúmenes y, a continuación, haga clic en **editar**.
3. Hola ** crear un grupo de volúmenes ** aparecerá el cuadro de diálogo. Puede cambiar hello **nombre**, **aplicaciones**, y **volúmenes** entradas.
4. Haga clic en **Aceptar** toosave los cambios.

## <a name="delete-a-volume-group"></a>Eliminar un grupo de volúmenes
Usar hello siguiendo el procedimiento toodelete un grupo de volúmenes. 

> [!WARNING]
> Esto también elimina todas las copias de seguridad de hello asociados con el grupo de volúmenes de Hola.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete un grupo de volúmenes
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **grupos de volúmenes** nodo, haga clic en un nombre de grupo de volúmenes y, a continuación, haga clic en **eliminar**.
3. Hola **eliminar grupo de volúmenes** aparecerá el cuadro de diálogo. Tipo de **confirmar** en Hola cuadro de texto y, a continuación, haga clic en **Aceptar**.
   
    Hola eliminar grupo de volúmenes desaparecerá de la lista de Hola Hola **resultados** panel y todas las copias de seguridad que están asociados a ese grupo de volúmenes se eliminan del catálogo de copia de seguridad de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple toocreate y administrar las directivas de copia de seguridad](storsimple-snapshot-manager-manage-backup-policies.md).

