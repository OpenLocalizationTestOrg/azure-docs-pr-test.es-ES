---
title: "aaaStorSimple conmutación por error, recuperación ante desastres para dispositivos 8000 serie | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail en su tooitself de dispositivo de StorSimple, otro dispositivo físico o un dispositivo de nube."
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
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>Conmutación por error y recuperación ante desastres para dispositivos de StorSimple de la serie 8000

## <a name="overview"></a>Información general

Este artículo describe la característica de conmutación por error de dispositivo de Hola para dispositivos de la serie StorSimple 8000 hello y cómo esta característica puede ser usado toorecover StorSimple dispositivos si se produce un desastre. StorSimple usa datos de saludo de toomigrate de conmutación por error de dispositivo desde un dispositivo de origen en el dispositivo de destino de tooanother Hola centro de datos. instrucciones de Hello en este artículo aplica a dispositivos físicos de tooStorSimple 8000 series y dispositivos en la nube con las versiones de software Update 3 y versiones posteriores.

StorSimple usa hello **dispositivos** característica hoja toostart Hola dispositivo conmutación por error en caso de hello de un desastre. Esta hoja enumera todos los hello StorSimple dispositivos conectados tooyour dispositivo el servicio StorSimple Manager.

![Hoja Dispositivos](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Recuperación ante desastres y conmutación por error del dispositivo

En un escenario de recuperación ante desastres, dispositivo primario Hola deja de funcionar. StorSimple usa el dispositivo primario de hello como _origen_ y mueve Hola asociado en la nube datos tooanother _destino_ dispositivo. Este proceso es que se hace referencia tooas hello *conmutación por error*. Hola siguiente gráfico ilustra el proceso Hola de conmutación por error.

![¿Qué ocurre en la conmutación por error de dispositivo?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

dispositivo de destino de Hola para una conmutación por error puede ser un dispositivo físico o incluso un dispositivo en la nube. Hello dispositivo de destino puede ser ubicado en hello misma o a una ubicación geográfica diferente de dispositivo de origen Hola.

Durante la conmutación por error de hello, puede seleccionar contenedores de volúmenes para la migración. StorSimple, a continuación, cambia la propiedad Hola de estos contenedores de volúmenes de hello origen dispositivo toohello dispositivo de destino. Una vez que los contenedores de volúmenes de hello cambiar la propiedad, StorSimple elimina estos contenedores Hola dispositivo de origen. Una vez completada la eliminación de hello, puede producir un error de dispositivo de destino de hello atrás. _Conmutación por recuperación_ transferencias Hola dispositivo de origen original de la propiedad toohello atrás.

### <a name="cloud-snapshot-used-during-device-failover"></a>Instantánea de nube usada durante la conmutación por error de dispositivo

Después de una recuperación ante desastres, copia de seguridad de hello más reciente en la nube es dispositivo de destino de toorestore usado Hola datos toohello. Para obtener más información sobre las instantáneas de nube, consulte [usar tootake de servicio de administrador de dispositivos de StorSimple de hello una copia de seguridad manual](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

En la serie StorSimple 8000, las directivas de copia de seguridad están asociadas a las copias de seguridad. Si hay varias directivas de copia de seguridad para hello mismo volumen y, a continuación, selecciona StorSimple Hola directiva de copia de seguridad con mayor número de volúmenes de Hola. StorSimple, a continuación, utiliza copia de seguridad más reciente de Hola de hello seleccionada Directiva de copia de seguridad toorestore Hola datos en el dispositivo de destino de Hola.

Supongamos que hay dos directivas de copia de seguridad, *defaultPol* y *customPol*:

* *defaultPol*: Un volumen, *vol1*; se ejecuta diariamente a las 22:30.
* *customPol*: Cuatro volúmenes, *vol1*, *vol2*, *vol3* y *vol4*, se ejecuta diariamente a las 22:00.

En este caso, StorSimple establece la prioridad para la coherencia de bloqueos y usa *customPol*, ya que tiene más volúmenes. Hola de copia de seguridad más reciente de esta directiva es toorestore usa datos. Para obtener más información acerca de cómo toocreate y administrar las directivas de copia de seguridad, vaya demasiado[usar directivas de copia de seguridad toomanage del servicio de administrador de dispositivos de StorSimple de hello](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Consideraciones comunes para la conmutación por error de dispositivo

Antes de conmutar un dispositivo, revise Hola siguiente información:

* Antes de inicia una conmutación por error de dispositivo, todos los volúmenes de hello dentro de contenedores de volúmenes de hello deben estar sin conexión. En una conmutación por error no planeada, los volúmenes de StotSimple se desconectan automáticamente. Pero si va a realizar una conmutación por error planeada (tootest DR), debe realizar todos los volúmenes de hello sin conexión.
* Hola solo los contenedores de volúmenes que tienen asociada una instantánea en la nube se enumeran para recuperación ante desastres. Debe haber al menos un contenedor de volumen a un toorecover de datos de instantánea de nube asociada.
* Si hay instantáneas de que se distribuyen entre varios contenedores de volúmenes, StorSimple conmuta por error a estos contenedores de volúmenes como un conjunto. En una instancia poco común, si hay instantáneas locales que se distribuyen entre varios contenedores de volumen pero no lo hacen las instantáneas asociadas en la nube, StorSimple conmutar por error las instantáneas locales de Hola y datos locales de Hola se pierde después de la recuperación ante desastres.
* dispositivos de destino disponibles Hola de DR son dispositivos que tienen suficiente tooaccommodate espacio Hola contenedores de volumen seleccionados. Los dispositivos que no tienen suficiente espacio no se muestran como dispositivos de destino.
* Después de un volcado de Dr. (durante un tiempo limitado), puede afectar al rendimiento de acceso de datos de hello considerablemente, como dispositivo de Hola necesita tooaccess Hola datos de nube de Hola y almacenan de forma local.

#### <a name="device-failover-across-software-versions"></a>Conmutación por error del dispositivo a través de las versiones de software

Un servicio Administrador de dispositivos de StorSimple en una implementación puede tener varios dispositivos, tanto virtuales como en la nube, y todos ellos pueden ejecutar versiones de software diferentes.

Usar hello después de la tabla toodetermine si puede conmutar por error o un error de dispositivo de back-tooanother ejecutan una versión diferente de software y cómo se comportan los tipos de volúmenes de Hola durante la recuperación ante desastres.

#### <a name="failover-and-failback-across-software-versions"></a>Conmutación por error y conmutación por recuperación entre versiones de software

| Conmutación por error / Conmutación por recuperación | Dispositivo físico | Dispositivo de nube |
| --- | --- | --- |
| La actualización 3 tooUpdate 4 |Los volúmenes en capas conmutan por error como capas. <br></br>Los volúmenes anclados localmente conmutan por error como anclados localmente. <br></br> Después de una conmutación por error al crear una instantánea en el dispositivo de hello Update 4, [seguimiento basado en el mapa térmico](storsimple-update4-release-notes.md#whats-new-in-update-4) se inicia. |Los volúmenes anclados localmente conmutan por error como capas. |
| Actualización 4 tooUpdate 3 |Los volúmenes en capas conmutan por error como capas. <br></br>Los volúmenes anclados localmente conmutan por error como anclados localmente. <br></br> Las copias de seguridad toorestore conservar los metadatos de mapa térmico. <br></br>El seguimiento basado en mapa térmico no está disponible en Update 3 después de una conmutación por recuperación. |Los volúmenes anclados localmente conmutan por error como capas. |


## <a name="device-failover-scenarios"></a>Escenarios de conmutación por error de dispositivo

Si se produce un desastre, puede elegir toofail en el dispositivo de StorSimple:

* [dispositivo físico de tooa](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [dispositivo de nube tooa](storsimple-8000-device-failover-cloud-appliance.md).

Hello artículos anteriores proporcionan pasos detallados para cada una de Hola por encima de los casos de conmutación por error.


## <a name="failback"></a>Conmutación por recuperación

Para Update 3 y versiones posteriores, StorSimple también admite la conmutación por recuperación. Conmutación por recuperación es simplemente Hola invertir de conmutación por error, destino Hola se convierte en el origen de Hola y dispositivo de origen original de Hola durante la conmutación por error Hola ahora se convierte en el dispositivo de destino de Hola. 

Durante la conmutación por recuperación, StorSimple vuelva a sincroniza la ubicación principal de hello datos toohello back-, detiene la E/S de Hola y de actividad de la aplicación y cambia la ubicación original de toohello back.

Una vez completada una conmutación por error, StorSimple realiza Hola siguientes acciones:

* StorSimple limpia los contenedores de volúmenes de Hola que se conmuten por error Hola dispositivo de origen.
* StorSimple inicia un trabajo en segundo plano por contenedor de volumen (conmutado) en el dispositivo de origen Hola. Si intentas toofail mientras Hola trabajo está en curso, recibirá un efecto de toothat de notificación. Espere hasta que el trabajo de hello conmutación por recuperación de toostart completa Hola.
* tiempo Hello toocomplete eliminación de Hola de contenedores de volumen depende de varios factores como la cantidad de datos, la antigüedad de los datos de hello, el número de copias de seguridad y ancho de banda de red a Hola disponible para la operación de Hola.

Si piensa probar la conmutación por error o la conmutación por recuperación, se recomienda que pruebe contenedores de volúmenes con menos datos (GB). Por lo general, puede iniciar 24 horas una vez completada la conmutación por error de Hola Hola conmutación por recuperación.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

P: **¿Qué ocurre si Hola recuperación ante desastres, se produce un error o tiene parcialmente correcta?**

A. Si se produce un error en la recuperación ante desastres de hello, se recomienda que vuelva a intentarlo. segundo trabajo de conmutación por error de dispositivo Hello es compatible con del progreso de hello del primer trabajo de Hola y se inicia desde ese punto en adelante.

P: **¿Puedo eliminar un dispositivo durante la conmutación por error de dispositivo de hello en curso?**

A. No se puede eliminar un dispositivo mientras se realiza una recuperación ante desastres. Sólo se puede eliminar el dispositivo una vez completada la recuperación ante desastres de Hola. Puede supervisar el progreso del trabajo de conmutación por error del dispositivo de Hola Hola **trabajos** hoja.

P: **¿Cuando inicia recolección Hola Hola dispositivo de origen para que se eliminan los datos locales de hello en dispositivo de origen?**

A. Recolección de elementos está habilitada en el dispositivo de origen Hola solo después de dispositivo de Hola se limpia por completo. limpieza de Hello incluye limpiar objetos que han conmutado Hola dispositivo de origen como volúmenes, objetos de copia de seguridad (no los datos), los contenedores de volúmenes y las directivas.

P: **¿Qué ocurre si Hola elimina trabajo asociado con los contenedores de volúmenes de hello en dispositivo de origen Hola se produce un error?**

A.  Si Hola elimina el trabajo se produce un error, puede eliminar manualmente los contenedores de volúmenes de Hola. Hola **dispositivos** hoja, seleccione el dispositivo de origen y haga clic en **contenedores de volúmenes**. Haga clic en contenedores de volúmenes de hello SELECT que no se pudo sobre y en la parte inferior de Hola de hoja de hello, **eliminar**. Después de haber eliminado todos los Hola conmutado contenedores de volúmenes en el dispositivo de origen de hello, puede iniciar Hola conmutación por recuperación. Para obtener más información, consulte demasiado[eliminar un contenedor de volúmenes](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>Recuperación ante desastres y continuidad empresarial (BCDR)

Un escenario de recuperación (BCDR) de desastres de continuidad de negocio se produce cuando Hola todo Azure centro de datos deja de funcionar. Este escenario puede afectar a su servicio de administrador de dispositivos de StorSimple y Hola asociadas dispositivos StorSimple.

Si se registró un dispositivo StorSimple justo antes de que se produzca un desastre, este dispositivo necesite tooundergo restablecer una fábrica. Después de un desastre hello, hello StorSimple dispositivos muestran en hello portal de Azure como sin conexión. Este dispositivo debe eliminarse del portal de Hola. Restablecer valores predeterminados de toofactory del dispositivo de Hola y vuelva a registrarlo con el servicio de Hola.

## <a name="next-steps"></a>Pasos siguientes

Si está listo tooperform una conmutación por error de dispositivo, elija uno de Hola para obtener instrucciones detalladas los escenarios siguientes:

- [Conmutar por error tooanother de dispositivo físico](storsimple-8000-device-failover-physical-device.md)
- [Conmutación por error toohello mismo dispositivo](storsimple-8000-device-failover-same-device.md)
- [Conmutar por error tooStorSimple dispositivo de nube](storsimple-8000-device-failover-cloud-appliance.md)

Si han conmutado el dispositivo, elija una de las siguientes opciones de hello:

* [Desactivar o eliminar el dispositivo de StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* [Use Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

