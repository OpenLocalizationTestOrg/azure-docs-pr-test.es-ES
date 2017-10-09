---
title: directivas de copia de seguridad aaaManage StorSimple 8000 series | Documentos de Microsoft
description: "Explica cómo puede utilizar toocreate de servicio del Administrador de dispositivos de StorSimple de Hola y administrar copias de seguridad manuales, las programaciones de copia de seguridad y retención de copia de seguridad en un dispositivo de la serie StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Usar el servicio de administrador de dispositivos de StorSimple de hello en las directivas de copia de seguridad de Azure toomanage portal


## <a name="overview"></a>Información general

Este tutorial le explica cómo toouse Hola servicio Administrador de dispositivos de StorSimple **directiva de copia de seguridad** procesos de copia de seguridad de toocontrol de hoja y retención de copia de seguridad de los volúmenes de StorSimple. También se describe cómo toocomplete una copia de seguridad manual.

Al hacer copia de seguridad de un volumen, puede elegir toocreate una instantánea local o una instantánea en la nube. Si está realizando una copia de seguridad de un volumen anclado localmente, se recomienda que especifique una instantánea de nube. La realización de un gran número de instantáneas de un volumen anclado localmente junto con un conjunto de datos que tenga una gran cantidad actividad dará como resultado una situación en la que podría quedarse rápidamente sin espacio local. Si elige tootake instantáneas locales, se recomienda que ocupan menos tooback instantáneas diarias estado más reciente de hello, mantenerlas durante un mismo día y eliminarlos.

Al tomar una instantánea de nube de un volumen anclado localmente, copiar solo Hola cambiar datos toohello en la nube, donde se desduplican y comprimido.

## <a name="hello-backup-policy-blade"></a>hoja de directiva de copia de seguridad de Hola

Hola **directiva de copia de seguridad** hoja para el dispositivo StorSimple permite las directivas de copia de seguridad de toomanage y programación local y en la nube. Directivas de copia de seguridad son programaciones de copia de seguridad utilizados tooconfigure y retención de copia de seguridad de un conjunto de volúmenes. Directivas de copia de seguridad le permiten tootake una instantánea de varios volúmenes simultáneamente. Esto significa que las copias de seguridad de hello creados por una directiva de copia de seguridad estará copias coherente para bloqueos.

lista tabular de directivas de copia de seguridad de Hola también permite toofilter Hola copia de seguridad las directivas existentes por uno o varios de hello después de campos:

* **Nombre de la directiva** : hello nombre asociado con la directiva de Hola. Hola distintos tipos de directivas incluyen:

  * Directivas programadas, creadas explícitamente por el usuario de Hola.
  * Las directivas importadas, creadas originalmente en hello StorSimple Snapshot Manager. Estas tienen una etiqueta que describe Hola Administrador de instantáneas StorSimple host que se importaron las directivas de Hola de.

  > [!NOTE]
  > Directivas de copia de seguridad automática o de forma predeterminada ya no están habilitadas en tiempo de Hola para crear un volumen.

* **Última copia de seguridad correcta** : Hola fecha y hora de hello última copia de seguridad correcta realizada con esta directiva.

* **Siguiente copia de seguridad** : Hola fecha y hora de hello siguiente copia de seguridad programada iniciada por esta directiva.

* **Volúmenes** : Hola volúmenes asociados con la directiva de Hola. Todos los volúmenes de hello asociados a una directiva de copia de seguridad se agrupan cuando se crean las copias de seguridad.

* **Programaciones** : Hola número de programaciones asociadas a la directiva de copia de seguridad de Hola.

operaciones de Hola de uso frecuente que puede realizar para las directivas de copia de seguridad son:

* Agregar una directiva de copia de seguridad
* Incorporación o modificación de una programación
* Incorporación o eliminación de un volumen
* Eliminación de una directiva de copia de seguridad
* Creación de una copia de seguridad manual

## <a name="add-a-backup-policy"></a>Agregar una directiva de copia de seguridad

Agregar una programación de tooautomatically de directiva de copia de seguridad de las copias de seguridad. Cuando crea un volumen por primera vez, no hay ninguna directiva de copia de seguridad predeterminada asociada a este. Es necesario tooadd y asignar una directiva de copia de seguridad tooprotect volumen de datos.

Realizar pasos de hello tooadd portal Azure una directiva de copia de seguridad para el dispositivo StorSimple de Hola. Después de Agregar directiva hello, puede definir una programación (vea [agregar o modificar una programación](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Incorporación o modificación de una programación

Puede agregar o modificar una programación que está adjunto tooan directiva de copia de seguridad existente en el dispositivo StorSimple. Realizar Hola pasos de hello Azure tooadd portal o modificar una programación.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Incorporación o eliminación de un volumen

Puede agregar o quitar un volumen asignado tooa directiva de copia de seguridad en el dispositivo StorSimple. Realizar Hola pasos de hello Azure tooadd portal o quitar un volumen.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Eliminación de una directiva de copia de seguridad

Realizar Hola siguiendo los pasos indicados en hello toodelete portal Azure una directiva de copia de seguridad en el dispositivo StorSimple.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Creación de una copia de seguridad manual

Realizar pasos de hello toocreate portal Azure bajo demanda (manual) copia de seguridad de un único volumen de Hola.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

