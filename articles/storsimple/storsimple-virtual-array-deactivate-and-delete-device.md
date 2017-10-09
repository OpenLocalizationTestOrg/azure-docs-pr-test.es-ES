---
title: aaaDeactivate y eliminar una matriz Virtual de Microsoft Azure StorSimple | Documentos de Microsoft
description: "Describe cómo el dispositivo de StorSimple tooremove de servicio, en primer lugar la desactivación y, a continuación, eliminarlo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Desactivación y eliminación de una matriz virtual de StorSimple

## <a name="overview"></a>Información general

Al desactivar una matriz Virtual de StorSimple, se rompe conexión Hola entre dispositivos de Hola y el servicio de administrador de dispositivos de StorSimple correspondiente de Hola. Este tutorial explica cómo realizar lo siguiente:

* Desactivación de un dispositivo 
* Eliminación de un dispositivo desactivado

información de Hello en este artículo aplica tooStorSimple arreglos de discos virtuales. Para obtener información sobre la 8000 serie, vaya toohow demasiado[desactivar o eliminar un dispositivo](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>¿Cuando toodeactivate?

La desactivación es una operación permanente y no se puede deshacer. No se puede registrar un dispositivo desactivado con hello servicio Administrador de dispositivos de StorSimple de nuevo. Puede necesita toodeactivate y eliminar una matriz Virtual de StorSimple en hello los escenarios siguientes:

* **Conmutación por error planeada** : el dispositivo está en línea y tiene previsto toofail sobre el dispositivo. Si tiene previsto tooupgrade tooa mayor dispositivo, deberá toofail sobre el dispositivo. Después de que se transfiere la propiedad de los datos Hola y Hola conmutación por error, se elimina automáticamente el dispositivo de origen Hola.
* **Conmutación por error imprevista** : el dispositivo está sin conexión y necesite toofail en relación con el dispositivo de Hola. Esta situación puede producirse durante un desastre cuando hay una interrupción en el centro de datos de Hola y el dispositivo principal está inactivo. Planear toofail durante hello tooa secundaria un dispositivo. Después de que se transfiere la propiedad de los datos Hola y Hola conmutación por error, se elimina automáticamente el dispositivo de origen Hola.
* **Retirar** : desee toodecommission Hola dispositivo. Para ello, deberá toofirst desactivar Hola dispositivo y, a continuación, elimínelo. Al desactivar un dispositivo, no podrá acceder a los datos almacenados localmente. Puede que solo acceso y recuperar Hola los datos almacenados en la nube de Hola. Si tiene previsto tookeep los datos del dispositivo Hola tras la desactivación, debe tomar una instantánea de nube de todos los datos antes de desactivar un dispositivo. Esta instantánea de nube permite toorecover Hola a todos los datos en una fase posterior.

## <a name="deactivate-a-device"></a>Desactivación de un dispositivo

toodeactivate el dispositivo, realizar Hola pasos.

#### <a name="toodeactivate-hello-device"></a>dispositivo de hello toodeactivate

1. En el servicio, vaya demasiado**Administración > dispositivos**. Hola **dispositivos** hoja, haga clic en y dispositivo Hola select que desea toodeactivate.
   
    ![Seleccione el dispositivo toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. En su **panel del dispositivo** hoja, haga clic en **... Más** y en la lista de hello, seleccione **desactivar**.
   
    ![Clic en Desactivar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. Hola **desactivar** hoja, nombre de dispositivo de tipo hello y, a continuación, haga clic en **desactivar**. 
   
    ![Confirmación de la desactivación](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Hola desactivar el proceso comienza y toma toocomplete unos minutos.
   
    ![Desactivación en curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Tras la desactivación, Hola lista de las actualizaciones de dispositivos.
   
    ![Desactivación completa](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Ahora puede eliminar este dispositivo.

## <a name="delete-hello-device"></a>Eliminar dispositivo Hola

Un dispositivo tiene toobe primera desactivado toodelete lo. Eliminar un dispositivo, quita de la lista Hola de dispositivos conectados toohello servicio. servicio Hello, a continuación, no podrá administrar dispositivos Hola eliminado. datos de Hello asociados Hola dispositivo sin embargo permanecen en nube Hola. A partir de ahí, estos datos acumulan cargos.

dispositivo de hello toodelete, realizar Hola pasos.

#### <a name="toodelete-hello-device"></a>dispositivo de hello toodelete

1. En el Administrador de dispositivos de StorSimple, vaya demasiado**Administración > dispositivos**. Hola **dispositivos** hoja, seleccione un dispositivo desactivado que desee toodelete.
2. Hola **panel del dispositivo** hoja, haga clic en **... Más** y, a continuación, haga clic en **eliminar**.
   
   ![Seleccione el dispositivo toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. Hola **eliminar** hoja, escriba un nombre hello de la eliminación de dispositivos tooconfirm hello y, a continuación, haga clic en **eliminar**. Eliminar dispositivo hello no elimina datos en la nube Hola asociados con el dispositivo de Hola. 
   
   ![Confirmar eliminación](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. eliminación de Hola se inicia y tarda unos toocomplete minutos.
   
   ![Eliminación en curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Después de elimina el dispositivo de hello, puede ver lista de hello actualizado de dispositivos.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información acerca de cómo toofail sobre, vaya demasiado[conmutación por error y recuperación ante desastres de la matriz Virtual de StorSimple](storsimple-virtual-array-failover-dr.md).

* toolearn Obtenga más información sobre cómo ir demasiado toouse Hola servicio de administrador de dispositivos de StorSimple,[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple la matriz Virtual de StorSimple](storsimple-virtual-array-manager-service-administration.md). 

