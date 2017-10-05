---
title: "Azure Active Directory B2C: descripción de directivas personalizadas del paquete de inicio | Microsoft Docs"
description: Un tema acerca de las directivas personalizadas de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="9e432-103">Descripción de las directivas personalizadas del paquete del inicio de directivas personalizadas de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="9e432-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="9e432-104">En esta sección se enumeran todos los elementos básicos de la directiva B2C_1A_base que se incluyen con el **paquete de inicio** y que se aprovechan para la creación de sus propias directivas mediante la herencia de la *directiva B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9e432-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="9e432-105">Como tal, se centra particularmente en los tipos de notificaciones, las transformaciones de notificación, las definiciones de contenido, los proveedores de notificaciones con sus perfiles técnicos y los recorridos de usuario principales ya definidos.</span><span class="sxs-lookup"><span data-stu-id="9e432-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e432-106">Microsoft no otorga ninguna garantía, expresa ni implícita, con respecto a la información proporcionada a continuación.</span><span class="sxs-lookup"><span data-stu-id="9e432-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="9e432-107">En cualquier momento se pueden introducir cambios, antes de la hora de disponibilidad general, en ese mismo momento o después.</span><span class="sxs-lookup"><span data-stu-id="9e432-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="9e432-108">Sus propias directivas y la directiva B2C_1A_base_extensions pueden invalidar estas definiciones y extender esta directiva principal proporcionando unas nuevas, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9e432-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="9e432-109">Los elementos básicos de la directiva *B2C_1A_base* son tipos de notificaciones, transformaciones de notificación y definiciones de contenido.</span><span class="sxs-lookup"><span data-stu-id="9e432-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="9e432-110">Se puede hacer referencia a estos elementos en sus propias directivas o en la *directiva B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9e432-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="9e432-111">Esquemas de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9e432-111">Claims schemas</span></span>

<span data-ttu-id="9e432-112">Estos esquemas de notificaciones se dividen en tres secciones:</span><span class="sxs-lookup"><span data-stu-id="9e432-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="9e432-113">La primera sección que muestra las notificaciones mínimas necesarias para que los recorridos de usuario funcionen correctamente.</span><span class="sxs-lookup"><span data-stu-id="9e432-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="9e432-114">Una segunda sección que muestra las notificaciones necesarias para que los parámetros de cadena de consulta y otros parámetros especiales se pasen a otros proveedores de notificaciones, en especial login.microsoftonline.com para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9e432-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="9e432-115">**No modifique estas notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e432-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="9e432-116">Y, finalmente, una tercera sección que muestra las notificaciones adicionales opcionales que pueden recopilarse del usuario, almacenarse en el directorio y enviarse en tokens durante el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9e432-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="9e432-117">En esta sección se pueden agregar los nuevos tipos de notificaciones que se recopilan del usuario o se envían en el token.</span><span class="sxs-lookup"><span data-stu-id="9e432-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e432-118">El esquema de notificaciones contiene restricciones sobre ciertas notificaciones, como contraseñas y nombres de usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="9e432-119">La directiva del marco de confianza (TF) trata a Azure AD como cualquier otro proveedor de notificaciones y todas sus restricciones se modelan en la directiva premium.</span><span class="sxs-lookup"><span data-stu-id="9e432-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="9e432-120">Una directiva se podría modificar para agregar más restricciones o usar otro proveedor de notificaciones para el almacenamiento de credenciales que tenga sus propias restricciones.</span><span class="sxs-lookup"><span data-stu-id="9e432-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="9e432-121">A continuación se enumeran los tipos de notificaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9e432-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="9e432-122">Notificaciones que son necesarias para los recorridos de usuario</span><span class="sxs-lookup"><span data-stu-id="9e432-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="9e432-123">Las siguientes notificaciones son necesarias para que los recorridos de usuario funcionen correctamente:</span><span class="sxs-lookup"><span data-stu-id="9e432-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="9e432-124">Tipo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9e432-124">Claims type</span></span> | <span data-ttu-id="9e432-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="9e432-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="9e432-126">*UserId*</span></span> | <span data-ttu-id="9e432-127">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="9e432-127">Username</span></span> |
| <span data-ttu-id="9e432-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="9e432-128">*signInName*</span></span> | <span data-ttu-id="9e432-129">Nombre de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="9e432-129">Sign in name</span></span> |
| <span data-ttu-id="9e432-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="9e432-130">*tenantId*</span></span> | <span data-ttu-id="9e432-131">Identificador de objeto (id.) del objeto de usuario en Azure AD B2C Premium.</span><span class="sxs-lookup"><span data-stu-id="9e432-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9e432-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="9e432-132">*objectId*</span></span> | <span data-ttu-id="9e432-133">Identificador de objeto (id.) del objeto de usuario en Azure AD B2C Premium.</span><span class="sxs-lookup"><span data-stu-id="9e432-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9e432-134">*password*</span><span class="sxs-lookup"><span data-stu-id="9e432-134">*password*</span></span> | <span data-ttu-id="9e432-135">Password</span><span class="sxs-lookup"><span data-stu-id="9e432-135">Password</span></span> |
| <span data-ttu-id="9e432-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="9e432-136">*newPassword*</span></span> | |
| <span data-ttu-id="9e432-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="9e432-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="9e432-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="9e432-138">*passwordPolicies*</span></span> | <span data-ttu-id="9e432-139">Directivas de contraseña usadas por Azure AD B2C Premium para determinar la seguridad de la contraseña, su caducidad, etc.</span><span class="sxs-lookup"><span data-stu-id="9e432-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="9e432-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="9e432-140">*sub*</span></span> | |
| <span data-ttu-id="9e432-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9e432-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="9e432-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="9e432-142">*identityProvider*</span></span> | |
| <span data-ttu-id="9e432-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="9e432-143">*displayName*</span></span> | |
| <span data-ttu-id="9e432-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="9e432-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="9e432-145">Número de teléfono del usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-145">User's telephone number</span></span> |
| <span data-ttu-id="9e432-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="9e432-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="9e432-147">*email*</span><span class="sxs-lookup"><span data-stu-id="9e432-147">*email*</span></span> | <span data-ttu-id="9e432-148">Dirección de correo electrónico que puede usarse para ponerse en contacto con el usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="9e432-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="9e432-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="9e432-150">Dirección de correo electrónico que el usuario puede usar para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="9e432-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="9e432-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="9e432-151">*otherMails*</span></span> | <span data-ttu-id="9e432-152">Direcciones de correo electrónico que pueden usarse para ponerse en contacto con el usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="9e432-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="9e432-153">*userPrincipalName*</span></span> | <span data-ttu-id="9e432-154">Nombre de usuario tal como se almacena en Azure AD B2C Premium.</span><span class="sxs-lookup"><span data-stu-id="9e432-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9e432-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="9e432-155">*upnUserName*</span></span> | <span data-ttu-id="9e432-156">Nombre de usuario para la creación del nombre principal de usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="9e432-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="9e432-157">*mailNickName*</span></span> | <span data-ttu-id="9e432-158">Nombre de alias de correo electrónico del usuario tal como se almacena en Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="9e432-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9e432-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="9e432-159">*newUser*</span></span> | |
| <span data-ttu-id="9e432-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="9e432-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="9e432-161">Notificación que especifica si se recopilaron atributos del usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="9e432-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="9e432-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="9e432-163">Notificación que especifica si se recopiló un nuevo número de teléfono del usuario.</span><span class="sxs-lookup"><span data-stu-id="9e432-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="9e432-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="9e432-164">*authenticationSource*</span></span> | <span data-ttu-id="9e432-165">Especifica si el usuario se autenticó en el proveedor de identidades sociales, login.microsoftonline.com o en una cuenta local.</span><span class="sxs-lookup"><span data-stu-id="9e432-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="9e432-166">Notificaciones necesarias para los parámetros de cadena de consulta y otros parámetros especiales</span><span class="sxs-lookup"><span data-stu-id="9e432-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="9e432-167">Para pasar parámetros especiales (incluidos algunos parámetros de cadena de consulta), se requieren las siguientes notificaciones a otros proveedores de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="9e432-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="9e432-168">Tipo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9e432-168">Claims type</span></span> | <span data-ttu-id="9e432-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="9e432-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="9e432-170">*nux*</span></span> | <span data-ttu-id="9e432-171">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="9e432-172">*nca*</span></span> | <span data-ttu-id="9e432-173">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="9e432-174">*prompt*</span></span> | <span data-ttu-id="9e432-175">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="9e432-176">*mkt*</span></span> | <span data-ttu-id="9e432-177">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="9e432-178">*lc*</span></span> | <span data-ttu-id="9e432-179">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="9e432-180">*grant_type*</span></span> | <span data-ttu-id="9e432-181">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="9e432-182">*scope*</span></span> | <span data-ttu-id="9e432-183">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="9e432-184">*client_id*</span></span> | <span data-ttu-id="9e432-185">Parámetro especial pasado para la autenticación con la cuenta local en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9e432-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9e432-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="9e432-186">*objectIdFromSession*</span></span> | <span data-ttu-id="9e432-187">Parámetro proporcionado por el proveedor de administración de sesiones predeterminado para indicar que el identificador de objeto se ha recuperado de una sesión SSO.</span><span class="sxs-lookup"><span data-stu-id="9e432-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="9e432-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="9e432-188">*isActiveMFASession*</span></span> | <span data-ttu-id="9e432-189">Parámetro proporcionado por la administración de sesiones MFA para indicar que el usuario tiene una sesión activa de MFA.</span><span class="sxs-lookup"><span data-stu-id="9e432-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="9e432-190">Notificaciones (opcionales) adicionales que se pueden recopilar</span><span class="sxs-lookup"><span data-stu-id="9e432-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="9e432-191">Las siguientes notificaciones son notificaciones adicionales que pueden recopilarse de los usuarios, almacenarse en el directorio y enviarse en el token.</span><span class="sxs-lookup"><span data-stu-id="9e432-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="9e432-192">Tal y como se ha descrito anteriormente, se pueden agregar notificaciones adicionales a esta lista.</span><span class="sxs-lookup"><span data-stu-id="9e432-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="9e432-193">Tipo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9e432-193">Claims type</span></span> | <span data-ttu-id="9e432-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="9e432-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="9e432-195">*givenName*</span></span> | <span data-ttu-id="9e432-196">Nombre dado del usuario (también conocido como nombre de pila)</span><span class="sxs-lookup"><span data-stu-id="9e432-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="9e432-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="9e432-197">*surname*</span></span> | <span data-ttu-id="9e432-198">Apellido del usuario (también conocido como nombre de familia)</span><span class="sxs-lookup"><span data-stu-id="9e432-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="9e432-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="9e432-199">*Extension_picture*</span></span> | <span data-ttu-id="9e432-200">Foto del usuario de las redes sociales</span><span class="sxs-lookup"><span data-stu-id="9e432-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="9e432-201">Transformaciones de notificación</span><span class="sxs-lookup"><span data-stu-id="9e432-201">Claim transformations</span></span>

<span data-ttu-id="9e432-202">Las transformaciones de notificación disponibles se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="9e432-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="9e432-203">Transformación de notificación</span><span class="sxs-lookup"><span data-stu-id="9e432-203">Claim transformation</span></span> | <span data-ttu-id="9e432-204">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="9e432-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="9e432-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="9e432-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="9e432-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="9e432-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="9e432-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="9e432-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="9e432-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="9e432-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9e432-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="9e432-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9e432-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="9e432-211">Definiciones de contenido</span><span class="sxs-lookup"><span data-stu-id="9e432-211">Content definitions</span></span>

<span data-ttu-id="9e432-212">En esta sección se describen las definiciones de contenido ya declaradas en la directiva *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="9e432-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="9e432-213">Se puede hacer referencia a estas definiciones de contenido, se pueden anular o se pueden extender según sea necesario en sus propias directivas, así como en la directiva *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9e432-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="9e432-214">Proveedor de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9e432-214">Claims provider</span></span> | <span data-ttu-id="9e432-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="9e432-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="9e432-216">*Facebook*</span></span> | |
| <span data-ttu-id="9e432-217">*Inicio de sesión en una cuenta local*</span><span class="sxs-lookup"><span data-stu-id="9e432-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="9e432-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="9e432-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="9e432-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="9e432-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="9e432-220">*Autoafirmado*</span><span class="sxs-lookup"><span data-stu-id="9e432-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="9e432-221">*Cuenta local*</span><span class="sxs-lookup"><span data-stu-id="9e432-221">*Local Account*</span></span> | |
| <span data-ttu-id="9e432-222">*Administración de sesiones*</span><span class="sxs-lookup"><span data-stu-id="9e432-222">*Session Management*</span></span> | |
| <span data-ttu-id="9e432-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="9e432-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="9e432-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="9e432-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="9e432-225">*Emisor de tokens*</span><span class="sxs-lookup"><span data-stu-id="9e432-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="9e432-226">Perfiles técnicos</span><span class="sxs-lookup"><span data-stu-id="9e432-226">Technical profiles</span></span>

<span data-ttu-id="9e432-227">En esta sección se describen los perfiles técnicos ya declarados por el proveedor de notificaciones en la directiva *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="9e432-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="9e432-228">Se puede hacer referencia adicionalmente a estos perfiles técnicos, se pueden anular o se pueden extender según sea necesario en sus propias directivas, así como en la directiva *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9e432-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="9e432-229">Perfiles técnicos de Facebook</span><span class="sxs-lookup"><span data-stu-id="9e432-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="9e432-230">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-230">Technical profile</span></span> | <span data-ttu-id="9e432-231">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="9e432-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="9e432-233">Perfiles técnicos de inicio de sesión en una cuenta local</span><span class="sxs-lookup"><span data-stu-id="9e432-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="9e432-234">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-234">Technical profile</span></span> | <span data-ttu-id="9e432-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="9e432-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="9e432-237">Perfiles técnicos de Phone Factor</span><span class="sxs-lookup"><span data-stu-id="9e432-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="9e432-238">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-238">Technical profile</span></span> | <span data-ttu-id="9e432-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="9e432-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="9e432-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="9e432-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="9e432-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="9e432-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="9e432-243">Perfiles técnicos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e432-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="9e432-244">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-244">Technical profile</span></span> | <span data-ttu-id="9e432-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="9e432-246">*AAD-Common*</span></span> | <span data-ttu-id="9e432-247">Perfil técnico incluido por los otros perfiles técnicos de AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="9e432-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="9e432-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9e432-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="9e432-249">Perfil técnico de inicios de sesión sociales</span><span class="sxs-lookup"><span data-stu-id="9e432-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="9e432-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9e432-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="9e432-251">Perfil técnico de inicios de sesión sociales</span><span class="sxs-lookup"><span data-stu-id="9e432-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="9e432-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="9e432-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="9e432-253">Perfil técnico de inicios de sesión sociales</span><span class="sxs-lookup"><span data-stu-id="9e432-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="9e432-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="9e432-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="9e432-255">Perfil técnico de cuentas locales</span><span class="sxs-lookup"><span data-stu-id="9e432-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="9e432-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="9e432-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="9e432-257">Perfil técnico de cuentas locales</span><span class="sxs-lookup"><span data-stu-id="9e432-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="9e432-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9e432-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="9e432-259">Perfil técnico de actualización de registros de usuario mediante objectId</span><span class="sxs-lookup"><span data-stu-id="9e432-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="9e432-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9e432-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="9e432-261">Perfil técnico de actualización de registros de usuario mediante objectId</span><span class="sxs-lookup"><span data-stu-id="9e432-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="9e432-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9e432-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="9e432-263">Perfil técnico de actualización de registros de usuario mediante objectId</span><span class="sxs-lookup"><span data-stu-id="9e432-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="9e432-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9e432-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="9e432-265">Perfil técnico que se usa para leer datos después de que se autentica el usuario</span><span class="sxs-lookup"><span data-stu-id="9e432-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="9e432-266">Perfiles técnicos autoafirmados</span><span class="sxs-lookup"><span data-stu-id="9e432-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="9e432-267">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-267">Technical profile</span></span> | <span data-ttu-id="9e432-268">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="9e432-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="9e432-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="9e432-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="9e432-271">Perfiles técnicos de cuenta local</span><span class="sxs-lookup"><span data-stu-id="9e432-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="9e432-272">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-272">Technical profile</span></span> | <span data-ttu-id="9e432-273">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="9e432-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="9e432-275">Perfiles técnicos de administración de sesiones</span><span class="sxs-lookup"><span data-stu-id="9e432-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="9e432-276">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-276">Technical profile</span></span> | <span data-ttu-id="9e432-277">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="9e432-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="9e432-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="9e432-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="9e432-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="9e432-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="9e432-281">Nombre de perfil que se usa para eliminar la ambigüedad en una sesión de AAD entre el registro y el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9e432-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="9e432-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="9e432-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="9e432-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="9e432-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="9e432-284">Perfiles técnicos de Trustframework Policy Engine TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="9e432-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="9e432-285">Actualmente, no se ha definido ningún perfil técnico para el proveedor de notificaciones **Trustframework Policy Engine TechnicalProfiles**.</span><span class="sxs-lookup"><span data-stu-id="9e432-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="9e432-286">Perfiles técnicos del emisor de tokens</span><span class="sxs-lookup"><span data-stu-id="9e432-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="9e432-287">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="9e432-287">Technical profile</span></span> | <span data-ttu-id="9e432-288">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9e432-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="9e432-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="9e432-290">Recorridos de usuario</span><span class="sxs-lookup"><span data-stu-id="9e432-290">User journeys</span></span>

<span data-ttu-id="9e432-291">En esta sección se describen los recorridos de usuario ya declarados en la directiva *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="9e432-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="9e432-292">Se puede hacer referencia adicionalmente a estos recorridos de usuario, se pueden anular o se pueden extender según sea necesario en sus propias directivas, así como en la directiva *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9e432-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="9e432-293">Recorrido de usuario</span><span class="sxs-lookup"><span data-stu-id="9e432-293">User journey</span></span> | <span data-ttu-id="9e432-294">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e432-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="9e432-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="9e432-295">*SignUp*</span></span> | |
| <span data-ttu-id="9e432-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="9e432-296">*SignIn*</span></span> | |
| <span data-ttu-id="9e432-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="9e432-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="9e432-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="9e432-298">*EditProfile*</span></span> | |
| <span data-ttu-id="9e432-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="9e432-299">*PasswordReset*</span></span> | |
