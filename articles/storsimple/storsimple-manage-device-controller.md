---
title: controladores de dispositivo de StorSimple aaaManage | Documentos de Microsoft
description: "Obtenga información acerca de cómo toostop, reiniciar, apagar o restablecer los controladores del dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Administrar controladores de su dispositivo StorSimple
## <a name="overview"></a>Información general
Este tutorial describen las operaciones diferentes Hola que pueden realizarse en los controladores de dispositivo de StorSimple. los controladores de Hello en el dispositivo StorSimple son controladores redundantes (del mismo nivel) en una configuración activo / pasivo. En un momento dado, solo un controlador está activo y procesa todas las operaciones de disco y red de Hola. Hello otro controlador está en el modo pasivo. Si se produce un error en el controlador activo hello, controlador pasivo Hola activará automáticamente.

Este tutorial incluye controladores de dispositivo de instrucciones paso a paso toomanage Hola utilizando el:

* **Controladores de** sección de hello **mantenimiento** página Hola el servicio StorSimple Manager
* Windows PowerShell para StorSimple

Se recomienda administrar controladores de dispositivo de hello mediante el servicio StorSimple Manager Hola. Si solo se puede realizar una acción mediante el uso de Windows PowerShell para StorSimple, tutorial Hola hace una nota del mismo.

Después de leer este tutorial, podrá:

* Reiniciar o apagar un controlador de dispositivo StorSimple
* Apagar un dispositivo StorSimple
* Restablecer los valores predeterminados toofactory del dispositivo de StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Reiniciar o apagar un solo controlador
No es necesario reiniciar o apagar un controlador como parte del funcionamiento normal del sistema. Las operaciones de apagado de un solo controlador de dispositivo son comunes solo en los casos en que un componente de hardware de dispositivo con error requiere reemplazo. También puede ser necesario reiniciar un controlador en situaciones en que el rendimiento se vea afectado por el uso excesivo de memoria o en la que un controlador no funcione correctamente. También deberá toorestart un controlador después de una sustitución del controlador correcta, si desea tooenable y Hola reemplazado controlador de pruebas.

Reinicio de un dispositivo no es tooconnected perturbador iniciadores, suponiendo que el controlador pasivo Hola está disponible. Si un controlador pasivo no está disponible o está desactivado, a continuación, reiniciar Hola active controlador puede dar lugar a Hola interrupción del servicio y el tiempo de inactividad.

> [!IMPORTANT]
> * **Un controlador en ejecución nunca debe moverse físicamente ya que esto podría provocar una pérdida de redundancia y un mayor riesgo de tiempo de inactividad.**
> * Hello siguiente procedimiento aplica sólo funciona StorSimple toohello como dispositivo físico. Para obtener información acerca de cómo ver toostart, detener y reiniciar el dispositivo virtual de hello, [trabajar con el dispositivo virtual hello](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

Puede reiniciar o apagar un controlador de dispositivo único mediante Hola portal de Azure clásico de servicio de StorSimple Manager de Hola o Windows PowerShell para StorSimple

toomanage los controladores del dispositivo de hello portal de Azure clásico, realizar Hola lo siguiente.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart o apagar un controlador en el portal clásico
1. Navegue demasiado**dispositivos > Mantenimiento**.
2. Vaya demasiado**estado del Hardware** y compruebe que el estado de Hola de ambos controladores hello en el dispositivo es **correcto**.
   
    ![Comprobar que los controladores del dispositivo StorSimple están en buen estado](./media/storsimple-manage-device-controller/IC766017.png)
3. Desde la parte inferior de Hola de hello **mantenimiento** página, haga clic en **administrar controladores**.
   
    ![Administrar controladores de dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Si no ve **administrar controladores**, deberá tooinstall actualizaciones. Para obtener más información, consulte [Actualizar dispositivo StorSimple](storsimple-update-device.md).
   > 
   > 
4. Hola **cambiar configuración de controlador** diálogo cuadro, Hola siguientes:
   
   1. De hello **seleccionar controlador** lista desplegable, que desea que toomanage del controlador que seleccione Hola. Opciones de Hello son controlador 0 y 1. Estos controladores también se identifican como activo o pasivo.
      
      > [!NOTE]
      > No se puede administrar un controlador si está disponible o está desactivado y no aparecerá en la lista desplegable de Hola.
      > 
      > 
   2. De hello **Seleccionar acción** desplegable Elija **reiniciar controlador** o **apagar controlador**.
      
       ![Reiniciar el controlador pasivo del dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766020.png)
   3. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-device-controller/IC740895.png).

Esto se reiniciar o apagar el controlador de Hola. tabla de Hello siguiente resume los detalles de Hola de lo que sucede según las selecciones de Hola que ha realizado en hello **cambiar configuración de controlador** cuadro de diálogo.  

| Número de selección | Si decide | Sucederá esto |
| --- | --- | --- |
| 1. |Reinicie el controlador pasivo Hola. |Se creará un trabajo de controlador de hello toorestart y se le notificará una vez se haya creado correctamente el trabajo de Hola. Esto iniciará el reinicio del controlador Hola. Puede supervisar el proceso de reinicio de hello accediendo **servicio > panel > Ver registros de operaciones** y, a continuación, el filtrado por servicio tooyour específico de parámetros. |
| 2. |Reinicie el controlador activo Hola. |Verá Hola siguiente advertencia: "si reinicia el controlador activo hello, dispositivo Hola conmutarán por error toohello el controlador pasivo. ¿Desea toocontinue?" </br>Si elige tooproceed con esta operación, pasos de hello será idéntico toothose utiliza toorestart Hola el controlador pasivo (vea selección 1). |
| 3. |Apague el controlador pasivo Hola. |Verá el siguiente mensaje de Hola: "una vez apagado, deberá toopush Hola botón de encendido en el controlador tooturn, en. ¿Está seguro de que desea tooshut hacia abajo de este controlador?" </br>Si elige tooproceed con esta operación, pasos de hello será idéntico toothose utiliza toorestart Hola el controlador pasivo (vea selección 1). |
| 4. |Apague el controlador activo Hola. |Verá el siguiente mensaje de Hola: "una vez apagado, deberá toopush Hola botón de encendido en el controlador tooturn, en. ¿Está seguro de que desea tooshut hacia abajo de este controlador?" </br>Si elige tooproceed con esta operación, pasos de hello será idéntico toothose utiliza toorestart Hola el controlador pasivo (vea selección 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart o apagar un controlador en Windows PowerShell para StorSimple
Realizar Hola siguiendo los pasos tooshut hacia abajo o reiniciar un controlador único en el dispositivo StorSimple de hello portal de Azure clásico.

1. Dispositivo de hello acceso mediante consola serie de Hola o una sesión de telnet desde un equipo remoto. Conectar tooController 0 o controlador 1 por hello siguiente pasos [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.
3. En el mensaje de pancarta hello, tome nota del controlador de Hola que esta conectado demasiado (controlador 0 o controlador 1) y si se active de Hola o controlador pasivo (en espera) de Hola.
   
   * tooshut hacia abajo un único controlador, en el símbolo del sistema de hello, tipo:
     
       `Stop-HcsController`
     
       Esto se apagará el controlador de Hola que están conectados a. Si se detiene el controlador activo hello, a continuación, conmutarán por error toohello el controlador pasivo antes del cierre.
   * toorestart un controlador, en el símbolo del sistema de hello, escriba:
     
       `Restart-HcsController`
     
       Esto reiniciará el controlador de Hola que están conectados a. Si reinicia el controlador activo hello, conmutarán por error toohello el controlador pasivo antes de reiniciar la Hola.

## <a name="shut-down-a-storsimple-device"></a>Apagar un dispositivo StorSimple
Esta sección se explica cómo tooshut hacia abajo un ejecución o un dispositivo de StorSimple con error desde un equipo remoto. Un dispositivo se ha desactivado después de cerrar ambos controladores de dispositivo de Hola. Un cierre del dispositivo se realiza cuando el dispositivo de Hola se mueve físicamente o se queda fuera de servicio.

> [!IMPORTANT]
> Antes de apagar el dispositivo de hello, compruebe el estado de Hola de componentes del dispositivo de Hola. Navegue demasiado**dispositivos > Mantenimiento > estado del Hardware** y compruebe que el estado de hello LED de todos los componentes de hello es verde. Solo los dispositivos correctos tendrán un estado verde. Si el dispositivo está apagando tooreplace un componente en mal estado, verá una error (rojo) o un estado degradado (amarillo) para Hola componentes correspondientes.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut hacia abajo un dispositivo de StorSimple
1. Hola de uso [reiniciar o apagar un controlador de](#restart-or-shut-down-a-single-controller) tooidentify de procedimiento y cierren el controlador pasivo hello en el dispositivo. Puede realizar esta operación en el portal de Azure clásico de Hola o en Windows PowerShell para StorSimple.
2. Repita Hola por encima del paso tooshut hacia abajo el controlador activo Hola.
3. Ahora deberá toolook en hello plano posterior del dispositivo de Hola. Después de dos controladores de hello apagados por completo, hello ambos controladores Hola dos LED de estado deberían parpadear en rojo. Si necesita tooturn desactivar dispositivo Hola completamente en este momento, interruptores de alimentación de voltear hello en los módulos de alimentación y refrigeración (PCM) toohello posición de apagado. Esto debe desactivar el dispositivo de Hola.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Restablecer la configuración predeterminada de hello dispositivo toofactory
> [!IMPORTANT]
> Si necesita la configuración predeterminada del dispositivo toofactory tooreset, póngase en contacto con Microsoft Support. procedimiento Hola descrito a continuación solo debe utilizarse junto con Microsoft Support.
> 
> 

Este procedimiento describe cómo tooreset la configuración predeterminada de Microsoft Azure StorSimple dispositivo toofactory mediante Windows PowerShell para StorSimple.
Al restablecer un dispositivo quita todos los datos y la configuración de clúster completo de Hola de forma predeterminada.

Lleve a cabo Hola siguiendo los pasos tooreset la configuración predeterminada de Microsoft Azure StorSimple dispositivo toofactory:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault configuración de dispositivos en Windows PowerShell para StorSimple
1. Dispositivo de Hola de acceso a través de su consola serie. Compruebe tooensure de mensaje de pancarta Hola que está conectado toohello controlador activo.
2. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.
3. En el símbolo de hello, escriba Hola después clúster completo de comando tooreset hello, quitar todos los valores de datos, metadatos y controlador:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead para restablecer un único controlador, usar hello [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet con hello `-scope` parámetro.)
   
    sistema de Hola se reiniciará varias veces. Se le notificará cuando Hola restablecimiento se haya completado correctamente. Según el modelo de sistema de hello, puede tardar 45 a 60 minutos para un dispositivo 8100 y 60 a 90 minutos un toofinish 8600 este proceso.
   
   > [!TIP]
   > * Si usa actualización 1.2 o versiones anteriores emplear hello `–SkipFirmwareVersionCheck` comprobación de la versión de firmware de parámetro tooskip Hola (en caso contrario, verá un error de coincidencia de firmware: restablecimiento de fábrica no puede continuar debido a falta de coincidencia de tooa en versiones de firmware de Hola. ).
   > * procedimiento de restablecimiento de fábrica de Hello puede producir un error en los dispositivos de StorSimple que se ejecutan Update 1 o 1.1 en el portal de administración pública de Hola y han llevado a cabo un reemplazo de controlador único o doble correcta (con controladores de sustitución que se enviaron con anterior a Update 1 software). Esto sucede al restablecimiento de fábrica de hello imagen se valida presencia de Hola de un archivo de SHA1 en controlador de Hola que no existe para el 1 de anteriores a la actualización de software. Si ve este generador de restablecer el error, póngase en contacto con Microsoft Support tooassist a Hola pasos siguientes. Este problema no se ve con controladores de sustitución que se enviaron desde el generador de hello con Update 1 o posterior del software.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Preguntas y respuestas sobre cómo administrar los controladores de dispositivo
En esta sección, hemos resumido algunos Hola preguntas más frecuentes sobre la administración de los controladores de dispositivo de StorSimple.

**P.** ¿Qué ocurre si ambos Hola controladores de mi dispositivo están encendido y en buen estado y puede reiniciar o apagar controlador activo Hola?

**R.** Si ambos controladores hello en el dispositivo están activados y figuran en adelante, se le pedirá confirmación. Puede elegir:

* **Reinicie el controlador activo Hola** : se le notificará que reiniciar un controlador activo provocará Hola dispositivo toofail sobre toohello el controlador pasivo. Hola controlador se reiniciará.
* **Apagar un controlador activo** : se le notificará que apagar un controlador activo resultará en tiempo de inactividad. También necesitará toopush botón de encendido Hola Hola tooturn de dispositivo en el controlador de Hola.

**P.** ¿Qué ocurre si el controlador pasivo hello en mi dispositivo está disponible o está desactivado y reiniciar o apagar controlador activo Hola?

**R.** Si el controlador pasivo de hello en el dispositivo no esté disponible o está desactivado y decide:

* **Reinicie el controlador activo Hola** : se le notificará que continuar la operación de hello dará como resultado una interrupción temporal del servicio de Hola y se le pedirá confirmación.
* **Apagar un controlador activo** : se le notificará que continuar la operación de hello dará como resultado un tiempo de inactividad y que necesitará toopush botón de encendido de hello en uno o ambos tooturn de controladores de dispositivo de Hola. Se le pedirá confirmación.

**P.** ¿Si Hola controlador reinicio o apagado no tiene éxito tooprogress?

**R.** El reinicio o apagado de un controlador puede producir un error si:

* Ye está en curso una actualización del dispositivo.
* Ya está en curso un reinicio del controlador.
* Ya está en curso un apagado del controlador.

**P.** ¿Cómo se puede saber si se ha reiniciado o apagado un controlador?

**R.** Puede comprobar el estado del controlador de hello en la página de mantenimiento de Hola. estado del controlador Hola indicará si un controlador ha sido reiniciado o apaga. Además, página de alertas de hello contendrá una alerta informativa si se reinicia o apaga el controlador de Hola. operaciones de reinicio y apagado del controlador de Hello también se registran en los registros de operaciones de Hola. Para obtener más información acerca de los registros de operación, vaya demasiado[ver registros de operaciones de hello](storsimple-service-dashboard.md#view-the-operations-logs).

**P.** ¿Hay cualquier toohello impacto E/s como resultado de la conmutación por error del controlador?

**R.** las conexiones TCP de Hello entre los iniciadores y el controlador activo se restablecerán como resultado de la conmutación por error de controlador, pero se restablecerá cuando el controlador pasivo Hola asuma la operación. Puede haber una pausa temporal (menos de 30 segundos) en la actividad de E/S entre los iniciadores y los dispositivos de Hola durante el transcurso de Hola de esta operación.

**P.** ¿Cómo devolver mi tooservice controlador después de cerrar y quitar?

**R.** tooreturn un tooservice de controlador, se debe insertar en el chasis de hello tal y como se describe en [reemplazar un módulo de controlador en el dispositivo StorSimple](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Pasos siguientes
* Si tiene algún problema con los controladores de dispositivo de StorSimple que no se puede resolver mediante el uso de procedimientos de hello incluidos en este tutorial, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md).
* toolearn más sobre el uso de servicio de StorSimple Manager hello, vaya demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

