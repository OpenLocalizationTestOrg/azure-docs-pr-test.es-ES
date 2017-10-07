---
title: "recuperación de desastres y conmutación por error aaaStorSimple | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail en su tooitself de dispositivo de StorSimple, otro dispositivo físico o un dispositivo virtual."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>Conmutación por error y recuperación ante desastres para el dispositivo StorSimple
## <a name="overview"></a>Información general
Este tutorial describe Hola pasos necesarios toofail a través de un dispositivo de StorSimple en caso de hello de un desastre. Una conmutación por error, podrá toomigrate los datos desde un dispositivo de origen en hello tooanother de centro de datos físico o incluso a un dispositivo virtual encuentran en hello misma o a una ubicación geográfica diferente. 

Recuperación ante desastres (DR) se organiza a través de la característica de conmutación por error de dispositivo de Hola y se inicia desde hello **dispositivos** página. Esta página tabula todos hello StorSimple dispositivos conectados tooyour el servicio StorSimple Manager. Para cada dispositivo, nombre descriptivo de hello, estado, capacidad de aprovisionamiento y máxima, se muestran el tipo y el modelo.

![Página de dispositivos](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

Guía de Hello en este tutorial aplica a dispositivos físicos y virtuales de tooStorSimple entre todas las versiones de software.

## <a name="disaster-recovery-dr-and-device-failover"></a>Recuperación ante desastres y conmutación por error del dispositivo
En un escenario de recuperación ante desastres, dispositivo primario Hola deja de funcionar. En esta situación, puede mover los datos de nube Hola asociados Hola error tooanother un dispositivo mediante dispositivo primario de hello como hello *origen* y especificando otro dispositivo como hello *destino*. Puede seleccionar uno o más volúmenes contenedores toomigrate toohello dispositivo de destino. Este proceso es que se hace referencia tooas hello *conmutación por error*. 

Durante la conmutación por error de hello, contenedores de volúmenes de hello de dispositivo de origen Hola cambiar la propiedad y son transferidos toohello dispositivo de destino. Una vez que los contenedores de volúmenes de hello cambiar la propiedad, estos se eliminan del dispositivo de origen Hola. Una vez completada la eliminación de hello, dispositivo de destino de hello puede, a continuación, se recuperarán tras los errores.

Normalmente después de una copia de seguridad más reciente de hello, recuperación ante desastres es el dispositivo de destino de toohello de toorestore usado Hola datos. Sin embargo, si hay varias directivas de copia de seguridad para Hola mismo volumen, a continuación, toma la directiva de copia de seguridad de hello con mayor número de volúmenes de Hola y Hola más reciente copia de seguridad desde dicha directiva toorestore usa datos de hello en dispositivo de destino de Hola.

Por ejemplo, si hay dos directivas de copia de seguridad (un valor predeterminado y uno personalizado) *defaultPol*, *customPol* con hello detalles siguientes:

* *defaultPol*: un volumen, *vol1*; se ejecuta diariamente a las 22:30.
* *customPol*: cuatro volúmenes, *vol1*, *vol2*, *vol3* y *vol4*; se ejecuta diariamente a las 22:00.

En este caso, se usará *customPol* , ya que es la que tiene más volúmenes, y establecemos prioridad para la coherencia de bloqueos. Hola de copia de seguridad más reciente de esta directiva es toorestore usa datos.

## <a name="considerations-for-device-failover"></a>Consideraciones para la conmutación por error del dispositivo
En caso de hello de un desastre, puede elegir toofail en el dispositivo de StorSimple:

* dispositivo físico de tooa 
* tooitself
* dispositivo virtual tooa

Para cualquier dispositivo de conmutación por error, tenga en siguiente Hola de cuenta:

* Hello requisitos previos de DR son que todos los volúmenes de hello dentro de contenedores de volúmenes de hello están desconectados y contenedores de volúmenes de hello tienen asociada una instantánea en la nube. 
* dispositivos de destino disponibles Hola de DR son dispositivos que tienen suficiente tooaccommodate espacio Hola contenedores de volumen seleccionados. 
* servicio Hello dispositivos que están conectado tooyour pero no cumplen los criterios de Hola de suficiente espacio no estarán disponible como dispositivos de destino.
* Después de una recuperación ante desastres, durante un tiempo limitado, puede afectar al rendimiento de acceso de datos de hello considerablemente, como dispositivo de hello necesitará tooaccess Hola datos de nube de Hola y almacenan de forma local.

#### <a name="device-failover-across-software-versions"></a>Conmutación por error del dispositivo a través de las versiones de software
Un servicio del administrador de StorSimple en una implementación puede tener varios dispositivos tanto virtuales como físicos, y todos ellos pueden ejecutar versiones de software diferentes. Tipos de volúmenes de hello en los dispositivos de hello según la versión de software de hello, también pueden ser diferentes. Por ejemplo, un dispositivo que ejecuta Update 2 o posterior tendría volúmenes anclados localmente y en capas (de tal forma que los archivos serían un subconjunto de las capas). Un dispositivo anterior a Update 2 en hello otra parte puede haber en niveles y los volúmenes de archivado. 

Usar hello después de la tabla toodetermine si puede conmutar por dispositivo de tooanother con un comportamiento de hello y versión de software diferente de tipos de volúmenes durante la recuperación ante desastres.

| Conmutación por error desde | Permitida para dispositivo físico | Permitida para dispositivo virtual |
| --- | --- | --- |
| Actualización 2 toopre-Update 1 (versión, 0.1, 0.2, 0.3) |No |No |
| Actualización 2 tooUpdate 1 (1, 1.1 y 1.2) |Sí <br></br>Si utiliza localmente anclado o niveles volúmenes o una combinación de dos, hello volúmenes se siempre conmutan por error como niveles. |Sí<br></br>Si utiliza volúmenes anclados localmente, su conmutación por error se realiza en capas. |
| Actualización 2 tooUpdate 2 (versión posterior) |Sí<br></br>Si usa volúmenes anclados localmente o en niveles o una combinación de dos, volúmenes de Hola se siempre conmutan por error como Hola a partir de tipo de volumen; en niveles como anclado localmente y en niveles anclado como localmente. |Sí<br></br>Si utiliza volúmenes anclados localmente, su conmutación por error se realiza en capas. |

#### <a name="partial-failover-across-software-versions"></a>Conmutación por error parcial entre versiones de software
Siga estas instrucciones si piensa tooperform una conmutación por error parcial con un dispositivo de origen de StorSimple con destino anterior a la actualización 1 tooa con Update 1 o posterior. 

| Conmutación por error parcial desde | Permitida para dispositivo físico | Permitida para dispositivo virtual |
| --- | --- | --- |
| Actualización previa 1 (versión, 0.1, 0.2, 0.3) tooUpdate 1 o posterior |Sí, vea a continuación de sugerencia de prácticas recomendada de Hola. |Sí, vea a continuación de sugerencia de prácticas recomendada de Hola. |

> [!TIP]
> Se produjo un cambio de formato de datos y metadatos de nube en la versión de actualización 1 y posteriores. Por lo tanto, no se recomienda una conmutación por error parcial de anteriores a la actualización 1 tooUpdate 1 o versiones posteriores. Si necesita tooperform una conmutación por error parcial, se recomienda que primero aplique Update 1 o posterior en ambos dispositivos hello (origen y destino) y, a continuación, continuar con la conmutación por error de Hola. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>Conmutar por error tooanother de dispositivo físico
Realizar Hola siguiendo los pasos toorestore el dispositivo físico de dispositivo tooa destino.

1. Compruebe que desea toofail sobre el contenedor de volumen Hola tenga asociadas instantáneas en la nube.
2. En hello **dispositivos** página, haga clic en hello **contenedores de volúmenes** ficha.
3. Seleccione un contenedor de volúmenes que desearía toofail sobre tooanother dispositivo. Haga clic en lista hello toodisplay de contenedor de volúmenes de Hola de volúmenes dentro de este contenedor. Seleccione un volumen y haga clic en **desconectar** volumen tootake Hola. Repita este proceso para todos los volúmenes de Hola Hola contenedor de volúmenes.
4. Paso anterior Hola repeticiones de Hola a todos los contenedores de volúmenes le gustaría toofail sobre tooanother dispositivo.
5. En hello **dispositivos** página, haga clic en **conmutación por error**.
6. En el Asistente de Hola que se abre, en **elegir toofail de contenedor de volumen en**:
   
   1. En lista de Hola de contenedores de volúmenes, seleccione los contenedores de volúmenes de hello sobre que le gustaría toofail.
      **Solo Hola contenedores de volúmenes con instantáneas en la nube asociado y se muestran los volúmenes sin conexión.**
   2. En **elegir un dispositivo de destino** para volúmenes de hello en contenedores de hello seleccionado, seleccione un dispositivo de destino desde la lista desplegable de Hola de dispositivos disponibles. Solo los dispositivos de Hola que tienen capacidad disponible de Hola se muestran en la lista desplegable de Hola.
   3. Por último, revise todas las opciones de conmutación por error de Hola de **confirmar conmutación por error**. Haga clic en el icono de verificación de hello ![el icono de comprobación](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Se crea un trabajo de conmutación por error que pueden controlarse a través de hello **trabajos** página. Si el contenedor de volúmenes de Hola que ha conmutado por error tiene volúmenes locales, verá los trabajos de restauración individuales para cada volumen local (no de volúmenes en capas) en el contenedor de Hola. Estos trabajos de restauración puede tardar bastante tiempo toocomplete. Es probable que el trabajo de conmutación por error Hola puede completarse anteriormente. Tenga en cuenta que estos volúmenes tendrá garantías locales solo cuando finalicen los trabajos de restauración de Hola. Una vez completada la conmutación por error de hello, vaya toohello **dispositivos** página.                                            
   
   1. Seleccione el dispositivo de Hola que se usó como dispositivo de destino de hello para el proceso de conmutación por error de Hola.
   2. Vaya toohello **contenedores de volúmenes** página. Todos los contenedores de volúmenes de hello, junto con los volúmenes de hello de dispositivo antiguo de hello, deberían aparecer.

## <a name="failover-using-a-single-device"></a>Conmutación por error usando un solo dispositivo
Realizar Hola siguientes pasos si solo tiene un único tooperform de dispositivo y la necesidad de una conmutación por error.

1. Tomar instantáneas de nube de todos los volúmenes de hello en el dispositivo.
2. Restablecer los valores predeterminados toofactory del dispositivo. Siga Hola detallada instrucciones [la configuración predeterminada de tooreset un toofactory de dispositivo de StorSimple](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Configure el dispositivo y vuelva a registrarlo con el servicio de Administrador de StorSimple.
4. En hello **dispositivos** dispositivo antiguo de Hola de página, debería aparecer como **sin conexión**. Hello dispositivo recién registrado debería ser **Online**.
5. Para el nuevo dispositivo hello, completar requisitos mínimos de configuración de dispositivo de Hola de hello primero. 
   
   > [!IMPORTANT]
   > **Si no se completa la configuración mínima de hello en primer lugar, se producirá un error en la recuperación ante desastres como resultado un error en la implementación actual de Hola. Este comportamiento se solucionará en una versión posterior.**
   > 
   > 
6. Seleccione el dispositivo antiguo de hello (estado sin conexión) y haga clic en **conmutación por error**. En Asistente Hola que aparece, conmutar por error este dispositivo y especifique el dispositivo de destino de hello como dispositivo recién registrado Hola. Para obtener instrucciones detalladas, consulte demasiado[conmutar por error dispositivo físico de tooanother](#fail-over-to-another-physical-device).
7. Se creará un trabajo de restauración de dispositivo que puede supervisar desde hello **trabajos** página.
8. Una vez se haya completado correctamente el trabajo de hello, acceder nuevo dispositivo de Hola y navegar toohello **contenedores de volúmenes** página. Todos los contenedores de volúmenes de hello de dispositivo antiguo de hello ahora debería toohello migrados nuevo dispositivo.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>Conmutar por error el dispositivo virtual StorSimple tooa
Debe tener un StorSimple dispositivo virtual creado y configurado toorunning anterior este procedimiento. Si ejecuta Update 2, considere el uso de un dispositivo virtual 8020 para hello DR que tiene 64 TB y utiliza almacenamiento Premium. 

Realizar Hola siguiendo los pasos toorestore Hola dispositivo tooa destino dispositivo virtual StorSimple.

1. Compruebe que desea toofail sobre el contenedor de volumen Hola tenga asociadas instantáneas en la nube.
2. En hello **dispositivos** página, haga clic en hello **contenedores de volúmenes** ficha.
3. Seleccione un contenedor de volúmenes que desearía toofail sobre tooanother dispositivo. Haga clic en lista hello toodisplay de contenedor de volúmenes de Hola de volúmenes dentro de este contenedor. Seleccione un volumen y haga clic en **desconectar** volumen tootake Hola. Repita este proceso para todos los volúmenes de Hola Hola contenedor de volúmenes.
4. Paso anterior Hola repeticiones de Hola a todos los contenedores de volúmenes le gustaría toofail sobre tooanother dispositivo.
5. En hello **dispositivos** página, haga clic en **conmutación por error**.
6. En el Asistente de Hola que se abre, en **elegir toofailover de contenedor de volumen**, complete Hola siguiente:
   
    a. En lista de Hola de contenedores de volúmenes, seleccione los contenedores de volúmenes de hello sobre que le gustaría toofail.
   
    **Solo Hola contenedores de volúmenes con instantáneas en la nube asociado y se muestran los volúmenes sin conexión.**
   
    b. En **elegir un dispositivo de destino para volúmenes de hello en contenedores de hello seleccionado**, seleccione Hola dispositivo virtual StorSimple desde la lista desplegable de Hola de dispositivos disponibles. **Solo los dispositivos de Hola que tienen suficiente capacidad se muestran en la lista desplegable de Hola.**  
7. Por último, revise todas las opciones de conmutación por error de Hola de **confirmar conmutación por error**. Haga clic en el icono de verificación de hello ![el icono de comprobación](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Una vez completada la conmutación por error de hello, vaya toohello **dispositivos** página.
   
    a. Seleccione el dispositivo virtual de hello StorSimple que se usó como dispositivo de destino de hello para el proceso de conmutación por error de Hola.
   
    b. Vaya toohello **contenedores de volúmenes** página. Deberían aparecer todos los contenedores de volúmenes de hello, junto con los volúmenes de hello de dispositivo antiguo de Hola.

![Vídeo disponible](./media/storsimple-device-failover-disaster-recovery/Video_icon.png)**Vídeo disponible**

Haga clic en un vídeo que muestra cómo se puede restaurar un error en el dispositivo virtual de tooa de dispositivo físico en la nube de hello, toowatch [aquí](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Conmutación por recuperación
Para Update 3 y versiones posteriores, StorSimple también admite la conmutación por recuperación. Una vez completada la conmutación por error de hello, hello realizan acciones siguientes:

* contenedores de volúmenes de Hola que se conmuten por error se borran Hola dispositivo de origen.
* Un trabajo en segundo plano por contenedor de volumen (conmutado) se inicia en el dispositivo de origen Hola. Si intentas toofailback mientras Hola trabajo está en curso, recibirá un efecto de toothat de notificación. Necesitará toowait hasta que se de trabajo de Hola Hola de toostart completa conmutación por recuperación. 
  
    Hola tiempo toocomplete Hola la eliminación de contenedores de volúmenes depende de varios factores como la cantidad de datos, la antigüedad de los datos de hello, el número de copias de seguridad y ancho de banda de red a Hola disponible para la operación de Hola. Si piensa probar la conmutación por error y la conmutación por recuperación, se recomienda que pruebe contenedores de volúmenes con menos datos (GB). En la mayoría de los casos, puede iniciar 24 horas una vez completada la conmutación por error de Hola Hola conmutación por recuperación. 

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
P: **¿Qué ocurre si Hola recuperación ante desastres, se produce un error o tiene parcialmente correcta?**

A. Si se produce un error en la recuperación ante desastres de hello, se recomienda que vuelva a intentarlo. Hello segunda vez, recuperación ante desastres sabe lo que todo se lleva a cabo y al proceso de hello detenido Hola primera vez. Hola proceso de recuperación ante desastres se inicia desde ese punto en adelante. 

P: **¿Puedo eliminar un dispositivo durante la conmutación por error de dispositivo de hello en curso?**

A. No se puede eliminar un dispositivo mientras se realiza una recuperación ante desastres. Sólo se puede eliminar el dispositivo una vez completada la recuperación ante desastres de Hola.

P:    **¿Cuando inicia recolección Hola Hola dispositivo de origen para que se eliminan los datos locales de hello en dispositivo de origen?**

A. Recolección de elementos se habilitará en el dispositivo de origen Hola solo después de dispositivo de Hola se limpia por completo. limpieza de Hello incluye limpiar objetos que han conmutado Hola dispositivo de origen como volúmenes, objetos de copia de seguridad (no los datos), los contenedores de volúmenes y las directivas.

P: **¿Qué ocurre si Hola elimina trabajo asociado con los contenedores de volúmenes de hello en dispositivo de origen Hola se produce un error?**

A.  Si Hola elimina el trabajo se produce un error, deberá eliminación de toomanually desencadenador Hola Hola de contenedores de volúmenes. Hola **dispositivos** , seleccione el dispositivo de origen y haga clic en **contenedores de volúmenes**. Haga clic en contenedores de volúmenes de hello SELECT que no se pudo sobre y en la parte inferior de Hola de página de hello, **eliminar**. Una vez haya eliminado todos los Hola conmutado contenedores de volúmenes en el dispositivo de origen de hello, puede iniciar Hola conmutación por recuperación.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Recuperación ante desastres y continuidad empresarial (BCDR)
Un escenario de recuperación (BCDR) de desastres de continuidad de negocio se produce cuando Hola todo Azure centro de datos deja de funcionar. Esto puede afectar a su servicio StorSimple Manager y Hola asociadas dispositivos StorSimple.

Si hay dispositivos de StorSimple que se han registrado justo antes de que se produzca un desastre, estos dispositivos de StorSimple necesite tooundergo restablecer una fábrica. Después de un desastre hello, dispositivo de StorSimple de Hola se mostrará como sin conexión. dispositivo de StorSimple de Hello debe eliminarse del portal de Hola y se debe realizar un restablecimiento de fábrica, seguido de un registro de actualización.

## <a name="next-steps"></a>Pasos siguientes
* Después de haber realizado una conmutación por error, puede que necesite demasiado[desactive o elimine el dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).
* Para obtener información acerca de cómo toouse Hola StorSimple Manager servicio, vaya demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

