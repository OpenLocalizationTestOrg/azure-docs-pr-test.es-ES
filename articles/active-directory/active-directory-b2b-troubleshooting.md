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
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="af219-103">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af219-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="af219-104">Estos son algunos de los recursos para solucionar problemas comunes relacionados con la colaboración B2B de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af219-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="af219-105">Ha agregado un usuario externo pero no los ve en mi libreta de direcciones Global o en el selector de personas de Hola</span><span class="sxs-lookup"><span data-stu-id="af219-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="af219-106">En casos donde los usuarios externos no se rellenan en la lista de hello, objeto de hello podría tardar tooreplicate unos minutos.</span><span class="sxs-lookup"><span data-stu-id="af219-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="af219-107">Un usuario invitado de B2B no aparece en el selector de personas de SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="af219-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="af219-108">Hola toosearch de capacidad de los usuarios existentes de invitado en el selector de personas de SharePoint Online (SPO) hello es OFF por comportamiento heredado de toomatch de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="af219-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="af219-109">Puede habilitar esta característica mediante Hola establecer nivel 'ShowPeoplePickerSuggestionsForGuestUsers' en hello inquilino y colección de sitios.</span><span class="sxs-lookup"><span data-stu-id="af219-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="af219-110">Puede establecer con hello conjunto SPOTenant y SPOSite del conjunto de cmdlets, que permite a los miembros de función de hello toosearch todos los usuarios invitados existente en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="af219-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="af219-111">Cambios en el ámbito del inquilino de hello no afectan a los sitios SPO ya aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="af219-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="af219-112">Las invitaciones se han deshabilitado para el directorio</span><span class="sxs-lookup"><span data-stu-id="af219-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="af219-113">Si se le notifica que no tienen permisos de los usuarios de tooinvite, compruebe que la cuenta de usuario está autorizado tooinvite usuarios externos en configuración de usuario:</span><span class="sxs-lookup"><span data-stu-id="af219-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="af219-114">Si ha modificado estos valores u Hola invitado Invitador rol tooa usuario asignado recientemente, puede haber un retraso de 15 a 60 minutos para que hello cambios surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="af219-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="af219-115">usuario de Hola que le invitó está recibiendo un error durante el canje</span><span class="sxs-lookup"><span data-stu-id="af219-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="af219-116">Estos son algunos de los errores comunes:</span><span class="sxs-lookup"><span data-stu-id="af219-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="af219-117">El administrador del invitado no permite que los usuarios de EmailVerified se creen en su inquilino</span><span class="sxs-lookup"><span data-stu-id="af219-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="af219-118">Cuando no exista invitar a usuarios cuya organización usa Azure Active Directory, pero donde Hola cuenta de usuario específica (por ejemplo, usuario de hello no existe en Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="af219-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="af219-119">Administrador de Hola de contoso.com puede tener una directiva en lugar de evitar que los usuarios que se está creando.</span><span class="sxs-lookup"><span data-stu-id="af219-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="af219-120">usuario de Hello debe comprobar con su administrador toodetermine si se permiten que los usuarios externos.</span><span class="sxs-lookup"><span data-stu-id="af219-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="af219-121">Hello del usuario externo que tenga tooallow comprobar el correo electrónico a los usuarios en su dominio (verlo [artículo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) en permitir a los usuarios comprobar de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="af219-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="af219-122">El usuario externo no se encuentra ya en un dominio federado</span><span class="sxs-lookup"><span data-stu-id="af219-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="af219-123">Si está usando la autenticación de federación y usuario de hello no existe ya en Azure Active Directory, no se puede invitar usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="af219-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="af219-124">tooresolve este problema, hello administrador del usuario externo debe sincronizar tooAzure de cuenta de usuario de hello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="af219-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="af219-125">¿Cómo "\#", que habitualmente no es un carácter válido, se sincroniza con Azure AD?</span><span class="sxs-lookup"><span data-stu-id="af219-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="af219-126">"\#" es un carácter reservado en UPN para la colaboración B2B de Azure AD o los usuarios externos, porque la cuenta de invitado de hello user@contoso.com se convierte en user_contoso.com#EXT@fabrikam.onmicrosoft.com. Por lo tanto, \# en UPN procedentes de locales no se permiten toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="af219-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="af219-127">Recibe un error al agregar los usuarios externos tooa sincronizado grupo</span><span class="sxs-lookup"><span data-stu-id="af219-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="af219-128">Los usuarios externos pueden agregarse sólo demasiado "asignado" o grupos de "Seguridad" y no toogroups que se controlan en local.</span><span class="sxs-lookup"><span data-stu-id="af219-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="af219-129">El usuario externo no recibió una tooredeem de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="af219-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="af219-130">el invitado Hola debe comprobar con su ISP o se permite tooensure de filtro de spam que Hola la siguiente dirección:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="af219-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="af219-131">Tenga en cuenta que ese mensaje personalizado de hello no se incluye con mensajes de invitación a veces</span><span class="sxs-lookup"><span data-stu-id="af219-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="af219-132">toocomply con las leyes de privacidad, nuestras API no incluye mensajes personalizados de invitación de correo electrónico de hello cuando:</span><span class="sxs-lookup"><span data-stu-id="af219-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="af219-133">invitador Hello no tiene una dirección de correo electrónico en hello invitar a los inquilinos</span><span class="sxs-lookup"><span data-stu-id="af219-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="af219-134">Cuando una entidad de seguridad de servicio de aplicaciones envía la invitación de Hola</span><span class="sxs-lookup"><span data-stu-id="af219-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="af219-135">Si este escenario es tooyou importante, puede suprimir el correo electrónico de invitación de API y enviarlo a través del mecanismo de correo electrónico de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="af219-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="af219-136">Consulte toomake de abogados de su organización seguro de cualquier correo electrónico que envíe esta forma también se cumple con las leyes de privacidad.</span><span class="sxs-lookup"><span data-stu-id="af219-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af219-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af219-137">Next steps</span></span>

<span data-ttu-id="af219-138">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="af219-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="af219-139">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="af219-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="af219-140">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="af219-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="af219-141">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="af219-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="af219-142">elementos de saludo de correo electrónico de invitación de colaboración B2B de hello</span><span class="sxs-lookup"><span data-stu-id="af219-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="af219-143">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="af219-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="af219-144">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="af219-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="af219-145">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="af219-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="af219-146">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af219-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="af219-147">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="af219-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="af219-148">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="af219-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="af219-149">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af219-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
