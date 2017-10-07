---
title: "contraseña de administrador de dispositivos de StorSimple Virtual Array aaaChange | Documentos de Microsoft"
description: "Describe cómo toouse Hola o portal de Azure o la contraseña de administrador dispositivo Hola de toochange de la interfaz de usuario de web de StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Cambiar contraseña del Administrador de dispositivos de StorSimple Virtual Array de Hola a través del Administrador de dispositivos de StorSimple

## <a name="overview"></a>Información general

Cuando usas tooaccess de interfaz de Windows PowerShell de Hola Hola StorSimple Virtual Array, estás tooenter requiere una contraseña de administrador de dispositivos. Cuando el dispositivo de StorSimple de hello en primer lugar se aprovisionan y se inicia, contraseña predeterminada de hello es *Password1*. Para la seguridad de Hola de los datos, contraseña predeterminada de hello expira hello primera vez que inicie una sesión y es necesario toochange esta contraseña.

También puede usar cualquier hello web local interfaz de usuario o hello toochange portal Azure Hola contraseña de administrador en cualquier momento después de que el dispositivo de Hola se implementa en el entorno de producción. En este artículo se describe cada uno de estos procedimientos.

 ![hoja de dispositivos](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Usar hello toochange portal Azure Hola contraseña

Realizar Hola siguiendo los pasos toochange Hola contraseña de administrador a través de hello portal de Azure.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>contraseña de administrador de dispositivos de toochange Hola a través de hello portal de Azure

1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **administración** sección, haga clic en **dispositivos**. Se abrirá hello **dispositivos** hoja que enumera todos los dispositivos de StorSimple Virtual Array.

2. Hola **dispositivos** hoja, haga doble clic en el dispositivo de Hola que requiere un cambio de contraseña.

3. Hola **configuración** hoja para el dispositivo, haga clic en **seguridad**.

4. Hola **configuración de seguridad** hoja, Hola siguientes:
   
   1. Desplácese hacia abajo toohello **contraseña de administrador de dispositivos** sección. Proporcione una contraseña de administrador que tenga entre 8 caracteres too15.
   2. Confirmar contraseña Hola.
   3. Haga clic en **guardar** princip Hola de hoja de Hola.

contraseña de administrador de dispositivos de Hola se ha actualizado. Puede usar este dispositivo de contraseña modificada tooaccess Hola localmente.

![Hoja Configuración de seguridad](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Usar hello web local UI toochange Hola contraseña

Realizar Hola siguiendo los pasos toochange Hola contraseña de administrador a través de la interfaz de usuario de web local Hola.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>contraseña del Administrador de dispositivos de toochange Hola a través de la interfaz de usuario de web local Hola

1. En la interfaz de usuario web local de hello, haga clic en **mantenimiento** > **cambio de contraseña** para el dispositivo.
   
    ![cambiar password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Escriba hello **contraseña actual**.
3. Introduzca una **Nueva contraseña**. contraseña de Hello debe ser al menos 8 caracteres. Debe contener 3 de 4 siguiente hello: caracteres en mayúsculas, minúsculas, numéricos y especiales.
   
    Tenga en cuenta que la contraseña no puede ser igual que Hola últimas 24 contraseñas Hola.
4. Vuelva a escribir Hola contraseña tooconfirm lo.
   
    ![cambiar password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. En la parte inferior de Hola de página de hello, haga clic en **aplicar**. Ahora se aplica la nueva contraseña de Hola. Si el cambio de contraseña hello no se realiza correctamente, verá Hola siguiente error:
   
    ![error de contraseña](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Una vez que se actualizó correctamente la contraseña de hello, se le notificará. A continuación, puede usar este dispositivo de contraseña modificada tooaccess Hola localmente.


## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[administrar la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).

