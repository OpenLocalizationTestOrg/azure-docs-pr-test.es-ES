---
title: "aaaStorSimple conmutación por error, tooa de recuperación ante desastres dispositivo de StorSimple en la nube | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail sobre su tooa de dispositivo físico de StorSimple 8000 series en la nube de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>Conmutar por error tooyour dispositivo de StorSimple en la nube

## <a name="overview"></a>Información general

Este tutorial describe Hola pasos necesarios toofail sobre un dispositivo físico de serie StorSimple 8000 tooa dispositivo de StorSimple en la nube si se produce un desastre. StorSimple usa datos toomigrate características de conmutación por error de dispositivo de Hola desde un dispositivo físico de origen de dispositivo de nube Hola datacenter tooa ejecuta en Azure. Guía de Hello en este tutorial aplica a dispositivos físicos de tooStorSimple 8000 series y dispositivos en la nube con las versiones de software Update 3 y versiones posteriores.

toolearn más información acerca de conmutación por error de dispositivo y su uso toorecover ante un desastre, vaya demasiado[conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail a través de un dispositivo físico de la tooanother de dispositivo físico StorSimple, vaya demasiado[conmutar por error el dispositivo físico StorSimple tooa](storsimple-8000-device-failover-physical-device.md). toofail a través de un dispositivo tooitself, vaya demasiado[una conmutación por error toohello mismo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Requisitos previos

- Asegúrese de revisar las consideraciones de Hola para conmutación por error de dispositivo. Para obtener más información, consulte demasiado[consideraciones comunes para conmutación por error de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- Antes de ejecutar este procedimiento, debe haber creado y configurado un dispositivo StorSimple Cloud Appliance. Si actualiza la versión del software de 3 o más adelante, considere el uso de un dispositivo en la nube 8020 para ejecución Hola recuperación ante desastres. modelo 8020 Hello tiene 64 TB y utiliza el almacenamiento Premium. Para obtener más información, consulte demasiado[implementar y administrar un dispositivo de nube de StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Pasos toofail sobre tooa dispositivo de nube

Realizar Hola siguiendo los pasos toorestore Hola dispositivo tooa destino dispositivo de StorSimple en la nube.

1.  Compruebe que desea toofail sobre el contenedor de volumen Hola tenga asociadas instantáneas en la nube. Para obtener más información, consulte demasiado[copias de seguridad de administrador de dispositivos de StorSimple de uso servicio toocreate](storsimple-8000-manage-backup-policies-u2.md).
2. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**. Hola **dispositivos** hoja, vaya toohello lista de dispositivos conectados con su servicio.
    ![Seleccionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Seleccione su dispositivo de origen y haga clic en él. dispositivo de origen de Hello tiene contenedores de volúmenes de Hola que desea toofail sobre. Vaya demasiado**configuración > contenedores de volúmenes**.

    ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Seleccione un contenedor de volúmenes que desearía toofail sobre tooanother dispositivo. Haga clic en lista hello toodisplay de contenedor de volúmenes de Hola de volúmenes dentro de este contenedor. Seleccione un volumen, el menú contextual y haga clic en **desconectar** volumen tootake Hola.

    ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Repita este proceso para todos los volúmenes de Hola Hola contenedor de volúmenes.

     ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Paso anterior Hola repeticiones de Hola a todos los contenedores de volúmenes le gustaría toofail sobre tooanother dispositivo.

7. Volver atrás toohello **dispositivos** hoja. En la barra de comandos de hello, haga clic en **una conmutación por error**.

    ![Acción de hacer clic en Conmutar por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. Hola **una conmutación por error** hoja, realizar Hola pasos:
   
    1. Haga clic en **Origen**. Seleccione toofail de contenedores de volumen de hello sobre. **Solo Hola contenedores de volúmenes con instantáneas en la nube asociado y se muestran los volúmenes sin conexión.**
        ![Seleccionar origen](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Haga clic en **Destino**. Seleccione un dispositivo de destino de la nube de lista desplegable de Hola de dispositivos disponibles. **Solo los dispositivos Hola que tienen contenedores de volúmenes de origen de tooaccommodate capacidad suficiente se muestran en la lista de Hola.**

        ![Seleccionar destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Revise la configuración de conmutación por error de hello en **resumen** y seleccione la casilla de verificación de hello, que indica que los volúmenes de hello en contenedores de volumen seleccionados están sin conexión. 

        ![Revisar la configuración de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Se crea un trabajo de conmutación por error. conmutación por error de toomonitor Hola de trabajo, haga clic en la notificación de trabajo de Hola.

    ![Supervisión del trabajo de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Una vez completada la conmutación por error de hello, vuelva atrás toohello **dispositivos** hoja.

    1. Seleccione el dispositivo de Hola que se usa como destino de Hola para hello conmutación por error.

       ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Haga clic en **Contenedores de volúmenes**. Todos los contenedores de volúmenes de hello, junto con los volúmenes de hello de dispositivo antiguo de hello, deberían aparecer.

       Si el contenedor de volúmenes de Hola que ha conmutado por error ha anclado localmente volúmenes, los volúmenes se conmutan por error como volúmenes en capas. Los volúmenes anclados localmente no se admiten en un dispositivo StorSimple Cloud Appliance.

       ![Visualización de contenedores de volúmenes de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Pasos siguientes

* Después de haber realizado una conmutación por error, puede que necesite demasiado[desactive o elimine el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

* Para obtener información acerca de cómo toouse Hola Administrador de dispositivos de StorSimple de servicio, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

