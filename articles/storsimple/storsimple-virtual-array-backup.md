---
title: tutorial de copia de seguridad de Azure StorSimple Virtual Array aaaMicrosoft | Documentos de Microsoft
description: "Describe cómo se comparte tooback de matriz Virtual de StorSimple y volúmenes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Copia de seguridad de recursos compartidos o volúmenes de la matriz virtual de StorSimple

## <a name="overview"></a>Información general

Hola StorSimple Virtual Array es un híbrido en la nube local virtual dispositivo de almacenamiento que se pueden configurar como un servidor de archivos o un servidor de iSCSI. matriz virtual Hola permite a Hola usuario toocreate copias de seguridad programadas y manuales de todos los recursos compartidos de Hola o volúmenes en el dispositivo de Hola. Cuando se configura como servidor de archivos, también permite la recuperación a nivel de elemento. Este tutorial describe cómo programar toocreate y copias de seguridad manuales y realizar la recuperación de nivel de elemento toorestore un archivo eliminado en la matriz virtual.

Este tutorial aplica toohello StorSimple Virtual sólo arreglos de discos. Para obtener información sobre la 8000 serie, vaya demasiado[crear una copia de seguridad de dispositivo de la 8000 serie](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Crear copias de seguridad de los recursos compartidos y volúmenes

Las copias de seguridad proporcionan seguridad a partir de un momento específico y mejoran la capacidad de recuperación, al mismo tiempo que reducen los tiempos de restauración de recursos compartidos y volúmenes. Puede hacer una copia de seguridad de un recurso compartido o de un volumen de su dispositivo StorSimple de dos maneras: **Programada** o **Manual**. Cada uno de los métodos de Hola se describe en las secciones siguientes de Hola.

## <a name="change-hello-backup-start-time"></a>Cambiar la hora de inicio de copia de seguridad de Hola

> [!NOTE]
> En esta versión, se crean copias de seguridad programadas por una directiva predeterminada que se ejecuta diariamente a una hora especificada y copia todos los recursos compartidos de Hola o volúmenes en el dispositivo de Hola. No es posible toocreate directivas personalizadas de copias de seguridad programadas en este momento.


La matriz Virtual de StorSimple tiene una directiva de copia de seguridad predeterminada que se inicia en un momento determinado del día (22:30) y realiza una copia de todos los recursos compartidos de Hola o volúmenes en el dispositivo de hello una vez al día. Puede cambiar el tiempo de hello en qué copia de seguridad empieza a hello, pero hello y frecuencia de hello retención (que especifica el número de Hola de copias de seguridad tooretain) no se puede cambiar. Durante estas copias de seguridad, dispositivo virtual completa de Hola se copia. Potencialmente Esto podría afectar al rendimiento de hello de dispositivo de Hola y afectan a las cargas de trabajo de hello implementadas en dispositivos de Hola. Por lo tanto, es aconsejable que programe que las copias de seguridad se realicen en horas de poca actividad.

 copia de seguridad predeterminada de toochange Hola hora de inicio, siga Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>Hola toochange hora de inicio de directiva de copia de seguridad de hello predeterminada

1. Vaya demasiado**dispositivos**. se mostrará la lista de Hola de dispositivos registrados con el servicio de administrador de dispositivos de StorSimple. 
   
    ![Navegue toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Seleccione y haga clic en el dispositivo. Hola **configuración** hoja se mostrarán. Vaya demasiado**administrar > directivas de copia de seguridad**.
   
    ![seleccionar un dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. Hola **directivas de copia de seguridad** hoja, hora de inicio de hello predeterminada es 22:30. Puede especificar la nueva hora de inicio Hola para programación diaria de hello en la zona horaria del dispositivo.
   
    ![navegar por las directivas de toobackup](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Haga clic en **Guardar**.

### <a name="take-a-manual-backup"></a>Creación de una copia de seguridad manual

Además tooscheduled copias de seguridad, puede realizar una copia de seguridad manual (a petición) de los datos del dispositivo en cualquier momento.

#### <a name="toocreate-a-manual-backup"></a>toocreate una copia de seguridad manual

1. Vaya demasiado**dispositivos**. Seleccione el dispositivo y haga clic en **...**  en hello más a la derecha de la fila seleccionada de Hola. En el menú contextual de hello, seleccione **realizar copia de seguridad**.
   
    ![navegar por la copia de seguridad de tootake](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. Hola **realizar copia de seguridad** hoja, haga clic en **realizar copia de seguridad**. Todos los recursos compartidos de hello en el servidor de archivos de Hola o todos los volúmenes de hello en el servidor de iSCSI realizará copia de seguridad. 
   
    ![inicio de la copia de seguridad](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Se inicia una copia de seguridad a petición y verá que se ha iniciado un trabajo de copia de seguridad.
   
    ![inicio de la copia de seguridad](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Una vez que se haya completado correctamente el trabajo de hello, se le notificará de nuevo. a continuación, inicia el proceso de copia de seguridad de Hola.
   
    ![trabajo de copia de seguridad creado](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. progreso de hello tootrack de copias de seguridad de Hola y busque en detalles del trabajo hello, haga clic en la notificación de Hola. Esto le llevará demasiado **detalles del trabajo**.
   
     ![detalles del trabajo de copia de seguridad](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Una vez completada la copia de seguridad de hello, vaya demasiado**Administración > catálogo de copia de seguridad**. Verá una instantánea en la nube de todos los recursos compartidos de hello (o volúmenes) en el dispositivo.
   
    ![Copia de seguridad completada](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Ver copias de seguridad existentes
copias de seguridad existentes de tooview hello, realizar Hola pasos de hello portal de Azure.

#### <a name="tooview-existing-backups"></a>tooview copias de seguridad existentes

1. Vaya demasiado**dispositivos** hoja. Seleccione y haga clic en el dispositivo. Hola **configuración** hoja, vaya demasiado**Administración > catálogo de copia de seguridad**.
   
    ![Navegar por catálogo toobackup](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Especifique Hola después toobe criterios usado para filtrar:
   
    - **Intervalo de tiempo**: puede ser **Última hora**, **Últimas 24 horas**, **Últimos 7 días**, **Últimos 30 días**, **Último año** y **Fecha personalizada**.
    
    - **Dispositivos** : seleccione en lista de Hola de servidores de archivos o servidores iSCSI registrados con el servicio de administrador de dispositivos de StorSimple.
   
    - **Iniciado**: pueden ser **programados** automáticamente (por una directiva de copia de seguridad) o iniciados **manualmente** (por usted).
   
    ![Filtrar copias de seguridad](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Haga clic en **Apply**. Hello lista filtrada de las copias de seguridad aparece en hello **catálogo de copia de seguridad** hoja. Tenga en cuenta que no se pueden mostrar más de cien elementos de copia de seguridad en un momento dado.
   
    ![Catálogo de copias de seguridad actualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).

