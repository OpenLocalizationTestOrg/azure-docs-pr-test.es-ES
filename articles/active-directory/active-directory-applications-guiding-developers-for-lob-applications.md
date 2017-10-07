---
title: aaaDevelop aplicaciones para Azure AD | Documentos de Microsoft
description: "Escrito para profesionales de TI de hello, este artículo proporciona instrucciones para la integración de aplicaciones de Azure con Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Desarrollo de aplicaciones de línea de negocio para Azure Active Directory
Esta guía proporciona información general sobre el desarrollo de aplicaciones de línea de negocio (LoB) de Azure Active Directory (AD) .hello pensado destinatarios son los administradores globales de Active Directory/Office 365.

## <a name="overview"></a>Información general
La creación de aplicaciones integradas con Azure AD proporciona a los usuarios de la organización inicio de sesión único con Office 365. Tiene la aplicación hello en Azure AD le permite que controlar a través de la directiva de autenticación de hello para la aplicación hello. más información sobre el acceso condicional y cómo ver aplicaciones tooprotect con la autenticación multifactor (MFA) toolearn [configuración de las reglas de acceso](active-directory-conditional-access-azuread-connected-apps.md).

Registrar su toouse aplicación Azure Active Directory. Registrar la aplicación hello significa que los desarrolladores pueden usar usuarios de Azure AD tooauthenticate y solicitar acceso a los recursos de toouser como correo electrónico, calendario y documentos.

Cualquier miembro del directorio (no invitados) puede registrar una aplicación, conocido también como *crear un objeto de aplicación*.

Registrar una aplicación, permite cualquier siguiente de hello toodo de usuario:

* Obtener una identidad para su aplicación que Azure AD reconoce
* Obtener uno o más secretos o claves que Hola aplicación puede usar tooauthenticate propio tooAD
* Aplicación hello de marca en el portal de Azure con un nombre personalizado, logotipo, etcetera Hola.
* Aplicar la aplicación de tootheir de características de autorización de Azure AD, incluidos:

  * Control de acceso basado en rol (RBAC)
  * Azure Active Directory como servidor de autorización de oAuth (proteger una API expuesta por la aplicación hello)
* Declarar permisos necesarios necesarios para toofunction de aplicación Hola según lo esperado, incluidos:

      - Permisos de la aplicación (solo administradores globales). Por ejemplo: pertenencia a roles en otro Azure AD aplicación o rol pertenencia relativa tooan recursos de Azure, grupo de recursos, o suscripción
      - Permisos delegados (cualquier usuario) Por ejemplo: Azure AD, inicio de sesión y perfil de lectura

> [!NOTE]
> De forma predeterminada, cualquier miembro puede registrar una aplicación. toolearn toorestrict permisos para el registro de los miembros de toospecific de aplicaciones, vea [cómo las aplicaciones se agregan tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Aquí es lo que, administrador global de hello, necesitan toodo toohelp desarrolladores que su aplicación esté listo para producción:

* Configurar las reglas de acceso (directiva de acceso/MFA)
* Configurar asignación de usuario de hello aplicación toorequire y asignar usuarios
* Suprimir experiencia de consentimiento del usuario Hola predeterminado

## <a name="configure-access-rules"></a>Configuración de las reglas de acceso
Configurar aplicaciones de SaaS de tooyour de reglas de acceso según la aplicación. Por ejemplo, puede requerir MFA o sólo permitir acceso toousers en redes de confianza. detalles de Hola para este están disponibles en el documento de hello [configuración de las reglas de acceso](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Configurar asignación de usuario de hello aplicación toorequire y asignar usuarios
De forma predeterminada, los usuarios pueden acceder a las aplicaciones sin asignación previa. Sin embargo, si la aplicación hello expone funciones o si desea que tooappear de aplicación hello en el panel de acceso de un usuario, debe requieren la asignación de usuario.

[Necesidad de asignación de usuarios](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Si es un suscriptor de Azure AD Premium o Enterprise Mobility Suite (EMS), se recomienda encarecidamente utilizar grupos. Asignar grupos de aplicación de toohello permite a propietario del toohello management toodelegate un acceso continuo del grupo de Hola. Puede crear grupo de Hola o pida a entidad responsable de hello en el grupo de organización toocreate hello mediante la utilidad de administración de grupo.

[Asignación de usuarios tooan aplicación](active-directory-applications-guiding-developers-assigning-users.md)  
[Asignar grupos de aplicación de tooan](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Supresión del consentimiento del usuario
De forma predeterminada, cada usuario pasa por un toosign de experiencia de consentimiento en. experiencia de consentimiento de Hello, pidiendo a los usuarios permisos de toogrant tooan aplicación, puede ser desconcertante para los usuarios que no estén familiarizados con dichas decisiones.

Para aplicaciones de confianza, puede simplificar la experiencia del usuario Hola consentimiento toohello aplicación en nombre de su organización.

Para obtener más información sobre el consentimiento del usuario y consentimiento de hello experiencia en Azure, consulte [integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Artículos relacionados
* [Permitir que las aplicaciones de tooon local de acceso remoto seguro con el Proxy de aplicación de Azure AD](active-directory-application-proxy-get-started.md)
* [Acceso condicional de Azure en versión de vista previa para aplicaciones SaaS](active-directory-conditional-access-azuread-connected-apps.md)
* [Administrar acceso tooapps con Azure AD](active-directory-managing-access-to-apps.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
