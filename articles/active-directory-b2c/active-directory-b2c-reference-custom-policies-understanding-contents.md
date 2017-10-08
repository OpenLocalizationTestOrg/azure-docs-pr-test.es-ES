---
title: "Azure B2C Directory Active: Descripción de las directivas personalizadas de módulo de inicio de Hola | Documentos de Microsoft"
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
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="a3341-103">Descripción de las directivas personalizadas de Hola de módulo de inicio de directiva personalizada de hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a3341-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="a3341-104">Esta sección enumeran todos los elementos básicos de Hola de directiva de hello B2C_1A_base que viene con hello **Starter Pack** y que se utiliza para crear sus propias directivas a través de la herencia de Hola de hello *B2C_1A_base_ Directiva de extensiones*.</span><span class="sxs-lookup"><span data-stu-id="a3341-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="a3341-105">Por lo tanto, lo más especialmente se centra en hello ya definido tipos, las transformaciones de notificaciones, las definiciones de contenido, proveedores de notificaciones con sus perfiles técnicas de notificación y Hola viajes de usuario principal.</span><span class="sxs-lookup"><span data-stu-id="a3341-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3341-106">Microsoft no otorga ninguna garantía, expresa ni implícita, con respecto toohello información proporciona ahora en adelante.</span><span class="sxs-lookup"><span data-stu-id="a3341-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="a3341-107">En cualquier momento se pueden introducir cambios, antes de la hora de disponibilidad general, en ese mismo momento o después.</span><span class="sxs-lookup"><span data-stu-id="a3341-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="a3341-108">Tanto sus propias directivas hello y B2C_1A_base_extensions directiva pueden invalidar estas definiciones y extender esta directiva principal proporcionando perfiles adicionales según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a3341-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="a3341-109">Hola elementos básicos de hello *B2C_1A_base directiva* son tipos de notificación, las transformaciones de notificaciones y las definiciones de contenido.</span><span class="sxs-lookup"><span data-stu-id="a3341-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="a3341-110">Estos elementos pueden toobe susceptible al que hace referencia en sus propias directivas así como en hello *B2C_1A_base_extensions directiva*.</span><span class="sxs-lookup"><span data-stu-id="a3341-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="a3341-111">Esquemas de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a3341-111">Claims schemas</span></span>

<span data-ttu-id="a3341-112">Estos esquemas de notificaciones se dividen en tres secciones:</span><span class="sxs-lookup"><span data-stu-id="a3341-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="a3341-113">Primera sección que enumera las notificaciones mínimo de Hola que son necesarios para hello usuario viajes toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="a3341-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="a3341-114">Una segunda sección que listas Hola notificaciones necesarias para los parámetros de cadena de consulta y otro parámetros especiales toobe pasa tooother proveedores de notificaciones, especialmente login.microsoftonline.com para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a3341-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="a3341-115">**No modifique estas notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="a3341-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="a3341-116">Y finalmente, una tercera sección que enumera las notificaciones adicionales y opcionales que se pueden recopilar de usuario de hello, almacenados en el directorio de Hola y envían en símbolos (tokens) durante el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a3341-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="a3341-117">Pueden agregarse nuevas notificaciones tipo toobe recopilados del usuario de Hola o enviados en el token de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="a3341-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3341-118">esquema de notificaciones de Hello contiene restricciones en ciertas notificaciones, como contraseñas y nombres de usuario.</span><span class="sxs-lookup"><span data-stu-id="a3341-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="a3341-119">Hola directiva de confianza Framework (TF) trata Azure AD como cualquier otro proveedor de notificaciones y todas sus restricciones se reproduzcan en la directiva de hello premium.</span><span class="sxs-lookup"><span data-stu-id="a3341-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="a3341-120">Una directiva podría ser modificado tooadd más restricciones o utilizar otro proveedor de notificaciones para el almacenamiento de credenciales que tendrá sus propias restricciones.</span><span class="sxs-lookup"><span data-stu-id="a3341-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="a3341-121">tipos de notificación disponibles Hola se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="a3341-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="a3341-122">Notificaciones que son necesarios para los viajes de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="a3341-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="a3341-123">Hola siguientes notificaciones se necesitan para usuario viajes toowork correctamente:</span><span class="sxs-lookup"><span data-stu-id="a3341-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="a3341-124">Tipo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a3341-124">Claims type</span></span> | <span data-ttu-id="a3341-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="a3341-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="a3341-126">*UserId*</span></span> | <span data-ttu-id="a3341-127">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="a3341-127">Username</span></span> |
| <span data-ttu-id="a3341-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="a3341-128">*signInName*</span></span> | <span data-ttu-id="a3341-129">Nombre de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a3341-129">Sign in name</span></span> |
| <span data-ttu-id="a3341-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="a3341-130">*tenantId*</span></span> | <span data-ttu-id="a3341-131">Identificador del inquilino (Id.) del objeto de usuario de hello en Premium de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a3341-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3341-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="a3341-132">*objectId*</span></span> | <span data-ttu-id="a3341-133">Identificador de objeto (Id.) del objeto de usuario de hello en Premium de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a3341-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3341-134">*password*</span><span class="sxs-lookup"><span data-stu-id="a3341-134">*password*</span></span> | <span data-ttu-id="a3341-135">Password</span><span class="sxs-lookup"><span data-stu-id="a3341-135">Password</span></span> |
| <span data-ttu-id="a3341-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="a3341-136">*newPassword*</span></span> | |
| <span data-ttu-id="a3341-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="a3341-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="a3341-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="a3341-138">*passwordPolicies*</span></span> | <span data-ttu-id="a3341-139">Directivas de contraseña que se usa seguridad de la contraseña de Azure AD B2C Premium toodetermine, expiración, etcetera.</span><span class="sxs-lookup"><span data-stu-id="a3341-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="a3341-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="a3341-140">*sub*</span></span> | |
| <span data-ttu-id="a3341-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3341-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="a3341-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="a3341-142">*identityProvider*</span></span> | |
| <span data-ttu-id="a3341-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="a3341-143">*displayName*</span></span> | |
| <span data-ttu-id="a3341-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="a3341-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="a3341-145">Número de teléfono del usuario.</span><span class="sxs-lookup"><span data-stu-id="a3341-145">User's telephone number</span></span> |
| <span data-ttu-id="a3341-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="a3341-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="a3341-147">*email*</span><span class="sxs-lookup"><span data-stu-id="a3341-147">*email*</span></span> | <span data-ttu-id="a3341-148">Dirección de correo electrónico que puede ser usado toocontact Hola usuario</span><span class="sxs-lookup"><span data-stu-id="a3341-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="a3341-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="a3341-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="a3341-150">Dirección de correo electrónico Hola usuario puede usar toosign en</span><span class="sxs-lookup"><span data-stu-id="a3341-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="a3341-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="a3341-151">*otherMails*</span></span> | <span data-ttu-id="a3341-152">Direcciones de correo electrónico que pueden ser usado toocontact Hola usuario</span><span class="sxs-lookup"><span data-stu-id="a3341-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="a3341-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="a3341-153">*userPrincipalName*</span></span> | <span data-ttu-id="a3341-154">Nombre de usuario tal como se almacena en hello Premium de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a3341-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3341-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="a3341-155">*upnUserName*</span></span> | <span data-ttu-id="a3341-156">Nombre de usuario para la creación del nombre principal de usuario.</span><span class="sxs-lookup"><span data-stu-id="a3341-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="a3341-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="a3341-157">*mailNickName*</span></span> | <span data-ttu-id="a3341-158">Nombre de nick de correo electrónico del usuario tal como se almacena en hello Premium de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a3341-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3341-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="a3341-159">*newUser*</span></span> | |
| <span data-ttu-id="a3341-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="a3341-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="a3341-161">Notificación que especifica si se recopilaron atributos de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="a3341-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="a3341-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="a3341-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="a3341-163">Notificación que especifica si se ha recopilado un nuevo número de teléfono de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="a3341-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="a3341-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="a3341-164">*authenticationSource*</span></span> | <span data-ttu-id="a3341-165">Especifica si se autenticó el usuario de hello en el proveedor de identidades sociales, login.microsoftonline.com o cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="a3341-166">Notificaciones necesarias para los parámetros de cadena de consulta y otros parámetros especiales</span><span class="sxs-lookup"><span data-stu-id="a3341-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="a3341-167">Hello notificaciones siguientes son necesarios toopass en proveedores de notificaciones de tooother parámetros especiales (incluidos algunos parámetros de cadena de consulta):</span><span class="sxs-lookup"><span data-stu-id="a3341-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="a3341-168">Tipo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a3341-168">Claims type</span></span> | <span data-ttu-id="a3341-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="a3341-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="a3341-170">*nux*</span></span> | <span data-ttu-id="a3341-171">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="a3341-172">*nca*</span></span> | <span data-ttu-id="a3341-173">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="a3341-174">*prompt*</span></span> | <span data-ttu-id="a3341-175">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="a3341-176">*mkt*</span></span> | <span data-ttu-id="a3341-177">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="a3341-178">*lc*</span></span> | <span data-ttu-id="a3341-179">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="a3341-180">*grant_type*</span></span> | <span data-ttu-id="a3341-181">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="a3341-182">*scope*</span></span> | <span data-ttu-id="a3341-183">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="a3341-184">*client_id*</span></span> | <span data-ttu-id="a3341-185">Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3341-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="a3341-186">*objectIdFromSession*</span></span> | <span data-ttu-id="a3341-187">Parámetro proporcionado por hello predeterminado sesión administración proveedor tooindicate que Hola Id. de objeto se ha recuperado de una sesión SSO</span><span class="sxs-lookup"><span data-stu-id="a3341-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="a3341-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="a3341-188">*isActiveMFASession*</span></span> | <span data-ttu-id="a3341-189">Parámetro proporcionada por hello MFA sesión administración tooindicate que Hola el usuario tiene una sesión activa de MFA</span><span class="sxs-lookup"><span data-stu-id="a3341-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="a3341-190">Notificaciones (opcionales) adicionales que se pueden recopilar</span><span class="sxs-lookup"><span data-stu-id="a3341-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="a3341-191">siguiente Hola notificaciones son notificaciones adicionales que se pueden recopilar de los usuarios de hello, almacenados en el directorio de Hola y enviados en el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3341-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="a3341-192">Tal y como se ha descrito antes, se pueden agregar notificaciones adicionales toothis lista.</span><span class="sxs-lookup"><span data-stu-id="a3341-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="a3341-193">Tipo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a3341-193">Claims type</span></span> | <span data-ttu-id="a3341-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="a3341-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="a3341-195">*givenName*</span></span> | <span data-ttu-id="a3341-196">Nombre dado del usuario (también conocido como nombre de pila)</span><span class="sxs-lookup"><span data-stu-id="a3341-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="a3341-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="a3341-197">*surname*</span></span> | <span data-ttu-id="a3341-198">Apellido del usuario (también conocido como nombre de familia)</span><span class="sxs-lookup"><span data-stu-id="a3341-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="a3341-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="a3341-199">*Extension_picture*</span></span> | <span data-ttu-id="a3341-200">Foto del usuario de las redes sociales</span><span class="sxs-lookup"><span data-stu-id="a3341-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="a3341-201">Transformaciones de notificación</span><span class="sxs-lookup"><span data-stu-id="a3341-201">Claim transformations</span></span>

<span data-ttu-id="a3341-202">transformaciones de notificación disponibles Hola se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="a3341-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="a3341-203">Transformación de notificación</span><span class="sxs-lookup"><span data-stu-id="a3341-203">Claim transformation</span></span> | <span data-ttu-id="a3341-204">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="a3341-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="a3341-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="a3341-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="a3341-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="a3341-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="a3341-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="a3341-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="a3341-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="a3341-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3341-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="a3341-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3341-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="a3341-211">Definiciones de contenido</span><span class="sxs-lookup"><span data-stu-id="a3341-211">Content definitions</span></span>

<span data-ttu-id="a3341-212">En esta sección se describe las definiciones de contenido de hello ya declaradas en hello *B2C_1A_base* directiva.</span><span class="sxs-lookup"><span data-stu-id="a3341-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="a3341-213">Estas definiciones de contenido son susceptibles de sufrir toobe al que hace referencia, se reemplaza o extender según sea necesario en sus propias directivas así como en hello *B2C_1A_base_extensions* directiva.</span><span class="sxs-lookup"><span data-stu-id="a3341-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="a3341-214">Proveedor de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a3341-214">Claims provider</span></span> | <span data-ttu-id="a3341-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="a3341-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="a3341-216">*Facebook*</span></span> | |
| <span data-ttu-id="a3341-217">*Inicio de sesión en una cuenta local*</span><span class="sxs-lookup"><span data-stu-id="a3341-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="a3341-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="a3341-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="a3341-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="a3341-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="a3341-220">*Autoafirmado*</span><span class="sxs-lookup"><span data-stu-id="a3341-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="a3341-221">*Cuenta local*</span><span class="sxs-lookup"><span data-stu-id="a3341-221">*Local Account*</span></span> | |
| <span data-ttu-id="a3341-222">*Administración de sesiones*</span><span class="sxs-lookup"><span data-stu-id="a3341-222">*Session Management*</span></span> | |
| <span data-ttu-id="a3341-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="a3341-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="a3341-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="a3341-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="a3341-225">*Emisor de tokens*</span><span class="sxs-lookup"><span data-stu-id="a3341-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="a3341-226">Perfiles técnicos</span><span class="sxs-lookup"><span data-stu-id="a3341-226">Technical profiles</span></span>

<span data-ttu-id="a3341-227">En esta sección se describe perfiles técnica Hola ya declarados por el proveedor de notificaciones en hello *B2C_1A_base* directiva.</span><span class="sxs-lookup"><span data-stu-id="a3341-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="a3341-228">Estos perfiles técnicos son susceptibles de sufrir toobe más al que hace referencia, se reemplaza o extender según sea necesario en sus propias directivas así como en hello *B2C_1A_base_extensions* directiva.</span><span class="sxs-lookup"><span data-stu-id="a3341-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="a3341-229">Perfiles técnicos de Facebook</span><span class="sxs-lookup"><span data-stu-id="a3341-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="a3341-230">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-230">Technical profile</span></span> | <span data-ttu-id="a3341-231">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="a3341-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="a3341-233">Perfiles técnicos de inicio de sesión en una cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="a3341-234">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-234">Technical profile</span></span> | <span data-ttu-id="a3341-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="a3341-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="a3341-237">Perfiles técnicos de Phone Factor</span><span class="sxs-lookup"><span data-stu-id="a3341-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="a3341-238">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-238">Technical profile</span></span> | <span data-ttu-id="a3341-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="a3341-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="a3341-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="a3341-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="a3341-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="a3341-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="a3341-243">Perfiles técnicos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3341-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="a3341-244">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-244">Technical profile</span></span> | <span data-ttu-id="a3341-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="a3341-246">*AAD-Common*</span></span> | <span data-ttu-id="a3341-247">Perfil técnica incluido por Hola otros perfiles técnicas AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="a3341-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="a3341-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3341-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="a3341-249">Perfil técnico de inicios de sesión sociales</span><span class="sxs-lookup"><span data-stu-id="a3341-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="a3341-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3341-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="a3341-251">Perfil técnico de inicios de sesión sociales</span><span class="sxs-lookup"><span data-stu-id="a3341-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="a3341-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="a3341-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="a3341-253">Perfil técnico de inicios de sesión sociales</span><span class="sxs-lookup"><span data-stu-id="a3341-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="a3341-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="a3341-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="a3341-255">Perfil técnico de cuentas locales</span><span class="sxs-lookup"><span data-stu-id="a3341-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="a3341-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="a3341-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="a3341-257">Perfil técnico de cuentas locales</span><span class="sxs-lookup"><span data-stu-id="a3341-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="a3341-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3341-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="a3341-259">Perfil técnico de actualización de registros de usuario mediante objectId</span><span class="sxs-lookup"><span data-stu-id="a3341-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="a3341-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3341-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="a3341-261">Perfil técnico de actualización de registros de usuario mediante objectId</span><span class="sxs-lookup"><span data-stu-id="a3341-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="a3341-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3341-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="a3341-263">Perfil técnico de actualización de registros de usuario mediante objectId</span><span class="sxs-lookup"><span data-stu-id="a3341-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="a3341-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3341-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="a3341-265">Perfil técnica es datos tooread usado cuando se autentica el usuario</span><span class="sxs-lookup"><span data-stu-id="a3341-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="a3341-266">Perfiles técnicos autoafirmados</span><span class="sxs-lookup"><span data-stu-id="a3341-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="a3341-267">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-267">Technical profile</span></span> | <span data-ttu-id="a3341-268">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="a3341-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="a3341-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="a3341-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="a3341-271">Perfiles técnicos de cuenta local</span><span class="sxs-lookup"><span data-stu-id="a3341-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="a3341-272">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-272">Technical profile</span></span> | <span data-ttu-id="a3341-273">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="a3341-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="a3341-275">Perfiles técnicos de administración de sesiones</span><span class="sxs-lookup"><span data-stu-id="a3341-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="a3341-276">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-276">Technical profile</span></span> | <span data-ttu-id="a3341-277">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="a3341-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="a3341-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="a3341-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="a3341-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="a3341-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="a3341-281">Nombre del perfil se sesión AAD toodisambiguate utilizado entre el inicio de sesión y la puesta iniciar sesión en</span><span class="sxs-lookup"><span data-stu-id="a3341-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="a3341-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="a3341-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="a3341-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="a3341-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="a3341-284">Perfiles técnicos de Trustframework Policy Engine TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="a3341-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="a3341-285">Actualmente, no hay perfiles técnicas se definen para hello **TechnicalProfiles de motor de directiva de Trustframework** proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3341-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="a3341-286">Perfiles técnicos del emisor de tokens</span><span class="sxs-lookup"><span data-stu-id="a3341-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="a3341-287">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a3341-287">Technical profile</span></span> | <span data-ttu-id="a3341-288">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3341-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="a3341-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="a3341-290">Recorridos de usuario</span><span class="sxs-lookup"><span data-stu-id="a3341-290">User journeys</span></span>

<span data-ttu-id="a3341-291">Esta sección describe los viajes de usuario de hello ya declarados en hello *B2C_1A_base* directiva.</span><span class="sxs-lookup"><span data-stu-id="a3341-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="a3341-292">Estos desplazamientos de usuario son susceptibles de sufrir toobe más al que hace referencia, se reemplaza o extender según sea necesario en sus propias directivas así como en hello *B2C_1A_base_extensions* directiva.</span><span class="sxs-lookup"><span data-stu-id="a3341-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="a3341-293">Recorrido de usuario</span><span class="sxs-lookup"><span data-stu-id="a3341-293">User journey</span></span> | <span data-ttu-id="a3341-294">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3341-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="a3341-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="a3341-295">*SignUp*</span></span> | |
| <span data-ttu-id="a3341-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="a3341-296">*SignIn*</span></span> | |
| <span data-ttu-id="a3341-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="a3341-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="a3341-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="a3341-298">*EditProfile*</span></span> | |
| <span data-ttu-id="a3341-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="a3341-299">*PasswordReset*</span></span> | |
