---
title: "catálogo de copia de seguridad de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento tooview y administrar el catálogo de copia de seguridad de Hola."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>Catálogo de copia de seguridad de hello toomanage use el Administrador de instantáneas StorSimple

## <a name="overview"></a>Información general
función principal de Hola de administrador de instantáneas de StorSimple es tooallow se toocreate coherentes con la aplicación copias de seguridad de volúmenes de StorSimple en forma de Hola de instantáneas. Las instantáneas se enumeran en un archivo XML llamado *catálogo de copia de seguridad*. catálogo de copia de seguridad de Hello organiza las instantáneas por grupo de volúmenes y, a continuación, por instantánea local o instantánea en la nube.

Este tutorial describe cómo puede usar hello **catálogo de copia de seguridad** hello toocomplete de nodo siguientes tareas:

* Restauración de un volumen
* Clonación de un volumen o un grupo de volúmenes
* Eliminación de una copia de seguridad
* Recuperación de un archivo
* Restaurar base de datos de administrador de instantáneas Storsimple Hola

Puede ver el catálogo de copia de seguridad de hello expandiendo hello **catálogo de copia de seguridad** nodo Hola **ámbito** panel y, a continuación, Expandir grupo de volúmenes de Hola.

* Si hace clic en nombre de grupo de volúmenes de hello, Hola **resultados** panel muestra el número de Hola de instantáneas locales y en la nube disponibles para el grupo de volúmenes de Hola. 
* Si hace clic en **instantánea Local** o **instantánea en la nube**, hello **resultados** panel muestra hello después de obtener información sobre cada instantánea de copia de seguridad (según su **Vista** configuración):
  
  * **Nombre** – se tomó la instantánea de Hola Hola del tiempo.
  * **Tipo** : si se trata de una instantánea local o una instantánea de nube.
  * **Propietario** : propietario del contenido Hola. 
  * **Disponible** : indica si la instantánea de hello está disponible actualmente. **True** indica esa instantánea Hola está disponible y puede restaurarse; **False** indica esa instantánea Hola ya no está disponible. 
  * **Importar** : indica si se importó la copia de seguridad de Hola. **True** indica que copia de seguridad de Hola se importó desde hello en dispositivo de hello tiempo Hola configuró en el Administrador de instantáneas de StorSimple; el Administrador de dispositivos de StorSimple **False** indica que no se ha importado, pero se creó mediante el Administrador de instantáneas de StorSimple. (Se puede identificar fácilmente un grupo de volúmenes importados porque se agrega un sufijo que identifica el dispositivo de Hola desde el que se importó el grupo de volúmenes de Hola.)
    
    ![Catálogo de copias de seguridad](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Si expande **instantánea Local** o **instantánea en la nube**y, a continuación, haga clic en el nombre de una instantánea, hello **resultados** panel muestra hello después de obtener información acerca de Hola instantánea que ha seleccionado:
  
  * **Nombre** : Hola volumen identificado por la letra de unidad. 
  * **Nombre local** – nombre local de Hola de unidad de hello (si está disponible). 
  * **Dispositivo** : hello nombre de dispositivo de hello en qué Hola reside el volumen. 
  * **Disponible** : indica si la instantánea de hello está disponible actualmente. **True** indica esa instantánea Hola está disponible y puede restaurarse; **False** indica esa instantánea Hola ya no está disponible. 

## <a name="restore-a-volume"></a>Restauración de un volumen
Usar hello siguiendo el procedimiento toorestore un volumen de copia de seguridad.

#### <a name="prerequisites"></a>Requisitos previos
Si no lo ha hecho ya, cree un volumen y un grupo de volúmenes y, a continuación, eliminar el volumen de Hola. De forma predeterminada, el Administrador de instantáneas StorSimple realiza una copia de un volumen antes de permitir toobe eliminado. Esta precaución puede evitar la pérdida de datos si se elimina accidentalmente volumen de Hola o si los datos de hello necesitan toobe recuperó por algún motivo. 

Administrador de instantáneas StorSimple muestra hello sigue el mensaje mientras crea la copia de seguridad preventiva Hola.

![Mensaje de instantánea automático](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> No se puede eliminar un volumen que forma parte de un grupo de volúmenes. opción de eliminación de Hello no está disponible. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore un volumen
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple. 
2. Hola **ámbito** panel, expanda hello **catálogo de copia de seguridad** nodo, expanda un grupo de volúmenes y, a continuación, haga clic en **instantáneas locales** o **instantáneas en la nube**. Aparece una lista de las instantáneas de copia de seguridad en hello **resultados** panel.
3. Copia de seguridad de Hola de búsqueda que desea toorestore, menú contextual y, a continuación, haga clic en **restaurar**.
   
    ![Restauración del catálogo de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. En la página de confirmación de hello, revise los detalles de hello, escriba **confirmar**y, a continuación, haga clic en **Aceptar**. Administrador de instantáneas StorSimple usa volumen Hola de hello toorestore copia de seguridad.
   
    ![Mensaje de confirmación de restauración](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. Puede supervisar la acción de restauración de hello mientras se ejecuta. Hola **ámbito** panel, expanda hello **trabajos** nodo y, a continuación, haga clic en **ejecutando**. Detalles del trabajo Hola aparecen en hello **resultados** panel. Cuando finalice el trabajo de restauración de hello, detalles del trabajo Hola son transferido toohello **últimas 24 horas** lista.

## <a name="clone-a-volume-or-volume-group"></a>Clonación de un volumen o un grupo de volúmenes
Usar hello siguiendo el procedimiento toocreate un duplicado (clon) de un volumen o un grupo de volúmenes.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone un volumen o grupo de volúmenes
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **catálogo de copia de seguridad** nodo, expanda un grupo de volúmenes y, a continuación, haga clic en **instantáneas en la nube**. Aparece una lista de copias de seguridad en hello **resultados** panel.
3. Busque el volumen de Hola o grupo de volúmenes que desee tooclone, contextual Hola nombre del volumen o grupo y haga clic en **clon**. Hola **instantánea en la nube clon** aparece el cuadro de diálogo.
   
    ![Clonación de una instantánea de nube](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Hola completa **instantánea en la nube clon** cuadro de diálogo como se indica a continuación: 
   
   1. Hola **nombre** cuadro de texto, escriba un nombre para hello clona el volumen. Este nombre aparecerá en hello **volúmenes** nodo. 
   2. (Opcional) seleccione **unidad**y, a continuación, seleccione una letra de unidad de la lista desplegable de Hola.
   3. (Opcional) seleccione **carpeta (NTFS)**, escriba una ruta de acceso de carpeta o haga clic en Examinar y seleccione una ubicación de carpeta de Hola. 
   4. Haga clic en **Crear**.
5. Cuando haya finalizado el proceso de clonación de hello, debe inicializar Hola clonar volumen. Inicie el Administrador del servidor y, a continuación, inicie Administración de discos. Para obtener instrucciones detalladas, consulte [Montar volúmenes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Una vez inicializado, volumen de Hola se enumerará en hello **volúmenes** nodo Hola **ámbito** panel. Si no ve los volúmenes de Hola que aparecen, actualice la lista de Hola de volúmenes (contextual hello **volúmenes** nodo y, a continuación, haga clic en **actualizar**).

## <a name="delete-a-backup"></a>Eliminación de una copia de seguridad
Usar hello siguiendo el procedimiento toodelete una instantánea de catálogo de copia de seguridad de Hola. 

> [!NOTE]
> Eliminar una instantánea, elimina Hola una copia de seguridad asociado a la instantánea de Hola. Sin embargo, el proceso de Hola de limpiar los datos de nube de hello puede tardar algún tiempo.<br>


#### <a name="toodelete-a-backup"></a>toodelete una copia de seguridad
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, expanda hello **catálogo de copia de seguridad** nodo, expanda un grupo de volúmenes y, a continuación, haga clic en **instantáneas locales** o **instantáneas en la nube**. Aparece una lista de instantáneas en hello **resultados** panel.
3. Menú contextual instantánea de Hola que desee toodelete y, a continuación, haga clic en **eliminar**.
4. Cuando aparezca el mensaje de bienvenida de confirmación, haga clic en **Aceptar**.

## <a name="recover-a-file"></a>Recuperación de un archivo
Si un archivo se elimina accidentalmente de un volumen, puede recuperar el archivo hello mediante la recuperación de una instantánea que previamente las fechas de eliminación de hello, mediante Hola instantánea toocreate un clon del volumen de hello y, a continuación, copiar el archivo hello de Hola volumen original toohello de volumen clonado.

#### <a name="prerequisites"></a>Requisitos previos
Antes de comenzar, asegúrese de que tiene una copia de seguridad actual del grupo de volúmenes de Hola. A continuación, elimine un archivo almacenado en uno de los volúmenes de hello en ese grupo de volúmenes. Por último, utilice el siguiente archivo de hello eliminado de toorestore de pasos de la copia de seguridad de Hola. 

#### <a name="toorecover-a-deleted-file"></a>toorecover un archivo eliminado
1. Haga clic en el icono de administrador de instantáneas de StorSimple de hello en el escritorio. aparece la ventana de consola de administrador de instantáneas StorSimple de Hola. 
2. Hola **ámbito** panel, expanda hello **catálogo de copia de seguridad** nodo y examinar tooa instantánea que contiene el archivo hello eliminado. Normalmente, debe seleccionar una instantánea que se creó antes de la eliminación de Hola.
3. Buscar Hola volumen que desea tooclone, menú contextual y haga clic en **clon**. Hola **instantánea en la nube clon** aparece el cuadro de diálogo.
   
    ![Clonación de una instantánea de nube](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Hola completa **instantánea en la nube clon** cuadro de diálogo como se indica a continuación: 
   
   1. Hola **nombre** cuadro de texto, escriba un nombre para hello clona el volumen. Este nombre aparecerá en hello **volúmenes** nodo. 
   2. (Opcional) Seleccione **unidad**y, a continuación, seleccione una letra de unidad de la lista desplegable de Hola. 
   3. (Opcional) Seleccione **carpeta (NTFS)**y escriba una ruta de acceso de carpeta o haga clic en **examinar** y seleccione una ubicación de carpeta de Hola. 
   4. Haga clic en **Crear**. 
5. Cuando haya finalizado el proceso de clonación de hello, debe inicializar Hola clonar volumen. Inicie el Administrador del servidor y, a continuación, inicie Administración de discos. Para obtener instrucciones detalladas, consulte [Montar volúmenes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Una vez inicializado, volumen de Hola se enumerará en hello **volúmenes** nodo Hola **ámbito** panel. 
   
    Si no ve los volúmenes de Hola que aparecen, actualice la lista de Hola de volúmenes (contextual hello **volúmenes** nodo y, a continuación, haga clic en **actualizar**).
6. Carpeta NTFS de hello abierto que contiene un volumen Hola clonado, expanda hello **volúmenes** nodo y, a continuación, abra Hola clonar volumen. Buscar archivo de Hola que desee toorecover y copiar toohello de volumen principal.
7. Después de restaurar el archivo hello, puede eliminar la carpeta NTFS de Hola que contiene Hola clonar un volumen.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Restaurar base de datos de administrador de instantáneas StorSimple Hola
Deben realizarse copias de la base de datos de administrador de instantáneas StorSimple de hello en el equipo de host de Hola. Si se produce un desastre o equipo de host de hello falla por alguna razón, a continuación, puede restaurar desde copia de seguridad de Hola. Crear copia de seguridad de base de datos de hello es un proceso manual.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback seguridad y restaurar base de datos de Hola
1. Detener Hola servicio de administración de StorSimple de Microsoft:
   
   1. Inicie el Administrador del servidor.
   2. En panel de administrador del servidor de hello, vaya a hello **herramientas** menú, seleccione **Services**.
   3. En hello **servicios** (ventana), seleccione hello **Microsoft StorSimple Management Service**.
   4. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **detener el servicio de hello**.
2. En el equipo de host de hello, examinar tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData es una carpeta oculta.
   > 
   > 
3. Buscar archivo XML del catálogo hello, copiar el archivo de Hola y almacenar Hola copiar en una ubicación segura o en la nube de Hola. Si se produce un error en el host de hello, puede usar este archivo de copia de seguridad toohelp recuperar hello las políticas de backup que creó en el Administrador de instantáneas de StorSimple.
   
    ![Archivo de catálogo de copia de seguridad de Azure StorSimple](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Reinicie Hola servicio de administración de StorSimple de Microsoft: 
   
   1. En panel de administrador del servidor de hello, vaya a hello **herramientas** menú, seleccione **Services**.
   2. En hello **servicios** (ventana), seleccione hello **Microsoft StorSimple Management Service**.
   3. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **reiniciar servicio hello**.
5. En el equipo de host de hello, examinar tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
6. Eliminar el archivo XML del catálogo hello y reemplazarla con la versión de copia de seguridad de Hola que ha creado. 
7. Haga clic en hello escritorio Administrador de instantáneas StorSimple icono toostart Administrador de instantáneas StorSimple. 

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre [mediante el Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga más información sobre las [tareas y flujos de trabajo de Snapshot Manager de StorSimple](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

