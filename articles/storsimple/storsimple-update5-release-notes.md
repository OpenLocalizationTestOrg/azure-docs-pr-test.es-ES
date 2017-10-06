---
title: "notas de la versión de aaaStorSimple 8000 Series Update 5 | Documentos de Microsoft"
description: "Describe nuevas características de hello, problemas y soluciones alternativas para StorSimple 8000 Series Update 5."
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>Notas de la versión de la serie StorSimple 8000 Update 5

## <a name="overview"></a>Información general

Hello siguientes notas de la versión describen características nuevas de hello e identifican problemas abiertos críticos de Hola para StorSimple 8000 Series Update 5. También contienen una lista de las actualizaciones de software de StorSimple Hola incluidos en esta versión.

La actualización 5 puede ser dispositivo de StorSimple de tooany aplicado ejecutar Update 0,1 a través de la actualización 4. versión del dispositivo Hola asociado con la actualización 5 es 6.3.9600.17845.

Revise la información de hello contenida en la versión de Hola notas antes de implementar Hola actualización de la solución StorSimple.

> [!IMPORTANT]
> * Update 5 tiene software de dispositivo, firmware del disco, seguridad del sistema operativo y otras actualizaciones del sistema operativo. Tarda aproximadamente 4 horas tooinstall esta actualización. La actualización del firmware de disco es una actualización perjudicial y provoca un tiempo de inactividad en el dispositivo. Se recomienda aplicar actualización 5 tookeep su dispositivo actualizado.
> * Para cada versión nueva, quizás no pueda ver las actualizaciones inmediatamente porque se realiza una implementación por fases de actualizaciones de Hola. Espere unos días y luego busque actualizaciones de nuevo, ya que estas estarán disponibles pronto.

## <a name="whats-new-in-update-5"></a>Novedades de Update 5

Hello siguientes claves mejoras y correcciones de errores se realizaron en la actualización 5.

* **Uso de tooauthenticate de Azure Active Directory (AAD) con el servicio de administrador de dispositivos de StorSimple** – de actualización 5 y versiones posteriores, Azure Active Directory es tooauthenticate usado con el servicio de administrador de dispositivos de StorSimple Hola. mecanismo de autenticación de Hello antigua dejará de utilizarse por diciembre de 2017. Todos los usuarios de hello deben incluir Hola nuevas direcciones URL de la autenticación en sus reglas de firewall. Para obtener más información, consulte demasiado[URL de autenticación que figuran en hello requisitos de red para el dispositivo StorSimple](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Si no se incluye la dirección URL de la autenticación de Hola en las reglas de firewall de hello, los usuarios de hello verán una alerta crítica que su dispositivo de StorSimple no pudo autenticar con el servicio de Hola. Si los usuarios de hello vean esta alerta, deberá tooinclude Hola nueva autenticación dirección URL. Para obtener más información, consulte demasiado[StorSimple redes alertas](storsimple-8000-manage-alerts.md#networking-alerts).

* **Nueva versión de StorSimple Snapshot Manager**: con Update 5 se lanza una nueva versión de StorSimple Snapshot Manager. Se recomienda que actualice la versión de toothis. Esta versión es compatible con todos los dispositivos de StorSimple de Hola que ejecutan la actualización 3 o posterior. Para obtener más información, consulte demasiado[implementar Administrador de instantáneas StorSimple](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Problemas corregidos en Update 5

Hello tabla siguiente proporciona un resumen de los problemas que se corrigieron en actualización 5.

| No | Característica | Problema | Se aplica a dispositivos toophysical | Se aplica a dispositivos toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Comunicación remota de Windows PowerShell |En la versión anterior de hello, un usuario recibiría un error al tratar de tooestablish un dispositivo de StorSimple en la nube mediante Windows PowerShell toohello de conexión remota. La causa raíz de este problema se corrigió en esta versión. |No |Sí |
| 2 |Plantillas de ancho de banda |En las versiones anteriores, hubo un problema con las plantillas de ancho de banda que dan como resultado un ancho de banda inferior a qué dispositivo Hola se configuró para. Este problema se ha corregido en esta versión. |Sí |Sí |
| 3 |Conmutación por error |En la versión anterior, cuando un dispositivo con un gran número de volúmenes se conmutó por dispositivo de tooanother ejecutar la actualización 4, proceso de hello produciría un error al tratar de registros de control de acceso de tooapply Hola. Este problema está corregido en esta versión. |Sí |Sí |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Problemas conocidos en Update 5 de las versiones anteriores

No hay ningún problema conocido en Update 5. Para obtener una lista de problemas que se realiza a través de tooUpdate 5 de las versiones anteriores, vaya demasiado[notas de la versión de actualización 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Controlador SCSI conectado en serie (SAS) y actualizaciones de firmware en Update 5

Esta versión tiene actualizaciones de firmware y controlador LSI y controlador SAS. Para obtener más información sobre cómo tooinstall estas actualizaciones, consulte [instalar la actualización 5](storsimple-8000-install-update-5.md) en el dispositivo StorSimple.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Actualizaciones de StorSimple Cloud Appliance en Update 5

Esta actualización no puede ser aplicada toohello dispositivo de StorSimple en la nube (también conocido como Hola dispositivo virtual). Nuevos dispositivos en la nube necesitan toobe creado mediante imagen Hola actualización 5. Para obtener información acerca de cómo toocreate un dispositivo StorSimple de nube, vaya demasiado[implementar y administrar un dispositivo de nube de StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Paso siguiente

Obtenga información acerca de cómo demasiado[instalar la actualización 5](storsimple-8000-install-update-5.md) en el dispositivo StorSimple.

