---
title: "aaaManage el catálogo de copia de seguridad de StorSimple | Documentos de Microsoft"
description: "Explica cómo toolist de página de la catálogo de copia de seguridad de servicio de administrador de StorSimple con toouse hello, seleccionar y eliminar los conjuntos de copia de seguridad de un volumen."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Usar el catálogo de copia de seguridad de toomanage de servicio de StorSimple Manager Hola
## <a name="overview"></a>Información general
el servicio StorSimple Manager Hello **catálogo de copia de seguridad** página muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o programados. Puede usar a este toolist página todas las copias de seguridad de Hola para una directiva de copia de seguridad o un volumen, seleccione o eliminar las copias de seguridad, o utilizar una copia de seguridad toorestore o clonar un volumen.

Este tutorial le explica cómo toolist, seleccionar y eliminar una copia de seguridad establecido. toolearn cómo toorestore el dispositivo de copia de seguridad, vaya demasiado[restaurar el dispositivo desde un conjunto de copia de seguridad](storsimple-restore-from-backup-set.md). toolearn cómo tooclone un volumen, vaya demasiado[clonar un volumen de StorSimple](storsimple-clone-volume.md).

![Catálogo de copias de seguridad](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Hola **catálogo de copia de seguridad** página proporciona una consulta toonarrow la selección de conjunto de copia de seguridad. Puede filtrar los conjuntos de copia de seguridad de Hola que se recuperan en función de hello parámetros siguientes:

* **Dispositivo** : dispositivo de hello en qué Hola se creó el conjunto de copia de seguridad.
* **Directiva o el volumen de copia de seguridad** : Hola directiva de copia de seguridad o el volumen asociado a este conjunto de copia de seguridad.
* **FROM y To** : Hola intervalo de fecha y hora cuando se creó el conjunto de copia de seguridad de Hola.

Hello conjuntos de copia de seguridad filtrados se tabulan en función de los siguientes atributos de hello:

* **Nombre** : hello nombre de directiva de copia de seguridad de Hola o volumen asociado con el conjunto de copia de seguridad de Hola.
* **Tamaño** : Hola a tamaño real del conjunto de copia de seguridad de Hola.
* **Fecha de creación de** : Hola fecha y la hora cuando se crearon las copias de seguridad de Hola. 
* **Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube. Una instantánea local es una copia de seguridad de todos los datos de volumen almacenados localmente en el dispositivo de hello, mientras que una instantánea de nube hace referencia toohello copia de seguridad de datos del volumen que reside en la nube de Hola. Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.
* **Iniciado por** : las copias de seguridad de Hola se pueden iniciar automáticamente una programación o manualmente por el usuario. Puede utilizar las copias de seguridad de un tooschedule de directiva de copia de seguridad. Como alternativa, puede usar hello **realizar copia de seguridad** opción tootake una copia de seguridad manual.

## <a name="list-backup-sets-for-a-volume"></a>Mostrar conjuntos de copia de seguridad para un volumen
Hola completa siguientes pasos se toolist todas las copias de seguridad de Hola para un volumen.

#### <a name="toolist-backup-sets"></a>conjuntos de copia de seguridad de toolist
1. En la página del servicio de administrador de StorSimple de hello, haga clic en hello **catálogo de copia de seguridad** ficha.
2. Filtrar las selecciones de hello como sigue:
   
   1. Seleccionar dispositivo apropiados de Hola.
   2. En la lista desplegable de hello, elija un volumen tooview Hola correspondiente hello las copias de seguridad.
   3. Especifique el intervalo de tiempo de Hola.
   4. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      copias de seguridad de Hello asociadas con el volumen de hello seleccionado deben aparecer en lista de Hola de conjuntos de copia de seguridad.

## <a name="select-a-backup-set"></a>Seleccionar un conjunto de copia de seguridad
Hola completa siguiendo los pasos tooselect una copia de seguridad establecido para una directiva de copia de seguridad o volumen.

#### <a name="tooselect-a-backup-set"></a>tooselect un conjunto de copia de seguridad
1. En la página del servicio de administrador de StorSimple de hello, haga clic en hello **catálogo de copia de seguridad** ficha.
2. Filtrar las selecciones de hello como sigue:
   
   1. Seleccionar dispositivo apropiados de Hola.
   2. En la lista desplegable de hello, elija la que desea tooselect de directiva de copia de seguridad o volumen de Hola para copia de seguridad de Hola.
   3. Especifique el intervalo de tiempo de Hola.
   4. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.
3. Selecciona y expanda un conjunto de copia de seguridad. Hola **restaurar** y **eliminar** opciones se muestran en la parte inferior de Hola de página de Hola. Puede realizar cualquiera de estas acciones en el conjunto de copia de seguridad de Hola que haya seleccionado.

## <a name="delete-a-backup-set"></a>Eliminación de un conjunto de copia de seguridad
Eliminar una copia de seguridad cuando ya no desea datos de hello tooretain asociados con él. Realizar Hola siguiendo los pasos toodelete un conjunto de copia de seguridad.

#### <a name="toodelete-a-backup-set"></a>toodelete un conjunto de copia de seguridad
1. En la página del servicio de administrador de StorSimple de hello, haga clic en hello **ficha catálogo de copia de seguridad**.
2. Filtrar las selecciones de hello como sigue:
   
   1. Seleccionar dispositivo apropiados de Hola.
   2. En la lista desplegable de hello, elija la que desea tooselect de directiva de copia de seguridad o volumen de Hola para copia de seguridad de Hola.
   3. Especifique el intervalo de tiempo de Hola.
   4. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.
3. Selecciona y expanda un conjunto de copia de seguridad. Hola **restaurar** y **eliminar** opciones se muestran en la parte inferior de Hola de página de Hola. Hacer clic en **Eliminar**.
4. Se le notificará cuando Hola eliminación está en curso y cuando haya finalizado correctamente. Después de realiza la eliminación de hello, actualizar la consulta de hello en esta página. conjunto de copia de seguridad de Hello eliminado ya no aparecerá en la lista de Hola de conjuntos de copia de seguridad de.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[uso Hola toorestore de catálogo de copia de seguridad, el dispositivo desde un conjunto de copia de seguridad](storsimple-restore-from-backup-set.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

