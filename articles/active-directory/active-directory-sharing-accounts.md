---
title: las cuentas de aaaSharing con Azure AD | Documentos de Microsoft
description: "Describe cómo Azure Active Directory permite que las cuentas de recurso compartido de las organizaciones toosecurely para aplicaciones locales y los servicios de nube de consumidor."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Uso compartido de cuentas con Azure AD
## <a name="overview"></a>Información general
A veces, las organizaciones necesitan toouse un nombre de usuario único y una contraseña para varias personas. Esto suele ocurrir en dos casos:

* Al acceder a aplicaciones que requieren un inicio de sesión único y una contraseña para cada usuario, ya sean aplicaciones locales o servicios en la nube de consumidor (por ejemplo, cuentas de medios sociales corporativos).
* Al crear entornos multiusuario. Puede tener una sola cuenta local que tiene privilegios elevados y puede ser usado toodo actividades básicas (p. ej. Hola "global" cuenta de administrador local para Office 365 o hello cuenta raíz en Salesforce) de configuración, la administración y la recuperación.

Tradicionalmente, estas cuentas se pueden compartir por distribuir a Hola credenciales (nombre de usuario/contraseña) toohello individuos o almacenarlas en una ubicación compartida donde varios confianza agentes pueden tener acceso a ellos.

modelo de uso compartido tradicional de Hello tiene varias desventajas:

* Permitir que las aplicaciones de toonew acceso requiere toodistribute credenciales tooeveryone que necesite tener acceso.
* Cada aplicación compartida puede requerir su propio conjunto único de credenciales compartidas, que requieren los usuarios tooremember varios conjuntos de credenciales. Cuando los usuarios tienen tooremember muchas de las credenciales, aumenta el riesgo de hello en el que volverá al estado toorisky prácticas. (por ejemplo, anotar las contraseñas).
* No puede determinar quién tiene acceso tooan aplicación.
* No se puede determinar quién *accedió* a una aplicación.
* Cuando necesite aplicación tooan de tooremove access, que tiene credenciales de Hola de tooupdate y volver a distribuirlos tooeveryone que necesita obtener acceso a la aplicación de toothat.

## <a name="azure-active-directory-account-sharing"></a>Uso compartido de cuentas de Azure Active Directory
Azure AD proporciona un nuevo enfoque cuentas toousing compartido que elimina estos inconvenientes.

Administrador de Azure AD Hola configura las aplicaciones que un usuario puede tener acceso mediante Hola Panel de acceso y elegir tipo de Hola de inicio de sesión único es adecuada para esa aplicación. Uno de esos tipos, *basada en contraseña de inicio de sesión único*, permite a Azure AD actuar como un tipo de "agente" durante Hola inicio de sesión en proceso para esa aplicación.

Los usuarios inician sesión una sola vez con sus cuentas profesionales. Se trata de hello misma cuenta que utilizan habitualmente tooaccess su escritorio o correo electrónico. Pueden detectar y acceder solo a aquellas aplicaciones que tienen asignadas. Con cuentas compartidas, esta lista de aplicaciones puede incluir cualquier número de credenciales compartidas. usuario final de Hello no necesita tooremember o anote Hola diferentes cuentas que porque podrían estar utilizando.

Las cuentas compartidas no solo aumentan la supervisión y mejoran la facilidad de uso, también optimizan la seguridad. Los usuarios con permisos toouse Hola credenciales no ven una contraseña compartida hello, pero en su lugar obtener contraseña para permisos toouse hello como parte de un flujo de autenticación de orquestaciones. Además, con algunas aplicaciones de SSO de contraseña, tendrá Hola opción toohave Azure AD periódicamente sustitución (actualización) Hola contraseña con contraseñas de grandes y complejas, aumenta la seguridad de la cuenta de hello. Administrador de Hello puede fácilmente conceder o revocar el acceso tooan aplicación y también saber quién tiene acceso toohello cuenta y quién accedió a él en hello anterior.

Azure AD admite las cuentas compartidas para cualquier usuario de Enterprise Mobility Suite (EMS), con licencia Premium o Básico, en todos los tipos de aplicaciones de inicio de sesión único con contraseña. Puede compartir las cuentas para cualquiera de los miles de aplicaciones previamente integradas en la Galería de aplicaciones de Hola y puede agregar su propia aplicación de autenticación de contraseña con [aplicaciones personalizadas de SSO](active-directory-sso-integrate-saas-apps.md).

Entre las características de Azure AD que permiten el uso compartido de las cuentas se incluyen las siguientes:

* [Inicio de sesión único con contraseña](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Agente de inicio de sesión único con contraseña
* [Asignación de grupos](active-directory-accessmanagement-self-service-group-management.md)
* Aplicaciones de contraseñas personalizadas
* [Panel/informes de uso de aplicaciones](active-directory-passwords-get-insights.md)
* Portales de acceso para usuarios finales
* [Proxy de aplicaciones](active-directory-application-proxy-get-started.md)
* [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Uso compartido de una cuenta
Azure AD toouse tooshare una cuenta debe:

* Agregar una aplicación de la [galería de aplicaciones](https://azure.microsoft.com/marketplace/active-directory/) o una [aplicación personalizada](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Configurar aplicación Hola para contraseña de inicio de sesión único (SSO)
* Use [asignación basada en el grupo](active-directory-accessmanagement-group-saasapps.md) y seleccione Hola opción tooenter una credencial compartida
* Opcional: en algunas aplicaciones, por ejemplo, Facebook, Twitter y LinkedIn, puede habilitar la opción de Hola para [Azure AD automatizada vuelco de contraseña](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

También puede hacer que su cuenta compartida más segura con la autenticación multifactor (MFA) (obtener más información acerca de [proteger las aplicaciones con Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) y se puede delegar hello toomanage de capacidad que tiene acceso a toohello aplicación mediante [Autoservicio de azure AD](active-directory-accessmanagement-self-service-group-management.md) administración de grupo.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Protección de aplicaciones con acceso condicional](active-directory-conditional-access.md)
* [Administración de grupos de autoservicio/SSAA](active-directory-accessmanagement-self-service-group-management.md)

