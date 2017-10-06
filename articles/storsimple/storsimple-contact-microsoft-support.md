---
title: "aaaLog incidencia de soporte técnico para la serie 8000 de StorSimple | Documentos de Microsoft"
description: "Obtenga información acerca de cómo solicitar toocreate compatibilidad e iniciar una sesión de soporte técnico en el dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Contacto con el soporte técnico de Microsoft para StorSimple
Si tiene algún problema con la solución de Microsoft Azure StorSimple, puede crear una solicitud de servicio de soporte técnico. En una sesión con su ingeniero de soporte técnico en línea, también puede ser necesario toostart una sesión de soporte técnico en el dispositivo StorSimple. Este artículo le enseñará a:

* Cómo solicitar toocreate un soporte técnico.
* ¿Cómo toostart una sesión de soporte técnico en Hola interfaz de Windows PowerShell del dispositivo StorSimple.

Hola de revisión [SLA de soporte técnico de StorSimple 8000 Series e información](https://msdn.microsoft.com/library/mt433077.aspx) antes de crear una solicitud de soporte técnico.

## <a name="create-a-support-request"></a>Crear una solicitud de soporte
Lleve a cabo Hola siguiendo los pasos toocreate una solicitud de soporte técnico:

#### <a name="toocreate-a-support-request"></a>toocreate una solicitud de soporte técnico
1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), en hello esquina superior derecha, haga clic en el nombre de cuenta y, a continuación, haga clic en **póngase en contacto con soporte técnico de Microsoft**.
   
    ![Ponerse en contacto con el soporte técnico de MS a través del Portal de administración](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. Será redirigido toohello nuevo portal de Azure (portal.azure.com). Haga clic en hello **nueva solicitud de soporte técnico** icono.
   
    ![Ponerse en contacto con el soporte técnico de MS a través del nuevo portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    En el lado derecho de Hola de pantalla de bienvenida, Hola **nueva solicitud de soporte técnico** aparece el panel. 
   
    ![Panel Nueva solicitud de soporte](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. Hola **Fundamentos** cuadro de diálogo, Hola completa después de:                                
   
   1. De hello **emitir tipo** lista desplegable, seleccione **técnica**.
   2. Seleccione un **suscripción** desde la lista desplegable de Hola.
   3. De hello **servicio** lista desplegable, seleccione **StorSimple**. 
   4. Seleccione un **plan de soporte técnico** desde la lista desplegable de Hola. Es necesario un tooenable del plan de soporte técnico de pago de soporte técnico.
4. Haga clic en **Siguiente**. Hola **problema** aparece el cuadro de diálogo.
   
    ![Panel Nueva solicitud de soporte](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. Hola **problema** cuadro de diálogo, Hola completa después de:
   
   1. Seleccione un **gravedad** nivel de lista desplegable de Hola.
   2. Seleccione un **tipo de problema** desde la lista desplegable de Hola.
   3. Seleccione un **categoría** desde la lista desplegable de Hola. 
   4. Hola **detalles** cuadro, describa brevemente su problema.
   5. Hola **período de tiempo** cuadro, indique la fecha de hello, hora y zona horaria correspondiente toohello más reciente aparición del problema.
   6. En **cargar el archivo**, haga clic en el paquete de soporte de hello carpeta icono toobrowse tooyour.
   7. Seleccione hello **compartir información de diagnóstico** casilla de verificación.
6. Haga clic en **Siguiente**. Hola **información de contacto** aparece el cuadro de diálogo.
   
    ![Panel Nueva solicitud de soporte](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Escriba la información de contacto y seleccione un método de contacto (teléfono o correo electrónico). 
8. Seleccione hello **guardar los cambios en los contactos para las solicitudes de la compatibilidad futura** casilla de verificación.
9. Haga clic en **Crear**.

Una vez ha enviado la solicitud, un ingeniero de soporte técnico se comunicará con usted tan pronto como sea posible tooproceed con su solicitud.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Iniciar una sesión de soporte en Windows PowerShell para StorSimple
tootroubleshoot los problemas que pueda experimentar con el dispositivo de StorSimple de hello, necesitará tooengage con el equipo de Microsoft Support Hola. Microsoft Support puede necesitar toouse un toolog de sesión de soporte técnico en tooyour dispositivo. 

Realizar Hola siguientes pasos toostart una sesión de soporte técnico:

#### <a name="toostart-a-support-session"></a>toostart una sesión de soporte técnico
1. En el dispositivo de hello acceso directamente desde la consola de serie de Hola o a través de una sesión de telnet desde un equipo remoto. toodo, siga los pasos en hello [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. En la sesión de Hola que se abre, presione hello **ENTRAR** clave tooget un símbolo del sistema.
3. En el menú de consola serie de hello, seleccione la opción 1, **iniciar sesión con acceso completo**.
4. En el símbolo de hello, escriba Hola después de contraseña: 
   
    `Password1`
5. En el símbolo de hello, escriba Hola siguiente comando:
   
    `Enable-HcsSupportAccess`
6. Una cadena cifrada se presentará tooyou. Copie esta cadena en un editor de texto como el Bloc de notas.
7. Guarde esta cadena y enviarlos en un tooMicrosoft de mensaje de correo electrónico soporte técnico. 

> [!IMPORTANT]
> Puede deshabilitar el acceso al soporte técnico ejecutando `Disable-HcsSupportAccess`. dispositivo de StorSimple de Hello intentará también acceso al soporte técnico de toodisable 8 horas después de que se inició la sesión de Hola. Es una mejor toochange de práctica el dispositivo StorSimple credenciales después de iniciar una sesión de soporte técnico.
> 
> 

