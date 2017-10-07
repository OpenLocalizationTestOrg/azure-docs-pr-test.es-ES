---
title: "aplicación de autenticador aaaMicrosoft ayuda y soporte técnico | Documentos de Microsoft"
description: "Proporciona una lista de las preguntas más frecuentes y respuestas de la aplicación de Microsoft Authentication toohello relacionados y la autenticación multifactor Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Preguntas más frecuentes de la aplicación Microsoft Authenticator

En este artículo respuestas a preguntas habituales que recibimos sobre la aplicación de Microsoft Authenticator hello. Si no ve una pregunta de respuesta tooyour, vaya toohello [foro de la aplicación de Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). También tenemos otra preguntas más frecuentes acerca de una característica específica de la aplicación hello, [inicien sesión con su teléfono preguntas más frecuentes sobre](microsoft-authenticator-app-phone-signin-faq.md).

aplicación de Microsoft Authenticator Hello reemplaza aplicación Azure Authenticator de hello y se recomienda aplicación Hola al utilizar la autenticación multifactor de Azure. está disponible para la aplicación de Microsoft Authenticator Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>¿Cuáles son los códigos de hello en la aplicación hello para? ¿Por qué número de hello mantener contando hacia abajo?

Cuando se abre la aplicación de Microsoft Authenticator hello, vea las cuentas de Hola que haya agregado y un número de seis u ocho dígitos por cada uno de ellos. Es posible que vea un temporizador de 30 segundos que cuenta de manera regresiva.

Estos códigos se usan al iniciar sesión en la cuenta de tooyour. Después de escribir el nombre de usuario y la contraseña, es posible que más frecuentes tooenter un código de comprobación. Abra Hola Microsoft Authenticator aplicación y copie Hola código que se está mostrando. Introducir ese código en hello toofinish de página de inicio de sesión.

motivo de Hola que códigos Hola cambio cada 30 segundos es para que nunca se utiliza Hola mismo código dos veces. No es como una contraseña que está ya debería estar tooremember. idea Hello es que sólo alguien con el teléfono de tooyour acceso sabe que su código de comprobación.

códigos de Hello no requieren internet o datos, por lo que no tiene tooworry relacionado con toosign de servicio de teléfono. Cuando se cierra la aplicación hello, no ejecutándose en segundo plano de Hola y no agotará la batería. Puede cerrar la aplicación hello y omitir hasta Hola próxima vez que inicie sesión en.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Solo recibir notificaciones cuando tengo aplicación hello abrir. Si no está abierta la aplicación hello, no se recibe ninguna notificación.

Si se reciben las notificaciones, pero no realizar ruido o vibrar a pesar de que el timbre con, compruebe primero la configuración de la aplicación hello. Habilitar el sonido de toouse aplicación Hola o Vibrar con sus notificaciones.

Si no obtiene las notificaciones en absoluto, compruebe Hola casos siguientes:

- ¿El teléfono se encuentra en modo silencioso o no molestar? Ese modo puede evitar que las aplicaciones envíen notificaciones.
- ¿Puede recibir notificaciones de otras aplicaciones? De lo contrario, puede haber un problema con las conexiones de red de hello en su teléfono o canal de notificaciones de Hola de Android o Apple. Puedes dirigirte a primera opción de hello en la configuración del teléfono, pero deberá proveedor de servicios de tootalk tooyour para obtener ayuda con la segunda opción de Hola.
- ¿Puede recibir notificaciones para algunas cuentas en la aplicación hello, pero no en otros? En caso afirmativo, quitar cuenta problemática hello de la aplicación y vuelva a agregarlo tooenable notificaciones de inserción. 

Si ha probado estas sugerencias de solución de problemas, pero sigue teniéndolos, envíenos sus registros para el diagnóstico. Vaya a configuración de la aplicación de toohello, a continuación, seleccione **ayuda y comentarios** y **enviar registros**. A continuación, ir toohello [foro de la aplicación de Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) y háganos saber lo que ve el problema y qué pasos se probó hasta ahora. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>Ya utilizo Hola aplicación Authenticator de Microsoft para códigos de comprobación. ¿Cómo se puede cambiar las notificaciones de inserción de tooone y haga clic en?
La aprobación de un inicio de sesión mediante notificaciones push solo está disponible para las cuentas personales, profesionales y educativas de Microsoft. No está disponible para cuentas de terceros, como Google o Facebook. Si tiene un trabajo o escuela cuenta Microsoft, su organización puede elegir toodisable esta opción.

Si usa una cuenta de Microsoft para su cuenta personal y desea tooswitch sobre toopush notificaciones, debe tooadd su cuenta de nuevo. Volver a registrar el dispositivo de hello con su cuenta y configurar las notificaciones de inserción.  

Si usas Microsoft Authenticator para su cuenta profesional o educativa, su organización decide si las notificaciones de un solo clic tooallow.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>¿Las notificaciones push de un solo clic funcionan con cuentas que no sean de Microsoft?
No, las notificaciones de inserción solo funcionan con cuentas de Microsoft y de Azure Active Directory. Si su trabajo o centro educativo utiliza cuentas de Azure AD, se puede deshabilitar esta característica.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>He restaurado el dispositivo de una copia de seguridad y me faltan los códigos de cuentas o no funcionan. ¿Qué ha ocurrido?
Por motivos de seguridad, no restauramos cuentas de copias de seguridad de aplicaciones.  Después de restaurar la aplicación hello, eliminar las cuentas y agréguelos de nuevo.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Tengo un nuevo dispositivo. ¿Cómo quitar la aplicación de Microsoft Authenticator Hola desde mi dispositivo antiguo y mover toohello uno nuevo?
Agregar Hola Microsoft Authenticator tooa nuevo dispositivo de aplicación no quita automáticamente de todos los demás dispositivos. toomanage qué dispositivos están configurados para su cuenta, visite Hola mismo sitio Web que use verificacion de toomanage y elija tooremove aplicaciones antiguas.

Para las cuentas de Microsoft personales, este sitio web es la página de su [cuenta seguridad](https://account.microsoft.com/security). Para las cuentas de Microsoft profesionales o educativas, este sitio web puede ser [Mis aplicaciones](https://myapps.microsoft.com) o un portal personalizado que su organización haya configurado.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>¿Cómo se puede quitar una cuenta de aplicación hello?
* iOS: desde la pantalla principal de bienvenida, deslice el dedo que queda en un icono de cuenta. Seleccione **Eliminar**.
* Windows Phone: Desde la pantalla principal de bienvenida, seleccione botón de menú de hello, a continuación, **editar cuentas**. Pulse hello **X** siguiente nombre de la cuenta de toohello.
* Android: Desde la pantalla principal de bienvenida, seleccione botón de menú de hello, a continuación, **editar cuentas**. Pulse hello **X** siguiente nombre de la cuenta de toohello.

Si tiene un dispositivo que está registrado en su organización, deberá toocomplete un paso adicional tooremove tu cuenta. En estos dispositivos, la aplicación de Microsoft Authenticator hello se registra automáticamente como administrador del dispositivo. Si desea que la aplicación hello de toocompletely desinstalar, necesita toofirst anular el registro de aplicación de hello en configuración de la aplicación hello.

### <a name="why-does-hello-app-request-so-many-permissions"></a>¿Por qué aplicación hello solicita permisos tantos?
Esta es una lista completa de permisos que le pidamos para y cómo se utilizan en la aplicación hello. permisos específicos de Hello que verá dependen de tipo hello de teléfono que tiene.

* **Cámara**: usamos sus códigos de tooscan QR cámara cuando se agrega un trabajo, escuela o cuenta no sea de Microsoft.
* **Contactos y teléfono**: cuando inicia sesión con tu cuenta Microsoft personal, intentamos proceso de hello toosimplify mediante la búsqueda de las cuentas existentes que utiliza en su teléfono.
* **SMS**: cuando inicia sesión con su cuenta personal de Microsoft para hello primera vez, tenemos que toomake seguro de que la coincide con números de teléfono Hola uno tenemos registrada. Enviamos un teléfono de toohello de mensaje de texto donde descargó la aplicación hello. mensaje de bienvenida contiene un código de comprobación de 6 a 8 dígitos. En lugar de pedirlas toofind este código y escríbala en la aplicación hello, se encontrará en el mensaje de bienvenida de texto por TI.
* **Dibuja sobre otras aplicaciones**: al recibir una notificación tooverify tu identidad, se muestra esa notificación a través de cualquier otra aplicación que podría estar ejecutándose.
* **Recibir datos de hello internet**: este permiso es necesario para enviar notificaciones.
* **Impedir que el teléfono entre en modo de suspensión**: si registra el dispositivo con su organización, puede cambiar esta directiva en su teléfono.
* **Controlar la vibración**: puede elegir si desea que una vibración siempre que reciba una notificación tooverify tu identidad.
* **Usar hardware de huella digital**: algunas cuentas profesionales o educativas requieran un PIN adicional cada vez que comprueba su identidad. proceso de hello toomake más fácil, permitimos toouse su huella digital en lugar de escribir Hola PIN.
* **Ver conexiones de red**: cuando se agrega una cuenta de Microsoft, aplicación hello requiere conexión de red o a internet.
* **Leer el contenido del saludo del almacenamiento**: este permiso sólo se usa al notificar un problema técnico a través de la configuración de la aplicación hello. Se recopila información de su almacenamiento problema de hello toodiagnose.
* **Acceso de red completo**: este permiso es necesario para enviar notificaciones tooverify tu identidad.
* **Se ejecutan al inicio**: si reinicia el teléfono, este permiso garantiza que continuará recibirá notificaciones tooverify tu identidad.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>¿Por qué Hola aplicación Authenticator de Microsoft le permite tooapprove una solicitud sin desbloquear dispositivo Hola?

No es necesario toounlock que la comprobación de tooapprove dispositivo solicita porque todo lo que necesita tooprove es que tiene el teléfono con usted. La verificación en dos pasos realiza dos comprobaciones: una comprobación de algo que sabe y una comprobación de algo que tiene. lo Hola que sabrá que es su contraseña. Hola que tiene es su teléfono (configurado con la aplicación de Microsoft Authenticator hello y registrado como una prueba de MFA). Por lo tanto, tener phone hello y aprobación de solicitud de hello cumple Hola criterios de segundo factor de autenticación de Hola. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>¿Qué significa el icono de candado de hello en la lista de cuentas de hello?

icono de candado Hola indica ese dispositivo Hola se registra en Azure AD y registradas toohello cuenta. El registro de dispositivos para iOS tiene lugar durante la inscripción de Microsoft Intune.

## <a name="next-steps"></a>Pasos siguientes

### <a name="contact-us"></a>Ponerse en contacto con nosotros
Si su pregunta no se responde aquí, es deseable toohear del usuario. Vaya toohello [foro de la aplicación de Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost tu pregunta y útil de comunidad de hello, o deje un comentario en esta página.


### <a name="related-topics"></a>Temas relacionados
* [Acerca de la comprobación en dos pasos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) de cuentas de Microsoft
* [Problemas con la verificación en dos pasos](multi-factor-authentication-end-user-troubleshoot.md) de la cuenta profesional o educativa
* [Usar Hola Microsoft Authenticator toosign en desde su teléfono](microsoft-authenticator-app-phone-signin-faq.md)

