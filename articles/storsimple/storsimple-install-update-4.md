---
title: "aaaInstall actualización 4 en el dispositivo StorSimple | Documentos de Microsoft"
description: "Explica cómo tooinstall StorSimple 8000 Series Update 4 en el dispositivo de la serie StorSimple 8000."
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
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Instalación de Update 4 en el dispositivo StorSimple

## <a name="overview"></a>Información general

Este tutorial le explica cómo tooinstall actualización 4 en un dispositivo de StorSimple con una versión anterior del software a través de Hola portal de Azure clásico y usar el método de revisión de hello. método de revisión de Hola se usa cuando se configura una puerta de enlace en una interfaz de red diferentes a DATA 0 del dispositivo de StorSimple de Hola y que está tratando de tooupdate desde una versión de software anterior a Update 1.

Update 4 incluye actualizaciones de software de dispositivo, firmware de USM, firmware y controlador LSI, Storport y Spaceport, seguridad de SO y varias otras actualizaciones de SO.  software de dispositivo de Hello, firmware USM, Spaceport, Storport y otras actualizaciones de sistema operativo son actualizaciones sin interrupciones. Hola no provocan interrupciones o regular actualizaciones pueden aplicarse a través del portal de Azure clásico de Hola o método de revisión de hello. las actualizaciones de firmware de disco Hola son actualizaciones potencialmente perjudiciales y solo pueden aplicarse a través del método de revisión de hello mediante la interfaz de Windows PowerShell de hello de dispositivo de Hola. 

> [!IMPORTANT]
> * Un conjunto de comprobaciones previas manuales y automáticas se realiza el estado del dispositivo anterior toohello instalación toodetermine hello en cuanto a conectividad de red y el estado de hardware. Estas comprobaciones previas se realizan solo si aplicar actualizaciones de Hola de hello portal de Azure clásico.
> * Se recomienda que instale software de Hola y otras actualizaciones periódicas a través de hello portal de Azure clásico. Solo debería ir toohello de interfaz de Windows PowerShell del dispositivo de hello (tooinstall actualizaciones) si se produce un error en la comprobación de la puerta de enlace anterior a la actualización de hello en el portal de Hola. Según la versión de Hola que va a actualizar desde, Hola actualizaciones pueden tardar cuatro horas (o posterior) tooinstall. actualizaciones del modo de mantenimiento de Hello también deben instalarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. Como las actualizaciones en modo de mantenimiento son perturbadoras, generarán un tiempo de inactividad para el dispositivo.
> * Si ejecuta hello opcional Administrador de instantáneas de StorSimple, asegúrese de que ha actualizado el dispositivo de administrador de instantáneas versión tooUpdate 4 anteriores tooupdating Hola.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>Instalar la actualización 4 a través del portal de Azure clásico Hola
Realizar el dispositivo Hola siguiendo los pasos tooupdate demasiado[actualización 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Si va a aplicar la actualización 2 o posterior (incluidas Update 2.1), Microsoft será capaz de toopull información de diagnóstico adicional desde dispositivo Hola. Como resultado, cuando el equipo de operaciones identifica los dispositivos que están experimentando problemas, estamos mejor equipada toocollect información de hello dispositivo y diagnosticar problemas. Al aceptar Update 2 o posterior, nos permitirá tooprovide esta compatibilidad automático. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Compruebe que el dispositivo está ejecutando **StorSimple 8000 Series Update 4 (6.3.9600.17820)**. Hola **actualizó por última vez fecha** también se debe modificar. 

* Ahora verá que hay disponibles actualizaciones de modo de mantenimiento de hello (este mensaje podría continuar toobe mostrado por la too24 horas después de instalar Hola actualizaciones). Actualizaciones del modo de mantenimiento son actualizaciones potencialmente perjudiciales que provocar tiempos de inactividad del dispositivo y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello del dispositivo.
 
* Descargar actualizaciones de modo de mantenimiento de hello mediante pasos de hello enumerados en [toodownload revisiones](#to-download-hotfixes) toosearch para y descargar KB4011837, que instala las actualizaciones de firmware de disco (hello otras actualizaciones deben ya estén instalados por ahora). Siga los pasos de hello enumerados en [instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes) actualizaciones del modo de mantenimiento de tooinstall Hola. 

## <a name="install-update-4-as-a-hotfix"></a>Instalación de Update 4 como una revisión
Hola recomienda tooinstall método que actualización 4 es a través de hello portal de Azure clásico.

Utilice este procedimiento si se producirá un error de comprobación de la puerta de enlace de hello al tratar de actualizaciones de hello tooinstall a través de hello portal de Azure clásico. se produce un error en la comprobación de Hello como tiene una puerta de enlace asignada tooa no son de datos interfaz de red 0 y el dispositivo está ejecutando una versión de software anterior tooUpdate 1.

versiones de software de Hola que se pueden actualizar utilizando el método de revisión de hello son:

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1, 2.2
* Update 3, 3.1 


método de revisión de Hello implica Hola siga tres pasos:

1. Descargan las revisiones de Hola de hello catálogo de Microsoft Update.
2. Instalar y comprobar las revisiones de modo normal de Hola.
3. Instalar y comprobar las revisiones de modo de mantenimiento de Hola.

#### <a name="download-updates-for-your-device"></a>Descargar las actualizaciones para el dispositivo

Debe descargar e instalar los siguientes Hola revisiones en hello lo prescrito, ordenar y Hola carpetas sugeridas:

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |Carpeta de instalación|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 archivos) |Actualización de software del dispositivo <br> Actualización del agente CiS/MDS |Regular  <br></br>Sin interrupciones |~ 25 min |FirstOrderUpdate <br> _Instale la actualización de software del dispositivo antes que la actualización del agente CiS/MDS._|
| 2A. |KB4011841 <br> KB4011842 |Actualizaciones de firmware y controlador LSI <br> Actualización de firmware de USM (versión 3.38) |Regular  <br></br>Sin interrupciones |~ 3 horas <br> (incluye 2A. + 2B. + 2C).|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |Paquete de actualizaciones de seguridad de SO |Regular  <br></br>Sin interrupciones |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Paquete de actualizaciones de SO |Regular  <br></br>Sin interrupciones |- |SecondOrderUpdate|

También puede que tenga las actualizaciones de firmware de disco tooinstall encima de todas las actualizaciones de Hola que se muestra en hello anterior tablas. Puede comprobar si necesita hello las actualizaciones de firmware de disco mediante la ejecución de hello `Get-HcsFirmwareVersion` cmdlet. Si se ejecutan estas versiones de firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, a continuación, no es necesario tooinstall estas actualizaciones.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación | Carpeta de instalación|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |Firmware del disco |Mantenimiento  <br></br>Perjudicial |~30 min | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Esta toobe de necesidades de procedimiento realiza solo una vez tooapply actualización 4. Puede usar las actualizaciones posteriores de hello Azure tooapply portal clásico.
> * Si actualiza desde la actualización 3 ó 3.1, la hora de instalación total hello es cerrar too4 horas.
> * Antes de usar este Hola de tooapply procedimiento actualizar, asegúrese de que ambos controladores de dispositivo de hello están en línea y todos los componentes de hardware de hello están en buen Estados.

Realizar Hola después toodownload pasos e instalar las revisiones de Hola.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [versión Update 4](storsimple-update4-release-notes.md).

