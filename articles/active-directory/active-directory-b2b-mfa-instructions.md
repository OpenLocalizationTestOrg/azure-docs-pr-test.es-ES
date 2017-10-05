---
title: "Acceso condicional para usuarios de colaboración B2B de Azure Active Directory | Microsoft Docs"
description: "La colaboración B2B de Azure Active Directory admite Multi-Factor Authentication (MFA) para poder acceder de manera selectiva a las aplicaciones corporativas."
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="6a0eb-103">Acceso condicional para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="6a0eb-104">Multi-Factor Authentication para usuarios B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="6a0eb-105">Con la colaboración B2B de Azure AD, las organizaciones pueden exigir directivas de autenticación multifactor (MFA) para usuarios de B2B.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="6a0eb-106">Estas directivas se pueden exigir en el nivel de inquilino, aplicación o usuario individual, del mismo modo que pueden habilitarse para empleados a tiempo completo y miembros de la organización.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="6a0eb-107">Se aplican las directivas MFA en la organización de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="6a0eb-108">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-108">Example:</span></span>
1. <span data-ttu-id="6a0eb-109">El administrador o el trabajador de la información de la empresa A invita a un usuario de la empresa B a una aplicación *Foo* de la empresa A.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="6a0eb-110">La aplicación *Foo* de la empresa A se configura para requerir MFA en el acceso.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="6a0eb-111">Cuando el usuario de la empresa B intenta acceder a la aplicación *Foo* en el inquilino de la empresa A, se le pide que realice un desafío de MFA.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="6a0eb-112">El usuario puede configurar su MFA con la empresa A y elegir su opción de MFA.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="6a0eb-113">Este escenario funciona con cualquier identidad (Azure AD o MSA, por ejemplo, si los usuarios de la empresa B se autentican con un identificador social).</span><span class="sxs-lookup"><span data-stu-id="6a0eb-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="6a0eb-114">La empresa A debe tener suficientes licencias de Azure AD Premium que admitan MFA.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="6a0eb-115">El usuario de la empresa B consume esta licencia de la empresa A.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="6a0eb-116">El inquilino que realiza la invitación siempre es responsable de MFA en los usuarios de la organización asociada, incluso si esta tiene funcionalidades MFA.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="6a0eb-117">Configuración de Multi-Factor Authentication para los usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="6a0eb-118">Para descubrir lo fácil que es configurar MFA para los usuarios de colaboración B2B, vea el siguiente vídeo:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="6a0eb-119">Experiencia de MFA de los usuarios B2B para el canje de ofertas</span><span class="sxs-lookup"><span data-stu-id="6a0eb-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="6a0eb-120">Consulte la siguiente animación para ver la experiencia de canje:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="6a0eb-121">Restablecimiento de la MFA para los usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="6a0eb-122">Actualmente, el administrador puede requerir que se vuelvan a probar los usuarios de colaboración B2B solo mediante los siguientes cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="6a0eb-123">Conectarse a Azure</span><span class="sxs-lookup"><span data-stu-id="6a0eb-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="6a0eb-124">Obtenga todos los usuarios con los métodos de prueba.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="6a0eb-125">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="6a0eb-126">Restablezca el método MFA en un usuario específico para exigir que el usuario de colaboración B2B establezca de nuevo los métodos de prueba.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="6a0eb-127">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="6a0eb-128">¿Por qué se realiza el MFA en el arrendamiento de recursos?</span><span class="sxs-lookup"><span data-stu-id="6a0eb-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="6a0eb-129">En la versión actual, MFA se encuentra siempre en el inquilino de recursos, por motivos de previsión.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="6a0eb-130">Por ejemplo, supongamos que un usuario de Contoso (Sally) está invitado a Fabrikam y Fabrikam ha habilitado MFA para usuarios de B2B.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="6a0eb-131">Si Contoso tiene habilitada la directiva MFA para App1 pero no para App2, si examinamos la notificación de MFA de Contoso, podríamos ver el siguiente problema:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="6a0eb-132">Día 1: un usuario tiene MFA en Contoso y accede a App1; así que no se muestra ningún mensaje adicional de MFA en Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="6a0eb-133">Día 2: el usuario ha accedido a App 2 en Contoso, así que ahora, al acceder a Fabrikam, debe registrarse ahí en MFA.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="6a0eb-134">Este proceso puede resultar confuso y podría dar lugar a que los inicios de sesión se queden sin terminar.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="6a0eb-135">Además, aunque Contoso tenga la funcionalidad de MFA, no siempre Fabrikam confiará en la directiva de MFA de Contoso.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="6a0eb-136">Por último, el MFA del inquilino de recursos también funciona en las MSA y los identificadores sociales, así como en las organizaciones asociadas que no tengan una configuración de MFA.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="6a0eb-137">Por lo tanto, la recomendación de MFA en usuarios de B2B es exigir siempre MFA en el inquilino que invita.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="6a0eb-138">Este requisito podría dar lugar a MFA doble en algunos casos, pero cada vez que se accede al inquilino que invita, la experiencia de los usuarios finales es predecible: Sally debe registrarse en MFA con el inquilino que invita.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="6a0eb-139">Acceso condicional basado en el dispositivo, la ubicación y el riesgo para usuarios de B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="6a0eb-140">Cuando Contoso habilita las directivas de acceso condicional basado en el dispositivo para sus datos corporativos, se impide el acceso desde dispositivos no administrados por Contoso y que no cumplen estas directivas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="6a0eb-141">Si el dispositivo del usuario de B2B no está administrado por Contoso, el acceso de usuarios de B2B de las organizaciones asociadas se bloqueará en el contexto en que se apliquen estas directivas.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="6a0eb-142">Sin embargo, Contoso puede crear listas de exclusión que contengan usuarios asociados específicos para excluirlos de la directiva de acceso condicional basado en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="6a0eb-143">Acceso condicional basado en ubicación para B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="6a0eb-144">Las directivas de acceso condicional basado en la ubicación se pueden aplicar a usuarios de B2B si la organización que invita no puede crear un intervalo de direcciones IP de confianza que defina sus organizaciones asociadas.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="6a0eb-145">Acceso condicional basado en riesgos para B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="6a0eb-146">Actualmente, no se pueden aplicar directivas de inicio de sesión basadas en el riesgo a los usuarios de B2B ya que la evaluación del riesgo se realiza en la organización principal del usuario de B2B.</span><span class="sxs-lookup"><span data-stu-id="6a0eb-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a0eb-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a0eb-147">Next steps</span></span>

<span data-ttu-id="6a0eb-148">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6a0eb-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6a0eb-149">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6a0eb-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6a0eb-150">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="6a0eb-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="6a0eb-151">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="6a0eb-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="6a0eb-152">Los elementos del correo electrónico de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="6a0eb-153">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6a0eb-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="6a0eb-154">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a0eb-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="6a0eb-155">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a0eb-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="6a0eb-156">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="6a0eb-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="6a0eb-157">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a0eb-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="6a0eb-158">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="6a0eb-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="6a0eb-159">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a0eb-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
