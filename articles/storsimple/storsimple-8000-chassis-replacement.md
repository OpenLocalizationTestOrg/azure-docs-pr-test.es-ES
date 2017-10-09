---
title: chasis de aaaReplace en el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo tooremove y reemplazar Hola chasis para el alojamiento principal de StorSimple o el alojamiento de EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Reemplazar el chasis de hello en el dispositivo StorSimple
## <a name="overview"></a>Información general
Este tutorial le explica cómo tooremove y reemplazar un chasis de un dispositivo de la serie StorSimple 8000. modelo de Hello StorSimple 8100 es un dispositivo de alojamiento (un chasis), mientras que Hola 8600 es un dispositivo de alojamiento doble (dos chasis). Para un modelo 8600, hay potencialmente dos chasis que pudieron producirse un error en el dispositivo de hello: Hola chasis para el alojamiento principal de Hola o chasis de Hola para hello alojamiento de EBOD.

En cualquier caso, el chasis de sustitución de Hola que Microsoft envía está vacío. No se incluirán Módulos de alimentación y refrigeración (PCM), módulos de controlador, unidades de disco de estado sólido (SSD), unidades de disco duro (HDD) o módulos EBOD.

> [!IMPORTANT]
> Antes de quitar y reemplazar el chasis de hello, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-hello-chassis"></a>Quitar el chasis de Hola
Realizar Hola después de chasis de pasos tooremove hello en el dispositivo StorSimple.

#### <a name="tooremove-a-chassis"></a>tooremove un chasis
1. Asegúrese de que ese dispositivo de StorSimple Hola está apagado y desconectado de todas las fuentes de alimentación de Hola.
2. Quite todos los red hello y cables SAS, si procede.
3. Quitar unidad de Hola de bastidor de Hola.
4. Quitar cada una de las unidades de Hola y anote las ranuras de Hola desde la que se quitan. Para obtener más información, consulte [quitar la unidad de disco de hello](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).
5. En hello alojamiento de EBOD (si se trata de chasis de Hola que no se pudo), quitar los módulos de controlador EBOD Hola. Para obtener más información, consulte [Quitar un controlador EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).
   
    En hello alojamiento principal (si se trata de chasis de Hola que no se pudo), quite los controladores de Hola y tenga en cuenta las ranuras de Hola desde la que se quitan. Para obtener más información, consulte [Quitar un controlador](storsimple-8000-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Instalar el chasis de Hola
Realizar Hola después de chasis de pasos tooinstall hello en el dispositivo StorSimple.

#### <a name="tooinstall-a-chassis"></a>tooinstall un chasis
1. Monte el chasis de hello en bastidor Hola. Para obtener más información, consulte [Montaje en bastidor del dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) o [Montaje en bastidor del dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Después de montar el chasis de hello en bastidor hello, instale los módulos de controlador de Hola Hola en que mismo coloca que estaban instaladas previamente.
3. Instalación Hola unidades en hello mismo posiciones y ranuras que estaban instaladas previamente en.
   
   > [!NOTE]
   > Se recomienda que instalar SSD de hello en los espacios de hello en primer lugar y, a continuación, instalar Hola HDD.
  
4. Con Hola dispositivo montado en bastidor de Hola y Hola se instalen, conectar los orígenes de dispositivo toohello alimentación adecuadas y encienda el dispositivo de Hola. Para obtener más información, consulte [Instalación de cables del dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [Instalación de cables StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).

