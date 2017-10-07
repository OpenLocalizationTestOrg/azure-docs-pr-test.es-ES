---
title: "aaaManage los contenedores de volúmenes de StorSimple en el dispositivo de la serie StorSimple 8000 Hola | Documentos de Microsoft"
description: "Explica cómo puede usar Hola Administrador de dispositivos de StorSimple contenedores de volúmenes de servicio página tooadd, modificar o eliminación un contenedor de volúmenes."
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
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Utilizar contenedores de volúmenes de StorSimple de toomanage servicio de administrador de dispositivos de StorSimple de Hola

## <a name="overview"></a>Información general
Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar contenedores de volúmenes de StorSimple.

En un dispositivo Microsoft Azure StorSimple, los contenedores de volúmenes contienen uno o varios volúmenes que comparten la configuración de cuentas de almacenamiento, cifrado y consumo de ancho de banda. Un dispositivo puede tener varios contenedores de volúmenes para todos sus volúmenes. 

Un contenedor de volúmenes tiene Hola siguientes atributos:

* **Volúmenes** : Hola en niveles o anclado localmente los volúmenes de StorSimple que se encuentran dentro del contenedor de volúmenes de Hola. 
* **Cifrado** : una clave de cifrado que se puede definir para cada contenedor de volúmenes. Esta clave se utiliza para cifrar los datos de Hola que se envían desde el dispositivo de StorSimple toohello de la nube. Se utiliza una clave de grado militar AES-256 bits con clave de hello escrito por el usuario. toosecure los datos, se recomienda habilitar siempre el cifrado de almacenamiento en nube.
* **Cuenta de almacenamiento** : Hola cuenta de almacenamiento de Azure que sea utilizado toostore Hola datos. Todos los volúmenes de Hola que residen en un contenedor de volúmenes comparten esta cuenta de almacenamiento. Puede elegir una cuenta de almacenamiento de una lista existente o crear una nueva cuenta al crear el contenedor de volúmenes de hello y, a continuación, especifique las credenciales de acceso de Hola para esa cuenta.
* **Ancho de banda en la nube** : Hola ancho de banda consumido por dispositivo de hello cuando se envía datos de hello de dispositivo de hello toohello en la nube. Puede aplicar un control del ancho de banda especificando un valor entre 1 y 1000 Mbps al definir este contenedor. Si desea Hola dispositivo tooconsume ancho de banda disponible, establezca este campo demasiado**Unlimited**. También puede crear y aplicar un ancho de banda tooallocate del plantilla de ancho de banda basada en programación.

Hello procedimientos siguientes explican cómo toouse Hola StorSimple **contenedores de volúmenes** Hola de hoja toocomplete las siguientes operaciones comunes:

* Agregar un contenedor de volúmenes
* Modificar un contenedor de volúmenes
* Eliminar un contenedor de volúmenes

## <a name="add-a-volume-container"></a>Agregar un contenedor de volúmenes
Realizar Hola siguiendo los pasos tooadd un contenedor de volúmenes.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificar un contenedor de volúmenes
Realizar Hola siguiendo los pasos toomodify un contenedor de volúmenes.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Eliminar un contenedor de volúmenes
Los contenedores de volúmenes contienen volúmenes. Se puede eliminar solo si primero se eliminan todos los volúmenes de hello contenidos en ella. Realizar Hola siguiendo los pasos toodelete un contenedor de volúmenes.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-8000-manage-volumes-u2.md). 
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

