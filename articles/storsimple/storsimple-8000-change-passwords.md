---
title: "aaaChange las contraseñas de StorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola toochange de servicio de administrador de dispositivos de StorSimple las contraseñas de administrador de administrador de instantáneas StorSimple y dispositivo."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Usar toochange de servicio del Administrador de dispositivos de StorSimple de hello las contraseñas de StorSimple

## <a name="overview"></a>Información general
Hola portal de Azure **configuración de dispositivo** opción contiene todos los parámetros de dispositivo de Hola que puede volver a configurar en un dispositivo de StorSimple que se administra mediante un servicio de administrador de dispositivos de StorSimple. Este tutorial le explica cómo puede usar hello **seguridad** opción **configuración de dispositivo** toochange el Administrador de dispositivos o la contraseña de administrador de instantáneas StorSimple.

## <a name="change-hello-device-administrator-password"></a>Cambiar contraseña de administrador de dispositivo de Hola
Cuando se usa el dispositivo de StorSimple de Windows PowerShell interfaz tooaccess Hola, son tooenter requiere una contraseña de administrador de dispositivos. Cuando el primer dispositivo de StorSimple Hola está registrado con un servicio, contraseña de hello predeterminada para esta interfaz es *Password1*. Por seguridad Hola de los datos, es necesario toochange esta contraseña en el final de Hola Hola del proceso de registro. No puede salir del proceso de registro de hello sin cambiar esta contraseña. Para obtener más información, consulte [paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

contraseña de Hola que primero se establece a través de la interfaz de Windows PowerShell de Hola durante el registro se puede cambiar más adelante a través de hello portal de Azure. Realizar Hola siguiendo la contraseña de administrador de pasos toochange Hola.

#### <a name="toochange-hello-device-administrator-password"></a>contraseña del Administrador de dispositivos de toochange Hola
1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**.

2. En la lista tabular de Hola de dispositivos, seleccione y haga clic en el dispositivo de hello cuya contraseña desea toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Hola **configuración** hoja, vaya demasiado**configuración del dispositivo > seguridad**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Hola **configuración de seguridad** hoja, haga clic en **contraseña** contraseña de administrador de dispositivos de toochange Hola.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. Hola **contraseña** hoja, proporcione una contraseña de administrador que tenga entre 8 caracteres too15. contraseña de Hello debe ser una combinación de 3 o más caracteres en mayúsculas, minúsculas, numéricos y especiales.

6. Confirmar contraseña Hola.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

Esto se actualizará la contraseña del Administrador de dispositivos de Hola. Puede usar esta interfaz de Windows PowerShell de contraseña modificada tooaccess Hola.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Establecer contraseña de administrador de instantáneas StorSimple Hola
Software de administrador de instantáneas StorSimple reside en el host de Windows y permite a los administradores toomanage copias de seguridad del dispositivo de StorSimple en forma de Hola de local y en la nube.

Al configurar un dispositivo en el Administrador de instantáneas de StorSimple, se le pedirá tooprovide Hola tooauthenticate de dirección y la contraseña de la IP de dispositivo, el dispositivo de almacenamiento.

Puede establecer o cambiar la contraseña de hello para el Administrador de instantáneas de StorSimple a través de hello portal de Azure. Realizar Hola siguiendo los pasos tooset o cambiar la contraseña de administrador de instantáneas StorSimple Hola.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>contraseña de administrador de instantáneas StorSimple hello tooset
1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**.

2. En la lista tabular de Hola de dispositivos, seleccione y haga clic en el dispositivo de hello cuya contraseña de administrador de instantáneas StorSimple va tooset o cambiar.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Hola **configuración** hoja, vaya demasiado**configuración del dispositivo > seguridad**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Hola **configuración de seguridad** hoja, haga clic en **contraseña** tooset o cambiar contraseña de administrador de instantáneas StorSimple Hola.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. Hola **contraseña** hoja, escriba una contraseña de 14 o 15 caracteres. Asegúrese de que esa contraseña hello contiene una combinación de 3 o más caracteres en mayúsculas, minúsculas, numéricos y especiales.

6. Confirmar contraseña Hola.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

Esto se actualizará la contraseña de administrador de instantáneas StorSimple Hola.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [seguridad de StorSimple](storsimple-8000-security.md).
* Obtenga más información sobre la [modificación de la configuración del dispositivo](storsimple-8000-modify-device-config.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

