---
title: "aaaTroubleshooting la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Recursos para solucionar problemas comunes con la colaboración B2B de Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Solución de problemas de colaboración B2B de Azure Active Directory

Estos son algunos de los recursos para solucionar problemas comunes relacionados con la colaboración B2B de Azure Active Directory (Azure AD).


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Ha agregado un usuario externo pero no los ve en mi libreta de direcciones Global o en el selector de personas de Hola

En casos donde los usuarios externos no se rellenan en la lista de hello, objeto de hello podría tardar tooreplicate unos minutos.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Un usuario invitado de B2B no aparece en el selector de personas de SharePoint Online/OneDrive 
 
Hola toosearch de capacidad de los usuarios existentes de invitado en el selector de personas de SharePoint Online (SPO) hello es OFF por comportamiento heredado de toomatch de forma predeterminada.

Puede habilitar esta característica mediante Hola establecer nivel 'ShowPeoplePickerSuggestionsForGuestUsers' en hello inquilino y colección de sitios. Puede establecer con hello conjunto SPOTenant y SPOSite del conjunto de cmdlets, que permite a los miembros de función de hello toosearch todos los usuarios invitados existente en el directorio de Hola. Cambios en el ámbito del inquilino de hello no afectan a los sitios SPO ya aprovisionados.

## <a name="invitations-have-been-disabled-for-directory"></a>Las invitaciones se han deshabilitado para el directorio

Si se le notifica que no tienen permisos de los usuarios de tooinvite, compruebe que la cuenta de usuario está autorizado tooinvite usuarios externos en configuración de usuario:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Si ha modificado estos valores u Hola invitado Invitador rol tooa usuario asignado recientemente, puede haber un retraso de 15 a 60 minutos para que hello cambios surtan efecto.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>usuario de Hola que le invitó está recibiendo un error durante el canje

Estos son algunos de los errores comunes:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>El administrador del invitado no permite que los usuarios de EmailVerified se creen en su inquilino

Cuando no exista invitar a usuarios cuya organización usa Azure Active Directory, pero donde Hola cuenta de usuario específica (por ejemplo, usuario de hello no existe en Azure AD contoso.com). Administrador de Hola de contoso.com puede tener una directiva en lugar de evitar que los usuarios que se está creando. usuario de Hello debe comprobar con su administrador toodetermine si se permiten que los usuarios externos. Hello del usuario externo que tenga tooallow comprobar el correo electrónico a los usuarios en su dominio (verlo [artículo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) en permitir a los usuarios comprobar de correo electrónico).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>El usuario externo no se encuentra ya en un dominio federado

Si está usando la autenticación de federación y usuario de hello no existe ya en Azure Active Directory, no se puede invitar usuario Hola.

tooresolve este problema, hello administrador del usuario externo debe sincronizar tooAzure de cuenta de usuario de hello Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>¿Cómo "\#", que habitualmente no es un carácter válido, se sincroniza con Azure AD?

"\#" es un carácter reservado en UPN para la colaboración B2B de Azure AD o los usuarios externos, porque la cuenta de invitado de hello user@contoso.com se convierte en user_contoso.com#EXT@fabrikam.onmicrosoft.com. Por lo tanto, \# en UPN procedentes de locales no se permiten toosign en toohello portal de Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Recibe un error al agregar los usuarios externos tooa sincronizado grupo

Los usuarios externos pueden agregarse sólo demasiado "asignado" o grupos de "Seguridad" y no toogroups que se controlan en local.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>El usuario externo no recibió una tooredeem de correo electrónico

el invitado Hola debe comprobar con su ISP o se permite tooensure de filtro de spam que Hola la siguiente dirección:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Tenga en cuenta que ese mensaje personalizado de hello no se incluye con mensajes de invitación a veces

toocomply con las leyes de privacidad, nuestras API no incluye mensajes personalizados de invitación de correo electrónico de hello cuando:

- invitador Hello no tiene una dirección de correo electrónico en hello invitar a los inquilinos
- Cuando una entidad de seguridad de servicio de aplicaciones envía la invitación de Hola

Si este escenario es tooyou importante, puede suprimir el correo electrónico de invitación de API y enviarlo a través del mecanismo de correo electrónico de Hola de su elección. Consulte toomake de abogados de su organización seguro de cualquier correo electrónico que envíe esta forma también se cumple con las leyes de privacidad.

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saludo de correo electrónico de invitación de colaboración B2B de hello](active-directory-b2b-invitation-email.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Concesión de licencias de colaboración B2B de Azure AD](active-directory-b2b-licensing.md)
* [Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)](active-directory-b2b-faq.md)
* [Personalización y API de colaboración B2B de Azure Active Directory](active-directory-b2b-api.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
