---
title: "aaaInstall 2.2 de actualización en el dispositivo StorSimple | Documentos de Microsoft"
description: "Explica cómo tooinstall StorSimple 8000 Series Update 2.2 en su dispositivo de la serie StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>Instalación de Update 2.2 en el dispositivo StorSimple
## <a name="overview"></a>Información general
Este tutorial le explica cómo tooinstall 2.2 de actualización en un dispositivo de StorSimple con una versión anterior del software a través de Hola portal de Azure clásico y usar el método de revisión de hello. método de revisión de Hola se usa cuando se configura una puerta de enlace en una interfaz de red diferentes a DATA 0 del dispositivo de StorSimple de Hola y que está tratando de tooupdate desde una versión de software anterior a Update 1.

Update 2.2 incluye software del dispositivo, WMI y actualizaciones de iSCSI. Si actualiza desde la versión 2.1, solo actualización de software de dispositivo de hello deberá toobe aplicado. Si actualiza desde una versión 2 anterior a la actualización, también será necesario tooapply LSI controlador, Spaceport, Storport y actualizaciones de firmware de disco. Hola software de dispositivo, WMI, iSCSI, controlador LSI, Spaceport y Storport correcciones de actualizaciones no causan interrupción y pueden aplicarse a través de hello portal de Azure clásico. las actualizaciones de firmware de disco Hola son actualizaciones potencialmente perjudiciales y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. 

> [!IMPORTANT]
> * Un conjunto de comprobaciones previas manuales y automáticas se realiza el estado del dispositivo anterior toohello instalación toodetermine hello en cuanto a conectividad de red y el estado de hardware. Estas comprobaciones previas se realizan solo si aplicar actualizaciones de Hola de hello portal de Azure clásico.
> * Se recomienda instalar el software de Hola y Hola de actualizaciones de controladores a través de portal de Azure clásico. Solo debería ir toohello de interfaz de Windows PowerShell del dispositivo de hello (tooinstall actualizaciones) si se produce un error en la comprobación de la puerta de enlace anterior a la actualización de hello en el portal de Hola. Según la versión de Hola que va a actualizar desde, Hola actualizaciones pueden tardar tooinstall 1.5 2,5 horas. actualizaciones del modo de mantenimiento de Hello deben instalarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. Como las actualizaciones en modo de mantenimiento son perturbadoras, generarán un tiempo de inactividad para el dispositivo.
> * Si ejecuta hello opcional Administrador de instantáneas de StorSimple, asegúrese de que ha actualizado el dispositivo el Administrador de instantáneas versión 2.2 tooUpdate tooupdating anterior Hola.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Instalar 2.2 de la actualización a través de hello portal de Azure clásico
Realizar el dispositivo Hola siguiendo los pasos tooupdate demasiado[actualización 2.2](storsimple-update21-release-notes.md).

> [!NOTE]
> Si va a aplicar la actualización 2 o posterior (incluidas Update 2.1), Microsoft será capaz de toopull información de diagnóstico adicional desde dispositivo Hola. Como resultado, cuando el equipo de operaciones identifica los dispositivos que están experimentando problemas, estamos mejor equipada toocollect información de hello dispositivo y diagnosticar problemas. Al aceptar Update 2 o posterior, nos permitirá tooprovide esta compatibilidad automático.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Compruebe que el dispositivo ejecuta la **serie StorSimple 8000 Update 2.2 (6.3.9600.17708)**. Hola **actualizó por última vez fecha** también se debe modificar. 
   
   Si está actualizando desde una tooUpdate anteriores de versión 2, también verá que hay disponibles actualizaciones de modo de mantenimiento de hello (este mensaje podría continuar toobe mostrado por la too24 horas después de instalar Hola actualizaciones).
   
   Actualizaciones del modo de mantenimiento son actualizaciones potencialmente perjudiciales que provocar tiempos de inactividad del dispositivo y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello del dispositivo. En algunos casos, cuando se ejecuta Update 1.2, el firmware del disco ya estén actualizado, en cuyo caso no es necesario tooinstall actualiza cualquier modo de mantenimiento.
   
   Si va a actualizar desde Update 2, el dispositivo debería estar ahora actualizado. Puede omitir Hola restantes pasos.
2. Descargar actualizaciones de modo de mantenimiento de hello mediante pasos de hello enumerados en [toodownload revisiones](#to-download-hotfixes) toosearch para y descargar KB3121899, que instala las actualizaciones de firmware de disco (hello otras actualizaciones deben ya estén instalados por ahora).
3. Siga los pasos de hello enumerados en [instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes) actualizaciones del modo de mantenimiento de tooinstall Hola. 

## <a name="install-update-22-as-a-hotfix"></a>Instalar Update 2.2 como una revisión
Utilice este procedimiento si se producirá un error de comprobación de la puerta de enlace de hello al tratar de actualizaciones de hello tooinstall a través de hello portal de Azure clásico. se produce un error en la comprobación de Hello como tiene una puerta de enlace asignada tooa no son de datos interfaz de red 0 y el dispositivo está ejecutando una versión de software anterior tooUpdate 1.

versiones de software de Hola que se pueden actualizar utilizando el método de revisión de hello son:

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1 

> [!IMPORTANT]
> * Si su dispositivo ejecuta la versión de lanzamiento (GA), póngase en contacto con [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist con hello actualizar.
> 
> 

método de revisión de Hello implica Hola siga tres pasos:

* Descargan las revisiones de Hola de hello catálogo de Microsoft Update.
* Instalar y comprobar las revisiones de modo normal de Hola.
* Instalar y comprobar la revisión del modo de mantenimiento de hello (solo cuando la actualización de software 2 anterior a la actualización).

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Descarga de actualizaciones para un dispositivo que ejecuta el software Update 2.1
**Si el dispositivo está ejecutando 2.1 actualizar**, debe descargar la actualización de software de dispositivo de hello solo KB3179904. Solo se instalan archivos binarios de hello prologa con 'all-hcsmdssoftwareudpate'. No se instala Hola elementos de configuración y actualización del agente de hello MDS se prologa con `all-cismdsagentupdatebundle`. Error toodo por lo que se producirá un error. Se trata de una actualización sin interrupciones, no se interrumpirán las E/S y dispositivos de hello no tendrá ningún tiempo de inactividad.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Descarga de actualizaciones para un dispositivo que ejecuta el software Update 2
**Si su dispositivo ejecuta Update 2**, también debe descargar e instalar Hola siguiendo las revisiones en hello lo prescrito, orden:

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Actualización de software &#42; |Regular  <br></br>Sin interrupciones |~45 min |
| 2. |KB3146621 |Paquete iSCSI |Regular  <br></br>Sin interrupciones |~20 min |
| 3. |KB3103616 |Paquete WMI |Regular  <br></br>Sin interrupciones |~12 min |

 &#42;  *Tenga en cuenta que la actualización de software consta de dos archivos binarios: actualización de software de dispositivo se prologa con `all-hcsmdssoftwareupdate` Hola Cis y agente de Mds se prologa con `all-cismdsagentupdatebundle`. actualización de software de dispositivo de Hola debe instalarse antes de agente de elementos de configuración y Mds Hola. También debe reiniciar el controlador activo de Hola a través de hello `Restart-HcsController` cmdlet después de aplicar hello elementos de configuración y actualización del agente de MDS (y antes de aplicar Hola actualizaciones restantes).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Descarga de actualizaciones para un dispositivo que ejecuta un software anterior a Update 2
**Si el dispositivo está ejecutando versiones 0,2, 0,3, 1.0 y 1.1**, debe descargar e instalación Hola LSI controladores y firmware además actualizan software toohello, iSCSI y las actualizaciones WMI. Esta actualización ya está instalada si ejecuta Update 1.2 o 2. 

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |Controlador LSI y firmware |Regular  <br></br>Sin interrupciones |~20 min |

<br></br>
**Si el dispositivo está ejecutando versiones 0,2, 0,3, 1.0, 1.1 y 1.2**, debe descargar e instalar hello Spaceport y corrección de Storport Hola. Ya estarán instaladas si ejecuta Update 2.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Revisión de Spaceport  </br> Windows Server 2012 R2 |Regular  <br></br>Sin interrupciones |~20 min |
| 6. |KB3080728 |Revisión de Storport  </br> Windows Server 2012 R2 |Regular  <br></br>Sin interrupciones |~20 min |

<br></br>
También puede que tenga las actualizaciones de firmware de disco tooinstall. Puede comprobar si necesita hello las actualizaciones de firmware de disco mediante la ejecución de hello `Get-HcsFirmwareVersion` cmdlet. Si se ejecutan estas versiones de firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, a continuación, no es necesario tooinstall estas actualizaciones.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Firmware del disco |Mantenimiento  <br></br>Perjudicial |~30 min |

<br></br>

> [!IMPORTANT]
> * Esta toobe de necesidades de procedimiento realiza solo una vez tooapply 2.2 de actualización. Puede usar las actualizaciones posteriores de hello Azure tooapply portal clásico.
> * Si la actualización de la actualización 2, la hora de instalación total hello es cerrar too1.5 horas.
> * Antes de usar este Hola de tooapply procedimiento actualizar, asegúrese de que ambos controladores de dispositivo de hello están en línea y todos los componentes de hardware de hello están en buen Estados.
> 
> 

Realizar Hola después toodownload pasos e instalar las revisiones de Hola.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [versión 2.1 de actualización](storsimple-update21-release-notes.md).

