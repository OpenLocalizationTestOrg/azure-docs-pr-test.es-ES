---
title: "aaaStorSimple Administrador de instantáneas y volúmenes | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento tooview y administrar volúmenes y copias de seguridad de tooconfigure."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>Use el Administrador de instantáneas StorSimple tooview y administrar volúmenes
## <a name="overview"></a>Información general
Puede utilizar Administrador de instantáneas StorSimple Hola **volúmenes** nodo (en hello **ámbito** panel) tooselect volúmenes y ver información acerca de ellos. Hola volúmenes se presentan como unidades que corresponden toohello montadas por host Hola. Hola **volúmenes** nodo muestra los volúmenes locales y los tipos de volúmenes que son compatibles con StorSimple, incluidos los volúmenes detectados mediante el uso de Hola de iSCSI y un dispositivo. 

Para obtener más información sobre los volúmenes admitidos, vaya demasiado[compatibilidad para varios tipos de volúmenes](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Lista de volúmenes en el panel Resultados](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Hola **volúmenes** nodo también le permite volver a examinar o eliminar volúmenes después de que el Administrador de instantáneas StorSimple detecta. 

Este tutorial explica cómo puede montar, inicializar y dar formato a volúmenes y usar luego Administrador de instantáneas StorSimple para:

* Ver información acerca de volúmenes 
* Eliminar volúmenes
* Volver a examinar volúmenes 
* Configurar un volumen básico y realizar una copia de seguridad
* Configurar un volumen reflejado dinámico y realizar una copia de seguridad

> [!NOTE]
> Todos los de hello **volumen** nodo acciones también están disponibles en hello **acciones** panel.
> 
> 

## <a name="mount-volumes"></a>Montaje de volúmenes
Hola de uso siguiente procedimiento toomount, inicializar y formatear volúmenes de StorSimple. Este procedimiento utiliza la administración de discos, una utilidad del sistema para administrar los discos duros y los volúmenes correspondientes Hola o particiones. Para obtener más información acerca de la administración de discos, vaya demasiado[administración de discos](https://technet.microsoft.com/library/cc770943.aspx) en el sitio Web de Microsoft TechNet Hola.

#### <a name="toomount-volumes"></a>volúmenes de toomount
1. En el equipo host, inicie el iniciador iSCSI de Microsoft de Hola.
2. Proporcione una de las direcciones IP de la interfaz de hello como portal de destino de Hola o la dirección IP de detección y conecte el dispositivo de toohello. Después de conecta el dispositivo de hello, volúmenes de hello dejarán de estar accesible tooyour sistema de Windows. Para obtener más información acerca del uso del iniciador iSCSI de Microsoft hello, vaya toohello sección "Dispositivo de destino de iSCSI de tooan de conexión" [iniciador iSCSI de instalar y configurar Microsoft][1].
3. Use cualquiera de hello después opciones toostart administración de discos:
   
   * Escriba Diskmgmt.msc Hola **ejecutar** cuadro.
   * Inicie el administrador del servidor, expanda hello **almacenamiento** nodo y, a continuación, seleccione **administración de discos**.
   * Iniciar **herramientas administrativas**, expanda hello **administración de equipos** nodo y, a continuación, seleccione **administración de discos**. 
     
     > [!NOTE]
     > Debe usar privilegios de administrador toorun administración de discos.
     > 
     > 
4. Tomar volúmenes hello en línea:
   
   1. En Administración de discos, haga clic con el botón derecho en cualquier volumen marcado **Sin conexión**.
   2. Haga clic en **Reactivar disco**. Hola disco debe marcarse **Online** después Hola se vuelva a activar.
5. Inicializar volúmenes de hello:
   
   1. Haga clic en volúmenes de hello detectado.
   2. En el menú de hello, seleccione **inicializar disco**.
   3. Hola **inicializar disco** cuadro de diálogo, discos de hello select que desee tooinitialize y, a continuación, haga clic en **Aceptar**.
6. Dé formato a volúmenes simples:
   
   1. Haga clic en un volumen que desea tooformat.
   2. En el menú de hello, seleccione **nuevo volumen Simple**.
   3. Usar el volumen hello tooformat de hello nuevo volumen Simple asistente:
      
      * Especifique el tamaño del volumen de Hola.
      * Proporcione una letra de unidad.
      * Seleccione el sistema de archivos NTFS de Hola.
      * Especifique un tamaño de unidad de asignación de 64 KB.
      * Realice un formateo rápido.
7. Dé formato a volúmenes de varias particiones. Para obtener instrucciones, consulte toohello sección "Particiones y volúmenes" [Implementing Disk Management](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Visualización de información acerca de los volúmenes
Usar hello siguiente procedimiento tooview información acerca de los volúmenes de StorSimple de Azure y local.

#### <a name="tooview-volume-information"></a>información de volumen de tooview
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple. 
2. Hola **ámbito** panel, haga clic en hello **volúmenes** nodo. Aparece una lista de los volúmenes locales y montados, incluidos todos los volúmenes de StorSimple de Azure, en hello **resultados** panel. Hola columnas Hola **resultados** panel son configurables. (Menú contextual hello **volúmenes** nodo, seleccione **vista**y, a continuación, seleccione **agregar o quitar columnas**.)
   
    ![Configurar columnas de Hola](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Columna Resultados | Descripción |
   |:--- |:--- |
   |  Nombre |Hola **nombre** columna contiene Hola unidad letra asignada tooeach detectado volumen. |
   |  Dispositivo |Hola **dispositivo** columna contiene la dirección IP de hello del equipo de host de hello dispositivo toohello conectado. |
   |  Nombre del volumen del dispositivo |Hola **nombre de volumen del dispositivo** columna contiene el nombre de Hola de Hola dispositivo volumen toowhich Hola seleccionada pertenece el volumen. Este es el nombre de volumen de hello definido en hello portal de Azure para ese volumen específico. |
   |  Rutas de acceso |Hola **rutas de acceso** columna muestra el volumen de toohello de ruta de acceso de Hola. Se trata de hello unidad letra o punto de montaje en qué Hola volumen está accesible en el equipo de host de Hola. |

## <a name="delete-a-volume"></a>Eliminar un volumen
Usar hello siguiendo el procedimiento toodelete un volumen desde el Administrador de instantáneas de StorSimple.

> [!NOTE]
> No se puede eliminar un volumen si forma parte de un grupo de volúmenes. (opción de eliminación de hello no está disponible para los volúmenes que son miembros de un grupo de volúmenes). Debe eliminar Hola todo grupo toodelete Hola volumen.

#### <a name="toodelete-a-volume"></a>toodelete un volumen
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en hello **volúmenes** nodo. 
3. Hola **resultados** panel, volumen de Hola de menú contextual que desea toodelete.
4. En el menú de hello, haga clic en **eliminar**. 
   
    ![Eliminar un volumen](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Hola **Eliminar volumen** aparece el cuadro de diálogo. Tipo de **confirmar** en Hola cuadro de texto y, a continuación, haga clic en **Aceptar**.
6. De forma predeterminada, Administrador de instantáneas StorSimple realiza una copia de seguridad de un volumen antes de eliminarlo. Esta precaución puede protegerle frente a pérdidas de datos si Hola eliminación es accidental. Administrador de instantáneas StorSimple muestra un **instantánea automática** recibe un mensaje de progreso mientras realiza una copia de volumen de Hola. 
   
    ![Mensaje de instantánea automático](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Volver a examinar volúmenes
Usar hello siguiendo el procedimiento toorescan Hola volúmenes conectados tooStorSimple Administrador de instantáneas.

#### <a name="toorescan-hello-volumes"></a>volúmenes de hello toorescan
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **volúmenes**y, a continuación, haga clic en **volver a examinar volúmenes**.
   
    ![Volver a examinar volúmenes](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Este procedimiento sincroniza la lista de volúmenes de hello con el Administrador de instantáneas de StorSimple. Los cambios, como nuevos volúmenes o volúmenes eliminados, se verán reflejados en los resultados de Hola.

## <a name="configure-and-back-up-a-basic-volume"></a>Configuración y copia de seguridad de un volumen básico
Usar hello siguiendo el procedimiento tooconfigure una copia de seguridad de un volumen básico y, a continuación, iniciar inmediatamente una copia de seguridad o crear una directiva de copias de seguridad programadas.

### <a name="prerequisites"></a>Requisitos previos
Antes de empezar:

* Asegúrese de que ese dispositivo de StorSimple de Hola y equipo host estén configurados correctamente. Para obtener más información, consulte demasiado[implementar el dispositivo de StorSimple local](storsimple-deployment-walkthrough-u2.md).
* Instalación y configuración de Administrador de instantáneas StorSimple Para obtener más información, consulte demasiado[implementar Administrador de instantáneas de StorSimple](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>tooconfigure copia de seguridad de un volumen básico
1. Crear un volumen básico en el dispositivo StorSimple Hola.
2. Montar, inicializar y formatear el volumen de hello tal y como se describe en [montar volúmenes](#mount-volumes). 
3. Haga clic en el icono de administrador de instantáneas de StorSimple de hello en el escritorio. Aparecerá la ventana del Administrador de instantáneas StorSimple Hola. 
4. Hola **ámbito** panel, contextual hello **volúmenes** nodo y, a continuación, seleccione **volver a examinar volúmenes**. Cuando haya finalizado el examen de hello, debería aparecer una lista de volúmenes en hello **resultados** panel. 
5. Hola **resultados** panel, haga clic en el volumen de hello y, a continuación, seleccione **crear grupo de volúmenes**. 
   
    ![Crear grupo de volúmenes](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. Hola **crear grupo de volúmenes** cuadro de diálogo, escriba un nombre para el grupo de volúmenes de hello, asignar volúmenes tooit y, a continuación, haga clic en **Aceptar**.
7. Hola **ámbito** panel, expanda hello **grupos de volúmenes** nodo. nuevo grupo de volúmenes Hola debería aparecer bajo hello **grupos de volúmenes** nodo. 
8. Haga clic en el nombre del grupo de volúmenes de Hola.
   
   * Haga clic en un trabajo de copia de seguridad (a petición) interactivo, toostart **hacer copia de seguridad**. 
   * Haga clic en una copia de seguridad automática, tooschedule **Crear directiva de copia de seguridad**. En hello **General** página, seleccione un grupo de volúmenes en lista de Hola. En hello **programación** página, escriba los detalles de la programación de Hola. Cuando haya terminado, haga clic en **Aceptar**. 
9. tooconfirm que Hola trabajo de copia de seguridad se ha iniciado, expanda hello **trabajos** nodo Hola **ámbito** panel y, a continuación, haga clic en hello **ejecutando** nodo. lista de Hola de trabajos en ejecución actualmente aparece en hello **resultados** panel. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Configuración y copia de seguridad de un volumen reflejado dinámico
Hola completa después de la copia de seguridad de tooconfigure de pasos de un volumen reflejado dinámico:

* Paso 1: Use Administración de discos toocreate un volumen reflejado dinámico. 
* Paso 2: Copia de seguridad Use el Administrador de instantáneas de StorSimple tooconfigure.

### <a name="prerequisites"></a>Requisitos previos
Antes de empezar:

* Asegúrese de que ese dispositivo de StorSimple de Hola y equipo host estén configurados correctamente. Para obtener más información, consulte demasiado[implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).
* Instalación y configuración de Administrador de instantáneas StorSimple Para obtener más información, consulte demasiado[implementar Administrador de instantáneas de StorSimple](storsimple-snapshot-manager-deployment.md).
* Configure dos volúmenes en el dispositivo StorSimple Hola. (En los ejemplos de hello, son volúmenes disponibles hello **Disk 1** y **disco 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Paso 1: Use Administración de discos toocreate un volumen reflejado dinámico
Administración de discos es una utilidad del sistema para administrar los discos duros y los volúmenes de Hola o particiones que contienen. Para obtener más información acerca de la administración de discos, vaya demasiado[administración de discos](https://technet.microsoft.com/library/cc770943.aspx) en el sitio Web de Microsoft TechNet Hola.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate un volumen reflejado dinámico
1. Use cualquiera de hello después opciones toostart administración de discos: 
   
   * Abra hello **ejecutar** , escriba **Diskmgmt.msc**, y presione ENTRAR.
   * Inicie el administrador del servidor, expanda hello **almacenamiento** nodo y, a continuación, seleccione **administración de discos**. 
   * Iniciar **herramientas administrativas**, expanda hello **administración de equipos** nodo y, a continuación, seleccione **administración de discos**. 
2. Asegúrese de que tiene dos volúmenes disponibles en el dispositivo StorSimple Hola. (En el ejemplo de Hola, son volúmenes disponibles hello **Disk 1** y **disco 2**.) 
3. En la ventana de administración de discos de hello en columna de la derecha Hola Hola inferior del panel de, haga clic en **Disk 1** y seleccione **nuevo volumen reflejado**. 
   
    ![Nuevo volumen reflejado](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. En hello **nuevo volumen reflejado** página del asistente, haga clic en **siguiente**.
5. En hello **seleccionar discos** , seleccione **disco 2** en hello **seleccionados** panel, haga clic en **agregar**y, a continuación, haga clic en **siguiente**. 
6. En hello **asignar letra de unidad o ruta de acceso** página, acepte los valores predeterminados de hello y, a continuación, haga clic en **siguiente**. 
7. En hello **formatear volumen** página Hola **tamaño de la unidad de asignación** cuadro, seleccione **64K**. Seleccione hello **realizar un formato rápido** casilla de verificación y, a continuación, haga clic en **siguiente**. 
8. En hello **finalización Hola nuevo volumen reflejado** página, revise la configuración y, a continuación, haga clic en **finalizar**. 
9. Aparece un mensaje tooindicate que Hola disco básico será tooa convertido de disco dinámico. Haga clic en **Sí**.
   
    ![Mensaje de conversión de disco dinámico](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. En Administración de discos, compruebe que los discos 1 y 2 se muestren como volúmenes reflejados dinámicos. (**Dinámica** debe aparecer en la columna de estado de Hola y color de barra de capacidad de hello debería cambiar toored, que indica un volumen reflejado.) 
    
    ![Discos dinámicos reflejados de Administración de discos](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Paso 2: Copia de seguridad tooconfigure Use el Administrador de instantáneas StorSimple
Usar hello siguiendo el procedimiento tooconfigure un volumen reflejado dinámico y, a continuación, iniciar inmediatamente una copia de seguridad o crear una directiva de copias de seguridad programadas.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>tooconfigure copia de seguridad de un volumen reflejado dinámico
1. Haga clic en el icono de administrador de instantáneas de StorSimple de hello en el escritorio. Aparecerá la ventana del Administrador de instantáneas StorSimple Hola. 
2. Hola **ámbito** panel, contextual hello **volúmenes** nodo y seleccione **volver a examinar volúmenes**. Cuando haya finalizado el examen de hello, debería aparecer una lista de volúmenes en hello **resultados** panel. volumen reflejado dinámico de Hello aparece como un único volumen. 
3. Hola **resultados** panel, haga clic en el volumen reflejado dinámico de hello y, a continuación, haga clic en **crear grupo de volúmenes**. 
4. Hola **crear grupo de volúmenes** cuadro de diálogo, escriba un nombre para el grupo de volúmenes de hello, asignar Hola volumen reflejado dinámico toothis grupo y, a continuación, haga clic en **Aceptar**. 
5. Hola **ámbito** panel, expanda hello **grupos de volúmenes** nodo. nuevo grupo de volúmenes Hola debería aparecer bajo hello **grupos de volúmenes** nodo. 
6. Haga clic en el nombre del grupo de volúmenes de Hola. 
   
   * Haga clic en un trabajo de copia de seguridad (a petición) interactivo, toostart **hacer copia de seguridad**. 
   * Haga clic en una copia de seguridad automática, tooschedule **Crear directiva de copia de seguridad**. En hello **General** página, grupo de volúmenes de hello seleccione de la lista de Hola. En hello **programación** página, escriba los detalles de la programación de Hola. Cuando haya terminado, haga clic en **Aceptar**. 
7. Puede supervisar el trabajo de copia de seguridad de hello mientras se ejecuta. Hola **ámbito** panel, expanda hello **trabajos** nodo y, a continuación, haga clic en **ejecutando**, detalles del trabajo Hola aparecen en hello **resultados** panel. Cuando finaliza el trabajo de copia de seguridad de hello, detalles de hello son transferido toohello **últimas 24** horas de trabajo de lista. 

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple toocreate y administrar grupos de volúmenes](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
