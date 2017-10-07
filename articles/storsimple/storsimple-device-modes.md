---
title: modo de dispositivo de StorSimple de hello aaaChange | Documentos de Microsoft
description: "Describe los modos de dispositivo de StorSimple de Hola y explica cómo toouse Windows PowerShell para StorSimple toochange Hola modo del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Cambiar el modo de dispositivo de hello en el dispositivo StorSimple
En este artículo se proporciona una breve descripción del programa Hola a distintos modos en los que puede operar el dispositivo StorSimple. El dispositivo StorSimple puede funcionar en tres modos: normal, de mantenimiento y de recuperación. 

Después de leer este artículo, sabrá acerca de:

* ¿Cuáles son los modos de dispositivo de StorSimple de Hola
* ¿Cómo toofigure qué modo Hola dispositivo StorSimple está en
* ¿Cómo toochange del modo de toomaintenance normal y *viceversa*

Hola por encima de las tareas de administración solo puede realizarse a través de la interfaz de Windows PowerShell de hello de dispositivo StorSimple.

## <a name="about-storsimple-device-modes"></a>Acerca de los modos del dispositivo StorSimple.
El dispositivo StorSimple puede funcionar en modo normal, de mantenimiento o de recuperación. A continuación se describe brevemente cada uno de estos modos.

### <a name="normal-mode"></a>Modo Normal
Esto se define como modo de funcionamiento normal de Hola para un dispositivo de StorSimple totalmente configurado. De manera predeterminada, su dispositivo debería estar en modo normal.

### <a name="maintenance-mode"></a>Modo Mantenimiento
A veces hello dispositivo StorSimple que necesite toobe pone en modo de mantenimiento. Este modo permite el mantenimiento de tooperform en dispositivo de Hola e instalar actualizaciones potencialmente perjudiciales, como las relacionadas con firmware toodisk.

Puede colocar sistema hello en modo de mantenimiento sólo a través de hello Windows PowerShell para StorSimple. En este modo, todas las solicitudes de E/S se interrumpen. También se detienen los servicios como la memoria de acceso aleatorio no volátil (NVRAM) o servicio de Cluster Server de Hola. Ambos controladores Hola se reinician cuando entra o sale de este modo. Al salir del modo de mantenimiento de hello, todos los servicios de hello continuará y deben estar en buen Estados. Esta operación puede tardar unos minutos.

> [!NOTE]
> **El modo Mantenimiento solo se admite en un dispositivo que funcione correctamente. No se admite en un dispositivo en el que uno o ambos de controladores de hello no funcionan.**
> </br>
> 
> 

### <a name="recovery-mode"></a>Modo Recuperación
El modo Recuperación puede describirse como el "Modo seguro de Windows con compatibilidad de red". Modo de recuperación pone el equipo de Microsoft Support hello y les permite tooperform diagnósticos en el sistema de Hola. Hola principal objetivo del modo de recuperación es registros del sistema tooretrieve Hola.

Si el sistema entra en modo de recuperación, debe ponerse en contacto con el soporte técnico de Microsoft para obtener asistencia. Para obtener más información, consulte demasiado[póngase en contacto con soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).

> [!NOTE]
> **No se puede colocar el dispositivo de hello en modo de recuperación. Si el dispositivo de hello está en mal estado, modo de recuperación intenta tooget dispositivo de hello en un estado en el que el personal de Microsoft Support pueda examinarlo.**
> 
> 

## <a name="determine-storsimple-device-mode"></a>Determinar el modo de dispositivo StorSimple
#### <a name="toodetermine-hello-current-device-mode"></a>modo toodetermine hello de dispositivo actual
1. Inicie sesión en la consola serie del dispositivo toohello siguiendo los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Mire el mensaje de pancarta hello en el menú de consola serie de hello de dispositivo de Hola. Este mensaje indica explícitamente si dispositivo Hola está en modo de mantenimiento o de recuperación. Si el mensaje de bienvenida no contiene ninguna información específica relativa a modo de sistema de toohello, dispositivo Hola está en modo normal.

## <a name="change-hello-storsimple-device-mode"></a>Cambiar el modo de dispositivo de StorSimple Hola
Puede colocar el dispositivo de StorSimple de hello en mantenimiento de tooperform modo (de modo normal) o instalar actualizaciones del modo de mantenimiento. Realizar Hola siguiendo el modo de mantenimiento de tooenter o salir de procedimientos.

> [!IMPORTANT]
> Antes de entrar en modo de mantenimiento, compruebe que ambos controladores de dispositivo están en buenas condiciones accediendo hello **estado del Hardware** en hello **mantenimiento** página Hola portal de Azure clásico. Si uno o ambos controladores hello no sean correcto, póngase en contacto con Microsoft Support para los pasos siguientes Hola. Para obtener más información, consulte demasiado[póngase en contacto con soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).
> 
> 

#### <a name="tooenter-maintenance-mode"></a>modo de mantenimiento de tooenter
1. Inicie sesión en la consola serie del dispositivo toohello siguiendo los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**. Cuando se le solicite, proporcione hello **contraseña de administrador de dispositivo**. contraseña de Hello predeterminada es: `Password1`.
3. En hello símbolo del sistema, escriba 
   
    `Enter-HcsMaintenanceMode`
4. Verá un mensaje de advertencia que le indica que el modo de mantenimiento interrumpirá todas las solicitudes de E/S y Hola conexión toohello portal de Azure clásico, y se le pedirá confirmación. Tipo de **Y** tooenter modo de mantenimiento.
5. Ambos controladores se reiniciarán. Una vez completado el reinicio de hello, aparecerá otro mensaje que indica que el dispositivo Hola está en modo de mantenimiento.

#### <a name="tooexit-maintenance-mode"></a>modo de mantenimiento de tooexit
1. Inicie sesión en la consola serie del dispositivo toohello. Compruebe de mensaje de pancarta Hola que el dispositivo está en modo de mantenimiento.
2. En hello símbolo del sistema, escriba:
   
    `Exit-HcsMaintenanceMode`
3. Aparecerán un mensaje de advertencia y un mensaje de confirmación. Tipo de **Y** tooexit modo de mantenimiento.
4. Ambos controladores se reiniciarán. Una vez completado el reinicio de hello, aparecerá otro mensaje que indica que el dispositivo Hola está en modo normal.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[aplicar las actualizaciones del modo normal y el mantenimiento](storsimple-update-device.md) en el dispositivo StorSimple.

