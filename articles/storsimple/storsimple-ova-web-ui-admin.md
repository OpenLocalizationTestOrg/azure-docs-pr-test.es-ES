---
title: "web de Virtual Array aaaStorSimple administración de la interfaz de usuario | Documentos de Microsoft"
description: "Describe cómo las tareas de administración de dispositivos básicos tooperform a través de la interfaz de usuario de web de StorSimple Virtual Array Hola."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Usar tooadminister de interfaz de usuario Web Hola la matriz Virtual de StorSimple
![flujo del proceso de instalación](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Información general
tutoriales de Hello en este artículo aplican versión de disponibilidad general (GA) de marzo de 2016 ejecución de toohello Microsoft Azure StorSimple Virtual Array (también conocido como hello StorSimple en dispositivo virtual local). En este artículo se describe algunos de los flujos de trabajo complejos de Hola y tareas de administración que se pueden realizar en hello StorSimple Virtual Array. Puede administrar Hola StorSimple Virtual Array mediante UI (portal de hello tooas que se hace referencia UI) del servicio de administrador de StorSimple de Hola y Hola de interfaz de usuario web local para dispositivos de Hola. En este artículo se centra en las tareas de Hola que puede realizar mediante la interfaz de usuario web de Hola.

Este artículo incluye Hola tutoriales:

* Obtener la clave de cifrado de datos del servicio de Hola
* Solucionar los problemas de instalación de la interfaz de usuario web
* Crear un paquete de registro
* Apagar o reiniciar el dispositivo

## <a name="get-hello-service-data-encryption-key"></a>Obtener la clave de cifrado de datos del servicio de Hola
Se genera una clave de cifrado de datos de servicio al registrar su primer dispositivo con hello el servicio StorSimple Manager. Esta clave es, a continuación, se requiere con hello servicio Registro tooregister clave dispositivos adicionales con el servicio StorSimple Manager hello.

Si el usuario ha perdido la clave de cifrado de datos de servicio y necesita tooretrieve, realizar Hola siguientes pasos de la interfaz de usuario del dispositivo de Hola de web local Hola registrados con el servicio.

#### <a name="tooget-hello-service-data-encryption-key"></a>clave de cifrado de datos del servicio de tooget Hola
1. Conectar la interfaz de usuario de web local toohello. Vaya demasiado**configuración** > **configuración de nube**.
2. En la parte inferior de Hola de página de hello, haga clic en **clave de cifrado de datos de servicio Get**. Aparecerá una clave. Cópiela y guárdela.
   
    ![obtener la clave de cifrado de los datos del servicio 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Solucionar los problemas de instalación de la interfaz de usuario web
Al configurar el dispositivo de Hola a través de web local de hello interfaz de usuario, en algunos casos pueden surgir de errores. toodiagnose y solucionar estos errores, puede ejecutar pruebas de diagnóstico de Hola.

#### <a name="toorun-hello-diagnostic-tests"></a>pruebas de diagnóstico de hello toorun
1. En la interfaz de usuario web local de hello, vaya demasiado**solución de problemas** > **pruebas de diagnóstico**.
   
    ![ejecutar diagnósticos 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. En la parte inferior de Hola de página de hello, haga clic en **ejecutar pruebas de diagnóstico**. Esto iniciará pruebas toodiagnose los posibles problemas con la red, dispositivos, proxy web, hora o configuración de la nube. Se le notificará que ese dispositivo Hola está ejecutando pruebas.
3. Una vez completadas las pruebas de hello, resultados de Hola se mostrarán. Hello en el ejemplo siguiente se muestra los resultados de Hola de pruebas de diagnóstico. Tenga en cuenta que no se configuraron la configuración del proxy web hello en este dispositivo y, por lo tanto, no se ejecutó la prueba de hello web proxy. Todos los Hola otras pruebas para la configuración de red, servidor DNS, y configuración de hora obtuvieron resultados satisfactorios.
   
    ![ejecutar diagnósticos 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Crear un paquete de registro
Un paquete de registros está formado por todos los registros pertinentes Hola que pueden ayudar a Microsoft Support a solucionar los problemas del dispositivo. En esta versión, se puede generar un paquete de registros a través de la interfaz de usuario de web local Hola.

#### <a name="toogenerate-hello-log-package"></a>paquete de registros de hello toogenerate
1. En la interfaz de usuario web local de hello, vaya demasiado**solución de problemas** > **registros del sistema**.
   
    ![crear un paquete de registro 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. En la parte inferior de Hola de página de hello, haga clic en **crear paquete de registro**. Se creará un paquete de registros de sistema de Hola. Este proceso tardará unos minutos.
   
    ![crear un paquete de registro 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Se le notificará una vez Hola paquete se creó correctamente y se actualizará la página de hello fecha cuando se creó el paquete de Hola y tooindicate Hola.
   
    ![crear un paquete de registro 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. Haga clic en **Descargar paquete de registro**. Se descargará un paquete comprimido en su sistema.
   
    ![crear un paquete de registro 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. Puede descomprimir paquete de registro descargado de Hola y ver archivos de registro del sistema de Hola.

## <a name="shut-down-and-restart-your-device"></a>Apagar y reiniciar el dispositivo
Puede apagar o reiniciar el dispositivo virtual mediante la interfaz de usuario de web local Hola. Se recomienda, antes de reiniciar, desconecte los volúmenes de Hola o recursos compartidos sin conexión en el host de hello y, a continuación, Hola dispositivo. Esto minimizará la posibilidad de daños en los datos. 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut hacia abajo el dispositivo virtual
1. En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **la configuración de energía**.
2. En la parte inferior de Hola de página de hello, haga clic en **apagado**.
   
    ![apagar el dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Aparecerá una advertencia que indica que un apagado de dispositivo de Hola interrumpirá la E/S que se encuentran en curso, lo que produce un tiempo de inactividad. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![advertencia de apagado del dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Se le notificará que el cierre Hola se ha iniciado.
   
    ![proceso de apagado del dispositivo iniciado](./media/storsimple-ova-web-ui-admin/image38.png)
   
    dispositivo de Hola se cerrará ahora. Si desea toostart el dispositivo, necesitará toodo que a través de administrador de Hyper-V de Hola.

#### <a name="toorestart-your-virtual-device"></a>toorestart el dispositivo virtual
1. En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **la configuración de energía**.
2. En la parte inferior de Hola de página de hello, haga clic en **reiniciar**.
   
    ![proceso de reinicio del dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. Aparecerá una advertencia que indica que ese dispositivo Hola reiniciar interrumpirá cualquier IOs que se encuentran en curso, lo que produce un tiempo de inactividad. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![advertencia de reinicio](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Se le notificará que el reinicio Hola se ha iniciado.
   
    ![proceso de reinicio comenzado](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Mientras Hola reinicio está en curso, perderá Hola conexión toohello interfaz de usuario. Puede supervisar Hola reinicio, actualice periódicamente Hola interfaz de usuario. Como alternativa, puede supervisar el estado de reinicio del dispositivo de Hola a través de administrador de Hyper-V de Hola.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[uso Hola toomanage de servicio de StorSimple Manager el dispositivo](storsimple-virtual-array-manager-service-administration.md).

