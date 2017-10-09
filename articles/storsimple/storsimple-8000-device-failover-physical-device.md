---
title: "aaaStorSimple conmutación por error, dispositivo físico de disaster recovery tooa StorSimple 8000 series | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail sobre el dispositivo físico tooanother del dispositivo físico de StorSimple 8000 series."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Conmutar por error dispositivo físico de tooa StorSimple 8000 series

## <a name="overview"></a>Información general

Este tutorial describe Hola pasos necesarios toofail sobre un dispositivo StorSimple 8000 series dispositivo físico tooanother StorSimple físico si se produce un desastre. StorSimple usa datos toomigrate características de conmutación por error de dispositivo de Hola desde un dispositivo físico de origen en el dispositivo físico de hello datacenter tooanother. Guía de Hello en este tutorial aplica a dispositivos físicos de tooStorSimple 8000 series con versiones de software Update 3 y versiones posteriores.

toolearn más información acerca de conmutación por error de dispositivo y su uso toorecover ante un desastre, vaya demasiado[conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail a través de un tooa de dispositivo físico StorSimple Appliance en la nube de StorSimple, vaya demasiado[conmutar por error tooa dispositivo de nube de StorSimple](storsimple-8000-device-failover-cloud-appliance.md). toofail sobre tooitself de un dispositivo físico, vaya demasiado[una conmutación por error toohello mismo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Requisitos previos

- Asegúrese de revisar las consideraciones de Hola para conmutación por error de dispositivo. Para obtener más información, consulte demasiado[consideraciones comunes para conmutación por error de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- Debe tener un dispositivo físico de StorSimple 8000 series implementado en el centro de datos de Hola. Hola dispositivo debe ejecutar Update 3 o versiones posteriores de software. Para obtener más información, consulte demasiado[implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Pasos toofail sobre tooa de dispositivo físico

Realizar Hola siguiendo los pasos toorestore el dispositivo físico de dispositivo tooa destino.

1. Compruebe que desea toofail sobre el contenedor de volumen Hola tenga asociadas instantáneas en la nube. Para obtener más información, consulte demasiado[copias de seguridad de administrador de dispositivos de StorSimple de uso servicio toocreate](storsimple-8000-manage-backup-policies-u2.md).
2. Tooyour Administrador de dispositivos de StorSimple y, a continuación, haga clic en **dispositivos**. Hola **dispositivos** hoja, vaya toohello lista de dispositivos conectados con su servicio.
    ![Seleccionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Seleccione su dispositivo de origen y haga clic en él. dispositivo de origen de Hello tiene contenedores de volúmenes de Hola que desea toofail sobre. Vaya demasiado**configuración > contenedores de volúmenes**.
4. Seleccione un contenedor de volúmenes que desearía toofail sobre tooanother dispositivo. Haga clic en lista hello toodisplay de contenedor de volúmenes de Hola de volúmenes dentro de este contenedor. Seleccione un volumen, el menú contextual y haga clic en **desconectar** volumen tootake Hola. Repita este proceso para todos los volúmenes de Hola Hola contenedor de volúmenes.
5. Paso anterior Hola repeticiones de Hola a todos los contenedores de volúmenes le gustaría toofail sobre tooanother dispositivo.
6. Volver atrás toohello **dispositivos** hoja. En la barra de comandos de hello, haga clic en **una conmutación por error**.
    Haga clic en ![Conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png).
    
7. Hola **una conmutación por error** hoja, realizar Hola pasos:
   
   1. Haga clic en **Origen**. se muestran los contenedores de volúmenes de Hello con volúmenes asociados con instantáneas en la nube. Solo los contenedores de hello mostrados son aptos para la conmutación por error. En lista de Hola de contenedores de volúmenes, seleccione los contenedores de volúmenes de hello sobre que le gustaría toofail. **Solo Hola contenedores de volúmenes con instantáneas en la nube asociado y se muestran los volúmenes sin conexión.**

       ![Seleccionar origen](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Haga clic en **Destino**. Para los contenedores de volumen de hello seleccionados en el paso anterior de hello, seleccione un dispositivo de destino desde la lista desplegable de Hola de dispositivos disponibles. Solo los dispositivos Hola que tienen contenedores de volúmenes de origen de tooaccommodate capacidad suficiente se muestran en la lista de Hola.

        ![Seleccionar destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Por último, revise todas las opciones de conmutación por error de Hola de **resumen**. Después de revisar la configuración de hello, seleccione Hola casilla de verificación que indica que los volúmenes de hello en contenedores de volumen seleccionados están sin conexión. Haga clic en **Aceptar**.

       ![Revisar la configuración de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple crea un trabajo de conmutación por error. Haga clic en hello notificación toomonitor Hola conmutación por error de trabajo a través de hello **trabajos** hoja.

    Si el contenedor de volúmenes de Hola que ha conmutado por error tiene volúmenes locales, vea los trabajos de restauración individuales para cada volumen local (no de volúmenes en capas) en el contenedor de Hola. Estos trabajos de restauración puede tardar bastante tiempo toocomplete. Es probable que el trabajo de conmutación por error Hola puede completarse anteriormente. Estos volúmenes tendrá garantías locales solo cuando finalicen los trabajos de restauración de Hola.

    ![Supervisión del trabajo de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Una vez completada la conmutación por error de hello, vaya toohello **dispositivos** hoja.
   
   1. Seleccione el dispositivo de Hola que se usó como dispositivo de destino de hello para el proceso de conmutación por error de Hola.

       ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Vaya toohello **contenedores de volúmenes** hoja. Todos los contenedores de volúmenes de hello, junto con los volúmenes de hello de dispositivo antiguo de hello, deberían aparecer.

       ![Ver contenedores de volúmenes de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Pasos siguientes

* Después de haber realizado una conmutación por error, puede que necesite demasiado[desactive o elimine el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Para obtener información acerca de cómo toouse Hola Administrador de dispositivos de StorSimple de servicio, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

