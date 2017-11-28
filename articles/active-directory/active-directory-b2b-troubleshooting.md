---
title: "Solución de problemas de colaboración B2B de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="6ecee-103">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ecee-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="6ecee-104">Estos son algunos de los recursos para solucionar problemas comunes relacionados con la colaboración B2B de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ecee-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="6ecee-105">He agregado un usuario externo, pero no lo veo en mi libreta de direcciones global o en el selector de personas</span><span class="sxs-lookup"><span data-stu-id="6ecee-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="6ecee-106">En los casos donde los usuarios externos no se rellenan en la lista, el objeto puede tardar unos minutos en replicarse.</span><span class="sxs-lookup"><span data-stu-id="6ecee-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="6ecee-107">Un usuario invitado de B2B no aparece en el selector de personas de SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="6ecee-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="6ecee-108">La posibilidad de buscar usuarios invitados existentes en el selector de personas de SharePoint Online (SPO) está desactivada de manera predeterminada para así coincidir con el comportamiento heredado.</span><span class="sxs-lookup"><span data-stu-id="6ecee-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="6ecee-109">Para habilitarla, use la configuración "ShowPeoplePickerSuggestionsForGuestUsers" en el nivel de inquilino y colección de sitios.</span><span class="sxs-lookup"><span data-stu-id="6ecee-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="6ecee-110">Para configurarla, use los cmdlets Set-SPOTenant y Set-SPOSite, que permiten que los miembros busquen a todos los usuarios invitados existentes en el directorio.</span><span class="sxs-lookup"><span data-stu-id="6ecee-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="6ecee-111">Los cambios en el ámbito del inquilino no afectan los sitios de SPO que ya se aprovisionaron.</span><span class="sxs-lookup"><span data-stu-id="6ecee-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="6ecee-112">Las invitaciones se han deshabilitado para el directorio</span><span class="sxs-lookup"><span data-stu-id="6ecee-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="6ecee-113">Si recibe una notificación de que no tiene permisos para invitar a usuarios, vaya a User Settings (Configuración de usuario) y compruebe que la cuenta de usuario está autorizada para invitar a usuarios externos.</span><span class="sxs-lookup"><span data-stu-id="6ecee-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="6ecee-114">Si hace poco ha modificado estos valores o asignado el rol de invitador invitado a un usuario, podría haber un retraso de 15 a 60 minutos para que los cambios surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="6ecee-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="6ecee-115">El usuario al que he invitado está recibiendo un error durante el canje</span><span class="sxs-lookup"><span data-stu-id="6ecee-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="6ecee-116">Estos son algunos de los errores comunes:</span><span class="sxs-lookup"><span data-stu-id="6ecee-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="6ecee-117">El administrador del invitado no permite que los usuarios de EmailVerified se creen en su inquilino</span><span class="sxs-lookup"><span data-stu-id="6ecee-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="6ecee-118">Cuando se invita a usuarios cuya organización usa Azure Active Directory, pero donde no existe la cuenta de usuario en concreto (por ejemplo, el usuario no existe en Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="6ecee-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="6ecee-119">El administrador de contoso.com puede tener una directiva en lugar de evitar que se creen usuarios.</span><span class="sxs-lookup"><span data-stu-id="6ecee-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="6ecee-120">El usuario debe consultar al administrador y determinar si se permiten los usuarios externos.</span><span class="sxs-lookup"><span data-stu-id="6ecee-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="6ecee-121">Es posible que el administrador del usuario externo necesite permitir usuarios comprobados por correo electrónico en el dominio (consulte este [artículo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) sobre cómo permitir usuarios comprobados por correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="6ecee-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="6ecee-122">El usuario externo no se encuentra ya en un dominio federado</span><span class="sxs-lookup"><span data-stu-id="6ecee-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="6ecee-123">Si va a usar la autenticación de federación y el usuario no existe en Azure Active Directory, no se puede invitar al usuario.</span><span class="sxs-lookup"><span data-stu-id="6ecee-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="6ecee-124">Para resolver este problema, el administrador del usuario externo debe sincronizar la cuenta del usuario con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6ecee-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="6ecee-125">¿Cómo "\#", que habitualmente no es un carácter válido, se sincroniza con Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6ecee-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="6ecee-126">"\#" es un carácter reservado en los UPN para la colaboración B2B de Azure AD o los usuarios externos, porque la cuenta de invitado user@contoso.com se convierte en user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6ecee-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="6ecee-127">Por lo tanto, los UPN con \# que proceden del entorno local no tienen permiso para iniciar sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6ecee-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="6ecee-128">Recibo un error al agregar los usuarios externos a un grupo sincronizado</span><span class="sxs-lookup"><span data-stu-id="6ecee-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="6ecee-129">Los usuarios externos pueden agregarse únicamente a los grupos "Seguridad" o "Asignado", y no a aquellos que se controlan localmente.</span><span class="sxs-lookup"><span data-stu-id="6ecee-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="6ecee-130">Mi usuario externo no ha recibido un correo electrónico para realizar el canje</span><span class="sxs-lookup"><span data-stu-id="6ecee-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="6ecee-131">El invitado debe ponerse en contacto con su ISP o comprobar su filtro de correo no deseado para asegurarse de que se permite la siguiente dirección: Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6ecee-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="6ecee-132">Tenga en cuenta que, en ocasiones, el mensaje personalizado no se incluye en los mensajes de invitación</span><span class="sxs-lookup"><span data-stu-id="6ecee-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="6ecee-133">Para cumplir con las leyes de privacidad, nuestras API no incluye mensajes personalizados en la invitación por correo electrónico cuando:</span><span class="sxs-lookup"><span data-stu-id="6ecee-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="6ecee-134">El invitador no tiene una dirección de correo electrónico en el inquilino que invita.</span><span class="sxs-lookup"><span data-stu-id="6ecee-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="6ecee-135">Cuando una entidad de seguridad de App Service envía la invitación</span><span class="sxs-lookup"><span data-stu-id="6ecee-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="6ecee-136">Si este escenario es importante para usted, puede suprimir nuestro correo electrónico de invitación de API y enviarlo a través del mecanismo de correo electrónico de su elección.</span><span class="sxs-lookup"><span data-stu-id="6ecee-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="6ecee-137">Consulte al asesor legal de su organización para asegurarse de que cualquier correo electrónico que envíe de esta forma también cumple las leyes de privacidad.</span><span class="sxs-lookup"><span data-stu-id="6ecee-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ecee-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ecee-138">Next steps</span></span>

<span data-ttu-id="6ecee-139">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6ecee-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6ecee-140">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6ecee-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6ecee-141">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="6ecee-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="6ecee-142">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="6ecee-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="6ecee-143">Los elementos del correo electrónico de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6ecee-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="6ecee-144">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6ecee-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="6ecee-145">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ecee-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="6ecee-146">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="6ecee-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="6ecee-147">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ecee-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="6ecee-148">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6ecee-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="6ecee-149">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="6ecee-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="6ecee-150">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ecee-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
