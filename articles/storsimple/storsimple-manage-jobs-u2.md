---
title: aaaView y administrar los trabajos de StorSimple | Documentos de Microsoft
description: "Describe la página de trabajos del servicio de administrador de StorSimple de Hola y cómo toouse, trabajos de copia de tootrack recientes, actual y programada."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a>Usar tooview de servicio de StorSimple Manager hello y administrar los trabajos de StorSimple (actualización 2)
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Información general
Hola **trabajos** página proporciona un solo portal central para ver y administrar los trabajos iniciados en los dispositivos conectados tooyour el servicio StorSimple Manager. Puede ver los trabajos programados, en ejecución, completados, cancelados y con error de varios dispositivos. Los resultados se presentan en un formato tabular. 

![Página de trabajos](./media/storsimple-manage-jobs-u2/jobs.png)

Puede buscar rápidamente los trabajos de Hola que le interesan filtrando en los campos, como:

* **Estado** : los trabajos pueden estar en ejecución, programados, con errores, cancelándose o completados con errores.
* **FROM y To** – trabajos pueden ser el intervalo de fecha y hora de hello en función de filtrado.
* **Tipo de** : tipo de trabajo de hello puede ser la copia de seguridad, copia de seguridad manual, restauración, clonación, conmutación por error de dispositivo, crear volumen anclado localmente, modificar el volumen, actualizar, admite el paquete o el aprovisionamiento del dispositivo virtual.
* **Dispositivos** – trabajos se inician en un servicio determinado tooyour de dispositivo conectado.
  Hello trabajos filtrados se tabulan en función de Hola de hello siguientes atributos:
  
  * **Tipo** : copia de seguridad, copia de seguridad manual, restaurar, clonar, conmutación por error de dispositivo, crear volumen anclado localmente, modificar volumen, actualizar, paquete de soporte o aprovisionamiento de dispositivos virtuales.
  * **Estado** : en ejecución, programados, con errores, cancelándose o completados con errores.
  * **Entidad** : Hola trabajos se pueden asociar con un volumen, una directiva de copia de seguridad o un dispositivo. Por ejemplo, un trabajo de clonación se asocia a un volumen, mientras que un trabajo de copia de seguridad programado está asociado a una directiva de copia de seguridad. Se crea un trabajo de dispositivo como resultado de una recuperación ante desastres (DR) o una operación de restauración.
  * **Dispositivo** : hello nombre de dispositivo de hello en qué Hola se inició el trabajo.
  * **Iniciado en** : tiempo de hello cuando se inició el trabajo de Hola.
  * **Curso** : Hola porcentaje de finalización de un trabajo en ejecución. Para un trabajo completado, este debe equivaler siempre al 100%.

lista de Hola de trabajos se actualiza cada 30 segundos.

Puede realizar Hola siguiente acciones relacionadas con el trabajo de esta página:

* Ver detalles del trabajo
* Cancelación de un trabajo

## <a name="view-job-details"></a>Ver detalles del trabajo
Realizar Hola pasos tooview Hola detalles de cualquier trabajo siguientes.

#### <a name="tooview-job-details"></a>Detalles del trabajo tooview
1. En hello **trabajos** página, muestre los trabajos de Hola que está interesado ejecutando una consulta con los filtros correspondientes. Puede buscar trabajos completados, en ejecución o cancelados.
2. Seleccione un trabajo.
3. En la parte inferior de Hola de página de hello, haga clic en **detalles**.
4. Hola **detalles del trabajo de copia de seguridad** cuadro de diálogo, puede ver el estado de hello, detalles, estadísticas de tiempo y las estadísticas de datos.
   
    ![Página Detalles del trabajo](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a>Cancelación de un trabajo
Realizar Hola siguiendo los pasos toocancel un trabajo en ejecución.

> [!NOTE]
> No se puede cancelar algunos trabajos, como modificar un tipo de volumen de volumen toochange Hola o expandir un volumen.
> 
> 

### <a name="toocancel-a-job"></a>toocancel un trabajo
1. En hello **trabajos** página, mostrar hello trabajos en ejecución que desea que toocancel mediante la ejecución de una consulta con los filtros correspondientes.
2. Seleccione el trabajo de Hola.
3. En la parte inferior de Hola de página de hello, haga clic en **cancelar**.
4. Cuando se le pida confirmación, haga clic en **Sí**.

Ahora se cancelará este trabajo.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[administrar las directivas de copia de seguridad de StorSimple](storsimple-manage-backup-policies.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

