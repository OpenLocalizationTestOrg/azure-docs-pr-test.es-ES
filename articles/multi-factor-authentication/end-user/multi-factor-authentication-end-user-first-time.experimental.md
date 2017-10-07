---
title: "aaaSet configuraste la verificación de mi cuenta profesional o educativa | Documentos de Microsoft"
description: "Si su empresa configura la autenticación multifactor Azure, podrás solicitada toosign hacia arriba para la verificación en dos pasos. Obtenga información acerca de cómo tooset, configúrelo. "
services: multi-factor-authentication
keywords: "¿Cómo toouse azure, active directory en la nube de hello, tutorial de active directory"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Configuración de mi cuenta para la comprobación en dos pasos
Verificación en dos pasos es un paso adicional de seguridad que ayuda a proteger su cuenta haciendo que sea más difícil para otro toobreak personas en. Si está leyendo este artículo, probablemente tiene un correo electrónico del administrador del trabajo o la escuela sobre Multi-Factor Authentication. O quizás intentó toosign en y se obtuvo un mensaje pidiéndole que tooset una comprobación de seguridad adicional. Si ese es el caso de hello, **no puede iniciar sesión hasta que haya completado el proceso de inscripción automática de hello**.

Este artículo le ayudará a configurar su **cuenta profesional o educativa**. Si desea tooenable verificacion de su propio personal cuenta de Microsoft, consulte [sobre la verificación en dos pasos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Configuración de la cuenta

Cuando el departamento de TI requiere toostart mediante la verificación en dos pasos, un comentario que pantalla **su administrador necesita que configure esta cuenta para la comprobación de seguridad adicional** aparece:

![Configuración](./media/multi-factor-authentication-end-user-first-time/first.png)

tooget iniciado, seleccione **configurar ahora.**

Si no ve una pantalla similar al siguiente al iniciar sesión, siga las instrucciones de hello en [administrar la configuración de verificación en dos pasos](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) página de configuración de hello toofind donde puede administrar las opciones de comprobación. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Decida cómo desea tooverify los inicios de sesión

primera pregunta de Hello en el proceso de inscripción de hello sea de su agrado nos toocontact. Eche un vistazo a las opciones de hello en la tabla de Hola y usar los pasos de configuración de hello vínculos toogo toohello para cada método.

| Método de contacto | Descripción |
| --- | --- |
| [Aplicación móvil](#use-a-mobile-app-as-the-contact-method) |- **Recibir notificaciones de comprobación.** Esta opción inserta una aplicación de autenticador de notificación toohello en su tableta o smartphone. Ver notificaciones de hello y, si es legítima, seleccione **Authenticate** en aplicación hello. Puede que su trabajo o escuela requiera que escriba un PIN para autenticarse.<br>- **Usar el código de comprobación.** En este modo, aplicación de autenticador de hello genera un código de comprobación que se actualiza cada 30 segundos. Escriba el código de comprobación más reciente de hello en la interfaz de inicio de sesión de Hola.<br>está disponible para la aplicación de Microsoft Authenticator Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Llamada de teléfono móvil o texto](#use-your-mobile-phone-as-the-contact-method) |- **Llamada de teléfono** coloca un número de teléfono toohello de llamada de voz automatizada que proporcione. Responder a la llamada de hello y presione # en hello phone teclado tooauthenticate.<br>- **Mensaje de texto** envía un mensaje de texto que contiene un código de comprobación. Después de símbolo del sistema de hello en texto hello, responder a mensajes de texto de toohello o introduzca el código de comprobación de hello proporcionado en la interfaz de inicio de sesión de Hola. |
| [Llamada de teléfono de la oficina](#use-your-office-phone-as-the-contact-method) |Coloca un número de teléfono toohello de llamada de voz automatizada que proporcione. Hola de respuesta llamada y presiona # en tooauthenticate de teclado del teléfono de Hola. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Usar una aplicación móvil como método de contacto de Hola
Con este método se requiere que instale una aplicación de autenticador en el teléfono o tableta. Hello pasos descritos en este artículo se basan aplicación de Microsoft Authenticator hello, que está disponible para [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Seleccione **aplicación móvil** desde la lista desplegable de Hola.
2. Seleccione **Recibir notificaciones de comprobación** o **Usar código de comprobación** y, luego, seleccione **Configurar**.

   ![Pantalla Comprobación de seguridad adicional](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. En su teléfono o tableta, abre la aplicación hello y selecciona  **+**  tooadd una cuenta. (En dispositivos Android, seleccione Hola tres puntos, a continuación, **Agregar cuenta**.)
4. Especifique que desea que tooadd una cuenta profesional o educativa. se abre el escáner de código QR de Hello en su teléfono. Si la cámara no funciona correctamente, puede seleccionar tooenter información de su empresa manualmente. Para más información, consulte [Incorporación manual de una cuenta](#add-an-account-manually).  
5. Digitalizar imagen de código QR de Hola que aparecieron con pantalla de bienvenida para configurar aplicación móvil de Hola.  Seleccione **realiza** pantalla de código de hello QR tooclose.  

   ![Pantalla de código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Cuando finaliza la activación en el teléfono de hello, seleccione **contacto me**.  Este paso envía una notificación o un teléfono de tooyour de código de comprobación. Seleccione **Comprobar**.  
7. Si su empresa requiere un PIN para aprobar la comprobación de inicio de sesión, escríbalo.

   ![Cuadro para escribir un NIP](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. Cuando haya terminado de escribir el PIN, seleccione **Cerrar**. A estas alturas, la verificación debería haberse realizado correctamente.
9. Se recomienda que escriba su número de teléfono móvil en caso de que pierda aplicación móvil de acceso tooyour. Especifica el país en la lista desplegable de Hola y escriba su número de teléfono móvil en nombre de país de hello cuadro siguiente toohello. Seleccione **Siguiente**.
10. En este momento, son solicitada tooset las contraseñas de aplicaciones para aplicaciones que no son de explorador como Outlook 2010 o anterior, o una aplicación de correo electrónico nativo de hello en dispositivos de Apple. Esta acción se debe a que algunas aplicaciones no admiten la verificación en dos pasos. Si no se utilizan estas aplicaciones, haga clic en **realiza** y omitir el resto de Hola de estos pasos.
11. Si utilizas estas aplicaciones, copiar la contraseña de aplicación de hello proporcionado y péguelo en la aplicación en lugar de la contraseña regular. Puede usar hello misma contraseña de aplicación para varias aplicaciones. Para más información, [ayuda con contraseñas de aplicación].
12. Haga clic en **Done**(Listo).

### <a name="add-an-account-manually"></a>Incorporación manual de una cuenta
Si desea que una aplicación móvil de cuenta toohello tooadd manualmente, en lugar de usar el lector de hello QR, siga estos pasos.

1. Seleccione hello **escriba cuenta manualmente** botón.  
2. Escriba el código de hello y la dirección URL de Hola que se proporcionan en hello la misma página que muestra Hola código de barras. Esta información va en hello **código** y **URL** cuadros en la aplicación móvil de Hola.

    ![Configuración](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Cuando haya finalizado la activación de hello, seleccione **contacto me**. Este paso envía una notificación o un teléfono de tooyour de código de comprobación. Seleccione **Comprobar**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Usar su teléfono móvil como método de contacto de Hola
1. Seleccione **teléfono de autenticación** desde la lista desplegable de Hola.  

    ![Configuración](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Seleccione su país de la lista desplegable de Hola y escriba su número de teléfono móvil.
3. Seleccionar método de hello prefiere toouse con su teléfono móvil - texto o llamada.
4. Seleccione **contacto me** tooverify su número de teléfono. Dependiendo del modo de saludo seleccionado, se envían un texto o llamada. Siga las instrucciones de hello proporcionadas en la pantalla de bienvenida, a continuación, seleccione **compruebe**.
5. En este momento, son solicitada tooset las contraseñas de aplicaciones para aplicaciones que no son de explorador como Outlook 2010 o anterior, o una aplicación de correo electrónico nativo de hello en dispositivos de Apple. Esta acción se debe a que algunas aplicaciones no admiten la verificación en dos pasos. Si no se utilizan estas aplicaciones, haga clic en **realiza** y omitir el resto de Hola de pasos de Hola.
6. Si utilizas estas aplicaciones, copiar la contraseña de aplicación de hello proporcionado y péguelo en la aplicación en lugar de la contraseña regular. Puede usar hello misma contraseña de aplicación para varias aplicaciones. Para más información, [ayuda con contraseñas de aplicación].
7. Haga clic en **Done**(Listo).

## <a name="use-your-office-phone-as-hello-contact-method"></a>Usar el teléfono del trabajo como método de contacto de Hola
1. Seleccione **teléfono del trabajo** en Hola de lista desplegable  

    ![Configuración](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. cuadro de número de teléfono de Hola se rellena automáticamente con la información de contacto de su empresa. Si el número de hello es incorrecto o que falta, pida a su administrador toomake cambios.
3. Seleccione **contacto me** tooverify su número de teléfono y se llamará a su número. Siga las instrucciones de hello proporcionadas en la pantalla de bienvenida, a continuación, seleccione **compruebe**.
4. En este momento, son solicitada tooset las contraseñas de aplicaciones para aplicaciones que no son de explorador como Outlook 2010 o anterior, o una aplicación de correo electrónico nativo de hello en dispositivos de Apple. Esta acción se debe a que algunas aplicaciones no admiten la verificación en dos pasos. Si no se utilizan estas aplicaciones, haga clic en **realiza** y omitir el resto de Hola de pasos de Hola.
5. Si utilizas estas aplicaciones, copiar la contraseña de aplicación de hello proporcionado y péguelo en la aplicación en lugar de la contraseña regular. Puede usar hello misma contraseña de aplicación para varias aplicaciones. Para más información, consulte [¿Cuáles son las contraseñas de aplicación?](multi-factor-authentication-end-user-app-passwords.md)
6. Haga clic en **Done**(Listo).

## <a name="next-steps"></a>Pasos siguientes
* Cambiar las opciones preferidas y [administrar la configuración de la comprobación en dos pasos](multi-factor-authentication-end-user-manage-settings.md)
* Configure las [contraseñas de aplicación](multi-factor-authentication-end-user-app-passwords.md) para las aplicaciones de dispositivos nativos que no admiten la comprobación en dos pasos.
* Extraer del repositorio hello [aplicación Microsoft Authenticator](microsoft-authenticator-app-how-to.md) para una rápida y de autenticación segura incluso cuando no tienes servicio de la celda.

