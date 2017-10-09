---
title: "aaaManage los contenedores de volúmenes de StorSimple | Documentos de Microsoft"
description: "Explica cómo puede usar hello StorSimple Manager página tooadd contenedores de volúmenes de servicio, modificar o eliminación un contenedor de volúmenes."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>Utilizar contenedores de volúmenes de StorSimple de hello StorSimple Manager servicio toomanage
## <a name="overview"></a>Información general
Este tutorial le explica cómo toouse Hola toocreate de servicio de StorSimple Manager y administrar contenedores de volúmenes de StorSimple.

En un dispositivo Microsoft Azure StorSimple, los contenedores de volúmenes contienen uno o varios volúmenes que comparten la configuración de cuentas de almacenamiento, cifrado y consumo de ancho de banda. Un dispositivo puede tener varios contenedores de volúmenes para todos sus volúmenes. 

Un contenedor de volúmenes tiene Hola siguientes atributos:

* **Volúmenes** : Hola en niveles o anclado localmente los volúmenes de StorSimple que se encuentran dentro del contenedor de volúmenes de Hola. Un contenedor de volúmenes puede contener too256 volúmenes de StorSimple.
* **Cifrado** : una clave de cifrado que se puede definir para cada contenedor de volúmenes. Esta clave se utiliza para cifrar los datos de Hola que se envían desde el dispositivo de StorSimple toohello de la nube. Se utiliza una clave de grado militar AES-256 bits con clave de hello escrito por el usuario. toosecure los datos, se recomienda habilitar siempre el cifrado de almacenamiento en nube.
* **Cuenta de almacenamiento** : Hola cuenta de almacenamiento que es el proveedor de servicios de almacenamiento de nube tooyour vinculado. Todos los volúmenes de Hola que residen en un contenedor de volúmenes comparten esta cuenta de almacenamiento. Puede elegir una cuenta de almacenamiento de una lista existente o crear una nueva cuenta al crear el contenedor de volúmenes de hello y, a continuación, especifique las credenciales de acceso de Hola para esa cuenta.
* **Ancho de banda en la nube** : Hola ancho de banda consumido por dispositivo de hello cuando se envía datos de hello de dispositivo de hello toohello en la nube. Puede aplicar un control del ancho de banda especificando un valor entre 1 y 1000 Mbps al definir este contenedor. Si desea Hola dispositivo tooconsume ancho de banda disponible en todos los, establezca este campo tooUnlimited. También puede crear y aplicar un ancho de banda tooallocate del plantilla de ancho de banda basada en programación.

![Página Contenedores de volúmenes](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

Este procedimientos siguientes explican cómo toouse Hola StorSimple **contenedores de volúmenes** hello toocomplete de página después de las operaciones comunes:

* Agregar un contenedor de volúmenes 
* Modificar un contenedor de volúmenes 
* Eliminar un contenedor de volúmenes 

## <a name="add-a-volume-container"></a>Agregar un contenedor de volúmenes
Realizar Hola siguiendo los pasos tooadd un contenedor de volúmenes.

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificar un contenedor de volúmenes
Realizar Hola siguiendo los pasos toomodify un contenedor de volúmenes.

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Eliminar un contenedor de volúmenes
Los contenedores de volúmenes contienen volúmenes. Se puede eliminar solo si primero se eliminan todos los volúmenes de hello contenidos en ella. Realizar Hola siguiendo los pasos toodelete un contenedor de volúmenes.

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-manage-volumes.md). 
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

