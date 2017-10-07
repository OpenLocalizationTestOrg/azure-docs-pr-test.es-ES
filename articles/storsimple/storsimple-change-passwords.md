---
title: "aaaChange contraseñas a través del Administrador de dispositivos de StorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola toochange de servicio de StorSimple Manager sus contraseñas de administrador de administrador de instantáneas StorSimple y dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Usar toochange de servicio de StorSimple Manager hello las contraseñas de StorSimple
## <a name="overview"></a>Información general
Hola portal de Azure clásico **configurar** página contiene todos los parámetros de dispositivo de Hola que puede volver a configurar en un dispositivo de StorSimple que se administra mediante un servicio de StorSimple Manager. Este tutorial le explica cómo puede usar hello **configurar** página toochange el Administrador de dispositivos o la contraseña de administrador de instantáneas StorSimple.

## <a name="change-hello-device-administrator-password"></a>Cambiar contraseña de administrador de dispositivo de Hola
Cuando se usa el dispositivo de StorSimple de Windows PowerShell interfaz tooaccess Hola, son tooenter requiere una contraseña de administrador de dispositivos. Cuando el primer dispositivo de StorSimple Hola está registrado con un servicio, contraseña de hello predeterminada para esta interfaz es *Password1*. Por seguridad Hola de los datos, es necesario toochange esta contraseña en el final de Hola Hola del proceso de registro. No puede salir del proceso de registro de hello sin cambiar esta contraseña. Para obtener más información, consulte [paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

contraseña de Hola que primero se establece a través de la interfaz de Windows PowerShell de Hola durante el registro, a continuación, puede cambiar a través de hello portal de Azure clásico. Realizar Hola siguiendo la contraseña de administrador de pasos toochange Hola.

#### <a name="toochange-hello-device-administrator-password"></a>contraseña del Administrador de dispositivos de toochange Hola
1. En el portal clásico de hello, haga clic en **dispositivos** > **configurar** para el dispositivo.
2. Desplácese hacia abajo toohello **contraseña de administrador de dispositivos** sección. Proporcione una contraseña de administrador que tenga entre 8 caracteres too15. contraseña de Hello debe ser una combinación de 3 o más caracteres en mayúsculas, minúsculas, numéricos y especiales.
3. Confirmar contraseña Hola.
4. Haga clic en **guardar** final Hola de página Hola.

Esto se actualizará la contraseña del Administrador de dispositivos de Hola. Puede usar esta interfaz de Windows PowerShell de contraseña modificada tooaccess Hola.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Cambiar la contraseña de administrador de instantáneas StorSimple Hola
Software de administrador de instantáneas StorSimple reside en el host de Windows y permite a los administradores toomanage copias de seguridad del dispositivo de StorSimple en forma de Hola de local y en la nube.

Al configurar un dispositivo en el Administrador de instantáneas de StorSimple, se le pedirá tooprovide Hola tooauthenticate de dirección y la contraseña de la IP de dispositivo, el dispositivo de almacenamiento. Esta contraseña primero se configura a través de la interfaz de Windows PowerShell de Hola. Para obtener más información, consulte [paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

contraseña de Hola que primero se establece a través de la interfaz de Windows PowerShell de Hola durante el registro, a continuación, se puede cambiar mediante el portal clásico de Hola. Realizar Hola siguiendo la contraseña de administrador de instantáneas StorSimple de pasos toochange Hola.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>contraseña de administrador de instantáneas StorSimple hello toochange
1. En el portal clásico de hello, haga clic en **dispositivos** > **configurar** para el dispositivo.
2. Desplácese hacia abajo toohello **StorSimple Snapshot Manager** sección. Escriba una contraseña que tenga 14 o 15 caracteres. Asegúrese de que esa contraseña hello contiene una combinación de 3 o más caracteres en mayúsculas, minúsculas, numéricos y especiales.
3. Confirmar contraseña Hola.
4. Haga clic en **guardar** final Hola de página Hola.

Esto se actualizará la contraseña de administrador de instantáneas StorSimple Hola.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [seguridad de StorSimple](storsimple-security.md).
* Obtenga más información sobre la [modificación de la configuración del dispositivo](storsimple-modify-device-config.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

