---
title: "aaaInstall 1.2 de actualización en el dispositivo StorSimple | Documentos de Microsoft"
description: "Explica cómo tooinstall StorSimple 8000 Series Update 1.2 en el dispositivo de la serie StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Instalación de Update 1.2 en el dispositivo StorSimple serie 8000
## <a name="overview"></a>Información general
Este tutorial le explica cómo tooinstall actualizar 1.2 en un dispositivo de StorSimple que se está ejecutando una versión de software anterior tooUpdate 1. tutorial de Hello también cubre Hola se requieren pasos adicionales para la actualización de hello cuando se configura una puerta de enlace en una interfaz de red diferentes a DATA 0 del dispositivo de StorSimple Hola.

La actualización 1.2 incluye actualizaciones de software del dispositivo, actualizaciones de controladores LSI y actualizaciones del firmware del disco. Hola software y actualizaciones de controladores de LSI actualizaciones no causan interrupción y pueden aplicarse a través de hello portal de Azure clásico. las actualizaciones de firmware de disco Hola son actualizaciones potencialmente perjudiciales y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola.

En función de la versión que se está ejecutando en el dispositivo, puede determinar si se aplicará la actualización 1.2. Puede comprobar la versión de software de hello de dispositivo desplazándose toohello **vista rápida** sección de su dispositivo **panel**.

</br>

| Si ejecuta la versión del software... | ¿Qué ocurre en el portal de hello? |
| --- | --- |
| Lanzamiento - GA |Si está ejecutando la versión de lanzamiento (GA), no aplique esta actualización. Por favor, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate el dispositivo. |
| Actualización 0.1 |El portal aplica la actualización 1.2. |
| Actualización 0.2 |El portal aplica la actualización 1.2. |
| Actualización 0.3 |El portal aplica la actualización 1.2. |
| Actualización 1 |Esta actualización no estará disponible. |
| Actualización 1.1 |Esta actualización no estará disponible. |

</br>

> [!IMPORTANT]
> * Es posible que no vea actualización 1.2 inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Busque actualizaciones de nuevo en unos días ya que estarán disponibles pronto.
> * Esta actualización incluye un conjunto de comprobaciones previas manuales y automáticas toodetermine Hola del estado del dispositivo en términos de conectividad de red y el estado de hardware. Estas comprobaciones previas se realizan solo si aplicar actualizaciones de Hola de hello portal de Azure clásico.
> * Se recomienda instalar el software de Hola y Hola de actualizaciones de controladores a través de portal de Azure clásico. Solo debería ir toohello de interfaz de Windows PowerShell del dispositivo de hello (tooinstall actualizaciones) si se produce un error en la comprobación de la puerta de enlace anterior a la actualización de hello en el portal de Hola. Hola actualizaciones pueden tardar tooinstall de entre 5 y 10 horas (incluidas las actualizaciones de Windows hello). actualizaciones del modo de mantenimiento de Hello deben instalarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. Como las actualizaciones en modo de mantenimiento son perturbadoras, generarán un tiempo de inactividad para el dispositivo.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Instalar 1.2 de actualización a través de hello portal de Azure clásico
Realizar el dispositivo Hola siguiendo los pasos tooupdate demasiado[actualización 1.2](storsimple-update1-release-notes.md). Use este procedimiento solo si tiene una puerta de enlace configurada en la interfaz de red DATA 0 del dispositivo.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Compruebe que el dispositivo está ejecutando **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**. Hola **actualizó por última vez fecha** también se debe modificar. También verá que hay disponibles actualizaciones de modo de mantenimiento (este mensaje podría continuar toobe mostrado por la too24 horas después de instalar Hola actualizaciones).
   
   Actualizaciones del modo de mantenimiento son actualizaciones potencialmente perjudiciales que provocar tiempos de inactividad del dispositivo y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello del dispositivo.
   
   ![Página de mantenimiento](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Página de mantenimiento")
2. Descargar actualizaciones de modo de mantenimiento de hello mediante pasos de hello enumerados en [toodownload revisiones](#to-download-hotfixes) toosearch para y descargar KB3063416, que instala las actualizaciones de firmware de disco (hello otras actualizaciones deben ya estén instalados por ahora).
3. Siga los pasos de hello enumerados en [instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes) actualizaciones del modo de mantenimiento de tooinstall Hola.
4. En el portal de Azure clásico de Hola, navegue toohello **mantenimiento** página y en la parte inferior de Hola de página de hello, haga clic en **examinar actualizaciones** toocheck las actualizaciones de Windows y, a continuación, haga clic en **instalar actualizaciones **. Habrá terminado después de que todos de hello las actualizaciones se instalaron correctamente.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Instale la actualización 1.2 en un dispositivo que tenga una puerta de enlace configurada para una interfaz de red que no sea DATA 0
Debería usar este procedimiento solo si se producirá un error de comprobación de la puerta de enlace de hello al tratar de actualizaciones de hello tooinstall a través de hello portal de Azure clásico. se produce un error en la comprobación de Hello como tiene una puerta de enlace asignada tooa no son de datos interfaz de red 0 y el dispositivo está ejecutando una versión de software anterior tooUpdate 1. Si el dispositivo no tiene una puerta de enlace en una interfaz de red 0 no son de datos, puede actualizar el dispositivo directamente desde el portal de Azure clásico Hola. Vea [instale la actualización 1.2 a través del portal de Azure clásico hello](#install-update-1.2-via-the-azure-classic-portal).

versiones de software de Hola que se pueden actualizar con este método son Update 0,1, actualización 0,2 y Update 0.3.

> [!IMPORTANT]
> * Si su dispositivo ejecuta la versión de lanzamiento (GA), póngase en contacto con [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist con hello actualizar.
> * Esta toobe de necesidades de procedimiento realiza solo una vez tooapply 1.2 de actualización. Puede usar las actualizaciones posteriores de hello Azure tooapply portal clásico.
> 
> 

Si el dispositivo está ejecutando el 1 de anteriores a la actualización software y tiene una puerta de enlace establecido para una interfaz de red diferentes a DATA 0, puede aplicar actualización 1.2 de hello maneras siguientes:

* **Opción 1**: Descargar la actualización de Hola y aplicar mediante hello `Start-HcsHotfix` cmdlet desde la interfaz de Windows PowerShell de hello de dispositivo de Hola. Se trata de hello método recomendado. **No utilice este tooapply método 1.2 de actualización si su dispositivo ejecuta la actualización 1.0 o 1.1 de actualización.**
* **Opción 2**: hello de instalación y configuración de puerta de enlace de hello Remove actualizan directamente desde el portal de Azure clásico Hola.

Se proporcionan instrucciones detalladas para cada uno de ellos en hello las secciones siguientes.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Opción 1: Usar Windows PowerShell para StorSimple tooapply 1.2 de actualización como una revisión
Debería usar este procedimiento solo si se ejecuta Update 0.1, 0.2, 0.3 y si la comprobación de la puerta de enlace no ha podido al tratar de actualizaciones de tooinstall de hello portal de Azure clásico. Si está ejecutando software de versión (GA), inicie [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate el dispositivo.

tooinstall 1.2 de actualización como una revisión, debe descargar e instalar Hola siguiendo las revisiones:

| Orden | KB | Descripción | Tipo de actualización |
| --- | --- | --- | --- |
| 1 |KB3063418 |Actualización de software |Normal |
| 2 |KB3043005 |Actualización del controlador SAS LSI |Normal |
| 3 |KB3063416 |Firmware del disco |Mantenimiento |

Antes de usar este Hola de tooapply procedimiento actualizar, asegúrese de que:

* Los dos controladores de dispositivo están en línea.

Realizar Hola siguiendo los pasos tooapply 1.2 de actualización. **actualizaciones de Hello podrían tardar aproximadamente 2 horas toocomplete (aproximadamente 30 minutos para el software, 30 minutos para los controladores, 45 minutos de firmware de disco).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Opción 2: Usar hello Azure tooapply portal clásico 1.2 de actualización después de quitar la configuración de puerta de enlace de Hola
Este procedimiento aplica solo los dispositivos tooStorSimple que ejecutan una versión de software anterior tooUpdate 1 y que tienen una puerta de enlace que se establece en una interfaz de red diferentes a DATA 0. Necesitará una actualización hello tooclear Hola gateway configuración tooapplying anterior.

actualización de Hello puede tardar unos toocomplete horas. Si los hosts están en subredes diferentes, quitando a la configuración de puerta de enlace de hello en interfaces de iSCSI de hello podría producir un tiempo de inactividad. Se recomienda que configure DATA 0 para el tiempo de inactividad hello tooreduce de tráfico de iSCSI.

Realizar Hola siguiendo la interfaz de red de pasos toodisable Hola con puerta de enlace de hello y, a continuación, aplique la actualización de Hola.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [versión 1.2 de actualización](storsimple-update1-release-notes.md).

