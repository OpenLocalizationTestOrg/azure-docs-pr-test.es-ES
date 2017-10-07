---
title: "aaaInstall actualización 5 en el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft"
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>Instalación de Update 5 en el dispositivo StorSimple

## <a name="overview"></a>Información general

Este tutorial le explica cómo tooinstall 5 de actualización en un dispositivo de StorSimple con una versión anterior del software a través de Hola portal de Azure y usar el método de revisión de hello. método de revisión de Hola se usa cuando se configura una puerta de enlace en una interfaz de red diferentes a DATA 0 del dispositivo de StorSimple de Hola y que está tratando de tooupdate desde una versión de software anterior a Update 1.

Update 5 incluye actualizaciones de software de dispositivo, firmware de USM, firmware y controlador LSI, Storport y Spaceport, seguridad del sistema operativo y varias otras actualizaciones de SO.  software de dispositivo de Hello, Spaceport, Storport, seguridad y otras actualizaciones de sistema operativo son actualizaciones sin interrupciones. Hola no provocan interrupciones o regular actualizaciones pueden aplicarse a través del portal de Azure de Hola o método de revisión de hello. las actualizaciones de firmware de disco Hola son actualizaciones potencialmente perjudiciales y se aplican al dispositivo de hello está en modo de mantenimiento a través del método de revisión de hello mediante la interfaz de Windows PowerShell de hello de dispositivo de Hola.

> [!IMPORTANT]
> * Un conjunto de comprobaciones previas manuales y automáticas se realiza el estado del dispositivo anterior toohello instalación toodetermine hello en cuanto a conectividad de red y el estado de hardware. Estas comprobaciones previas se realizan solo si aplicar actualizaciones de Hola de hello portal de Azure.
> * Se recomienda que instale software de Hola y otras actualizaciones periódicas a través de hello portal de Azure. Solo debería ir toohello de interfaz de Windows PowerShell del dispositivo de hello (tooinstall actualizaciones) si se produce un error en la comprobación de la puerta de enlace anterior a la actualización de hello en el portal de Hola. Según la versión de Hola que va a actualizar desde, Hola actualizaciones pueden tardar cuatro horas (o posterior) tooinstall. actualizaciones del modo de mantenimiento de Hello deben instalarse a través de la interfaz de Windows PowerShell de hello de dispositivo de Hola. Como las actualizaciones en modo de mantenimiento generan interrupciones, provocan un tiempo de inactividad en el dispositivo.
> * Si ejecuta hello opcional Administrador de instantáneas de StorSimple, asegúrese de que ha actualizado el dispositivo de Hola de administrador de instantáneas versión tooUpdate 5 tooupdating anterior.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Instalar la actualización 5 a través de hello portal de Azure
Realizar el dispositivo Hola siguiendo los pasos tooupdate demasiado[actualización 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft extrae información de diagnóstico adicional desde dispositivo Hola. Como resultado, cuando el equipo de operaciones identifica los dispositivos que están experimentando problemas, estamos mejor equipada toocollect información de hello dispositivo y diagnosticar problemas.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Compruebe que el dispositivo está ejecutando **StorSimple 8000 Series Update 5 (6.3.9600.17845)**. Hola **actualizó por última vez fecha** debe modificarse.

* Ahora verá que hay disponibles actualizaciones de modo de mantenimiento de hello (este mensaje podría continuar toobe mostrado por la too24 horas después de instalar Hola actualizaciones). Actualizaciones del modo de mantenimiento son actualizaciones potencialmente perjudiciales que provocar tiempos de inactividad del dispositivo y solo pueden aplicarse a través de la interfaz de Windows PowerShell de hello del dispositivo.

* Descargar actualizaciones de modo de mantenimiento de hello mediante pasos de hello enumerados en [toodownload revisiones](#to-download-hotfixes) toosearch para y descargar KB4011837, que instala las actualizaciones de firmware de disco (hello otras actualizaciones deben ya estén instalados por ahora). Siga los pasos de hello enumerados en [instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes) actualizaciones del modo de mantenimiento de tooinstall Hola.

## <a name="install-update-5-as-a-hotfix"></a>Instalación de Update 5 como una revisión


versiones de software de Hola que se pueden actualizar utilizando el método de revisión de hello son:

* Update 0.1, 0.2, 0.3
* Update 1, 1.1, 1.2
* Update 2, 2.1, 2.2
* Update 3, 3.1
* Update 4

> [!NOTE] 
> Hola recomienda tooinstall método que 5 de actualización es a través de hello portal de Azure. Utilice este procedimiento si se producirá un error de comprobación de la puerta de enlace de hello al tratar de actualizaciones de hello tooinstall a través de hello portal de Azure. se produce un error en la comprobación de Hello cuando tiene una puerta de enlace asignada tooa no son de datos interfaz de red 0 y el dispositivo está ejecutando una versión de software anterior a Update 1.

método de revisión de Hello implica Hola siga tres pasos:

1. Descargan las revisiones de Hola de hello catálogo de Microsoft Update.
2. Instalar y comprobar las revisiones de modo normal de Hola.
3. Instalar y comprobar las revisiones de modo de mantenimiento de Hola.

#### <a name="download-updates-for-your-device"></a>Descargar las actualizaciones para el dispositivo

Debe descargar e instalar los siguientes Hola revisiones en hello lo prescrito, ordenar y Hola carpetas sugeridas:

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |Carpeta de instalación|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Actualización de software<br> Descargar tanto _HcsSfotwareUpdate.exe_ como _CisMSDAgent.exe_ |Regular  <br></br>Sin interrupciones |~ 25 min |FirstOrderUpdate|

Si actualiza desde un dispositivo que ejecuta Update 4, solo necesita actualizaciones acumulativas del sistema operativo de hello tooinstall como segundo actualizaciones de pedido.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |Carpeta de instalación|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |Paquete de actualizaciones acumulativas de SO <br> Descargar la versión R2 de Windows Server 2012 |Regular  <br></br>Sin interrupciones |- |SecondOrderUpdate|

Si la instalación de un dispositivo que ejecuta Update 3 o versiones anteriores, instale hello además siguiendo las actualizaciones acumulativas de toohello.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación |Carpeta de instalación|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |Actualizaciones de firmware y controlador LSI <br> Actualización de firmware de USM (versión 3.38) |Regular  <br></br>Sin interrupciones |~ 3 horas <br> (incluye 2A. + 2B. + 2C).|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |Paquete de actualizaciones de seguridad de SO <br> Descargar la versión R2 de Windows Server 2012 |Regular  <br></br>Sin interrupciones |- |SecondOrderUpdate|
| 2D. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |Paquete de actualizaciones de SO <br> Descargar la versión R2 de Windows Server 2012 |Regular  <br></br>Sin interrupciones |- |SecondOrderUpdate|


También puede que tenga las actualizaciones de firmware de disco tooinstall encima de todas las actualizaciones de Hola que se muestra en hello anterior tablas. Puede comprobar si necesita hello las actualizaciones de firmware de disco mediante la ejecución de hello `Get-HcsFirmwareVersion` cmdlet. Si se ejecutan estas versiones de firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, a continuación, no es necesario tooinstall estas actualizaciones.

| Orden | KB | Descripción | Tipo de actualización | Hora de instalación | Carpeta de instalación|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Firmware del disco |Mantenimiento  <br></br>Perjudicial |~30 min | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Si la actualización de la actualización 4, la hora de instalación total hello es cerrar too4 horas.
> * Antes de usar este Hola de tooapply procedimiento actualizar, asegúrese de que ambos controladores de dispositivo de hello están en línea y todos los componentes de hardware de hello están en buen Estados.

Realizar Hola después toodownload pasos e instalar las revisiones de Hola.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [actualización 5 versión](storsimple-update5-release-notes.md).

