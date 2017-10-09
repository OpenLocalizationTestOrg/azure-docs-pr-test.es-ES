---
title: aaaView y administrar los trabajos de la serie 8000 de StorSimple | Documentos de Microsoft
description: "Describe la hoja de trabajos de servicio de administrador de dispositivos de StorSimple de Hola y cómo toouse, trabajos de copia de tootrack recientes, actual y programada."
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Usar tooview de servicio del Administrador de dispositivos de StorSimple de Hola y administrar trabajos (actualización 3 y posterior)

## <a name="overview"></a>Información general
Hola **trabajos** hoja proporciona un solo portal central para ver y administrar los trabajos iniciados en dispositivos de servicio de administrador de dispositivos de StorSimple de tooyour conectado. Puede ver los trabajos programados, en ejecución, completados, cancelados y con error de varios dispositivos. Los resultados se presentan en un formato tabular.

![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

Puede buscar rápidamente los trabajos de Hola que le interesan filtrando en los campos, como:

* **Estado**: los trabajos pueden tener los siguientes estados: en curso, correcto, cancelado, erróneo, cancelando o se completó con errores.
* **El intervalo de tiempo** – trabajos pueden ser el intervalo de fecha y hora de hello en función de filtrado. intervalos de Hello son después de 1 hora, últimas 24 horas, más allá de 7 días, últimos 30 días, año pasado o fecha personalizado.
* **Tipo de** : tipo de trabajo de Hola puede ser la copia de seguridad programada, la copia de seguridad manual, la copia de seguridad de la restauración, clonar volumen, conmutar por error contenedores de volúmenes, crear volumen anclado localmente, modificar el volumen, instalar actualizaciones, recopilar registros de soporte técnico y crear el dispositivo en la nube.
* **Dispositivos** – trabajos se inician en un servicio determinado tooyour de dispositivo conectado.
  
Hello trabajos filtrados se tabulan en función de Hola de hello siguientes atributos:
  
* **Nombre**: copia de seguridad programada, copia de seguridad manual, restauración de copia de seguridad, clonación de volumen, conmutación por error de contenedores de volúmenes, creación de volúmenes anclados localmente, modificación de volumen, instalación de actualizaciones, recopilación de registros de soporte técnico o creación de dispositivos en la nube.
* **Estado** : en ejecución, programados, con errores, cancelándose o completados con errores.
* **Entidad** : Hola trabajos se pueden asociar con un volumen, una directiva de copia de seguridad o un dispositivo. Por ejemplo, un trabajo de clonación se asocia a un volumen, mientras que un trabajo de copia de seguridad programado está asociado a una directiva de copia de seguridad. Se crea un trabajo de dispositivo como resultado de una recuperación ante desastres (DR) o una operación de restauración.
* **Dispositivo** : hello nombre de dispositivo de hello en qué Hola se inició el trabajo.
* **Iniciado en** : tiempo de hello cuando se inició el trabajo de Hola.
* **Duración** : trabajo hello toocomplete necesario Hola.

lista de Hola de trabajos se actualiza cada 30 segundos.

Puede realizar Hola siguiente acciones relacionadas con el trabajo de esta página:

* Ver detalles del trabajo
* Cancelación de un trabajo

## <a name="view-job-details"></a>Ver detalles del trabajo
Realizar Hola pasos tooview Hola detalles de cualquier trabajo siguientes.

#### <a name="tooview-job-details"></a>Detalles del trabajo tooview
1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **trabajos**.

2. Hola **trabajos** hoja, trabajos de Hola de presentación que está interesado ejecutando una consulta con los filtros correspondientes. Puede buscar trabajos completados, en ejecución o cancelados.

    ![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Seleccione y haga clic en un trabajo.

    ![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. En la hoja de detalles del trabajo de hello, puede ver estado de hello, detalles, estadísticas de tiempo y las estadísticas de datos.
   
    ![Detalles del trabajo](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Cancelación de un trabajo
Realizar Hola siguiendo los pasos toocancel un trabajo en ejecución.

> [!NOTE]
> No se puede cancelar algunos trabajos, como modificar un tipo de volumen de volumen toochange Hola o expandir un volumen.


### <a name="toocancel-a-job"></a>toocancel un trabajo
1. En hello **trabajos** página, mostrar hello trabajos en ejecución que desea que toocancel mediante la ejecución de una consulta con los filtros correspondientes. Seleccione el trabajo de Hola.

2. Haga doble clic en el menú contextual de hello trabajo seleccionado tooinvoke hello y haga clic en **cancelar**.

    ![Detalles del trabajo](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Cuando se le pida confirmación, haga clic en **Sí**. Ahora se cancelará este trabajo.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[administrar las directivas de copia de seguridad de StorSimple](storsimple-8000-manage-backup-policies-u2.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

