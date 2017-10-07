---
title: un volumen de StorSimple de copia de seguridad aaaRestore | Documentos de Microsoft
description: "Explica cómo toouse Hola toorestore de página de catálogo de copia de seguridad de servicio de administrador de StorSimple un volumen de StorSimple de un conjunto de copia de seguridad."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Restaurar un volumen de StorSimple de un conjunto de copia de seguridad
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Información general
Hola **catálogo de copia de seguridad** página muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o automatizadas. Puede usar a este toolist página todas las copias de seguridad de Hola para una directiva de copia de seguridad o un volumen, seleccione o eliminar las copias de seguridad, o utilizar una copia de seguridad toorestore o clonar un volumen.

 ![Página del catálogo de copias de seguridad](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

Este tutorial le explica cómo hello toouse **catálogo de copia de seguridad** página toorestore un volumen en el dispositivo desde un conjunto de copia de seguridad.

## <a name="how-toouse-hello-backup-catalog"></a>¿Cómo toouse Hola catálogo de copia de seguridad
Hola **catálogo de copia de seguridad** página proporciona una consulta que le ayuda a toonarrow la selección de conjunto de copia de seguridad. Puede filtrar Hola conjuntos de copia que se recuperan en función de hello parámetros siguientes:

* **Dispositivo** : dispositivo de hello en qué Hola se creó el conjunto de copia de seguridad.
* **Directiva de copia de seguridad** o **volumen** : Hola directiva de copia de seguridad o el volumen asociado a este conjunto de copia de seguridad.
* **De** y **a** : Hola intervalo de fecha y hora cuando se creó el conjunto de copia de seguridad de Hola.

Hello conjuntos de copia de seguridad filtrados se tabulan en función de los siguientes atributos de hello:

* **Nombre** : hello nombre de directiva de copia de seguridad de Hola o volumen asociado con el conjunto de copia de seguridad de Hola.
* **Tamaño** : Hola a tamaño real del conjunto de copia de seguridad de Hola.
* **Crear en** : Hola fecha y la hora cuando se crearon las copias de seguridad de Hola. 
* **Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube. Una instantánea local es una copia de seguridad de todos los datos de volumen almacenados localmente en el dispositivo de hello, mientras que una instantánea de nube hace referencia toohello copia de seguridad de datos del volumen que reside en la nube de Hola. Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.
* **Iniciado por** : las copias de seguridad de Hola se pueden iniciar automáticamente según la programación de tooa o manualmente por el usuario. (Puede usar copias de seguridad de tooschedule de una directiva de copia de seguridad. Como alternativa, puede usar hello **realizar copia de seguridad** opción tootake una copia de seguridad interactiva.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Cómo toorestore su volumen de StorSimple desde una copia de seguridad
Puede usar hello **catálogo de copia de seguridad** página toorestore su volumen de StorSimple desde una copia de seguridad específica. 

> [!WARNING]
> Restaurar a partir de una copia de seguridad sustituirá los volúmenes existentes de copia de seguridad de Hola Hola. Esto puede provocar la pérdida de Hola de los datos que se escriben después de que se realizó la copia de seguridad de Hola.
> 
> 

Antes de iniciar una restauración en un volumen, asegúrese de que el volumen de hello está sin conexión. Necesitará tootake Hola volumen sin conexión Hola host primero y, a continuación, Hola dispositivo. Siga los pasos de hello en [desconectar un volumen](storsimple-manage-volumes.md#take-a-volume-offline). Realizar Hola siguiendo los pasos toorestore un volumen de un conjunto de copia de seguridad.

### <a name="toorestore-from-a-backup-set"></a>toorestore de un conjunto de copia de seguridad
1. En la página del servicio de administrador de StorSimple de hello, haga clic en hello **catálogo de copia de seguridad** ficha.
   
    ![Catálogo de copias de seguridad](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Seleccione una copia de seguridad de la siguiente manera:
   
   1. Seleccionar dispositivo apropiados de Hola.
   2. En la lista desplegable de hello, elija la que desea tooselect de directiva de copia de seguridad o volumen de Hola para copia de seguridad de Hola.
   3. Especifique el intervalo de tiempo de Hola.
   4. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.
3. Expandir tooview Hola asociado volúmenes de hello conjunto de copia de seguridad. Estos volúmenes deben realizarse sin conexión en el host de Hola y el dispositivo antes de que pueda restaurarlos al completo. Siga los pasos de hello en [desconectar un volumen](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Asegúrese de que haya desconectado Hola volúmenes en el host de hello en primer lugar, antes de poner sin conexión los volúmenes de hello en dispositivo Hola. Si no se realiza sin conexión los volúmenes de hello en el host de hello, pudieron causar daños toodata.
   > 
   > 
4. Seleccione un conjunto de copia de seguridad. Haga clic en **restaurar** final Hola de página Hola.
5. Se le pedirá confirmación. 
   
    ![Página de confirmación](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Revise la información de restauración de Hola y haga clic en el icono de verificación de hello ![icono de comprobación](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Esto iniciará un trabajo de restauración que se puede ver mediante el acceso a hello **trabajos** página. 
7. Una vez completada la restauración de hello, puede comprobar que el contenido de Hola de los volúmenes se reemplaza por volúmenes de copia de seguridad de Hola.

![Vídeo disponible](./media/storsimple-restore-from-backup-set/Video_icon.png)**Vídeo disponible**

Haga clic en un vídeo que muestra cómo puede usar clon hello y restaurar las características de StorSimple toorecover eliminar archivos, toowatch [aquí](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[StorSimple administrar volúmenes](storsimple-manage-volumes.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

