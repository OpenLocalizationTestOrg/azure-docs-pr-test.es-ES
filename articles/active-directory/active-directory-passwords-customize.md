---
title: "Personalización: SSPR de Azure AD | Microsoft Docs"
description: "Opciones de personalización para el restablecimiento de contraseñas de autoservicio de Azure AD"
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
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Personalice la funcionalidad de autoservicio de restablecimiento de contraseña de Azure AD

Busca el restablecimiento de contraseña de autoservicio de toodeploy los profesionales de TI pueden personalizar Hola experiencia toomatch sus usuarios.

## <a name="customize-hello-contact-your-administrator-link"></a>Personalizar el vínculo del Administrador de contacto de Hola

Incluso si SSPR no está habilitado a los usuarios todavía un "Póngase en contacto con el Administrador de" vínculo contraseña Hola portal de restablecimiento.  Al hacer clic en este vínculo por correo electrónico los administradores que pregunta para obtener ayuda para cambiar la contraseña del usuario de Hola. Este correo electrónico se envía toohello siguientes a destinatarios de hello siguiendo el orden:

1. Si hello **Administrador de contraseñas** está asignado el rol, se notificación a los administradores a este rol
2. Si no hay administradores de contraseñas se asignan, a continuación, los administradores con hello **usuario administrador** se notifica a rol
3. Si ninguno de los roles anteriores Hola se asignaron, a continuación, **los administradores globales** notificación

En todos los casos, se notificará a un máximo de 100 destinatarios en total.

toofind más información sobre roles de administrador distintas de Hola y cómo tooassign ellos vea Hola documento [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Deshabilitar los correos electrónicos de contacto con los administradores

Si su organización no desea que los administradores una notificación acerca de la contraseña de solicitudes de restablecimiento, hello configuración siguiente se puede habilitar

* Habilite el autoservicio de restablecimiento de contraseñas para todos los usuarios finales. Esta opción está disponible en **Restablecimiento de contraseña > Propiedades**.
    * Si no desea que los usuarios tooreset sus propias contraseñas, se puede establecer el ámbito de grupo vacío de acceso tooan **no se recomienda esta opción**.
* Personalizar tooprovide de vínculo de soporte técnico de hello una dirección URL web o mailto: dirección que los usuarios pueden usar tooget asistencia. Esta opción se encuentra en **Restablecimiento de contraseña > Personalización > Dirección URL o correo electrónico del departamento de soporte técnico personalizados**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>Personalización de la página de inicio de sesión de ADFS para SSPR

Los administradores de AD FS puede agregar una vínculo tootheir página Inicio de sesión usando la orientación de Hola se encuentra en el artículo hello [descripción de la página de inicio de sesión de agregar](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

Utilizando el comando de Hola que sigue en el servidor de ADFS, agrega una página de inicio de sesión ADFS de vínculo toohello directamente lo que permite a los usuarios tooenter Hola contraseña de autoservicio restablecimiento de flujo de trabajo.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Personalizar Hola inicio de sesión y acceso panel Apariencia

Cuando los usuarios tener acceso a la página de inicio de sesión de hello, puede personalizar el logotipo de Hola que aparece junto con toofit de imagen de página de inicio de sesión de hello su marcas de empresa.

Estos gráficos se muestran en hello siguientes circunstancias:

* Después de que un usuario escribe su nombre de usuario.
* Cuando el usuario accede a la dirección URL personalizada.
    * Hola pasar "whr" parámetro toohello password restablece página, como "https://login.microsoftonline.com/?whr=contoso.com"
    * Al pasar Hola "username" parámetro toohello de restablecimiento de contraseña página, como "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Detalles de gráficos

Permitir características visuales de hello toochange de página de inicio de sesión de Hola Hola siguientes opciones y pueden encontrarse en **Azure Active Directory**, **información de marca**, **editar empresa personalización de marca**

* La imagen de la página de inicio de sesión debe ser un archivo PNG o JPG de 1420x1200 píxeles, con un tamaño máximo de 500 KB. Se recomienda toobe aproximadamente 200 KB para obtener los mejores resultados.
* Color de fondo de la página de inicio de sesión se utiliza en las conexiones de alta latencia y debe estar en formato hexadecimal de RGB Hola.
* La imagen del banner debe ser un archivo PNG o JPG de 60x280 píxeles, con un tamaño máximo de 10 KB.
* El logotipo debe ser cuadrado (tema normal u oscuro) y debe ser un archivo PNG o JPG de 240x240 píxeles (redimensionable), con un tamaño máximo de 10 KB.

### <a name="sign-in-text-options"></a>Opciones de texto de inicio de sesión

Hola después de la configuración le permite organización tooyour relevantes de tooadd texto toohello página de inicio de sesión. Esta configuración se puede encontrar en **Azure Active Directory**, **Personalización de marca de empresa**, **Editar personalización de marca de empresa**.

* **Sugerencia de nombre de usuario** reemplaza texto de ejemplo de Hola someone@example.com con algo más adecuado para los usuarios, se recomienda toobe izquierdo predeterminado como apoyo para los usuarios internos y externos
* El **texto de la página de inicio de sesión** admite una longitud máxima de 256 caracteres. Este texto aparece en cualquier parte de su inicio de sesión de los usuarios en línea y en hello experiencia Azure AD Join en Windows 10. Utilice este texto para los términos de uso, las instrucciones y las sugerencias para los usuarios. **Cualquier usuario puede ver la página de inicio de sesión, por lo que no debe proporcionar ninguna información confidencial aquí.**

### <a name="keep-me-signed-in-disabled"></a>Se deshabilitó la opción Mantener la sesión iniciada

opción de Hola "mantener la sesión iniciada en deshabilitado" permite tooremain usuarios iniciado sesión cuando cierre y vuelva a abrir las ventanas del explorador. Esta opción no afecta a la duración de las sesiones. Esta configuración se encuentra en **Azure Active Directory > Personalización de marca de empresa > Editar personalización de marca de empresa**.

Algunas características de SharePoint Online y Office 2010 tienen una dependencia en los usuarios que están toocheck capaz de este cuadro. Si oculta esta opción, los usuarios pueden obtener solicitudes de inicio de sesión adicionales e inesperadas.

### <a name="directory-name"></a>Nombre de directorio

Puede cambiar el atributo de nombre de hello en **Azure Active Directory > propiedades** tooshow un nombre de organización descriptivo aparece en el portal de Hola y automatizar las comunicaciones. Esta opción es más visible en forma de Hola de mensajes de correo electrónico automatizadas en los formularios de Hola que siguen

* Nombre descriptivo del correo electrónico "Demostración de Microsoft en nombre de CONTOSO"
* Línea de asunto del correo electrónico "Código de verificación del correo electrónico de la cuenta de demostración CONTOSO"

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Escritura diferida de contraseñas**](active-directory-passwords-writeback.md): cómo funciona la escritura diferida de contraseñas con su directorio local.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR

