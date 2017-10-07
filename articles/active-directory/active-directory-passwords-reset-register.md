---
title: 'Azure AD: registro de SSPR | Microsoft Docs'
description: "Registro de datos de autenticación de autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>Registro para el autoservicio de restablecimiento de contraseñas

> [!IMPORTANT]
> **¿Está aquí porque tiene problemas para iniciar sesión?** Si es así, [aquí aprenderá a cambiar y restablecer la contraseña](active-directory-passwords-update-your-own-password.md).

Como un usuario final, puede restablecer su contraseña o desbloquear su cuenta sin necesidad de toospeak tooa persona mediante el restablecimiento de contraseña de autoservicio (SSPR). Para poder usar esta funcionalidad, debe tener métodos de autenticación tooregister o confirmar Hola predefinido métodos de autenticación se ha rellenado el administrador.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>Registro o confirmación de los datos de autenticación con SSPR

1. Explorador de web Hola abierto en el dispositivo y vaya toohello [página de registro de restablecimiento de contraseña](http://aka.ms/ssprsetup)
2. Escriba el nombre de usuario y la contraseña proporcionada por el administrador
3. Dependiendo de cómo haya configurado su personal de TI cosas, uno o varios de los siguientes Hola opciones están disponibles para tooconfigure y compruebe. El administrador puede rellenar parte de esto automáticamente si tienen la información sobre los permisos toouse Hola.
    * Teléfono del trabajo es sólo puede toobe establecida por el administrador
    * Teléfono de autenticación debe establecerse como número de teléfono de tooanother tendría acceso toolike un teléfono móvil que puede recibir una llamada o texto.
    * Se debe establecer tooan dirección de correo electrónico alternativa que puede tener acceso a correo electrónico de autenticación sin contraseña Hola necesita tooreset.
    * Preguntas de seguridad proporciona una lista de preguntas que el administrador ha aprobado para tooanswer. No se puede usar Hola misma pregunta o responder a más de una vez.
4. Proporcionar y compruebe la información de hello requerido por el administrador. Si hay más de una opción, se recomienda registrar varios flexibilidad de tooprovide métodos cuando no está disponible otro método (ejemplo: tooaccess durante sus viajes y no se puede el teléfono del trabajo)

    ![Registrar los métodos de autenticación y hacer clic en Finalizar][Register]

5. Cuando haya terminado con el paso 4 elija **finalizar** y ahora estará toouse capaz de restablecimiento de contraseña cuando necesite tooin Hola futuro.

Si escribe datos en Hola teléfono de autenticación o de correo electrónico de autenticación, no es visible en el directorio global Hola. Hola únicamente las personas que pueden ver estos datos son y los administradores. Solo puede ver Hola responde tooyour preguntas de seguridad.

Los administradores pueden requerir los métodos de autenticación tooconfirm tras un período de tiempo toomake aún dispone de los métodos adecuados de hello registrados.

## <a name="common-problems-and-their-solutions"></a>problemas comunes y sus soluciones

 A continuación se presentan algunos casos terror comunes y sus soluciones:

| Caso de error| ¿Qué tipo de error aparece?| Solución |
| --- | --- | --- |
| Al escribir mi identificador de usuario, aparece una página "Póngase en contacto con su administrador" | Póngase en contacto con el administrador <br> <br> Hemos detectado que la contraseña de su cuenta de usuario no está administrada por Microsoft. Como resultado, estamos no se puede tooautomatically restablecer su contraseña. <br> <br> Debe toocontact su personal de TI para obtener ayuda. | Está viendo este mensaje porque su personal de TI administra la contraseña en su entorno local y no podrá tooreset la contraseña de la no puede acceder a su vínculo de la cuenta. <br> <br> tooreset su contraseña, póngase en contacto con su personal de TI directamente para ayudar a y que les permiten conocer desea tooreset su contraseña, por lo que puede habilitar esta característica para usted.|
| Después de escribir mi identificador de usuario, recibo el error "Su cuenta no está habilitada para el restablecimiento de contraseña". | La cuenta no está habilitada para restablecer la contraseña <br> <br> Su personal de TI no ha configurado la cuenta para utilizarla con este servicio. <br> <br> Si lo desea, podremos contactar con un administrador de su organización tooreset la contraseña automáticamente. | Está viendo este mensaje porque su personal de TI no habilitó el restablecimiento de contraseña de su organización desde el no puede acceder a su vínculo de la cuenta o no con una licencia de característica de hello toouse. <br> <br> tooreset su contraseña, haga clic en el contacto un toosend de vínculo de administrador una empresa tooyour de correo electrónico del personal de TI y hágales saber desea tooreset su contraseña por lo que puede habilitar esta característica para usted. |
| Después de escribir mi identificador de usuario, recibo el error "No se pudo comprobar su cuenta". | No se ha podido comprobar su cuenta. <br> <br> Si lo desea, podremos contactar con un administrador de su organización tooreset la contraseña automáticamente. | Está viendo este mensaje porque están habilitados para restablecer la contraseña, pero no se ha registrado el servicio de hello toouse. tooregister de contraseña para restablecer, vaya toohttp://aka.ms/ssprsetup después de que se ha recuperado el acceso tooyour cuenta. <br> <br> tooreset su contraseña, haga clic en el contacto con un administrador vínculo toosend una empresa tooyour de correo electrónico personal de TI. |

## <a name="next-steps"></a>Pasos siguientes

* [Cómo toochange su mediante contraseña de autoservicio de restablecimiento de contraseña](active-directory-passwords-update-your-own-password.md)
* [Página de registro en el restablecimiento de contraseña](http://aka.ms/ssprsetup)
* [Portal de restablecimiento de contraseña](https://passwordreset.microsoftonline.com/)
* [No puede iniciar sesión en tooyour cuenta de Microsoft](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Página de registro en el restablecimiento de contraseña que muestra los métodos registrados y botón Finalizar"

