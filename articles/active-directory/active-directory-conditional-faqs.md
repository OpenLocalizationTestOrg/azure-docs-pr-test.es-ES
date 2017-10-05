---
title: "Preguntas más frecuentes sobre el acceso condicional de Azure Active Directory | Microsoft Docs"
description: "Obtenga respuestas a las preguntas más frecuentes sobre el acceso condicional en Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="1daf0-103">Preguntas más frecuentes sobre el acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1daf0-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="1daf0-104">¿Qué aplicaciones funcionan con directivas de acceso condicional?</span><span class="sxs-lookup"><span data-stu-id="1daf0-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="1daf0-105">Para obtener información sobre las aplicaciones que funcionan con directivas de acceso condicional, consulte [Aplicaciones y navegadores que usan reglas de acceso condicional en Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1daf0-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="1daf0-106">¿Se aplican directivas de acceso condicional a usuarios de colaboración B2B o invitados?</span><span class="sxs-lookup"><span data-stu-id="1daf0-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="1daf0-107">Se exigen directivas a los usuarios de la colaboración de negocio a negocio (B2B),</span><span class="sxs-lookup"><span data-stu-id="1daf0-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="1daf0-108">pero en algunos casos un usuario podría no satisfacer los requisitos de las directivas.</span><span class="sxs-lookup"><span data-stu-id="1daf0-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="1daf0-109">Por ejemplo, la organización de un usuario invitado podría no admitir la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="1daf0-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="1daf0-110">¿Se aplica la directiva de SharePoint Online también a OneDrive para la Empresa?</span><span class="sxs-lookup"><span data-stu-id="1daf0-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="1daf0-111">Sí.</span><span class="sxs-lookup"><span data-stu-id="1daf0-111">Yes.</span></span> <span data-ttu-id="1daf0-112">Las directivas de SharePoint Online también se aplican a OneDrive para la Empresa.</span><span class="sxs-lookup"><span data-stu-id="1daf0-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="1daf0-113">¿Por qué no se puede establecer una directiva en las aplicaciones cliente, como Word o Outlook?</span><span class="sxs-lookup"><span data-stu-id="1daf0-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="1daf0-114">Una directiva de acceso condicional establece los requisitos para obtener acceso a un servicio.</span><span class="sxs-lookup"><span data-stu-id="1daf0-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="1daf0-115">Se aplica cuando se produce la autenticación con ese servicio.</span><span class="sxs-lookup"><span data-stu-id="1daf0-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="1daf0-116">La directiva no se establece directamente en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="1daf0-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="1daf0-117">En su lugar, se aplica cuando un cliente llama a un servicio.</span><span class="sxs-lookup"><span data-stu-id="1daf0-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="1daf0-118">Por ejemplo, una directiva establecida en SharePoint se aplicará a los clientes que llamen a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1daf0-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="1daf0-119">Una directiva establecida en Exchange se aplica a Outlook.</span><span class="sxs-lookup"><span data-stu-id="1daf0-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="1daf0-120">¿Se aplica una directiva de acceso condicional a las cuentas de servicio?</span><span class="sxs-lookup"><span data-stu-id="1daf0-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="1daf0-121">Las directivas de acceso condicional se aplican a todas las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="1daf0-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="1daf0-122">Aquí se incluyen las cuentas de usuario que se usan como cuentas de servicio.</span><span class="sxs-lookup"><span data-stu-id="1daf0-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="1daf0-123">A menudo sucede que una cuenta de servicio que se ejecuta de forma desatendida no puede satisfacer los requisitos de una directiva de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="1daf0-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="1daf0-124">Por ejemplo, se podría requerir una autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="1daf0-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="1daf0-125">Las cuentas de servicio se pueden excluir de una directiva mediante la configuración de administración de directivas de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="1daf0-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="1daf0-126">¿Están disponibles las API Graph para configurar directivas de acceso condicional?</span><span class="sxs-lookup"><span data-stu-id="1daf0-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="1daf0-127">Actualmente no.</span><span class="sxs-lookup"><span data-stu-id="1daf0-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="1daf0-128">¿Qué es la directiva de exclusión predeterminada para plataformas de dispositivos no compatibles?</span><span class="sxs-lookup"><span data-stu-id="1daf0-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="1daf0-129">Actualmente, las directivas de acceso condicional se aplican de forma selectiva a los usuarios de dispositivos iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="1daf0-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="1daf0-130">De forma predeterminada, las aplicaciones de otras plataformas de dispositivos no se ven afectadas por la directiva de acceso condicional para dispositivos iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="1daf0-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="1daf0-131">Un administrador de inquilinos puede optar por invalidar la directiva global para impedir el acceso a los usuarios en las plataformas no compatibles.</span><span class="sxs-lookup"><span data-stu-id="1daf0-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="1daf0-132">¿Cómo funcionan las directivas de acceso condicional para Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="1daf0-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="1daf0-133">Microsoft Teams se basa principalmente en Exchange Online y SharePoint Online para los principales escenarios de productividad, como las reuniones, los calendarios y el uso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="1daf0-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="1daf0-134">Las directivas de acceso condicional que se establecen para estas aplicaciones de nube se aplican a Microsoft Teams cuando un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="1daf0-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="1daf0-135">Microsoft Teams también se admite por separado como aplicación de nube en las directivas de acceso condicional de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1daf0-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="1daf0-136">Las directivas de entidad de certificación que se establecen para una aplicación de nube se aplican a Microsoft Teams cuando un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="1daf0-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="1daf0-137">Los clientes de escritorio de Microsoft Teams para Windows y Mac admiten la autenticación moderna.</span><span class="sxs-lookup"><span data-stu-id="1daf0-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="1daf0-138">La autenticación moderna proporciona un inicio de sesión basado en la biblioteca de autenticación de Azure Active Directory (ADAL) para las aplicaciones cliente de Microsoft Office en distintas plataformas.</span><span class="sxs-lookup"><span data-stu-id="1daf0-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 