---
title: "Instalación de actualizaciones en la matriz virtual de StorSimple | Microsoft Docs"
description: "Se describe cómo usar la interfaz de usuario web de la matriz virtual de StorSimple para aplicar actualizaciones mediante el portal y el método de revisiones."
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
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Instalación de actualizaciones en la matriz virtual de StorSimple
## <a name="overview"></a>Información general
En este artículo se describen los pasos necesarios para instalar actualizaciones en la matriz virtual de StorSimple mediante la interfaz de usuario web local y el Portal de Azure clásico. Deberá aplicar alguna actualización o revisión de software para mantener actualizada la matriz virtual de StorSimple. 

Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo. Dado que la matriz virtual de StorSimple es un dispositivo de nodo único, se interrumpirá cualquier operación de E/S que esté en curso y el dispositivo permanecerá un rato inactivo. 

Antes de aplicar una actualización, se recomienda que desconecte primero los volúmenes o recursos compartidos en el host y, luego, el dispositivo. Esto minimizará la posibilidad de daños en los datos.

> [!IMPORTANT]
> Si está ejecutando Update 0.1 o versiones de software de GA, debe utilizar el método de revisión a través de la interfaz de usuario web local para instalar Update 0.3. Si ejecuta Update 0.2, recomendamos que instale las actualizaciones a través del Portal de Azure clásico.
> 
> 

## <a name="use-the-local-web-ui"></a>Uso de la interfaz de usuario web local
Se pueden seguir dos pasos con la interfaz de usuario web local:

* Descargar la actualización o la revisión
* Instalar la actualización o la revisión

### <a name="download-the-update-or-the-hotfix"></a>Descargar la actualización o la revisión
Realice los pasos siguientes para descargar la actualización de software desde el catálogo de Microsoft Update.

#### <a name="to-download-the-update-or-the-hotfix"></a>Para descargar la actualización o la revisión
1. Inicie Internet Explorer y vaya a [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Si esta es la primera vez que utiliza el Catálogo de Microsoft Update en este equipo, haga clic en **Instalar** cuando se le solicite que instale el complemento del Catálogo de Microsoft Update.
3. En el cuadro de búsqueda del Catálogo de Microsoft Update, escriba el número de Knowledge Base correspondiente a la revisión que quiera descargar. Escriba **3182061** para Update 0.3 y luego haga clic en **Buscar**.
   
    Aparece la lista de revisiones, por ejemplo, **StorSimple Virtual Array Update 0.3**.
   
    ![Búsqueda de catálogo](./media/storsimple-ova-install-update-01/download1.png)
4. Haga clic en **Agregar**. La actualización se agrega a la cesta.
5. Haga clic en **Ver cesta**.
6. Haga clic en **Descargar**. Especifique o **busque** una ubicación local en la que quiera que aparezcan las descargas. Las actualizaciones se descargan en la ubicación especificada y se colocan en una subcarpeta con el mismo nombre que la actualización. La carpeta también se puede copiar en un recurso compartido de red que sea accesible desde el dispositivo.
7. Abra la carpeta copiada, debería ver un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`. Este archivo se utiliza para instalar la actualización o revisión.

### <a name="install-the-update-or-the-hotfix"></a>Instalar la actualización o la revisión
Antes de instalar la actualización o la revisión, asegúrese de que tiene la actualización o la revisión descargada de forma local en el host o que puede acceder a ella a través de un recurso compartido de red. 

Utilice este método para instalar actualizaciones en un dispositivo que ejecute las versiones de software Update 0.1 o GA. Este procedimiento tarda menos de 2 minutos en completarse. Realice los pasos siguientes para instalar la actualización o revisión.

#### <a name="to-install-the-update-or-the-hotfix"></a>Instalar la actualización o la revisión
1. En la interfaz de usuario web local, vaya a **Mantenimiento** > **Actualización de software**.
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. En **Update file path**(Ruta de acceso del archivo de actualización), escriba el nombre del archivo de actualización o de revisión. Asimismo, también puede acceder al archivo de instalación de la actualización o de la revisión si está en un recurso compartido de red. Haga clic en **Aplicar**.
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. Se mostrará una advertencia. Dado que se trata de un dispositivo de nodo único, una vez aplicada la actualización, se reiniciará el dispositivo y habrá un tiempo de inactividad. Haga clic en el icono de marca de verificación.
   
   ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. Se inicia la actualización. Una vez que el dispositivo se actualice correctamente, este se reiniciará. La interfaz de usuario local no será accesible durante este tiempo.
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. Una vez completado el reinicio, se le llevará a la página de **inicio de sesión** . Para comprobar que el software del dispositivo se ha actualizado, en la interfaz de usuario de web local, vaya a **Mantenimiento** > **Actualización de software**. La versión de software mostrada debe ser **10.0.0.0.0.10288.0** para Update 0.3.
   
   > [!NOTE]
   > Las versiones de software se muestran de forma ligeramente distinta en la interfaz de usuario web local y el Portal de Azure clásico. Por ejemplo, la misma versión aparece como **10.0.0.0.0.10288** en la interfaz de usuario web local y como **10.0.10288.0** en el Portal de Azure clásico. 
   > 
   > 
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a>Uso del Portal de Azure clásico
Si se ejecuta Update 0.2, recomendamos que instale las actualizaciones a través del Portal de Azure clásico. El procedimiento del Portal requiere que el usuario examine, descargue e instale las actualizaciones. Este procedimiento tarda aproximadamente 7 minutos en completarse. Realice los pasos siguientes para instalar la actualización o revisión.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Una vez que la instalación esté completa (podrá comprobarlo cuando el estado del trabajo esté al 100 %), vaya a **Dispositivos > Mantenimiento > Actualizaciones de software**. La versión de software que aparece debe ser 10.0.10288.0.

![actualizar dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).

