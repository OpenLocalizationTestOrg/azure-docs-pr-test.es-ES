---
title: "acceso de aaaConditional para los usuarios de la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Colaboración B2B de Active Directory de Azure es compatible con la autenticación multifactor (MFA) para las aplicaciones corporativas acceso selectivo tooyour"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="99041-103">Acceso condicional para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="99041-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="99041-104">Multi-Factor Authentication para usuarios B2B</span><span class="sxs-lookup"><span data-stu-id="99041-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="99041-105">Con la colaboración B2B de Azure AD, las organizaciones pueden exigir directivas de autenticación multifactor (MFA) para usuarios de B2B.</span><span class="sxs-lookup"><span data-stu-id="99041-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="99041-106">Estas directivas se pueden aplicar en el nivel de usuario individual, aplicación o inquilino Hola Hola igual que están habilitados para los empleados a jornada completa y los miembros de la organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="99041-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="99041-107">Se aplican las directivas MFA en la organización de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="99041-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="99041-108">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99041-108">Example:</span></span>
1. <span data-ttu-id="99041-109">Trabajo de administrador o información de la compañía A invita a usuario de la aplicación de la compañía B tooan *Foo* de compañía A.</span><span class="sxs-lookup"><span data-stu-id="99041-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="99041-110">Aplicación *Foo* de compañía A es toorequire configurado MFA en el acceso.</span><span class="sxs-lookup"><span data-stu-id="99041-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="99041-111">Cuando el usuario de saludo de la compañía B intente tooaccess aplicación *Foo* en un inquilino de empresa de hello, son más frecuentes toocomplete un desafío MFA.</span><span class="sxs-lookup"><span data-stu-id="99041-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="99041-112">Hola usuario puede configurar su MFA con la compañía A y elige la opción de MFA.</span><span class="sxs-lookup"><span data-stu-id="99041-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="99041-113">Este escenario funciona con cualquier identidad (Azure AD o MSA, por ejemplo, si los usuarios de la empresa B se autentican con un identificador social).</span><span class="sxs-lookup"><span data-stu-id="99041-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="99041-114">La empresa A debe tener suficientes licencias de Azure AD Premium que admitan MFA.</span><span class="sxs-lookup"><span data-stu-id="99041-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="99041-115">usuario de saludo de la compañía B utiliza esta licencia de compañía A.</span><span class="sxs-lookup"><span data-stu-id="99041-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="99041-116">arquitectura multiempresa invitar a Hello siempre es responsable de MFA para los usuarios de la organización del asociado de hello, incluso si la organización del asociado de hello tiene capacidades de MFA.</span><span class="sxs-lookup"><span data-stu-id="99041-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="99041-117">Configuración de Multi-Factor Authentication para los usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="99041-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="99041-118">toodiscover lo fácil que es tooset MFA de para los usuarios de la colaboración B2B, vea cómo en Hola después de vídeo:</span><span class="sxs-lookup"><span data-stu-id="99041-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="99041-119">Experiencia de MFA de los usuarios B2B para el canje de ofertas</span><span class="sxs-lookup"><span data-stu-id="99041-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="99041-120">Extraer del repositorio Hola después de la experiencia de animación toosee Hola canje:</span><span class="sxs-lookup"><span data-stu-id="99041-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="99041-121">Restablecimiento de la MFA para los usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="99041-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="99041-122">Actualmente, Hola, administrador puede requerir volver a tooproof de los usuarios de la colaboración B2B de únicamente mediante Hola siguientes cmdlets de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="99041-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="99041-123">Conectar tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="99041-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="99041-124">Obtenga todos los usuarios con los métodos de prueba.</span><span class="sxs-lookup"><span data-stu-id="99041-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="99041-125">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99041-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="99041-126">Restablecer el método MFA de hello para un usuario específico toorequire Hola B2B colaboración usuario tooset prueba métodos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="99041-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="99041-127">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99041-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="99041-128">¿Por qué se realizar MFA en inquilinos de recursos de hello?</span><span class="sxs-lookup"><span data-stu-id="99041-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="99041-129">En la versión actual de hello, MFA siempre está en inquilinos de recursos de hello, por motivos de la predicción.</span><span class="sxs-lookup"><span data-stu-id="99041-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="99041-130">Por ejemplo, supongamos que un usuario de Contoso (Sally) es tooFabrikam invitado y Fabrikam habilitó MFA para usuarios de B2B.</span><span class="sxs-lookup"><span data-stu-id="99041-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="99041-131">Si Contoso tiene una directiva MFA habilitada para App1 pero no App2, a continuación, si miramos Hola notificación Contoso MFA en el token de hello, tengamos que vemos Hola siguiente problema:</span><span class="sxs-lookup"><span data-stu-id="99041-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="99041-132">Día 1: un usuario tiene MFA en Contoso y accede a App1; así que no se muestra ningún mensaje adicional de MFA en Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="99041-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="99041-133">Día 2: Hola usuario tiene acceso a 2 de la aplicación en Contoso, por lo que ahora al tener acceso a Fabrikam, deben registrarse para MFA no existe.</span><span class="sxs-lookup"><span data-stu-id="99041-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="99041-134">Este proceso puede resultar confuso y podría provocar toodrop en las finalizaciones de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99041-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="99041-135">Además, incluso si Contoso tiene capacidad MFA, no siempre es Hola Hola mayúsculas Fabrikam confiarán en hello directiva de MFA de Contoso.</span><span class="sxs-lookup"><span data-stu-id="99041-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="99041-136">Por último, el MFA del inquilino de recursos también funciona en las MSA y los identificadores sociales, así como en las organizaciones asociadas que no tengan una configuración de MFA.</span><span class="sxs-lookup"><span data-stu-id="99041-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="99041-137">Por lo tanto, la recomendación de Hola para MFA para los usuarios de B2B es tooalways requerir MFA Hola invitar a los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="99041-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="99041-138">Este requisito puede provocar toodouble MFA en algunos casos, pero cada vez que se obtiene acceso a los inquilinos invitar a hello, experiencia de los usuarios finales de hello es predecible: Sally debe registrar para MFA con inquilinos invitar a Hola.</span><span class="sxs-lookup"><span data-stu-id="99041-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="99041-139">Acceso condicional basado en el dispositivo, la ubicación y el riesgo para usuarios de B2B</span><span class="sxs-lookup"><span data-stu-id="99041-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="99041-140">Cuando Contoso permite que las directivas de acceso condicional basado en el dispositivo para datos de su empresa, se impida el acceso desde dispositivos que no están administrados por Contoso y no son compatibles con las directivas de dispositivo de Contoso Hola.</span><span class="sxs-lookup"><span data-stu-id="99041-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="99041-141">Si no administra el dispositivo del usuario de hello B2B por Contoso, acceso de B2B a los usuarios de organizaciones de socios comerciales de hello está bloqueado en el contexto de estas directivas se aplican.</span><span class="sxs-lookup"><span data-stu-id="99041-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="99041-142">Sin embargo, Contoso puede crear listas que contengan socio específico a los usuarios tooexclude de Hola directiva de acceso condicional basado en dispositivos de exclusión.</span><span class="sxs-lookup"><span data-stu-id="99041-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="99041-143">Acceso condicional basado en ubicación para B2B</span><span class="sxs-lookup"><span data-stu-id="99041-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="99041-144">Las directivas de acceso condicional basado en la ubicación se pueden aplicar para que los usuarios de B2B si organización invitar a hello es capaz de toocreate un intervalo de direcciones IP confianza que define sus organizaciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="99041-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="99041-145">Acceso condicional basado en riesgos para B2B</span><span class="sxs-lookup"><span data-stu-id="99041-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="99041-146">Actualmente, directivas basadas en el riesgo de inicio de sesión no pueden ser tooB2B aplicados a los usuarios, ya que se realiza la evaluación del riesgo de hello en organización principal del usuario de hello B2B.</span><span class="sxs-lookup"><span data-stu-id="99041-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99041-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99041-147">Next steps</span></span>

<span data-ttu-id="99041-148">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="99041-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="99041-149">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="99041-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="99041-150">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="99041-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="99041-151">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="99041-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="99041-152">elementos de saludo de correo electrónico de invitación de colaboración B2B de hello</span><span class="sxs-lookup"><span data-stu-id="99041-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="99041-153">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="99041-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="99041-154">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99041-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="99041-155">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99041-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="99041-156">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="99041-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="99041-157">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99041-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="99041-158">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="99041-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="99041-159">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99041-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
