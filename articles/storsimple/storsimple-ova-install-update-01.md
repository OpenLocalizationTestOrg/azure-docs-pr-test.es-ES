---
title: Actualizaciones de aaaInstall en una matriz Virtual de StorSimple | Documentos de Microsoft
description: "Describe cómo toouse hello StorSimple Virtual Array web UI tooapply actualiza usando el método de portal y la revisión de hello"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Instalación de actualizaciones en la matriz virtual de StorSimple
## <a name="overview"></a>Información general
Este artículo describe Hola pasos tooinstall requiere actualizaciones en la matriz Virtual de StorSimple a través de la interfaz de usuario de web local de Hola y Hola portal de Azure clásico. Debe tookeep de revisiones o actualizaciones de software de tooapply la matriz Virtual de StorSimple actualizado. 

Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo. Dado que hello StorSimple Virtual Array es un dispositivo de nodo único, se interrumpe cualquier E/S en curso y el dispositivo produce un tiempo de inactividad. 

Antes de aplicar una actualización, se recomienda que permitirán que los volúmenes de Hola o recursos compartidos sin conexión en hello hospedan en primer lugar y, a continuación, Hola dispositivo. Esto minimizará la posibilidad de daños en los datos.

> [!IMPORTANT]
> Si está ejecutando Update 0,1 o versiones de software de disponibilidad general, debe usar el método de revisión de hello a través de la interfaz de usuario tooinstall update 0.3 de hello web local. Si está ejecutando Update 0.2, se recomienda que instale actualizaciones de Hola a través de hello portal de Azure clásico.
> 
> 

## <a name="use-hello-local-web-ui"></a>Usar la interfaz de usuario de web local Hola
Cuando se usa la interfaz de usuario de web local de hello, hay dos pasos:

* Descargar la actualización de Hola o una revisión de Hola
* Instalar la actualización de Hola o revisión de Hola

### <a name="download-hello-update-or-hello-hotfix"></a>Descargar la actualización de Hola o una revisión de Hola
Realizar Hola tras la actualización de software de pasos toodownload Hola de Hola catálogo de Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>revisión de actualización u Hola Hola toodownload
1. Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.
3. En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de hello desea toodownload. Escriba **3182061** para Update 0.3 y luego haga clic en **Buscar**.
   
    Hello revisión aparece listado, por ejemplo, **StorSimple Virtual Array Update 0.3**.
   
    ![Búsqueda de catálogo](./media/storsimple-ova-install-update-01/download1.png)
4. Haga clic en **Agregar**. actualización de Hola se agrega toohello cesta.
5. Haga clic en **Ver cesta**.
6. Haga clic en **Descargar**. Especifique o **examinar** tooa ubicación local donde desee Hola descarga tooappear. Hello las actualizaciones se descargan toohello ubicación especificada y se coloca en una subcarpeta con el mismo nombre como actualización de Hola de Hola. carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.
7. Abra Hola copiado la carpeta, debería ver un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`. Este archivo es utilizado tooinstall Hola actualización o revisión.

### <a name="install-hello-update-or-hello-hotfix"></a>Instalar la actualización de Hola o revisión de Hola
Instalación de actualización o revisión de toohello anteriores, asegúrese de que tiene Hola actualización o revisión Hola descargado localmente en el host o accesible a través de un recurso compartido de red. 

Usar este método tooinstall actualiza en un dispositivo que ejecuta GA o actualizar 0.1 versiones de software. Este procedimiento toma inferior toocomplete de 2 minutos. Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>revisión de actualización u Hola Hola tooinstall
1. En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **actualización de Software**.
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. En **ruta de acceso de archivo de actualización**, escriba el nombre de archivo de hello para la actualización de Hola u Hola revisión. También puede examinar los archivos de instalación de actualización o revisión de toohello si se coloca en un recurso compartido de red. Haga clic en **Apply**.
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. Se mostrará una advertencia. Debido a esto es un dispositivo de nodo único, después de que se aplica la actualización de hello, Hola dispositivo se reinicia y no hay tiempo de inactividad. Haga clic en el icono de verificación de Hola.
   
   ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. inicia la actualización de Hola. Después de que el dispositivo de Hola se actualizó correctamente, éste se reinicia. Hello interfaz de usuario local no es accesible durante este proceso.
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. Una vez completado el reinicio de hello, se toman toohello **iniciar sesión en** página. tooverify que ha actualizado el software de dispositivo de hello, en web local de hello interfaz de usuario, vaya demasiado**mantenimiento** > **actualización de Software**. Hello muestra la versión de software debe tener **10.0.0.0.0.10288.0** para actualización 0.3.
   
   > [!NOTE]
   > Se informan de versiones de software de Hola de forma ligeramente diferente en la interfaz de usuario de web local de Hola y Hola portal de Azure clásico. Por ejemplo, Hola informes de interfaz de usuario web local **10.0.0.0.0.10288** y Hola informes portal de Azure clásicos **10.0.10288.0** para hello misma versión. 
   > 
   > 
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Usar hello portal de Azure clásico
Si ejecuta Update 0.2, se recomienda que instale las actualizaciones a través de hello portal de Azure clásico. procedimiento portal Hola requiere Hola usuario tooscan, descargue e instale las actualizaciones de Hola. Este procedimiento toma toocomplete unos 7 minutos. Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Después de hello instalación está completa (tal y como se indica con el estado del trabajo al 100%), ir demasiado**dispositivos > Mantenimiento > actualizaciones de Software**. versión de software de muestra de Hola debe ser 10.0.10288.0.

![actualizar dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).

