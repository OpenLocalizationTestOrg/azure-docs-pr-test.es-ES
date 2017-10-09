---
title: aaaClone su volumen de StorSimple | Documentos de Microsoft
description: "Describe tipos de clon diferentes de Hola y cuándo toouse y explica cómo puede utilizar un tooclone un volumen individual de conjunto de copia de seguridad."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a>Usar servicio tooclone un volumen de hello StorSimple Manager
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Información general
el servicio StorSimple Manager Hello **catálogo de copia de seguridad** página muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o automatizadas. Puede usar a este toolist página todas las copias de seguridad de Hola para una directiva de copia de seguridad o un volumen, seleccione o eliminar las copias de seguridad, o utilizar una copia de seguridad toorestore o clonar un volumen.

![Página del catálogo de copias de seguridad](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

Este tutorial describe cómo puede utilizar un tooclone un volumen individual de conjunto de copia de seguridad. También explica diferenciar en hello *transitorio* y *permanente* clones. 

## <a name="create-a-clone-of-a-volume"></a>Crear un clon de un volumen
Puede crear un clon en hello mismo dispositivo, otro dispositivo o incluso una máquina virtual mediante el uso de una variable local o una instantánea en la nube.

#### <a name="tooclone-a-volume"></a>tooclone un volumen
1. En la página del servicio de administrador de StorSimple de hello, haga clic en hello **catálogo de copia de seguridad** pestaña y seleccione un conjunto de copia de seguridad.
2. Expandir tooview Hola asociado volúmenes de hello conjunto de copia de seguridad. Haga clic en y seleccione un volumen de copia de seguridad Hola.
   
     ![Clonar un volumen](./media/storsimple-clone-volume/HCS_Clone.png) 
3. Haga clic en **clon** toobegin clonar volumen Hola seleccionado.
4. En el Asistente para clonar volumen de hello, en **especificar nombre y ubicación**:
   
   1. Identifique un dispositivo de destino. Se trata de ubicación de Hola donde se creará la clonación de Hola. Puede elegir Hola mismo dispositivo o especificar otro dispositivo. Si elige un volumen asociado con otros proveedores de servicios de nube hello (no Azure), lista desplegable lista de dispositivos de destino de hello, solo se mostrarán los dispositivos físicos. No se puede clonar un volumen asociado a otros proveedores de servicios en la nube en un dispositivo virtual.
      
      > [!NOTE]
      > Asegúrese de que capacidad de hello requerida para que se clona hello es inferior al capacidad Hola disponible en el dispositivo de destino de Hola.
      > 
      > 
   2. Especifique un nombre de volumen único para el clon. Hola nombre debe contener entre 3 y 127 caracteres.
   3. Haga clic en el icono de flecha de Hola ![icono de flecha](./media/storsimple-clone-volume/HCS_ArrowIcon.png) página siguiente de tooproceed toohello.
5. En **Especificar los hosts que pueden usar este volumen**:
   
   1. Especifique un registro de control de acceso (ACR) para que se clona Hola. Puede agregar un nuevo ACR o elegir de lista existente de Hola.
   2. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-clone-volume/HCS_CheckIcon.png)operación de hello toocomplete.
6. Se iniciará un trabajo de clonación y se le notificará cuando se crea correctamente clon Hola. Haga clic en **ver trabajo** toomonitor trabajo de clonación de hello en hello **trabajos** página.
7. Después de hello trabajo de clonación completada:
   
   1. Vaya toohello **dispositivos** página y seleccione hello **contenedores de volúmenes** ficha. 
   2. Seleccione el contenedor de volúmenes de Hola que está asociado con el volumen de origen de Hola que se clonó. En la lista de Hola de volúmenes, debería ver clon Hola que acaba de crear.

> [!NOTE]
> La copia de seguridad predeterminada y la supervisión se deshabilitan automáticamente en un volumen clonado.
> 
> 

Los clones que se creen de esta forma son clones transitorios. Para obtener más información acerca de los tipos de clon, consulte [Clones transitorios frente a clones permanentes](#transient-vs-permanent-clones).

Este clonación es ahora un volumen normal, y cualquier operación que sea posible en un volumen estarán disponible para que se clona Hola. Necesitará tooconfigure este volumen para las copias de seguridad.

## <a name="transient-vs-permanent-clones"></a>Clones transitorios frente a clones permanentes
Clones transitorios y permanentes se crean solamente cuando está clonando en tooa otro dispositivo. Puede clonar un volumen específico de un conjunto de copia de seguridad tooa otro dispositivo. Los clones que se creen de esta forma son clones *transitorios* . clonación transitoria Hola tendrá referencias toohello original volumen y usará ese tooread volumen mientras se escribe de forma local. 

Después de tomar una instantánea de un clon transitorio en la nube, clon resultante de hello será un *permanente* clon. clonación permanente Hello es independiente y no tiene ningún volumen original de toohello de referencias que se clonó desde.  

## <a name="scenarios-for-transient-and-permanent-clones"></a>Escenarios para clones transitorios y permanentes
Hola siguientes secciones describe situaciones de ejemplo en el que se pueden usar clones transitorios y permanentes.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperación de nivel de elemento con un clon transitorio
Debe toorecover un archivo de presentación de Microsoft PowerPoint de un año de antigüedad. El Administrador de TI identifica Hola copia de seguridad específica de ese intervalo de tiempo y, a continuación, filtros Hola volumen. Administrador de Hello clona el volumen de hello, busca el archivo hello que desea obtener y proporciona tooyou. En este escenario, se usa un clon transitorio. 

![Vídeo disponible](./media/storsimple-clone-volume/Video_icon.png)**Vídeo disponible**

Haga clic en un vídeo que muestra cómo puede usar clon hello y restaurar las características de StorSimple toorecover eliminar archivos, toowatch [aquí](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Realización de pruebas en el entorno de producción de hello con una clonación permanente
Deberá tooverify un error de prueba en el entorno de producción de hello. Crear un clon del volumen de hello en el entorno de producción de hello tomando una instantánea de nube de este clon. Hello volumen clonado es ahora independiente. En este escenario, se usa un clon permanente.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[restaurar un volumen de StorSimple a partir de un conjunto de copia de seguridad](storsimple-restore-from-backup-set.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

