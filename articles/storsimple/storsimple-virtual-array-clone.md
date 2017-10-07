---
title: una copia de seguridad de StorSimple Virtual Array aaaClone | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooclone una copia de seguridad y recuperar un archivo de la matriz Virtual de StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Clonación a partir de una copia de seguridad de StorSimple Virtual Array

## <a name="overview"></a>Información general

Este artículo describe paso a paso cómo tooclone una conjunto de copia de los recursos compartidos o volúmenes en la matriz Virtual de Microsoft Azure StorSimple. copia de seguridad clonado Hello es toorecover usa un archivo eliminado o se pierden. artículo de Hello también incluye tooperform pasos detallados que una recuperación de nivel de elemento en la matriz Virtual de StorSimple configurada como un servidor de archivos.

## <a name="clone-shares-from-a-backup-set"></a>Clonación de recursos compartidos de un conjunto de copias de seguridad

**Antes de intentar recursos compartidos de tooclone, asegúrese de que haya espacio suficiente en hello dispositivo toocomplete esta operación.** tooclone desde una copia de seguridad, en hello [portal de Azure](https://portal.azure.com/), realizar Hola pasos.

#### <a name="tooclone-a-share"></a>tooclone un recurso compartido

1. Examinar demasiado**dispositivos** hoja. Seleccione el dispositivo, haga clic en él y, después, en **Recursos compartidos**. Seleccionar recurso compartido de Hola que desea tooclone, Hola recurso compartido tooinvoke Hola menú contextual. Seleccione **Clonar**.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. Hola **clon** hoja, haga clic en **copia de seguridad > seleccione** y, a continuación, Hola siguientes: 
   
   a.    Filtrar una copia de seguridad en este dispositivo basado en intervalo de tiempo de Hola. Puede elegir entre **Últimos 7 días**, **Últimos 30 días** y **Último año**.
   
   b.    En lista de Hola de copias de seguridad filtrados muestra, seleccione una copia de seguridad tooclone de.
   
   c.    Haga clic en **OK**.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. Hola **clon** hoja, haga clic en **destino configuración** y, a continuación, Hola siguientes:
   
   a.    Proporcione un nombre de recurso compartido. nombre de recurso compartido de Hello debe contener 3 y 127 caracteres.
   
   b.    Opcionalmente, proporcione una descripción de recurso compartido de hello clonado.
   
   c.    No se puede cambiar el tipo hello del recurso compartido de Hola que va a restaurar. Los recursos compartidos en niveles se clonan “por niveles”, mientras que los recursos compartidos anclados localmente como “anclados localmente”.
   
   d.    capacidad de Hola se establece como toohello de igual tamaño del recurso compartido de hello de que está clonando.
   
   e.    Asignar a los administradores de Hola para este recurso compartido. Una vez completada la clonación de hello, es posible que pueda toomodify propiedades del recurso compartido de Hola a través del explorador de archivos.
   
   f.    Haga clic en **Aceptar**.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Haga clic en **clon** toostart un trabajo de clonación. Una vez completado el trabajo de hello, inicia una operación de clonación hello y se le notificará. progreso de hello toomonitor de clonación, vaya toohello **trabajos** hoja y haga clic en hello tooview trabajo detalles del trabajo.
5. Después de clonar Hola se crea correctamente, vaya toohello Atrás **recursos compartidos** hoja en el dispositivo.
6. Ahora puede ver Hola nuevo clonado recurso compartido en la lista de Hola de recursos compartidos en el dispositivo. Los recursos compartidos en capas se clonarán “en capas”, mientras que los recursos compartidos anclados localmente se clonarán como “anclados localmente”.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Clonación de volúmenes a partir de un conjunto de copias de seguridad

tooclone desde una copia de seguridad, en el portal de Azure, hello tiene tooperform pasos similares toohello los al clonar un recurso compartido. una operación de clonación Hola clona el nuevo volumen de copia de seguridad tooa de hello en hello mismo dispositivo virtual; no se puede clonar tooa otro dispositivo.

#### <a name="tooclone-a-volume"></a>tooclone un volumen

1. Examinar demasiado**dispositivos** hoja. Seleccione el dispositivo, haga clic en él y, después, en **Volúmenes**. Volumen de hello Seleccio que desea tooclone, haga clic en el menú contextual de hello volumen tooinvoke Hola. Seleccione **Clonar**.
   
   ![Clonar un volumen](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. Hola **clon** hoja, haga clic en **copia de seguridad** y, a continuación, Hola siguientes: 
   
   a.    Filtrar una copia de seguridad en este dispositivo basado en intervalo de tiempo de Hola. Puede elegir entre **Últimos 7 días**, **Últimos 30 días** y **Último año**. 
   
   b.    En lista de Hola de copias de seguridad filtrados muestra, seleccione una copia de seguridad tooclone de.
   
   c.    Haga clic en **OK**.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. Hola **clon** hoja, haga clic en **configuración de volumen de destino** y, a continuación, Hola siguientes::
   
   a. nombre de dispositivo de Hola se rellena automáticamente.
   
   b. Proporcione un nombre de volumen para hello **clonar volumen**. nombre del volumen Hola debe contener 3 too127 caracteres.
   
   c. tipo de volumen de Hola se establece automáticamente el volumen original toohello. Los volúmenes en capas se clonan “en capas”, mientras que los volúmenes anclados localmente se clonan como “anclados localmente”.
   
   d. Para hello **hosts conectados**, haga clic en **seleccione**.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. Hola **hosts conectados** hoja, seleccione desde un ACR existente o agregar un nuevo ACR. tooadd un nuevo ACR, necesitará un nombre ACR tooprovide y IQN del host Hola. Haga clic en **Seleccionar**.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Haga clic en **clon** toolaunch un trabajo de clonación.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Después de crea el trabajo de clonación de hello, se iniciará la clonación. Una vez creado el clon hello, se muestra en la hoja de volúmenes de hello en el dispositivo. Tenga en cuenta que los volúmenes en capas se clonan “en capas”, mientras que los volúmenes anclados localmente se clonan como “anclados localmente”.
   
   ![Clonar una copia de seguridad](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Una vez que el volumen de hello aparece en pantalla, en la lista de Hola de volúmenes, volumen de hello está disponible para su uso. En el host de iniciador de iSCSI de hello, actualice la lista de Hola de destinos en la ventana de propiedades del iniciador de iSCSI. Un nuevo destino que contiene el nombre del volumen clonado Hola debe aparecer como 'inactive' en la columna de estado de Hola.
8. Seleccione el destino de Hola y haga clic en **conectar**. Una vez iniciador Hola destino toohello conectado, estado de hello debería cambiar demasiado**conectado**.
9. Hola **administración de discos** ventana, hello volúmenes montados aparecerán como se muestra en hello siguiente ilustración. Haga clic en el volumen de hello detectado (haga clic en el nombre del disco de hello) y, a continuación, haga clic en **Online**.

> [!IMPORTANT]
> Al intentar tooclone un volumen o un recurso compartido de un conjunto de copia de seguridad, si se produce un error en el trabajo de clonación de hello, un volumen de destino o recurso compartido puede seguirá creando en el portal de Hola. Es importante que elimine este volumen de destino o recurso compartido en el portal toominimize de hello los futuros problemas derivados de este elemento.
> 
> 

## <a name="item-level-recovery-ilr"></a>Recuperación a nivel de elemento (ILR)

Esta versión introduce la recuperación de nivel de elemento (ILR) de hello en una matriz Virtual de StorSimple configurado como un servidor de archivos. característica de Hello permite toodo de recuperación granular de archivos y carpetas desde una copia de seguridad de la nube de todos los recursos compartidos de hello en el dispositivo StorSimple Hola. Puede recuperar los archivos eliminados de las copias de seguridad recientes mediante un modelo de autoservicio.

Cada recurso compartido tiene un *.backups* carpeta que contiene las copias de seguridad más reciente de Hola. Puede navegar toohello copia de seguridad deseada, copie los archivos pertinentes y carpetas de copia de seguridad de Hola y restaurarlos. Esta característica elimina tooadministrators de llamadas para restaurar archivos de copias de seguridad.

1. Al realizar hello ILR, puede ver las copias de seguridad de Hola a través del explorador de archivos. Haga clic en recurso compartido específico Hola que desee toolook en copia de seguridad de Hola de. Verá un *.backups* carpeta creada en el recurso compartido de Hola que almacena todas las copias de seguridad de Hola. Expanda hello *.backups* copias de seguridad de carpeta tooview Hola. carpeta de Hello muestra hello exploded vista de jerarquía de copia de seguridad completa de Hola. Esta vista se crea a petición y por lo general tiene solo un par de toocreate segundos.
   
   las copias de cinco últimos seguridad Hola se muestran en este modo y pueden tener recuperación tooperform usa un nivel de elemento. Hello cinco copias de seguridad recientes incluyen ambos Hola programadas de manera predeterminada y Hola copias de seguridad manuales.
   
   * **Copias de seguridad programadas** denominadas &lt;nombreDeDispositivo&gt; DailySchedule-AAAAMMDD-HHMMSS-UTC.
   * **Copias de seguridad manuales** denominadas Ad-hoc-AAAAMMDD-HHMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Identificar la copia de seguridad de Hola que contiene la versión más reciente de Hola de archivo hello eliminado. Aunque el nombre de la carpeta de hello contiene una marca de tiempo UTC en cada uno de hello delante de los casos, tiempo de hello en qué Hola se creó la carpeta es hora del dispositivo real de hello cuando hello inicia copia de seguridad. Usar toolocate de marca de tiempo de carpeta Hola e identificar las copias de seguridad de Hola.

3. Localice la carpeta de Hola o el archivo hello que desee toorestore en copia de seguridad de Hola que identificó en el paso anterior de Hola. Tenga en cuenta que solo se pueden ver Hola archivos o carpetas que tienen permisos para. Si no puede acceder a determinados archivos o carpetas, póngase en contacto con un administrador de recursos compartidos. Administrador de Hello puede usar permisos de recurso compartido de explorador de archivos tooedit hello y proporcionarle acceso toohello archivo o carpeta específicos. Es una práctica recomendada que Hola Administrador de recurso compartido es un grupo de usuarios en lugar de un solo usuario.

4. Copiar archivo hello o hello toohello adecuado uso compartido de carpetas en el servidor de archivos de StorSimple.

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de cómo demasiado[administrar la matriz Virtual de StorSimple mediante la interfaz de usuario de web local hello](storsimple-ova-web-ui-admin.md).

