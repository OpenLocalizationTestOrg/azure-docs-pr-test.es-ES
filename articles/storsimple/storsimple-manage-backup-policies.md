---
title: aaaManage las directivas de copia de seguridad de StorSimple | Documentos de Microsoft
description: "Explica cómo puede utilizar toocreate de servicio de StorSimple Manager hello y administrar copias de seguridad manuales, las programaciones de copia de seguridad y retención de copia de seguridad."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a>Usar directivas de copia de seguridad toomanage del servicio de administrador de StorSimple de Hola
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Información general
Este tutorial le explica cómo toouse Hola el servicio StorSimple Manager **directivas de copia de seguridad** página procesos de copia de seguridad de toocontrol y retención de copia de seguridad de los volúmenes de StorSimple. También se describe cómo toocomplete una copia de seguridad manual.

Hola **directivas de copia de seguridad** página permite las directivas de copia de seguridad de toomanage y programación local y en la nube. (Las directivas de copia de seguridad son programaciones de copia de seguridad de tooconfigure usado y retención de copia de seguridad de un conjunto de volúmenes). Directivas de copia de seguridad le permiten tootake una instantánea de varios volúmenes simultáneamente. Esto significa que las copias de seguridad de hello creados por una directiva de copia de seguridad estará copias coherente para bloqueos. Esta página enumera las directivas de copia de seguridad de hello, sus tipos, volúmenes Hola asociado, número de Hola de copias de seguridad retenidas y Hola tooenable opción estas directivas.

Hola **directivas de copia de seguridad** página también permite toofilter Hola copia de seguridad las directivas existentes por uno o varios de hello siguientes campos:

* **Nombre de la directiva** : hello nombre asociado con la directiva de Hola. Hola distintos tipos de directivas incluyen:
  
  * Directivas programadas, creadas explícitamente por el usuario de Hola.
  * Directivas automáticas, que se crean cuando se habilitó la copia de seguridad de hello predeterminado para esta opción de volumen en tiempo de Hola para crear un volumen. Estas directivas se denominan Nombredevolumen_predeterminado donde el nombre de volumen hace referencia toohello nombre de volumen de StorSimple configurado por el usuario de hello en el portal de Azure clásico Hola Hola. directivas automáticas Hola dar lugar a instantáneas diarias en la nube empezando por hora del dispositivo 22:30.
  * Las directivas importadas, creadas originalmente en hello StorSimple Snapshot Manager. Estas tienen una etiqueta que describe Hola Administrador de instantáneas StorSimple host que se importaron las directivas de Hola de.
* **Volúmenes** : Hola volúmenes asociados con la directiva de Hola. Todos los volúmenes de hello asociados a una directiva de copia de seguridad se agrupan cuando se crean las copias de seguridad.
* **Última copia de seguridad correcta** : Hola fecha y hora de hello última copia de seguridad correcta realizada con esta directiva.
* **Siguiente copia de seguridad** : Hola fecha y hora de hello siguiente copia de seguridad programada iniciada por esta directiva.
* **Programaciones** : Hola número de programaciones asociadas a la directiva de copia de seguridad de Hola.

operaciones de Hola de uso frecuente que puede realizar desde esta página son:

* Agregar una directiva de copia de seguridad 
* Incorporación o modificación de una programación 
* Eliminación de una directiva de copia de seguridad 
* Creación de una copia de seguridad manual 
* Creación de una directiva de copia de seguridad personalizada con varios volúmenes y programaciones 

## <a name="add-a-backup-policy"></a>Agregar una directiva de copia de seguridad
Agregar una programación de tooautomatically de directiva de copia de seguridad de las copias de seguridad. Realizar Hola siguiendo los pasos de hello tooadd portal clásico una directiva de copia de seguridad para el dispositivo StorSimple de Azure. Después de Agregar directiva hello, puede definir una programación (vea [agregar o modificar una programación](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![Vídeo disponible](./media/storsimple-manage-backup-policies/Video_icon.png)**Vídeo disponible**

Haga clic en un vídeo que muestra cómo toocreate una variable local o en la nube de copia de seguridad Directiva, toowatch [aquí](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Incorporación o modificación de una programación
Puede agregar o modificar una programación que está adjunto tooan directiva de copia de seguridad existente en el dispositivo StorSimple. Realizar pasos de hello Azure tooadd portal clásico de Hola o modificar una programación.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>Eliminación de una directiva de copia de seguridad
Realizar Hola siguiendo los pasos indicados en hello toodelete portal clásico una directiva de copia de seguridad de Azure en el dispositivo StorSimple.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Creación de una copia de seguridad manual
Realizar pasos de hello Azure toocreate portal clásico a petición (manual) copia de seguridad de un único volumen de Hola.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Creación de una directiva de copia de seguridad personalizada con varios volúmenes y programaciones
Realizar Hola pasos de hello toocreate portal clásico una directiva de copia de seguridad personalizada que tiene varios volúmenes y programas de Azure.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

