---
title: "aaaIntegrate inicio de sesión único en Azure Active Directory con aplicaciones de SaaS | Documentos de Microsoft"
description: "Habilite la autenticación de inicio de sesión único y la administración del acceso centralizado para el aprovisionamiento de usuarios de las aplicaciones SaaS en Azure Active Directory. Información general sobre cómo toointegrate Azure Active Directory tooSaaS aplicaciones."
services: active-directory
keywords: integrar Azure AD con aplicaciones SaaS
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Integración del inicio de sesión único de Azure Active Directory con aplicaciones SaaS
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-enterprise-apps-manage-sso.md)
> * [Portal de Azure clásico](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget iniciado la configuración de inicio de sesión único para una aplicación que utiliza en su organización, va a usar un directorio existente en Azure Active Directory (Azure AD). Puede usar un directorio de Azure AD que obtenga a través de Microsoft Azure, Office 365 o Windows Intune. Si tiene dos o más de estos, consulte [administrar su directorio Azure AD](active-directory-administer.md) toodetermine qué uno toouse.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo centrar tooassign roles de administrador en Azure AD Hola, administrador, consulte [asignar roles de administrador en Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Autenticación
Para las aplicaciones que admiten Hola SAML 2.0, WS-Federation, o protocolos de OpenID Connect, usa Azure Active Directory firma relaciones de confianza de certificados tooestablish. Para obtener más información, consulte [Administración de certificados para inicio de sesión único federado](active-directory-sso-certs.md).

Para las aplicaciones que admiten sólo HTML basada en formularios con inicio de sesión de, las relaciones de confianza de Azure Active Directory utiliza 'reasignación contraseña' tooestablish. Este Hola permite a los usuarios de su organización toobe inicia sesión automáticamente tooa aplicación de SaaS con Azure AD utilizando la información de cuenta de usuario de Hola de hello aplicación SaaS. Azure AD recopila y almacena de forma segura la información de cuenta de usuario de Hola y contraseña correspondiente de Hola. Para obtener más información, consulte [Inicio de sesión único con contraseña](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Autorización
Una cuenta aprovisionada habilita un toouse toobe autorizada de usuario una aplicación después de que han autenticado a través de un inicio de sesión único. Aprovisionamiento de usuarios puede realizarse manualmente o, en algunos casos, puede agregar y quitar la información de usuario de aplicación de SaaS hello según los cambios realizados en Active Directory de Azure. Para más información sobre el uso de conectores de Azure AD existentes para el aprovisionamiento automatizado, consulte [Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md).

En caso contrario, puede manualmente Agregar aplicación de tooan de información de usuario, o usar otras soluciones de aprovisionamiento que están disponibles en el mercado de Hola.

## <a name="access"></a>Access
Azure AD proporciona varias maneras de personalizables de aplicaciones que toodeploy tooend los usuarios de su organización. No se bloquea en cualquier implementación concreta o solución de acceso. Puede usar [Hola solución que mejor se adapte a sus necesidades](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Consideraciones adicionales para las aplicaciones ya en uso
Configurando el inicio de sesión único en con una aplicación que utiliza su organización ya es un proceso diferente del proceso de Hola de creación de nuevas cuentas para una nueva aplicación. Hay un par de pasos preliminares que se incluyen: la asignación de identidades de usuario de identidades de hello aplicaciones tooAzure AD y comprender cómo los usuarios experimentarán el registro de aplicación tooan después de que está integrado.

> [!NOTE]
> tooset de SSO para una aplicación existente, que necesita derechos de administrador global de toohave en ambos Azure AD y Hola aplicación SaaS.
>
>

### <a name="mapping-user-accounts"></a>Asignación de cuentas de usuario
Normalmente, la identidad de un usuario tiene un identificador único que podría ser una dirección de correo electrónico o un nombre principal de usuario (UPN). Necesitará toolink (map) cada aplicación identidad tootheir respectivo Azure AD identidad de usuario. Hay un par de maneras tooaccomplish esto dependiendo de cómo requisito hello de la autenticación de la aplicación.

Para obtener más información sobre la asignación de identidades de aplicaciones con identidades de Azure AD, consulte [personalizar las notificaciones emitidas en el token SAML de hello](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) y [Personalizar asignaciones de atributos para aprovisionamiento](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Descripción de registro del usuario de hello en experiencia
Cuando integra SSO para una aplicación que ya está en uso, es importante toorealize que Hola experiencia del usuario se verán afectada. Para todas las aplicaciones, los usuarios iniciará usando su toosign de credenciales de Azure AD en. También podría ser que se debe utilizar una aplicación de hello tooaccess portal diferente.

SSO para algunas aplicaciones puede realizarse en el inicio de sesión de la aplicación hello en la interfaz, pero para otras aplicaciones, Hola usuario tendrá toogo a través de un portal central como ([mis aplicaciones](http://myapps.microsoft.com) o [Office365](http://portal.office.com/myapps)) toosign en. Obtener más información sobre los diferentes tipos de Hola de SSO y sus experiencias de usuario en [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

Otro recurso útil es *suprimir el consentimiento del usuario* en hello [directrices a los desarrolladores](active-directory-applications-guiding-developers-for-lob-applications.md) artículo.

## <a name="next-steps"></a>Pasos siguientes
Para las aplicaciones SaaS que encuentre en hello Galería de aplicaciones, Azure AD proporciona un número de [tutoriales sobre cómo las aplicaciones de SaaS toointegrate](active-directory-saas-tutorial-list.md).

Si la aplicación no está en la Galería de aplicaciones, puede [agregar toohello Galería de aplicaciones de Azure AD como una aplicación personalizada](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Hay mucho más detalle en todos estos problemas en la biblioteca de Azure.com hello, comenzando con [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

Además, no se pierda hello [índice de artículos para la administración de la aplicación en Azure Active Directory](active-directory-apps-index.md).
