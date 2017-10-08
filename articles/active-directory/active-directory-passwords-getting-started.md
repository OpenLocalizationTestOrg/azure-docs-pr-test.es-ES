---
title: "Inicio rápido: SSPR de Azure AD | Microsoft Docs"
description: "Implementación rápida del autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Inicio rápido: Autoservicio de restablecimiento de contraseña de Azure AD

> [!IMPORTANT]
> **¿Está aquí porque tiene problemas para iniciar sesión?** Si es así, [aquí aprenderá a cambiar y restablecer la contraseña](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Implementación rápida del autoservicio de restablecimiento de contraseña

Restablecimiento de contraseña de autoservicio (SSPR) ofrece un sencillo significa "" para TI administradores tooempower usuarios tooreset o desbloquear sus cuentas o contraseñas. Hello sistema incluye tootrack informes detallado cuando los usuarios usen el sistema de hello junto con las notificaciones tooalert toomisuse, o controlar el abuso.

En esta guía se da por hecho que ya dispone de un inquilino de Azure AD con licencia o una prueba operativa. Si necesita ayuda para configurar Azure AD, vea el artículo de hello [Introducción a Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).

1. En su inquilino de Azure AD existente, seleccione **"Restablecimiento de contraseña"**.

2. De hello **"Propiedades"** pantalla, en la opción Hola "Autoservicio servicio contraseña restablecer habilitado" Elija uno de los siguientes Hola
    * Nadie - no hay uno es la funcionalidad SSPR toouse capaz de
    * Sólo los miembros de un anuncio de Azure específico de un grupo: grupo que elija son funciones de Autoservicio pueda toouse
    * Todos los usuarios: todos los usuarios con cuentas en su inquilino de Azure AD son toouse capaz de funcionalidad de Autoservicio

3. De hello **"Métodos de autenticación"** elija pantalla
    * Número de métodos requerido tooreset: se admite un mínimo de uno o dos como máximo
    * Métodos disponibles toousers - se necesita al menos uno, pero nunca viene mal toohave una opción adicional disponible
        * **Correo electrónico** envía un correo electrónico con un usuario de toohello código configurar dirección de correo electrónico de autenticación
        * **Teléfono móvil** proporciona Hola usuario Hola elección tooreceive una llamada o texto con un tootheir código configura el número de teléfono móvil
        * **Teléfono del trabajo** configurada por el usuario de Hola de llamadas con un código tootheir número de teléfono
        * **Preguntas de seguridad** requiere toochoose
            * Número de preguntas requerido tooregister: como mínimo, Hola para registrarse correctamente, lo que significa que un usuario puede elegir tooanswer toocreate más toopull de preguntas de un grupo de. Esta opción puede establecerse entre 3 y 5 y debe ser mayor que o igual toohello número de preguntas necesario tooreset.
                * Se pueden agregar preguntas personalizados, haga clic en el botón de "Custom" hello al seleccionar preguntas de seguridad
            * Número de preguntas necesarias tooreset - puede establecerse entre 3 y 5 preguntas toobe responder correctamente antes de permitir una toobe de contraseña a los usuarios restablecer o desbloqueada.

4. RECOMENDADO: **"Personalización"** permite toochange Hola "Póngase en contacto con el Administrador de" vínculo toopoint tooa página o dirección de correo define

5. OPCIONAL: Hola **"Registro"** pantalla proporciona a los administradores opciones Hola para:
    * Requerir a los usuarios tooregister cuando inicien sesión en
    * Número de días antes de que los usuarios son más frecuentes tooreconfirm su información de autenticación

6. OPCIONAL: Hola **"Notificaciones"** pantalla proporciona a los administradores opciones Hola para:
    * ¿Quiere notificar a los usuarios los restablecimientos de contraseña?
    * ¿Quiere notificar a todos los administradores cuando otros administradores restablezcan su contraseña?

**Ya ha configurado SSPR para su inquilino de Azure AD**. Puede detener aquí o continuar en tooconfigure sincronización de contraseñas tooan dominio de Active Directory local.

> [!NOTE]
> Pruebe SSPR con un usuario que no sea administrador, ya que Microsoft impone estrictos requisitos de autenticación para las cuentas de tipo administrador de Azure. Para obtener más información sobre la directiva de contraseñas de administrador de hello, consulte nuestro [artículo de la directiva de contraseña](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Configurar origen de sincronización tooexisting identidad

tooenable tooAzure de sincronización de identidad AD local, necesita tooinstall y configurar [Azure AD Connect](./connect/active-directory-aadconnect.md) en un servidor en su organización. Esta aplicación controla la sincronización de usuarios y grupos de su inquilino de Azure AD existente de identidad origen tooyour.

* [Actualizar desde DirSync o sincronización de Azure AD tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Introducción a Azure AD Connect mediante la configuración rápida](./connect/active-directory-aadconnect-get-started-express.md)
* [Configurar la escritura diferida de contraseñas](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite contraseñas de Azure AD hacer copia de directorio local de tooyour.

## <a name="disabling-self-service-password-reset"></a>Deshabilitación del autoservicio de restablecimiento de contraseña

Deshabilitar el restablecimiento de contraseña de autoservicio es tan sencillo como abrir su inquilino de Azure AD y va demasiado**de restablecimiento de contraseña > propiedades** > elija **ninguno** en **autoservicio de restablecimiento de contraseña Habilitado**

### <a name="learn-more"></a>Más información
Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo restablece la contraseña de autoservicio de tooconfigure para los usuarios. toocontinue toohello toocomplete portal Azure siguen estos pasos Hola vínculo situado debajo de portal de toohello.

> [!div class="nextstepaction"]
> [Habilitar el autoservicio de restablecimiento de contraseña](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

