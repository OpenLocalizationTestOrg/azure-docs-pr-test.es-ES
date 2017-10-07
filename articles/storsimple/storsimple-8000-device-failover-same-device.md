---
title: "aaaStorSimple conmutación por error, recuperación ante desastres para dispositivos 8000 serie | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail sobre su toohello de dispositivo de StorSimple mismo dispositivo."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>Conmutar por error el dispositivo de toosame del dispositivo físico de StorSimple

## <a name="overview"></a>Información general

Este tutorial describe Hola pasos necesarios toofail sobre un tooitself de dispositivo físico de StorSimple 8000 series si se produce un desastre. StorSimple usa datos toomigrate características de conmutación por error de dispositivo de Hola desde un dispositivo físico de origen en el dispositivo físico de hello datacenter tooanother. Guía de Hello en este tutorial aplica a dispositivos físicos de tooStorSimple 8000 series con versiones de software Update 3 y versiones posteriores.

toolearn más información acerca de conmutación por error de dispositivo y su uso toorecover ante un desastre, vaya demasiado[conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail a través de un dispositivo físico tooanother de dispositivo físico, vaya demasiado[una conmutación por error toohello mismo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md). toofail a través de un tooa de dispositivo físico StorSimple Appliance en la nube de StorSimple, vaya demasiado[conmutar por error tooa dispositivo de nube de StorSimple](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Requisitos previos

- Asegúrese de revisar las consideraciones de Hola para conmutación por error de dispositivo. Para obtener más información, consulte demasiado[consideraciones comunes para conmutación por error de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Pasos toofail sobre toohello mismo dispositivo

Realizar Hola siguientes pasos si necesita toofail sobre toohello mismo dispositivo.

1. Tomar instantáneas de nube de todos los volúmenes de hello en el dispositivo. Para obtener más información, consulte demasiado[copias de seguridad de administrador de dispositivos de StorSimple de uso servicio toocreate](storsimple-8000-manage-backup-policies-u2.md).
2. Restablecer los valores predeterminados toofactory del dispositivo. Siga Hola detallada instrucciones [la configuración predeterminada de tooreset un toofactory de dispositivo de StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Servicio de administrador de dispositivos de StorSimple toohello go y, a continuación, seleccione **dispositivos**. Hola **dispositivos** hoja, dispositivo antiguo de hello debería aparecer como **sin conexión**.

    ![Dispositivo de origen sin conexión](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Configure el dispositivo y vuelva a registrarlo con el servicio StorSimple Device Manager. Hello dispositivo recién registrado debería ser **listo tooset seguridad**. nombre de dispositivo de Hello para el nuevo dispositivo de hello es hello igual que el dispositivo antiguo de hello pero le anexa un numeral tooindicate ese dispositivo Hola era restablecimiento toofactory predeterminada y vuelva a registrar.

    ![Los dispositivos recién registrados listo tooset seguridad](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Para el nuevo dispositivo hello, complete la instalación de dispositivo de Hola. Para obtener más información, consulte demasiado[paso 4: completar el programa de instalación mínima del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). En hello **dispositivos** hoja, cambia de estado de hello de dispositivo de hello demasiado**Online**.

   > [!IMPORTANT]
   > **Completar la configuración mínima de hello en primer lugar, o puede producir un error en la recuperación ante desastres.**

    ![Dispositivo recién registrado en línea](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Seleccione el dispositivo antiguo de hello (estado sin conexión) y en la barra de comandos de hello, haga clic en **una conmutación por error**. Hola **una conmutación por error** hoja, seleccione el dispositivo anterior como origen de Hola y especifique dispositivo de destino de hello según Hola recién registrado el dispositivo.

    ![Resumen de la conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Para obtener instrucciones detalladas, consulte demasiado[conmutar por error dispositivo físico de tooanother](#fail-over-to-another-physical-device).

7. Se crea un trabajo de restauración de dispositivo que puede supervisar desde hello **trabajos** hoja.

8. Una vez se haya completado correctamente el trabajo de hello, acceder nuevo dispositivo de Hola y navegar toohello **contenedores de volúmenes** hoja. Compruebe que todos los contenedores de volúmenes de hello de dispositivo antiguo de hello migraron toohello nuevo dispositivo.

   ![Contenedores de volúmenes migrados](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Una vez completada la conmutación por error de hello, puede desactivar y eliminar dispositivo antiguo de Hola desde el portal de Hola. Seleccione Hola antiguo dispositivo (sin conexión), menú contextual y, a continuación, seleccione **desactivar**. Después de desactiva el dispositivo hello, estado de hello de dispositivo de Hola se actualiza.

     ![Dispositivo de origen desactivado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Hola seleccione desactivado el dispositivo, menú contextual y, a continuación, seleccione **eliminar**. Esto elimina el dispositivo de hello en lista de Hola de dispositivos.

    ![Dispositivo de origen eliminado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Pasos siguientes

* Después de haber realizado una conmutación por error, puede que necesite demasiado[desactive o elimine el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Para obtener información acerca de cómo toouse Hola Administrador de dispositivos de StorSimple de servicio, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

