---
title: "aaaInstall actualización 0,6 en StorSimple Virtual Array | Documentos de Microsoft"
description: "Describe cómo toouse actualizaciones de tooapply de la interfaz de usuario de hello StorSimple Virtual Array web mediante hello Azure portal y la revisión (método)"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a>Instalación de Update 0.6 en StorSimple Virtual Array

## <a name="overview"></a>Información general

Este artículo describe Hola pasos necesarios tooinstall actualización 0,6 en la matriz Virtual de StorSimple a través de la interfaz de usuario de web local de Hola y Hola portal de Azure. Aplicar hello tookeep de revisiones o actualizaciones de software de la matriz Virtual de StorSimple actualizado.

Antes de aplicar una actualización, se recomienda que permitirán que los volúmenes de Hola o recursos compartidos sin conexión en hello hospedan en primer lugar y, a continuación, Hola dispositivo. Esto minimizará la posibilidad de daños en los datos. Después de hello volúmenes o recursos compartidos sin conexión, también debe tener manual de un copia de seguridad del dispositivo de Hola.

> [!IMPORTANT]
> - Actualización 0,6 corresponde demasiado**10.0.10293.0** versión de software en el dispositivo. Para obtener información sobre lo que es nuevo en esta actualización, vaya demasiado[notas de la versión de actualización de 0,6](storsimple-virtual-array-update-06-release-notes.md).
>
> - Si está ejecutando Update 0,2 o una versión posterior, se recomienda que instala actualizaciones de Hola a través de hello portal de Azure. Si está ejecutando Update 0,1 o versiones de software de disponibilidad general, debe usar método de revisión de hello a través de la interfaz de usuario tooinstall actualización 0,6 de hello web local.
>
> - Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo. Dado que hello StorSimple Virtual Array es un dispositivo de nodo único, se interrumpe cualquier E/S en curso y el dispositivo produce un tiempo de inactividad.

## <a name="use-hello-azure-portal"></a>Usar hello portal de Azure

Si ejecuta Update 0.2 y versiones posteriores, se recomienda que instale las actualizaciones a través de hello portal de Azure. procedimiento portal Hola requiere Hola usuario tooscan, descargue e instale las actualizaciones de Hola. Este procedimiento toma toocomplete unos 7 minutos. Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Después de hello instalación está completa, vaya tooyour servicio de administrador de dispositivos de StorSimple. Seleccione **dispositivos** y, a continuación, seleccione y haga clic en el dispositivo de Hola que acaba de actualizar. Vaya demasiado**configuración > Administrar > actualizaciones del dispositivo**. Hello muestra la versión de software debe tener **10.0.10293.0**.

## <a name="use-hello-local-web-ui"></a>Usar la interfaz de usuario de web local Hola

Cuando se usa la interfaz de usuario de web local de hello, hay dos pasos:

* Descargar la actualización de Hola o una revisión de Hola
* Instalar la actualización de Hola o revisión de Hola

### <a name="download-hello-update-or-hello-hotfix"></a>Descargar la actualización de Hola o una revisión de Hola

Realizar Hola tras la actualización de software de pasos toodownload Hola de Hola catálogo de Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>revisión de actualización u Hola Hola toodownload

1. Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Si utilizas Hola catálogo de Microsoft Update para hello primera vez en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.

3. En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de hello desea toodownload. Escriba **4023268** para Update 0.6 y, luego, haga clic en **Buscar**.
   
    Hello revisión aparece listado, por ejemplo, **StorSimple Virtual Array Update 0,6**.
   
    ![Búsqueda de catálogo](./media/storsimple-virtual-array-install-update-06/download1.png)

4. Haga clic en **Descargar**.

5. Debería ver cinco toodownload de archivos. Descargar cada una de esas carpetas tooa de archivos. carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.

6. Abra la carpeta de Hola donde se encuentran los archivos de saludo.
    ![Archivos de paquete de Hola](./media/storsimple-virtual-array-install-update-06/update06folder.png)

    Se ve lo siguiente:
    -  Un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`. Este archivo es un software de dispositivo de hello tooupdate usado.
    - Un archivo de paquete del agente de supervisión de Geneva `GenevaMonitoringAgentPackageInstaller`. Este archivo es el agente del servicio (MDS) de supervisión y diagnóstico de hello tooupdate usado. Haga doble clic en el archivo cab de Hola. Aparece un archivo _.msi_. Archivo de SELECT hello, menú contextual y, a continuación, **extraer** archivo hello. Usar hello _.msi_ agente de archivos tooupdate Hola.

        ![Extracción del archivo de actualización del agente de MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > No es necesario el agente MDS hello tooupdate si está ejecutando StorSimple Update 0,5 (0.0.10293.0).

    - Tres archivos que contienen actualizaciones críticas de seguridad de Windows: `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64` y `windows8.1-kb4019213-x64`.


### <a name="install-hello-update-or-hello-hotfix"></a>Instalar la actualización de Hola o revisión de Hola

Instalación de actualización o revisión de toohello anteriores, asegúrese de que tiene Hola actualización o revisión Hola descargado localmente en el host o accesible a través de un recurso compartido de red.

Usar este método tooinstall actualiza en un dispositivo que ejecuta GA o actualizar 0.1 versiones de software. Este procedimiento toma toocomplete de 12 minutos aproximadamente. Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>revisión de actualización u Hola Hola tooinstall

1. En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **actualización de Software**. Tome nota de la versión de software de Hola que se está ejecutando. Si está ejecutando **10.0.10290.0**, no es necesario tooupdate agente MDS hello en el paso 6.
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. En **ruta de acceso de archivo de actualización**, escriba el nombre de archivo de hello para la actualización de Hola u Hola revisión. También puede examinar los archivos de instalación de actualización o revisión de toohello si se coloca en un recurso compartido de red. Haga clic en **Apply**.
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Se mostrará una advertencia. Proporcionado Hola matriz virtual es un dispositivo de nodo único, después de que se aplica la actualización de hello, Hola dispositivo se reinicia y no hay tiempo de inactividad. Haga clic en el icono de verificación de Hola.
   
   ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. inicia la actualización de Hola. Después de que el dispositivo de Hola se actualizó correctamente, éste se reinicia. Hello interfaz de usuario local no es accesible durante este proceso.
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Una vez completado el reinicio de hello, se toman toohello **iniciar sesión en** página. tooverify que ha actualizado el software de dispositivo de hello, en web local de hello interfaz de usuario, vaya demasiado**mantenimiento** > **actualización de Software**. Hello muestra la versión de software debe tener **10.0.0.0.0.10293** de actualización de 0,6.
   
   > [!NOTE]
   > Se informan de versiones de software de Hola de forma ligeramente diferente en la interfaz de usuario de web local de Hola y Hola portal de Azure. Por ejemplo, Hola informes de interfaz de usuario web local **10.0.0.0.0.10293** y Hola informes del portal Azure **10.0.10293.0** para hello misma versión.
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. Omita este paso si se estaba ejecutando StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) antes de aplicar esta actualización. Realiza una nota de la versión de software de hello en el paso 1 antes de que comenzara tooupdate. Si estaba ejecutando Update 0.5, el agente MDS ya está actualizado.

    Si está ejecutando una versión de software anterior tooUpdate 0,5, Hola siguiente paso para usted es agente de tooupdate Hola MDS. Hola **actualización de Software** página, vaya toohello **ruta de acceso de archivo de actualización** y examinar toohello `GenevaMonitoringAgentPackageInstaller.msi` archivo. Repita los pasos del 2 al 4. Una vez reiniciado matriz virtual hello, inicie sesión en la interfaz de usuario de web local de Hola.

7. Repita el paso 2-4 tooinstall la seguridad de Windows de hello correcciones con archivos `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, y `windows8.1-kb4019213-x64`. matriz virtual Hola se reinicia después de todas las instalaciones y deberá toosign en la interfaz de usuario de web local Hola.

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).

