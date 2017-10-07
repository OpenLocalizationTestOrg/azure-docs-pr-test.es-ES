---
title: aaaDeactivate y eliminar un dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo el dispositivo de StorSimple tooremove de servicio, en primer lugar la desactivación y, a continuación, eliminarlo."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Desactivación y eliminación de un dispositivo de StorSimple

## <a name="overview"></a>Información general

Este artículo se describe cómo toodeactivate y eliminar un dispositivo de StorSimple que está conectado tooa servicio de administrador de dispositivos de StorSimple. Guía de Hello en este artículo aplica sólo dispositivos serie 8000 tooStorSimple incluyendo aparatos de hello StorSimple en la nube. Si está utilizando una matriz Virtual de StorSimple, a continuación, vaya demasiado[desactivar y eliminar una matriz Virtual de StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Desactivación servidores conexión Hola entre dispositivos Hola y el servicio de administrador de dispositivos de StorSimple de Hola correspondiente. Es recomendable tootake un dispositivo de StorSimple fuera de servicio (por ejemplo, si va a reemplazar o actualizar el dispositivo o si ya no usa StorSimple). Si es así, necesita toodeactivate Hola dispositivo antes de poder eliminarlo.

Al desactivar un dispositivo, los datos que se almacenan localmente en el dispositivo de hello ya no son accesibles. Solo los datos de hello asociados dispositivo Hola almacenada en la nube de Hola se pueden recuperar.

> [!WARNING]
> La desactivación es una operación permanente y no se puede deshacer. No se puede registrar un dispositivo desactivado con hello servicio Administrador de dispositivos de StorSimple a menos que sea Restablecer valores predeterminados de toofactory.
>
> restablecimiento de fábrica de Hello procesar las eliminaciones todos los datos de Hola que se almacenan localmente en el dispositivo. Por consiguiente, debe realizar una instantánea en la nube de todos los datos antes de desactivar un dispositivo. Esta instantánea de nube permite toorecover Hola a todos los datos en una fase posterior.

Después de leer este tutorial, podrá:

* Desactivar un dispositivo y eliminar datos de Hola.
* Desactivar un dispositivo y conservar los datos de Hola.

> [!NOTE]
> Antes de desactivar un dispositivo virtual o aplicación de nube de StorSimple, detenga o elimine los clientes y hosts que dependen de dicho dispositivo.


## <a name="deactivate-and-delete-data"></a>Desactivación y eliminación de datos

Si está interesado en Eliminar dispositivo Hola por completo y no desea tooretain datos de hello en dispositivo hello, a continuación, complete Hola pasos.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>datos del hello de dispositivo y eliminación de hello toodeactivate

1. Antes de desactivar un dispositivo, debe eliminar todos los Hola volumen contenedores (y volúmenes de hello) asociados con el dispositivo de Hola. Puede eliminar contenedores de volúmenes solo después de haber eliminado las copias de seguridad de hello asociado.

    > [!NOTE]
    > Antes de desactivar un dispositivo físico StorSimple o el dispositivo en la nube, asegúrese de que los datos de Hola de contenedor de volúmenes de hello eliminado se eliminan realmente del dispositivo de Hola. Puede supervisar los gráficos de consumo de nube de Hola y cuando consulte uso de la nube de hello drop debido a las copias de seguridad de hello que ha eliminado, puede continuar toodeactivate dispositivo de Hola. Si desactiva el dispositivo de hello antes de este menú se produce, Hola datos inútiles en la cuenta de almacenamiento de Hola y acumula cargos.

2. Desactivar el dispositivo de hello como se indica a continuación:
   
   1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**. Hola **dispositivos** hoja, un dispositivo de hello select que desea toodeactivate, menú contextual y, a continuación, haga clic en **desactivar**.

        ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Hola **desactivar** hoja, escriba tooconfirm de nombre de dispositivo de hello y, a continuación, haga clic en **desactivar**. Hola desactivar el proceso comienza y toma toocomplete unos minutos.

        ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Tras la desactivación, puede eliminar completamente el dispositivo de Hola. Eliminar un dispositivo, quita de la lista Hola de dispositivos conectados toohello servicio. servicio Hello, a continuación, no podrá administrar dispositivos Hola eliminado. Usar hello siguiente dispositivo de hello toodelete de pasos:
   
   1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**. Hola **dispositivos** hoja, un dispositivo de hello seleccione desactivado que desee toodelete, menú contextual y, a continuación, haga clic en **eliminar**.

        ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Hola **eliminar** hoja, escriba tooconfirm de nombre de dispositivo de hello y, a continuación, haga clic en **eliminar**. eliminación de Hello toma toocomplete unos minutos.

        ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Una vez completada correctamente la eliminación de hello, se le notificará. lista de dispositivos de Hello también actualiza la eliminación de hello tooreflect.

## <a name="deactivate-and-retain-data"></a>Desactivación y conservación de los datos

Si está interesado en Eliminar dispositivo Hola pero desea que los datos de hello tooretain, a continuación, complete Hola pasos:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate un dispositivo y conservar los datos de Hola
1. Desactivar el dispositivo de Hola. Hola a todos los contenedores de volúmenes y las instantáneas de hello de dispositivo de hello permanecen.
   
   1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**. Hola **dispositivos** hoja, un dispositivo de hello select que desea toodeactivate, menú contextual y, a continuación, haga clic en **desactivar**.

         ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Hola **desactivar** hoja, escriba tooconfirm de nombre de dispositivo de hello y, a continuación, haga clic en **desactivar**. Hola desactivar el proceso comienza y toma toocomplete unos minutos.

         ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Ahora puede conmutar contenedores de volúmenes de Hola y las instantáneas de hello asociado. Para conocer los procedimientos, vaya demasiado[conmutación por error y recuperación ante desastres para el dispositivo StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. Tras la desactivación y la conmutación por error, puede eliminar completamente el dispositivo de Hola. Eliminar un dispositivo, quita de la lista Hola de dispositivos conectados toohello servicio. servicio Hello, a continuación, no podrá administrar dispositivos Hola eliminado. dispositivo de hello toodelete, Hola completa pasos:
   
   1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**. Hola **dispositivos** hoja, un dispositivo de hello seleccione desactivado que desee toodelete, menú contextual y, a continuación, haga clic en **eliminar**.

       ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Hola **eliminar** hoja, escriba tooconfirm de nombre de dispositivo de hello y, a continuación, haga clic en **eliminar**. eliminación de Hello toma toocomplete unos minutos.

       ![Desactivar dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Una vez completada correctamente la eliminación de hello, se le notificará. lista de dispositivos de Hello también actualiza la eliminación de hello tooreflect.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Desactivación y eliminación de una aplicación en la nube

Para un dispositivo StorSimple de nube, desactivación desde el portal de hello desasigna y elimina la máquina virtual de hello y los recursos de hello creados en el aprovisionamiento. Después de dispositivo de la nube de hello está desactivada, no se puede restaurar el estado anterior de tooits.

![Desactivación de StorSimple Cloud Appliance](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Resultados de desactivación de hello siguientes acciones:

* Hola aparato de nube de StorSimple se quita del servicio de Hola.
* se elimina la máquina virtual de Hola para hello de dispositivo de StorSimple en la nube.
* el disco del sistema operativo de Hola y discos de datos creados para hello de dispositivo de StorSimple en la nube se quitan.
* servicio hospedado de Hola y red Virtual que se crearon durante el aprovisionamiento se conservan. Si no usa estas entidades, debe eliminarlas manualmente.
* Se conservan las instantáneas de nube creadas por hello de dispositivo de StorSimple en la nube.

Una vez desactivado el aparato de nube de hello, puede eliminarla en lista de Hola de dispositivos. Hola seleccione desactivado el dispositivo, menú contextual y, a continuación, haga clic en **eliminar**. StorSimple le notifica una vez que el dispositivo de Hola se elimina y Hola lista de actualizaciones de dispositivos.

## <a name="next-steps"></a>Pasos siguientes

* toorestore Hola los valores predeterminados de dispositivo desactivado toofactory, vaya demasiado[restablecer la configuración predeterminada de hello dispositivo toofactory](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Para obtener asistencia técnica, [póngase en contacto con el soporte técnico de Microsoft](storsimple-8000-contact-microsoft-support.md).
* toolearn Obtenga más información sobre cómo ir demasiado toouse Hola servicio de administrador de dispositivos de StorSimple,[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

