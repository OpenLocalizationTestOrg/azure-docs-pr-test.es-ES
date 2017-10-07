---
title: "aaaAzure AD en niveles de seguridad de contraseña | Documentos de Microsoft"
description: "Explica cómo Azure AD aplica contraseñas seguras y protege las contraseñas de los usuarios frente a los ciberdelincuentes."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Un enfoque de varios niveles tooAzure AD contraseña de seguridad

En este artículo se describe algunos procedimientos recomendados que puede seguir como un usuario o un administrador tooprotect su Azure Active Directory (Azure AD) o Account de Microsoft.

 > [!NOTE]
 > Administradores de Azure AD pueden restablecer las contraseñas de usuario usando la orientación de hello en el artículo hello [Hola restablecimiento de contraseñas para un usuario en Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Los usuarios pueden restablecer su contraseña usando la orientación de hello en el artículo hello [ayuda he olvidado mi contraseña de Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Requisitos de contraseña

Azure AD incorpora Hola después de contraseñas de toosecuring enfoques comunes:

* Requisitos de longitud de contraseña
* Requisitos de complejidad de contraseña
* Expiración de contraseña normal y periódica

Para obtener información sobre el restablecimiento de contraseña en Azure Active Directory, vea el tema de hello [Azure AD restablecimiento de contraseña para profesionales de TI de hello](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Protección de contraseñas de Azure AD

Azure AD y aproxime de hello sistema de cuentas Microsoft usar comprobadas de la industria tooensure protección segura de las contraseñas de usuario y al administrador incluidos:

* Contraseñas prohibidas dinámicamente
* Smart Password Lockout

Para obtener información acerca de la administración de contraseñas basada en la investigación actual, vea notas del producto hello [contraseña instrucciones](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Contraseñas prohibidas dinámicamente

Azure AD y el sistema de cuentas de Microsoft salvaguardan la protección de contraseñas mediante la prohibición dinámica de las contraseñas de uso más común. equipo de protección de la identidad de Azure identificador Hello habitualmente analiza las listas de contraseñas prohibido, evitar que los usuarios de la selección de contraseñas utilizadas comúnmente. Este servicio está disponible tooAzure AD y clientes del servicio de cuenta de Microsoft Hola.

Al crear las contraseñas, es importante para los administradores tooencourage usuarios toochoose contraseña frases que contienen una combinación única de letras, números, caracteres o palabras. Este enfoque ayuda a las contraseñas de usuario de toomake toobe sea casi imposible en peligro pero más fácil para los usuarios tooremember.

#### <a name="password-breaches"></a>Infracciones de contraseña

Microsoft está trabajando siempre toostay un paso por delante de delincuentes intrusos.

equipo de Azure AD Identity Protection Hola analiza continuamente las contraseñas que se usan con frecuencia. Delincuentes intrusos también utilizan similar tooinform estrategias sus ataques, como crear una [tabla de arco iris](https://en.wikipedia.org/wiki/Rainbow_table) para descifrar un hash de contraseña.

Microsoft lo analiza continuamente [las infracciones de datos](https://www.privacyrights.org/data-breaches) toomaintain una lista de contraseña prohibida actualizado dinámicamente, lo que garantiza que las contraseñas vulnerables están expulsadas antes de que se conviertan en un número real de amenaza tooAzure AD clientes. Para obtener más información sobre nuestros esfuerzos de seguridad actual, vea hello [informe de inteligencia de seguridad de Microsoft](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Smart Password Lockout

Cuando AD Azure detecta un toohack de tratar de intrusos penales potencial en una contraseña de usuario, se bloquear cuenta de usuario de hello inteligente el bloqueo de contraseña. Azure AD está diseñado riesgo de hello toodetermine asociado a las sesiones de inicio de sesión específico. A continuación, utilizando los datos de seguridad más actualizadas de hello, aplicamos amenazas de ciberseguridad de toostop de semántica de bloqueo.

Si un usuario está bloqueado fuera de Azure AD, su pantalla tiene un aspecto similar toohello que sigue:

  ![Bloqueado en Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Para otras cuentas de Microsoft, su pantalla tiene un aspecto similar toohello que sigue:

  ![Bloqueado en una cuenta de Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Para obtener información sobre el restablecimiento de contraseña en Azure Active Directory, vea el tema de hello [Azure AD restablecimiento de contraseña para profesionales de TI de hello](active-directory-passwords.md).

  >[!NOTE]
  >Si eres un administrador de Azure AD, puede que desee toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid que los usuarios crea contraseñas tradicionales por completo.
  >

## <a name="next-steps"></a>Pasos siguientes

* [Cómo tooupdate su propia contraseña](active-directory-passwords-update-your-own-password.md)
* [aspectos básicos de Hola de administración de identidades de Azure](fundamentals-identity.md)
* [Informe sobre la actividad de restablecimiento de contraseña](active-directory-passwords-reporting.md)


