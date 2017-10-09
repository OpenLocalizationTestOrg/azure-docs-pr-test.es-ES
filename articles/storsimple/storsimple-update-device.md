---
title: aaaUpdate el dispositivo StorSimple | Documentos de Microsoft
description: "Explica cómo toouse hello StorSimple actualizar tooinstall característica regular y actualizaciones del modo de mantenimiento y las revisiones."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Actualización del dispositivo de la serie StorSimple 8000
## <a name="overview"></a>Información general
Hello StorSimple actualizaciones características le permiten tooeasily mantener actualizado el dispositivo StorSimple. Según el tipo de actualización de hello, puede aplicar el dispositivo de toohello de las actualizaciones a través del portal de Azure clásico de Hola o a través de la interfaz de Windows PowerShell de Hola. Este tutorial describen los tipos de actualización de Hola y cómo tooinstall de ellos.

Puede aplicar dos tipos de actualizaciones de dispositivo: 

* Actualizaciones normales (o en modo normal)
* Actualizaciones en modo de mantenimiento

Puede instalar actualizaciones periódicas a través de hello portal de Azure clásico o Windows PowerShell; Sin embargo, debe usar las actualizaciones del modo de mantenimiento de Windows PowerShell tooinstall. 

A continuación se describe cada tipo de actualización.

### <a name="regular-updates"></a>Actualizaciones normales
Las actualizaciones normales son las actualizaciones no causan interrupción y que se pueden instalar cuando el dispositivo de hello está en modo Normal. Estas actualizaciones se aplican a través de controlador de dispositivo de tooeach de sitio Web de Microsoft Update de Hola. 

> [!IMPORTANT]
> Un controlador de conmutación por error puede producirse durante el proceso de actualización de Hola. Sin embargo, esto no afectará a la disponibilidad ni al funcionamiento del sistema.
> 
> 

* Para obtener detalles sobre cómo tooinstall actualizaciones frecuentes a través de hello portal de Azure clásico, consulte [instale actualizaciones periódicas a través del portal de Azure clásico hello](#install-regular-updates-via-the-azure-classic-portal).
* También puede instalar actualizaciones normales a través de Windows PowerShell para StorSimple. Para obtener más información, consulte [Instalación de actualizaciones normales a través de Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Actualizaciones en modo de mantenimiento
Se trata de actualizaciones con interrupciones, como las actualizaciones de firmware de disco. Estas actualizaciones requieren Hola dispositivo toobe poner en modo de mantenimiento. Para obtener más información, consulte [Paso 2: Acceso al modo de mantenimiento](#step2). No se puede usar actualizaciones del modo de mantenimiento de hello Azure tooinstall portal clásico. En su lugar, debe usar Windows PowerShell para StorSimple. 

Para obtener detalles sobre cómo actualiza el modo de mantenimiento de tooinstall, consulte [actualizaciones del modo de mantenimiento de la instalación a través de Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Modo de mantenimiento de actualizaciones deben aplicarse por separado tooeach controlador. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Instale actualizaciones periódicas a través de hello portal de Azure clásico
Puede usar el dispositivo de StorSimple de tooyour de las actualizaciones de hello Azure tooapply portal clásico.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Instalación de actualizaciones normales a través de Windows PowerShell para StorSimple
Como alternativa, puede usar Windows PowerShell para las actualizaciones de StorSimple tooapply normal (modo Normal).

> [!IMPORTANT]
> Aunque puede instalar las actualizaciones normales mediante Windows PowerShell para StorSimple, recomendamos encarecidamente que instale actualizaciones periódicas a través de hello portal de Azure clásico. A partir de Update 1, comprobaciones previas será tooinstalling anteriores realizan actualizaciones desde el portal de Hola. Estas comprobaciones previas previenen los errores y garantizan una experiencia con menos complicaciones. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Instalación de actualizaciones en modo de mantenimiento a través de Windows PowerShell para StorSimple
Usar Windows PowerShell para StorSimple tooapply mantenimiento modo actualizaciones tooyour el dispositivo StorSimple. En este modo, todas las solicitudes de E/S se interrumpen. También se detienen los servicios como la memoria de acceso aleatorio no volátil (NVRAM) o servicio de Cluster Server de Hola. Al entrar o salir de este modo, se reinician ambos controladores. Al salir de este modo, todos los servicios de hello continuará y deben estar en buen Estados. Esto puede tardar unos minutos.

Si necesita actualizaciones del modo de mantenimiento tooapply, recibirá una alerta a través del portal de Azure clásico de Hola que tiene actualizaciones que se deben instalar. Esta alerta incluirá instrucciones para usar Windows PowerShell para las actualizaciones de StorSimple tooinstall Hola. Después de actualizar el dispositivo, use Hola mismo modo de procedimiento toochange Hola dispositivo tooRegular. Para obtener instrucciones detalladas, consulte [Paso 4: Salir del modo de mantenimiento](#step4).

> [!IMPORTANT]
> * Antes de entrar en modo de mantenimiento, compruebe que ambos controladores de dispositivo están en buenas condiciones comprobando hello **estado del Hardware** en hello **mantenimiento** página Hola portal de Azure clásico. Si el controlador de hello no es correcto, póngase en contacto con Microsoft Support para los pasos siguientes Hola. Para obtener más información, visite tooContact Microsoft Support. 
> * Cuando esté en modo de mantenimiento, necesita tooapply Hola actualización primero en un controlador y, a continuación, en Hola otro controlador.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Paso 1: Conectar la consola serie toohello<a name="step1">
En primer lugar, utilice una aplicación como PuTTY tooaccess Hola consola serie. Hello siguiente procedimiento se explica cómo toouse tooconnect PuTTY toohello consola en serie.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Paso 2: Acceso al modo de mantenimiento <a name="step2">
Después de conectar la consola de toohello, determinar si existen actualizaciones tooinstall y escriba tooinstall de modo de mantenimiento ellos.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Paso 3: Instalación de las actualizaciones <a name="step3">
A continuación, instale las actualizaciones.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Paso 4: Salir del modo de mantenimiento <a name="step4">
Por último, salga del modo de mantenimiento.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Instale las reparaciones mediante Windows PowerShell para StorSimple
A diferencia de las actualizaciones para Microsoft Azure StorSimple, las revisiones se instalan desde una carpeta compartida. Al igual que en el caso de las actualizaciones, hay dos tipos de revisiones: 

* Revisiones normales 
* Revisiones en modo de mantenimiento  

Hello procedimientos siguientes explican cómo toouse Windows PowerShell para StorSimple tooinstall regular y las revisiones de modo de mantenimiento.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>¿Qué ocurre restablecer tooupdates si lleva a cabo una fábrica del dispositivo de hello?
Si un dispositivo es restablecer toofactory configuración, todas las actualizaciones de Hola se pierden. Después de hello restablecimiento de fábrica está registrado y configurado, necesitará toomanually instalar las actualizaciones a través de hello portal de Azure clásico o Windows PowerShell para StorSimple. Para obtener más información sobre el restablecimiento de fábrica, consulte [restablecer la configuración predeterminada de hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre [mediante Windows PowerShell para StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

