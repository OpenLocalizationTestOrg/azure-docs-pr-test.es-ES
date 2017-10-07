---
title: una unidad de disco en un dispositivo de la serie StorSimple 8000 aaaReplace | Documentos de Microsoft
description: "Explica cómo unidad tooreplace un disco en un alojamiento principal de StorSimple o un alojamiento de EBOD."
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
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a>Reemplazo de una unidad de disco en un dispositivo de la serie StorSimple 8000

## <a name="overview"></a>Información general
Este tutorial explica cómo quitar y reemplazar una unidad de disco duro que no funciona correctamente o defectuosa en un dispositivo StorSimple de Microsoft Azure. tooreplace una unidad de disco, debe:

* Desactivar el bloqueo contra manipulaciones Hola
* Quitar unidad de disco de Hola
* Instalar la unidad de disco de reemplazo de Hola

> [!IMPORTANT]
> Antes de quitar y reemplazar una unidad de disco, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).
 

## <a name="disengage-hello-antitamper-lock"></a>Desactivar el bloqueo contra manipulaciones Hola
Este procedimiento explica cómo se pueden acoplar o desacoplar al reemplazar unidades de disco de hello bloqueos contra manipulaciones de hello en el dispositivo StorSimple. los bloqueos contra manipulaciones Hola se ajustan en identificadores de portadora de unidad de Hola y se tiene acceso a través de una pequeña abertura en la sección del identificador hello enganche de Hola. Las unidades se suministran con hello bloqueos conjunto toohello bloqueado posición.

#### <a name="toounlock-hello-antitamper-lock"></a>bloqueo contra manipulaciones de hello toounlock
1. Inserte con cuidado la llave de bloqueo de hello (un destornillador T10 "impide las alteraciones" que Microsoft proporciona) en hello abertura identificador hello y en su zócalo. 
   
   Si está activado el bloqueo contra manipulaciones de hello, indicador de hello rojo esté visible en la abertura Hola.
  
    ![Unidad de disco bloqueada](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Figura 1** Bloqueo antisabotaje activado
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |Orificio indicador |
   | 2 |Bloqueo antisabotaje |
2. Gire la llave de hello en una dirección en sentido contrario hasta que no esté visible en la abertura Hola por encima de la clave de Hola indicador rojo Hola.
3. Quitar clave Hola.
   
    ![Unidad de disco desbloqueada](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Figura 2** Unidad de disco desbloqueada
4. Ahora se puede quitar la unidad de disco de Hola.

Siga los pasos de Hola de bloqueo de hello tooengage inversa.

## <a name="remove-hello-disk-drive"></a>Quitar unidad de disco de Hola
El dispositivo StorSimple es compatible con una configuración de espacios de almacenamiento similares a RAID 10. Esto implica que puede funcionar normalmente con un disco, unidad de estado sólido (SSD), o unidad de disco duro (HDD) defectuoso.

> [!IMPORTANT]
> * Si el sistema tiene más de un disco erróneo, no quite más de un SSD o HDD del sistema de Hola en cualquier momento en el tiempo. Esto puede provocar la pérdida de datos.
> * Asegúrese de colocar un SSD de reemplazo en una ranura que previamente contenía un SSD. Asegúrese de colocar un HDD de reemplazo en una ranura que previamente contenía un HDD.
> * Hola portal de Azure, las ranuras se numeran del 0 al 11. Por lo tanto, si el portal de hello muestra que un disco en la ranura 2 ha dado error, el dispositivo de hello, busque Hola disco erróneo en la tercera ranura a contar Hola desde parte superior de hello izquierda.
> 
> 

Unidades de disco pueden quitar y reemplazar mientras el sistema de hello está funcionando.

#### <a name="tooremove-a-drive"></a>tooremove una unidad
1. Hola tooidentify error de disco, en hello portal de Azure, vaya tooyour dispositivo **configuración > estado del Hardware**. Dado que puede producir un error en un disco en el alojamiento principal de Hola o en un alojamiento de EBOD (si está utilizando un modelo de 8600), mire estado de Hola de discos de hello en **componentes compartidos** y en **componentes compartidos de EBOD** . Un disco defectuoso en cualquier gabinete se mostrará con un estado rojo.
2. Busque las unidades de hello en la parte delantera de Hola de alojamiento principal de Hola o alojamiento de EBOD Hola. 
3. Si el disco de hello no está bloqueado, continúe toohello siguiente paso. Si está bloqueado el disco de hello, desbloquéelo siguiendo el procedimiento de hello en [desactivar el bloqueo contra manipulaciones de hello](#disengage-the-antitamper-lock).
4. Presione Hola negro bloqueos temporales en el módulo portador de unidades de Hola y de extracción asa Hola hacia afuera desde la parte frontal de Hola de chasis de Hola.
   
    ![Liberar el asa de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Figura 3** asa de si se liberan Hola
5. Cuando el asa Hola esté completamente extendida, deslice el portador de unidades de hello fuera del chasis de Hola. 
   
    ![Deslizamiento del disco fuera de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Figura 4** deslizante Hola de unidad de disco fuera de transportista Hola

## <a name="install-hello-replacement-disk-drive"></a>Instalar la unidad de disco de reemplazo de Hola
Después de una unidad de error en el dispositivo StorSimple y haya extraído, siga este procedimiento tooreplace con una nueva unidad.

#### <a name="tooinsert-a-drive"></a>tooinsert una unidad
1. Asegúrese de asa Hola esté completamente extendida, tal como se muestra en hello después de la imagen.
   
    ![Unidad de disco con asa extendida](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Figura 5** Unidad con asa extendida
2. Deslice portador de unidades de hello todos forma hello en el chasis de Hola.
   
    ![Deslizamiento del disco hacia el transportador de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Figura 6** deslizante portador de unidades de hello en el chasis de Hola
3. Con Hola Hola insertado, cierre unidad portadora asa mientras continúa portador de unidades de hello toopush en el chasis de hello, hasta que su Hola asa se cierre en una posición bloqueada.
4. Usar clave de bloqueo de Hola que ha proporcionado asa del portador de Microsoft (destornillador de Torx a prueba) toosecure hello en su lugar activando Hola tornillo de bloqueo un cuarto de vuelta a la derecha.
5. Compruebe que el reemplazo de hello fue correcto y Hola unidad está operativa. Acceder Hola portal de Azure y navegar demasiado**configuración** > **estado del Hardware**. En **componentes compartidos** o **componentes compartidos de EBOD**, estado de la unidad de hello debe ser verde, que indica que es correcto.
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > Puede tardar varias horas tooturn de estado de disco de hello verde tras la sustitución de Hola.
  
## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).

