---
title: "aaaManage el catálogo de copia de seguridad de StorSimple | Documentos de Microsoft"
description: "Explica cómo toouse hello toolist de página de catálogo de copia de seguridad de servicio de administrador de dispositivos de StorSimple, seleccionar y eliminar conjuntos de copia de seguridad."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Usar toomanage de servicio del Administrador de dispositivos de StorSimple de hello en el catálogo de copia de seguridad
## <a name="overview"></a>Información general
Hola servicio Administrador de dispositivos de StorSimple **catálogo de copia de seguridad** hoja muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o programados. Puede usar a este toolist página todas las copias de seguridad de Hola para una directiva de copia de seguridad o un volumen, seleccione o eliminar las copias de seguridad, o utilizar una copia de seguridad toorestore o clonar un volumen.

Este tutorial le explica cómo toolist, seleccionar y eliminar una copia de seguridad establecido. toolearn cómo toorestore el dispositivo de copia de seguridad, vaya demasiado[restaurar el dispositivo desde un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md). toolearn cómo tooclone un volumen, vaya demasiado[clonar un volumen de StorSimple](storsimple-8000-clone-volume-u2.md).

![Catálogo de copias de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Hola **catálogo de copia de seguridad** hoja proporciona una consulta toonarrow la selección de conjunto de copia de seguridad. Puede filtrar los conjuntos de copia de seguridad de Hola que se recuperan en función de hello parámetros siguientes:

* **Dispositivo** : dispositivo de hello en qué Hola se creó el conjunto de copia de seguridad.
* **Directiva de copia de seguridad o el volumen** : Hola directiva de copia de seguridad o el volumen asociado a este conjunto de copia de seguridad.
* **FROM y To** : Hola intervalo de fecha y hora cuando se creó el conjunto de copia de seguridad de Hola.

Hello conjuntos de copia de seguridad filtrados se tabulan en función de los siguientes atributos de hello:

* **Nombre** : hello nombre de directiva de copia de seguridad de Hola o volumen asociado con el conjunto de copia de seguridad de Hola.
* **Tamaño** : Hola a tamaño real del conjunto de copia de seguridad de Hola.
* **Fecha de creación de** : Hola fecha y la hora cuando se crearon las copias de seguridad de Hola. 
* **Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube. Una instantánea local es una copia de seguridad de todos los datos de volumen almacenados localmente en el dispositivo de hello, mientras que una instantánea de nube hace referencia toohello copia de seguridad de datos del volumen que reside en la nube de Hola. Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.
* **Iniciado por** : las copias de seguridad de Hola se pueden iniciar automáticamente una programación o manualmente por el usuario. Puede utilizar las copias de seguridad de un tooschedule de directiva de copia de seguridad. Como alternativa, puede usar hello **realizar copia de seguridad** opción tootake una copia de seguridad manual.

## <a name="list-backup-sets-for-a-backup-policy"></a>Mostrar conjuntos de copia de seguridad para una directiva de copia de seguridad
Hola completa siguientes pasos se toolist todas las copias de seguridad de Hola para una directiva de copia de seguridad.

#### <a name="toolist-backup-sets"></a>conjuntos de copia de seguridad de toolist
1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **catálogo de copia de seguridad**.

2. Filtrar las selecciones de hello como sigue:
   
   1. Especifique el intervalo de tiempo de Hola.
   2. Seleccionar dispositivo apropiados de Hola.
   3. Filtrar por **directiva de copia de seguridad** tooview Hola copias de seguridad de hello correspondiente.
   3. En lista de desplegable de directiva de copia de seguridad de hello, elija **todos los** tooview todos Hola copias de seguridad en hello seleccionado dispositivo.
   4. Haga clic en **aplicar** tooexecute esta consulta.
      
      copias de seguridad de Hello asociadas con la directiva de copia de seguridad de hello seleccionado deben aparecer en lista de Hola de conjuntos de copia de seguridad.

      ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Seleccionar un conjunto de copia de seguridad
Hola completa siguiendo los pasos tooselect una copia de seguridad establecido para una directiva de copia de seguridad o volumen.

#### <a name="tooselect-a-backup-set"></a>tooselect un conjunto de copia de seguridad
1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **catálogo de copia de seguridad**.
2. Filtrar las selecciones de hello como sigue:
   
   1. Especifique el intervalo de tiempo de Hola. 
   2. Seleccionar dispositivo apropiados de Hola. 
   3. Filtrar por la directiva de copia de seguridad o volumen de copia de seguridad de Hola que desea tooselect.
   4. Haga clic en **aplicar** tooexecute esta consulta.
      
      Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.

      ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selecciona y expanda un conjunto de copia de seguridad. Ahora puede ver conjuntos de copia de seguridad de hello desglosados por volúmenes de Hola que contiene. Hola **restaurar** y **eliminar** opciones están disponibles a través del menú contextual de hello (ratón) para el conjunto de copia de seguridad de Hola. Puede realizar cualquiera de estas acciones en el conjunto de copia de seguridad de Hola que haya seleccionado.

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Eliminación de un conjunto de copia de seguridad
Eliminar una copia de seguridad cuando ya no desea datos de hello tooretain asociados con él. Realizar Hola siguiendo los pasos toodelete un conjunto de copia de seguridad.

#### <a name="toodelete-a-backup-set"></a>toodelete un conjunto de copia de seguridad
 Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **catálogo de copia de seguridad**.
2. Filtrar las selecciones de hello como sigue:
   
   1. Especifique el intervalo de tiempo de Hola. 
   2. Seleccionar dispositivo apropiados de Hola. 
   3. Filtrar por la directiva de copia de seguridad o volumen de copia de seguridad de Hola que desea tooselect.
   4. Haga clic en **aplicar** tooexecute esta consulta.
      
      Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.

      ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selecciona y expanda un conjunto de copia de seguridad. Ahora puede ver conjuntos de copia de seguridad de hello desglosados por volúmenes de Hola que contiene. Hola **restaurar** y **eliminar** opciones están disponibles a través del menú contextual de hello (ratón) para el conjunto de copia de seguridad de Hola. Haga clic en el conjunto de copia de seguridad de hello seleccionado y en el menú contextual de hello, seleccione **eliminar**.

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Cuando se le pida confirmación, revise la información de la muestra de Hola y haga clic en **eliminar**. copia de seguridad de Hello seleccionada se eliminará definitivamente.

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Se le notificará cuando Hola eliminación está en curso y cuando haya finalizado correctamente. Después de realiza la eliminación de hello, actualizar la consulta de hello en esta página. conjunto de copia de seguridad de Hello eliminado ya no aparecerá en la lista de Hola de conjuntos de copia de seguridad de.

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[uso Hola toorestore de catálogo de copia de seguridad, el dispositivo desde un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

