---
title: aaaDeactivate y eliminar un dispositivo de StorSimple | Documentos de Microsoft
description: "Describe cómo el dispositivo de StorSimple tooremove de servicio, en primer lugar la desactivación y, a continuación, eliminarlo."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Desactivación o eliminación de un dispositivo StorSimple serie 8000 mediante el servicio StorSimple Manager
## <a name="overview"></a>Información general
Es recomendable tootake un dispositivo de StorSimple fuera de servicio (por ejemplo, si va a reemplazar o actualizar el dispositivo o si ya no usa StorSimple). Si éste es el caso de hello, deberá dispositivo de hello toodeactivate antes de poder eliminarlo. La desactivación de servidores de conexión de hello entre el dispositivo de Hola y el servicio StorSimple Manager correspondiente Hola. Este tutorial le explica cómo tooremove un dispositivo de StorSimple de servicio, en primer lugar la desactivación y, a continuación, eliminarlo. 

Al desactivar un dispositivo, los datos que se almacenan localmente en el dispositivo de hello ya no serán accesibles. Solo los datos de hello asociados dispositivo Hola almacenada en la nube de Hola se pueden recuperar.  

> [!WARNING]
> La desactivación es una operación permanente y no se puede deshacer. Un dispositivo desactivado no se puede registrar con el servicio StorSimple Manager Hola a menos que sea el primero Restablecer configuración predeterminada de fábrica de toohello. 
> 
> restablecimiento de fábrica de Hello procesar las eliminaciones todos los datos de Hola que se almacenan localmente en el dispositivo. Por lo tanto, es esencial que realice una instantánea en la nube de todos los datos antes de desactivar un dispositivo. Esto le permitirá toorecover Hola a todos los datos en una fase posterior.
> 
> 

Este tutorial explica cómo realizar lo siguiente:

* Desactivar un dispositivo y eliminar datos de Hola
* Desactivar un dispositivo y conservar los datos de Hola

También se explica cómo funcionan la desactivación y eliminación en un dispositivo virtual de StorSimple.

> [!NOTE]
> Antes de desactivar un dispositivo físico o virtual de StorSimple, realizar toostop seguro o eliminar los clientes y hosts que dependen de dicho dispositivo.
> 
> 

## <a name="deactivate-and-delete-data"></a>Desactivación y eliminación de datos
Si está interesado en Eliminar dispositivo Hola por completo y no desea tooretain datos de hello en dispositivo hello, a continuación, complete Hola pasos.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>datos del hello de dispositivo y eliminación de hello toodeactivate
1. Toodeactivating anterior un dispositivo, debe eliminar todos los Hola volumen contenedores (y volúmenes de hello) asociados con el dispositivo de Hola. Puede eliminar contenedores de volúmenes solo después de haber eliminado las copias de seguridad de hello asociado.
2. Desactivar el dispositivo de hello como se indica a continuación:
   
   1. En el servicio StorSimple Manager hello **dispositivos** página, el dispositivo de hello select que desea toodeactivate y, en la parte inferior de Hola de página de hello, haga clic en **desactivar**.
   2. Aparecerá un mensaje de confirmación. Haga clic en **Sí** toocontinue. Hola desactivar el proceso empezará y tardará unos toocomplete minutos.
3. Tras la desactivación, puede eliminar completamente el dispositivo de Hola. Eliminar un dispositivo, quita de la lista Hola de dispositivos conectados toohello servicio. servicio Hello, a continuación, no podrá administrar dispositivos Hola eliminado. Usar hello siguiente dispositivo de hello toodelete de pasos:
   
   1. En el servicio StorSimple Manager hello **dispositivos** , seleccione un dispositivo desactivado que desee toodelete.
   2. En la parte inferior de hello en la página de hello, haga clic en **eliminar**.
   3. Se le pedirá confirmación. Haga clic en **Sí** toocontinue.
      
      Puede tardar unos minutos para hello toobe de dispositivo eliminado.

## <a name="deactivate-and-retain-data"></a>Desactivación y conservación de los datos
Si está interesado en Eliminar dispositivo Hola pero desea que los datos de hello tooretain, a continuación, complete Hola pasos.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate un dispositivo y conservar los datos de Hola
1. Desactivar el dispositivo de Hola. Hola a todos los contenedores de volúmenes y las instantáneas de hello de dispositivo de hello permanecerá.
   
   1. En el servicio StorSimple Manager hello **dispositivos** página, el dispositivo de hello select que desea toodeactivate y, en la parte inferior de Hola de página de hello, haga clic en **desactivar**.
   2. Aparecerá un mensaje de confirmación. Haga clic en **Sí** toocontinue. Hola desactivar el proceso empezará y tardará unos toocomplete minutos.
2. Ahora puede conmutar contenedores de volúmenes de Hola y las instantáneas de hello asociado. Para conocer los procedimientos, vaya demasiado[conmutación por error y recuperación ante desastres para el dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).
3. Tras la desactivación y la conmutación por error, puede eliminar completamente el dispositivo de Hola. Eliminar un dispositivo, quita de la lista Hola de dispositivos conectados toohello servicio. servicio Hello, a continuación, no podrá administrar dispositivos Hola eliminado. Hola completa después de dispositivo de hello toodelete de pasos:
   
   1. En el servicio StorSimple Manager hello **dispositivos** , seleccione un dispositivo desactivado que desee toodelete.
   2. En la parte inferior de hello en la página de hello, haga clic en **eliminar**.
   3. Se le pedirá confirmación. Haga clic en **Sí** toocontinue.
      
      Puede tardar unos minutos para hello toobe de dispositivo eliminado.

## <a name="deactivate-and-delete-a-virtual-device"></a>Desactivación y eliminación de un dispositivo virtual
Para un dispositivo virtual StorSimple, desactivación cancela la asignación de máquina virtual de Hola. A continuación, puede eliminar máquina virtual de Hola y los recursos de hello creados en el aprovisionamiento. Después de dispositivo virtual Hola está desactivada, no se puede restaurar el estado anterior de tooits. 

Resultados de desactivación de hello siguientes acciones:

* se quita el dispositivo virtual StorSimple Hola.
* Hola OSDisk y los discos de datos creados para el dispositivo virtual StorSimple Hola se quitan.
* Hello servicio hospedado y la red Virtual que se crearon durante el aprovisionamiento se conservan. Si no usa estas entidades, debe eliminarlas manualmente.
* Instantáneas en la nube creadas por el dispositivo virtual StorSimple Hola se conservan.

## <a name="next-steps"></a>Pasos siguientes
* toorestore Hola los valores predeterminados de dispositivo desactivado toofactory, vaya demasiado[restablecer la configuración predeterminada de hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Para obtener asistencia técnica, [póngase en contacto con el soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).
* toolearn Obtenga más información sobre cómo ir demasiado toouse Hola servicio StorSimple Manager,[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md). 

