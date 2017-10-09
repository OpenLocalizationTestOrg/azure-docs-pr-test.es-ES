---
title: aaaInstall Update 2 en el dispositivo StorSimple | Documentos de Microsoft
description: "Explica cómo tooinstall StorSimple 8000 Series Update 2 en el dispositivo de la serie StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Instalar Update 2 en el dispositivo de StorSimple
## <a name="overview"></a>Información general
Este tutorial le explica cómo tooinstall Update 2 en un dispositivo de StorSimple con una versión anterior del software a través de hello portal de Azure clásico. tutorial de Hola también cubre los pasos de hello necesarios para la actualización de hello cuando se configura una puerta de enlace en una interfaz de red diferentes a DATA 0 del dispositivo de StorSimple de Hola y que está tratando de tooupdate desde una versión de software anterior a la actualización 1.

En Update 2 se incluyen actualizaciones de software del dispositivo, actualizaciones de controladores LSI y actualizaciones del firmware del disco. software de dispositivo de Hola y actualizaciones de LSI actualizaciones no causan interrupción y pueden aplicarse a través de hello portal de Azure clásico. las actualizaciones de firmware de disco Hola son actualizaciones potencialmente perjudiciales y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola.

> [!IMPORTANT]
> * Es posible que no vea Update 2 inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Busque actualizaciones de nuevo en unos días ya que estarán disponibles pronto.
> * Un conjunto de comprobaciones previas manuales y automáticas se realiza el estado del dispositivo anterior toohello instalación toodetermine hello en cuanto a conectividad de red y el estado de hardware. Estas comprobaciones previas se realizan solo si aplicar actualizaciones de Hola de hello portal de Azure clásico.
> * Se recomienda instalar el software de Hola y Hola de actualizaciones de controladores a través de portal de Azure clásico. Solo debería ir toohello de interfaz de Windows PowerShell del dispositivo de hello (tooinstall actualizaciones) si se produce un error en la comprobación de la puerta de enlace anterior a la actualización de hello en el portal de Hola. Hola actualizaciones pueden tardar tooinstall 4-7 horas (incluidas las actualizaciones de Windows hello). actualizaciones del modo de mantenimiento de Hello deben instalarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. Como las actualizaciones en modo de mantenimiento son perturbadoras, generarán un tiempo de inactividad para el dispositivo.
> * Si ejecuta hello opcional Administrador de instantáneas de StorSimple, asegúrese de que ha actualizado el dispositivo de administrador de instantáneas versión tooUpdate 2 anterior tooupdating Hola.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Instale la actualización 2 a través de hello portal de Azure clásico
Realizar el dispositivo Hola siguiendo los pasos tooupdate demasiado[Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Actualización 2 permite que Microsoft toopull información de diagnóstico adicional desde dispositivo Hola. Como resultado, cuando el equipo de operaciones identifica los dispositivos que están experimentando problemas, estamos mejor equipada toocollect información de hello dispositivo y diagnosticar problemas. Si se acepta la actualización 2, nos permitirá tooprovide esta compatibilidad automático.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Compruebe que el dispositivo ejecuta **StorSimple 8000 Series Update 2 (6.3.9600.17673)**. Hola **actualizó por última vez fecha** también se debe modificar. También verá que hay disponibles actualizaciones de modo de mantenimiento (este mensaje podría continuar toobe mostrado por la too24 horas después de instalar Hola actualizaciones).
   
   Actualizaciones del modo de mantenimiento son actualizaciones potencialmente perjudiciales que provocar tiempos de inactividad del dispositivo y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello del dispositivo. En algunos casos, cuando se ejecuta Update 1.2, el firmware del disco ya estén actualizado, en cuyo caso no es necesario tooinstall actualiza cualquier modo de mantenimiento.
2. Descargar actualizaciones de modo de mantenimiento de hello mediante pasos de hello enumerados en [toodownload revisiones](#to-download-hotfixes) toosearch para y descargar KB3121899, que instala las actualizaciones de firmware de disco (hello otras actualizaciones deben ya estén instalados por ahora).
3. Siga los pasos de hello enumerados en [instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes) actualizaciones del modo de mantenimiento de tooinstall Hola.

## <a name="install-update-2-as-a-hotfix"></a>Instalar Update 2 como una revisión
Utilice este procedimiento si se producirá un error de comprobación de la puerta de enlace de hello al tratar de actualizaciones de hello tooinstall a través de hello portal de Azure clásico. se produce un error en la comprobación de Hello como tiene una puerta de enlace asignada tooa no son de datos interfaz de red 0 y el dispositivo está ejecutando una versión de software anterior tooUpdate 1.

versiones de software de Hola que se pueden actualizar mediante el método de revisión de hello son actualización 0,1, actualización 0,2 y actualización 0.3, Update 1, actualización 1.1 y 1.2 de actualización. método de revisión de Hello implica Hola siga tres pasos:

* Descargan las revisiones de Hola de hello catálogo de Microsoft Update.
* Instalar y comprobar las revisiones de modo normal de Hola.
* Instalar y comprobar las revisiones de modo de mantenimiento de Hola.

tooinstall como una revisión de la actualización 2, debe descargar e instalar Hola siguiendo las revisiones:

| Orden | KB | Descripción | Tipo de actualización |
| --- | --- | --- | --- |
| 1 |KB3121901 |Actualización de software |Normal |
| 2 |KB3121900 |Controlador LSI |Normal |
| 3 |KB3080728 |Revisión de Storport  </br> Windows Server 2012 R2 |Normal |
| 4 |KB3090322 |Revisión de Spaceport  </br> Windows Server 2012 R2 |Normal |
| 5 |KB3121899 |Firmware del disco |Mantenimiento |

> [!IMPORTANT]
> * Si su dispositivo ejecuta la versión de lanzamiento (GA), póngase en contacto con [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist con hello actualizar.
> * Esta toobe de necesidades de procedimiento realiza solo una vez tooapply Update 2. Puede usar las actualizaciones posteriores de hello Azure tooapply portal clásico.
> * Cada instalación de revisión puede tardar unos 20 minutos toocomplete. La hora de instalación total es cerrar too2 horas.
> * Antes de usar este Hola de tooapply procedimiento actualizar, asegúrese de que ambos controladores de dispositivo estén en línea y todos los componentes de hardware de hello están en buen Estados.
> 
> 

Realizar Hola siguiendo los pasos tooapply esta actualización como una revisión.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [versión 2 actualización](storsimple-update2-release-notes.md).

