---
title: 'Lanzamiento: SSPR de Azure AD | Microsoft Docs'
description: "Sugerencia para el lanzamiento del autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Lanzamiento del restablecimiento de contraseña para los usuarios

Mayoría de los clientes siga los pasos de Hola que siguen tooensure una implementación suave de funcionalidad de Autoservicio.

1. [Habilitación del restablecimiento de contraseña en el directorio](active-directory-passwords-getting-started.md)
2. [Configuración de los permisos de AD local para la escritura diferida de contraseñas](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Configurar la escritura diferida de contraseñas](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite contraseñas de Azure AD hacer copia de directorio local de tooyour
4. [Asignación y comprobación de las licencias necesarias](active-directory-passwords-licensing.md)
5. Si desea que tooroll out gradualmente, puede, opcionalmente, límite restablecimiento de contraseña tooa grupo de usuarios tooroll característica Hola lenta con el tiempo. toodo Esto establece hello **Self Service contraseñas restablecer habilitado** alternar de **todo el mundo** demasiado**un grupo** y seleccione un tooenable del grupo de seguridad para restablecer la contraseña. debe tener todas las licencias asignadas toothem Hello miembros de este grupo y es una excelente manera tooenable [grupo en función de licencias](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Rellenar el conjunto mínimo de Hola de [datos de autenticación](active-directory-passwords-data.md), en función de la directiva.
7. Enseñar a los usuarios cómo toouse SSPR, mediante el envío de instrucciones tooshow ellos cómo tooregister y cómo tooreset.
    > [!NOTE]
    > Pruebe SSPR con un usuario que no sea administrador, ya que Microsoft impone estrictos requisitos de autenticación para las cuentas de tipo administrador de Azure. Para obtener más información sobre la directiva de contraseñas de administrador de hello, consulte nuestro [artículo profundización](active-directory-passwords-how-it-works.md).

8. Puede elegir Registro tooenforce en cualquier momento y requieren los usuarios tooreconfirm su información de autenticación tras un período de tiempo determinado. Si no desea que su tooregister de toohave de los usuarios, puede [implementar el restablecimiento de contraseña sin necesidad de registro del usuario final](active-directory-passwords-data.md).
9. Con el tiempo, revise los usuarios registrar y utilizar viendo hello [reporting proporcionada por Azure AD](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Implementación basada en correo electrónico

Muchos clientes le resulte una campaña de correo electrónico con instrucciones de toouse simple, hello más fácil manera tooget usuarios toouse SSPR. [Hemos creado tres correos electrónicos simples que puede usar como plantillas toohelp en la implementación.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Próximamente** toobe de plantilla que se usa en hello semanas o días antes de que los usuarios de implementación toolet saben que necesitan toodo algo de correo electrónico.
* **Está disponible ahora** día de hello toobe usa de plantilla de inicio toodrive usuarios tooregister de correo electrónico y confirmar sus datos de autenticación para que puedan usar SSPR cuando lo necesiten.
* **Registrarse recordatorio** plantilla para tooweeks unos días de correo electrónico después de la implementación tooremind usuarios tooregister y confirmar sus datos de autenticación.

## <a name="creating-your-own-password-portal"></a>Creación de su propio portal de contraseñas

Muchos de nuestros clientes más grandes elegir página Web toohost y crear una entrada DNS, como https://passwords.contoso.com de raíz. Rellena esta página con el restablecimiento de contraseña de vínculos toohello Azure AD, registro, el portal de cambio de contraseñas y otra información específica de la organización de restablecimiento de contraseña. En las comunicaciones por correo electrónico o los folletos, enviar, a continuación, puede incluir una marca, fácil de recordar, dirección URL que los usuarios pueden ir toowhen que necesitan los servicios de hello toouse.

* Portal de restablecimiento de contraseña: https://passwordreset.microsoftonline.com/
* Portal de registro para el restablecimiento de contraseña: http://aka.ms/ssprsetup
* Portal para el cambio de contraseña: https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Uso del registro exigido

Si desea que su tooregister a los usuarios para restablecer la contraseña, puede obligarlos tooregister cuando inician sesión con Azure AD. Puede habilitar esta opción desde el directorio **de restablecimiento de contraseña** hoja habilitando hello **tooRegister de obligar a los usuarios cuando inician sesión en** opción en hello **registro** pestaña.

Los administradores pueden solicitar toore el registro de los usuarios después de un período de tiempo por establecer hello **número de días antes de que los usuarios son más frecuentes tooreconfirm su información de autenticación** entre 0 y 730 días.

Después de habilitar esta opción, los usuarios que inician verá un mensaje que les informa de su administrador les pide tooverify su información de autenticación.

## <a name="populate-authentication-data"></a>Rellenado de los datos de autenticación

Si se [rellenar los datos de autenticación para los usuarios](active-directory-passwords-data.md), a continuación, los usuarios no necesitan tooregister de restablecimiento de contraseña antes de que se va a toouse capaz de Autoservicio. Siempre y cuando los usuarios tienen datos de autenticación de hello definidos que cumplen la directiva de restablecimiento de contraseña de Hola ha definido, los usuarios son tooreset capaz de sus contraseñas.

## <a name="disabling-self-service-password-reset"></a>Deshabilitación del autoservicio de restablecimiento de contraseña

Deshabilitar el restablecimiento de contraseña de autoservicio es tan sencillo como abrir su inquilino de Azure AD y va demasiado**de restablecimiento de contraseña**, **propiedades**y elegir **nadie** en  **Autoservicio de restablecimiento de contraseña habilitado**

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Escritura diferida de contraseñas**](active-directory-passwords-writeback.md): cómo funciona la escritura diferida de contraseñas con su directorio local.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR
