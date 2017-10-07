---
title: aaaInstall Update 3 en el dispositivo StorSimple | Documentos de Microsoft
description: "Explica cómo tooinstall StorSimple 8000 Series Update 3 en el dispositivo de la serie StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>Instalación de Update 3 en el dispositivo StorSimple serie 8000

## <a name="overview"></a>Información general

Este tutorial le explica cómo tooinstall Update 3 en un dispositivo de StorSimple con una versión anterior del software a través de Hola portal de Azure clásico y usar el método de revisión de hello. método de revisión de Hola se usa cuando se configura una puerta de enlace en una interfaz de red diferentes a DATA 0 del dispositivo de StorSimple de Hola y que está tratando de tooupdate desde una versión de software anterior a Update 1.

Update 3 incluye actualizaciones de software de dispositivo, controlador LSI y firmware, Storport y Spaceport. Si actualiza desde Update 2 o una versión anterior, también ser necesario tooapply iSCSI, WMI y en algunos casos, las actualizaciones de firmware de disco. Hola software de dispositivo, WMI, iSCSI, controlador LSI, Spaceport y Storport correcciones de actualizaciones no causan interrupción y pueden aplicarse a través de hello portal de Azure clásico. las actualizaciones de firmware de disco Hola son actualizaciones potencialmente perjudiciales y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. 

> [!IMPORTANT]
> * Un conjunto de comprobaciones previas manuales y automáticas se realiza el estado del dispositivo anterior toohello instalación toodetermine hello en cuanto a conectividad de red y el estado de hardware. Estas comprobaciones previas se realizan solo si aplicar actualizaciones de Hola de hello portal de Azure clásico.
> * Se recomienda instalar el software de Hola y Hola de actualizaciones de controladores a través de portal de Azure clásico. Solo debería ir toohello de interfaz de Windows PowerShell del dispositivo de hello (tooinstall actualizaciones) si se produce un error en la comprobación de la puerta de enlace anterior a la actualización de hello en el portal de Hola. Según la versión de Hola que va a actualizar desde, Hola actualizaciones pueden tardar tooinstall 1.5 2,5 horas. actualizaciones del modo de mantenimiento de Hello deben instalarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. Como las actualizaciones en modo de mantenimiento son perturbadoras, generarán un tiempo de inactividad para el dispositivo.
> * Si ejecuta hello opcional Administrador de instantáneas de StorSimple, asegúrese de que ha actualizado el dispositivo de administrador de instantáneas versión tooUpdate 2 anterior tooupdating Hola.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Instalar Update 3 a través de hello portal de Azure clásico
Realizar el dispositivo Hola siguiendo los pasos tooupdate demasiado[Update 3](storsimple-update3-release-notes.md).

> [!NOTE]
> Si va a aplicar la actualización 2 o posterior (incluidas Update 2.1), Microsoft será capaz de toopull información de diagnóstico adicional desde dispositivo Hola. Como resultado, cuando el equipo de operaciones identifica los dispositivos que están experimentando problemas, estamos mejor equipada toocollect información de hello dispositivo y diagnosticar problemas. Al aceptar Update 2 o posterior, nos permitirá tooprovide esta compatibilidad automático.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Compruebe que el dispositivo está ejecutando **StorSimple 8000 Series Update 3 (6.3.9600.17759)**. Hola **actualizó por última vez fecha** también se debe modificar. 
   - Si está actualizando desde una tooUpdate anteriores de versión 2, también verá que hay disponibles actualizaciones de modo de mantenimiento de hello (este mensaje podría continuar toobe mostrado por la too24 horas después de instalar Hola actualizaciones).
     Actualizaciones del modo de mantenimiento son actualizaciones potencialmente perjudiciales que provocar tiempos de inactividad del dispositivo y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello del dispositivo. En algunos casos, cuando se ejecuta Update 1.2, el firmware del disco ya estén actualizado, en cuyo caso no es necesario tooinstall actualiza cualquier modo de mantenimiento.
   - Si va a actualizar desde Update 2 o posterior, el dispositivo debería estar ahora actualizado. Puede omitir el paso siguiente de saludo.

Descargar actualizaciones de modo de mantenimiento de hello mediante pasos de hello enumerados en [toodownload revisiones](#to-download-hotfixes) toosearch para y descargar KB3121899, que instala las actualizaciones de firmware de disco (hello otras actualizaciones deben ya estén instalados por ahora). Siga los pasos de hello enumerados en [instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes) actualizaciones del modo de mantenimiento de tooinstall Hola. 

## <a name="install-update-3-as-a-hotfix"></a>Instalar Update 3 como una revisión
Utilice este procedimiento si se producirá un error de comprobación de la puerta de enlace de hello al tratar de actualizaciones de hello tooinstall a través de hello portal de Azure clásico. se produce un error en la comprobación de Hello como tiene una puerta de enlace asignada tooa no son de datos interfaz de red 0 y el dispositivo está ejecutando una versión de software anterior tooUpdate 1.

versiones de software de Hola que se pueden actualizar utilizando el método de revisión de hello son:

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1, 2.2 

> [!IMPORTANT]
> * Si su dispositivo ejecuta la versión de lanzamiento (GA), póngase en contacto con [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist con hello actualizar.
> 
> 

método de revisión de Hello implica Hola siga tres pasos:

1. Descargan las revisiones de Hola de hello catálogo de Microsoft Update.
2. Instalar y comprobar las revisiones de modo normal de Hola.
3. Instalar y comprobar la revisión del modo de mantenimiento de hello (solo cuando la actualización de software 2 anterior a la actualización).

#### <a name="download-updates-for-your-device"></a>Descargar las actualizaciones para el dispositivo
**Si su dispositivo ejecuta Update 2.1 o 2.2**, también debe descargar e instalar Hola siguiendo las revisiones en hello lo prescrito, orden:

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |Actualización de software &#42; |Regular  <br></br>Sin interrupciones |~45 min |
| 2. |KB3186859 |Controlador LSI y firmware |Regular  <br></br>Sin interrupciones |~20 min |
| 3. |KB3121261 |Revisión de Storport y Spaceport  </br> Windows Server 2012 R2 |Regular  <br></br>Sin interrupciones |~20 min |

&#42;  *Nota esa actualización de software de hello consta de dos archivos binarios: actualización de software de dispositivo se prologa con `all-hcsmdssoftwareupdate` Hola Cis y agente de Mds se prologa con `all-cismdsagentupdatebundle`. actualización de software de dispositivo de hello debe instalarse antes de hello Cis y Mds agente. También debe reiniciar el controlador activo de Hola a través de hello `Restart-HcsController` cmdlet después de aplicar hello elementos de configuración y actualización del agente de Mds (y antes de aplicar Hola actualizaciones restantes).* 

**Si su dispositivo ejecuta Update 0.1, 0.2, 0.3, 1.0, 1.1, 1.2 o 2.0**, también debe descargar e instalar Hola siguiendo las revisiones en software de adición de toohello, controlador LSI y (Hola se muestra en la tabla anterior), actualizaciones de firmware en hello lo prescrito, orden:

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |Paquete iSCSI |Regular  <br></br>Sin interrupciones |~20 min |
| 5. |KB3103616 |Paquete WMI |Regular  <br></br>Sin interrupciones |~12 min |

<br></br>

**Si el dispositivo está ejecutando versiones 0,2, 0,3, 1.0, 1.1 y 1.2**, es posible que tenga las actualizaciones de firmware de disco tooinstall encima de todas las actualizaciones de Hola se muestra en hello anterior tablas. Puede comprobar si necesita hello las actualizaciones de firmware de disco mediante la ejecución de hello `Get-HcsFirmwareVersion` cmdlet. Si se ejecutan estas versiones de firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, a continuación, no es necesario tooinstall estas actualizaciones.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |Firmware del disco |Mantenimiento  <br></br>Perjudicial |~30 min |

<br></br>

> [!IMPORTANT]
> * Esta toobe de necesidades de procedimiento realiza solo una vez tooapply Update 3. Puede usar las actualizaciones posteriores de hello Azure tooapply portal clásico.
> * Si actualiza desde 2.2 de actualización, la hora de instalación total hello es cerrar too1.1 horas.
> * Antes de usar este Hola de tooapply procedimiento actualizar, asegúrese de que ambos controladores de dispositivo de hello están en línea y todos los componentes de hardware de hello están en buen Estados.
> 
> 

Realizar Hola después toodownload pasos e instalar las revisiones de Hola.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [versión 3 de actualización](storsimple-update3-release-notes.md).

