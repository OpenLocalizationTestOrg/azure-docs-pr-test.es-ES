---
title: controladores de dispositivo de aaaManage StorSimple 8000 series | Documentos de Microsoft
description: "Obtenga información acerca de cómo toostop, reiniciar, apagar o restablecer los controladores del dispositivo StorSimple."
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
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Administrar controladores de su dispositivo StorSimple

## <a name="overview"></a>Información general

Este tutorial describen las operaciones diferentes Hola que pueden realizarse en los controladores de dispositivo de StorSimple. los controladores de Hello en el dispositivo StorSimple son controladores redundantes (del mismo nivel) en una configuración activo / pasivo. En un momento dado, solo un controlador está activo y procesa todas las operaciones de disco y red de Hola. Hello otro controlador está en el modo pasivo. Si se produce un error en el controlador activo de hello, el controlador pasivo Hola se convierte automáticamente en activo.

Este tutorial incluye controladores de dispositivo de instrucciones paso a paso toomanage Hola utilizando el:

* **Controladores** hoja para el dispositivo en hello servicio Administrador de dispositivos de StorSimple.
* Windows PowerShell para StorSimple

Se recomienda administrar controladores de dispositivo de Hola a través del servicio de administrador de dispositivos de StorSimple Hola. Si solo se puede realizar una acción mediante el uso de Windows PowerShell para StorSimple, tutorial Hola hace una nota del mismo.

Después de leer este tutorial, podrá:

* Reiniciar o apagar un controlador de dispositivo StorSimple
* Apagar un dispositivo StorSimple
* Restablecer los valores predeterminados toofactory del dispositivo de StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Reiniciar o apagar un solo controlador
No es necesario reiniciar o apagar un controlador como parte del funcionamiento normal del sistema. Las operaciones de apagado de un solo controlador de dispositivo son comunes solo en los casos en que un componente de hardware de dispositivo con error requiere reemplazo. También puede ser necesario reiniciar un controlador en situaciones en que el rendimiento se vea afectado por el uso excesivo de memoria o en la que un controlador no funcione correctamente. También deberá toorestart un controlador después de una sustitución del controlador correcta, si desea tooenable y Hola reemplazado controlador de pruebas.

Reinicio de un dispositivo no es tooconnected perturbador iniciadores, suponiendo que el controlador pasivo Hola está disponible. Si un controlador pasivo no está disponible o está desactivado, a continuación, reiniciar Hola active controlador puede dar lugar a Hola interrupción del servicio y el tiempo de inactividad.

> [!IMPORTANT]
> * **Un controlador en ejecución nunca debe moverse físicamente ya que esto podría provocar una pérdida de redundancia y un mayor riesgo de tiempo de inactividad.**
> * Hello siguiente procedimiento aplica sólo funciona StorSimple toohello como dispositivo físico. Para obtener información acerca de cómo toostart, detenga y Hola de reinicio del dispositivo de StorSimple en la nube, consulte [trabajar con el dispositivo de nube de hello](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

Puede reiniciar o apagar un controlador de dispositivo único a través de hello Azure portal del servicio de administrador de dispositivos de StorSimple de Hola o de Windows PowerShell para StorSimple.

toomanage los controladores del dispositivo de hello portal de Azure, realizar Hola lo siguiente.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart o apagar un controlador en el portal de Azure
1. En el servicio Administrador de dispositivos de StorSimple, vaya demasiado**dispositivos**. Seleccione el dispositivo de la lista de Hola de dispositivos. 

    ![Selección de un dispositivo](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Vaya demasiado**configuración > controladores**.
   
    ![Comprobar que los controladores del dispositivo StorSimple están en buen estado](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. Hola **controladores** hoja, compruebe que el estado de Hola de ambos controladores hello en el dispositivo es **correcto**. Seleccione un controlador, haga clic con el botón derecho y luego seleccione **Reiniciar** o **Apagar**.

    ![Selección de reinicio o apagado de los controladores del dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Un trabajo se crea toorestart o apagar el controlador de Hola y se presentan con advertencias aplicables, si lo hay. toomonitor Hola reinicio o apagado, vaya demasiado**servicio > registros de actividad** y, a continuación, filtrar por servicio tooyour específico de parámetros. Si se cerró un controlador, deberá toopush Hola power botón tooturn en hello controlador tooturn en.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart o apagar un controlador en Windows PowerShell para StorSimple
Realizar Hola siguiendo los pasos tooshut hacia abajo o reiniciar un controlador único en el dispositivo StorSimple de hello Windows PowerShell para StorSimple.

1. Dispositivo de Hola de acceso a través de la consola serie de Hola o una sesión de telnet desde un equipo remoto. tooconnect tooController 0 o controlador 1, siga los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.
3. En el mensaje de pancarta hello, tome nota del controlador de Hola que esta conectado demasiado (controlador 0 o controlador 1) y si se active de Hola o controlador pasivo (en espera) de Hola.
   
   * tooshut hacia abajo un único controlador, en el símbolo del sistema de hello, tipo:
     
       `Stop-HcsController`
     
       Esto apaga el controlador de Hola que están conectados a. Si se detiene el controlador activo hello, dispositivo Hola conmuta toohello el controlador pasivo.

   * toorestart un controlador, en el símbolo del sistema de hello, escriba:
     
       `Restart-HcsController`
     
       Esto reinicia el controlador de Hola que están conectados a. Si reinicia el controlador activo hello, se conmuta por error el controlador pasivo toohello antes de reiniciar la Hola.

## <a name="shut-down-a-storsimple-device"></a>Apagar un dispositivo StorSimple

Esta sección se explica cómo tooshut hacia abajo un ejecución o un dispositivo de StorSimple con error desde un equipo remoto. Un dispositivo se ha desactivado después de que se apagan ambos controladores de dispositivo de Hola. Un cierre del dispositivo se realiza cuando el dispositivo de Hola se mueve físicamente o se queda fuera de servicio.

> [!IMPORTANT]
> Antes de apagar el dispositivo de hello, compruebe el estado de Hola de componentes del dispositivo de Hola. Navegue tooyour dispositivo y, a continuación, haga clic en **configuración > estado del Hardware**. Hola **estado de hardware y estado** hoja, compruebe que el estado de hello LED de todos los componentes de hello es verde. Un dispositivo en buen estado tiene un estado verde. Si el dispositivo está apagando tooreplace un componente en mal estado, verá una error (rojo) o un estado degradado (amarillo) para Hola componentes correspondientes.


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut hacia abajo un dispositivo de StorSimple

1. Hola de uso [reiniciar o apagar un controlador de](#restart-or-shut-down-a-single-controller) tooidentify de procedimiento y cierren el controlador pasivo hello en el dispositivo. Puede realizar esta operación en hello portal de Azure o en Windows PowerShell para StorSimple.
2. Repita Hola por encima del paso tooshut hacia abajo el controlador activo Hola.
3. Debe Ahora volvamos en hello plano del dispositivo de Hola. Después de dos controladores de hello apagados por completo, hello ambos controladores Hola dos LED de estado deberían parpadear en rojo. Si necesita tooturn desactivar dispositivo Hola completamente en este momento, interruptores de alimentación de voltear hello en los módulos de alimentación y refrigeración (PCM) toohello posición de apagado. Esto debe desactivar el dispositivo de Hola.

## <a name="reset-hello-device-toofactory-default-settings"></a>Restablecer la configuración predeterminada de hello dispositivo toofactory

> [!IMPORTANT]
> Si necesita la configuración predeterminada del dispositivo toofactory tooreset, póngase en contacto con Microsoft Support. procedimiento Hola descrito a continuación solo debe utilizarse junto con Microsoft Support.

Este procedimiento describe cómo tooreset la configuración predeterminada de Microsoft Azure StorSimple dispositivo toofactory mediante Windows PowerShell para StorSimple.
Al restablecer un dispositivo quita todos los datos y la configuración de clúster completo de Hola de forma predeterminada.

Lleve a cabo Hola siguiendo los pasos tooreset la configuración predeterminada de Microsoft Azure StorSimple dispositivo toofactory:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault configuración de dispositivos en Windows PowerShell para StorSimple
1. Dispositivo de Hola de acceso a través de su consola serie. Compruebe tooensure de mensaje de pancarta Hola que está conectado toohello **Active** controlador.
2. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.
3. En el símbolo de hello, escriba Hola después clúster completo de comando tooreset hello, quitar todos los valores de datos, metadatos y controlador:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead para restablecer un único controlador, usar hello [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet con hello `-scope` parámetro.)
   
    sistema de Hola se reiniciará varias veces. Se le notificará cuando Hola restablecimiento se haya completado correctamente. Según el modelo de sistema de hello, puede tardar 45 a 60 minutos para un dispositivo 8100 y 60 a 90 minutos un toofinish 8600 este proceso.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Preguntas y respuestas sobre cómo administrar los controladores de dispositivo
En esta sección, hemos resumido algunos Hola preguntas más frecuentes sobre la administración de los controladores de dispositivo de StorSimple.

**P.** ¿Qué ocurre si ambos Hola controladores de mi dispositivo están encendido y en buen estado y puede reiniciar o apagar controlador activo Hola?

**R.** Si ambos controladores hello en el dispositivo están activados y figuran en adelante, se le solicitará confirmación. Puede elegir:

* **Reinicie el controlador activo Hola** : se le notificará que reiniciar un controlador activo provocado Hola dispositivo toofail sobre toohello el controlador pasivo. reinicia el controlador de Hola.
* **Apagar un controlador activo**: se le notifica que apagar un controlador activo dará lugar a tiempo de inactividad. También debe toopush botón de encendido Hola Hola tooturn de dispositivo en el controlador de Hola.

**P.** ¿Qué ocurre si el controlador pasivo hello en mi dispositivo está disponible o está desactivado y reiniciar o apagar controlador activo Hola?

**R.** Si el controlador pasivo de hello en el dispositivo no esté disponible o está desactivado y decide:

* **Reinicie el controlador activo Hola** : se le notifica que continuar la operación de hello dará como resultado una interrupción temporal del servicio de Hola y se le solicitará confirmación.
* **Apagar un controlador activo** : se le notificará que continuar operación Hola da como resultado un tiempo de inactividad. También debe toopush botón de encendido de hello en uno o ambos tooturn de controladores de dispositivo de Hola. Se le pedirá confirmación.

**P.** ¿Si Hola controlador reinicio o apagado no tiene éxito tooprogress?

**R.** El reinicio o apagado de un controlador puede producir un error si:

* Ye está en curso una actualización del dispositivo.
* Ya está en curso un reinicio del controlador.
* Ya está en curso un apagado del controlador.

**P.** ¿Cómo se puede saber si se ha reiniciado o apagado un controlador?

**R.** Puede comprobar el estado del controlador de hello en el módulo de controlador. estado del controlador Hola indicará si un controlador está en proceso de Hola de reiniciar o apagar. Además, Hola **alertas** hoja contienen una alerta informativa si se reinicia o apaga el controlador de Hola. operaciones de reinicio y apagado del controlador de Hello también se registran en los registros de actividad de Hola. Para obtener más información acerca de los registros de actividad, vaya demasiado[ver los registros de actividad de hello](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**P.** ¿Hay cualquier toohello impacto E/S como resultado de la conmutación por error del controlador?

**R.** las conexiones TCP de Hello entre los iniciadores y el controlador activo se restablecerán como resultado de la conmutación por error de controlador, pero se restablecerá cuando el controlador pasivo Hola asuma la operación. Puede haber una pausa temporal (menos de 30 segundos) en la actividad de E/S entre los iniciadores y los dispositivos de Hola durante el transcurso de Hola de esta operación.

**P.** ¿Cómo devolver mi tooservice controlador después de cerrar y quitar?

**R.** tooreturn un tooservice de controlador, se debe insertar en el chasis de hello tal y como se describe en [reemplazar un módulo de controlador en el dispositivo StorSimple](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Pasos siguientes
* Si tiene algún problema con los controladores de dispositivo de StorSimple que no se puede resolver mediante el uso de procedimientos de hello incluidos en este tutorial, [póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* toolearn más sobre el uso de servicio de administrador de dispositivos de StorSimple de hello, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

