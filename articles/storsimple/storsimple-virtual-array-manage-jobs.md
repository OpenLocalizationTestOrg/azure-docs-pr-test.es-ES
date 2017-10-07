---
title: aaaView y administrar los trabajos de StorSimple Virtual Array | Documentos de Microsoft
description: "Describe la página de trabajos de servicio de administrador de dispositivos de StorSimple de Hola y cómo toouse se tootrack trabajos actuales y recientes de hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Utilice trabajos de tooview de servicio de administrador de dispositivos de StorSimple de Hola para hello StorSimple Virtual Array
## <a name="overview"></a>Información general
Hola **trabajos** hoja proporciona un solo portal central para ver y administrar trabajos que se inician en arreglos de discos virtuales que están conectado tooyour servicio de administrador de dispositivos de StorSimple. Puede ver los trabajos en ejecución, finalizados y con error de varios dispositivos virtuales. Los resultados se presentan en un formato tabular.

![Hoja de trabajos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

Puede buscar rápidamente los trabajos de Hola que le interesan filtrando en los campos, como:

* **El intervalo de tiempo** – trabajos pueden ser el intervalo de fecha y hora de hello en función de filtrado.
* **Dispositivos** – trabajos se inician en un servicio de tooyour dispositivo conectado. Hello trabajos filtrados se tabulan en función de hello siguientes atributos:
  
  * **Nombre** : puede ser el nombre del trabajo de hello **todos los**, **copia de seguridad**, **clon**, **una conmutación por error**, **descargar actualizaciones** , o **instalar actualizaciones**.
  * **Estado**: los trabajos pueden **Todos**, **En curso**, **Correcto**, **Error** o **Cancelado**.
  * **Entidad** : Hola trabajos se pueden asociar con un volumen, un recurso compartido o un dispositivo.
  * **Dispositivo** : hello nombre de dispositivo de hello en qué Hola se inició el trabajo.
  * **Iniciado en** : tiempo de hello cuando se inició el trabajo de Hola.
  * **Duración** : hello duración de en qué trabajo Hola se ejecutó.
* **Estado** : puede buscar todos los trabajos o los trabajos en ejecución, completados o con error.
* **Tipo de trabajo** : tipo de trabajo de hello puede ser la copia de seguridad, restauración all, conmutación por error, descargar las actualizaciones o instalar actualizaciones.

lista de Hola de trabajos se actualiza cada 30 segundos.

## <a name="view-job-details"></a>Ver detalles del trabajo
Realizar Hola pasos tooview Hola detalles de cualquier trabajo siguientes.

#### <a name="tooview-job-details"></a>Detalles del trabajo tooview
1. En hello **trabajos** hoja, trabajos de Hola de presentación que está interesado ejecutando una consulta con los filtros correspondientes. Puede buscar los trabajos completados o en ejecución.
2. Seleccione un trabajo de la lista tabular de Hola de trabajos.
   
    ![Hoja de trabajos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. En la parte inferior de Hola de página de hello, haga clic en **detalles**.
4. Hola **detalles** cuadro de diálogo, puede ver el estado, los detalles y las estadísticas de tiempo. Hello en la ilustración siguiente se muestra un ejemplo de Hola **detalles del trabajo de copia de seguridad** cuadro de diálogo.
   
    ![Detalles del trabajo](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Errores en el trabajo cuando se pausa la máquina virtual de hello en el hipervisor de Hola
Cuando un trabajo está en curso en la matriz Virtual de StorSimple y el dispositivo de hello (aprovisionado en el hipervisor de máquina virtual) se detiene durante más de 15 minutos, se produce un error en el trabajo de Hola. Esto es debido a tiempo de StorSimple Virtual Array tooyour dejen de estar sincronizado con la hora de Microsoft Azure Hola. 

Verá Hola siguiente error: "la hora del dispositivo no está sincronizada con el tiempo de Microsoft Azure hello en más de 15 minutos. Asegúrese de que Hola hipervisor y las horas de dispositivo de Hola se sincronizan con un servidor NTP. Compruebe que no haya ningún problema de conectividad. problemas de conectividad de tootroubleshoot, ejecutar pruebas de diagnóstico de interfaz de usuario del dispositivo virtual de web local de hello."

Estos errores aplican trabajos toobackup, restauración, actualización y conmutación por error. Si la máquina virtual se aprovisiona en Hyper-V, máquina Hola sincroniza finalmente tiempo con el hipervisor. Cuando esto ocurra, puede reiniciar el trabajo.

## <a name="next-steps"></a>Pasos siguientes
[Obtenga información acerca de cómo toouse Hola tooadminister de interfaz de usuario web local a la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).

