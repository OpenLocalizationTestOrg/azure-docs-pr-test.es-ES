---
title: "Preguntas más frecuentes de acceso condicional de Active Directory aaaAzure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes sobre el acceso condicional en Azure Active Directory."
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
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="d881c-103">Preguntas más frecuentes sobre el acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d881c-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="d881c-104">¿Qué aplicaciones funcionan con directivas de acceso condicional?</span><span class="sxs-lookup"><span data-stu-id="d881c-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="d881c-105">Para obtener información sobre las aplicaciones que funcionan con directivas de acceso condicional, consulte [Aplicaciones y navegadores que usan reglas de acceso condicional en Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d881c-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="d881c-106">¿Se aplican directivas de acceso condicional a usuarios de colaboración B2B o invitados?</span><span class="sxs-lookup"><span data-stu-id="d881c-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="d881c-107">Se exigen directivas a los usuarios de la colaboración de negocio a negocio (B2B),</span><span class="sxs-lookup"><span data-stu-id="d881c-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="d881c-108">Sin embargo, en algunos casos, un usuario podría ser capaz de toosatisfy requisitos de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="d881c-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="d881c-109">Por ejemplo, la organización de un usuario invitado podría no admitir la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="d881c-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="d881c-110">¿Aplica también una directiva de SharePoint Online tooOneDrive para la empresa?</span><span class="sxs-lookup"><span data-stu-id="d881c-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="d881c-111">Sí.</span><span class="sxs-lookup"><span data-stu-id="d881c-111">Yes.</span></span> <span data-ttu-id="d881c-112">Una directiva de SharePoint Online tooOneDrive también aplica para la empresa.</span><span class="sxs-lookup"><span data-stu-id="d881c-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="d881c-113">¿Por qué no se puede establecer una directiva en las aplicaciones cliente, como Word o Outlook?</span><span class="sxs-lookup"><span data-stu-id="d881c-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="d881c-114">Una directiva de acceso condicional establece los requisitos para obtener acceso a un servicio.</span><span class="sxs-lookup"><span data-stu-id="d881c-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="d881c-115">Se aplica cuando se produce el servicio de autenticación toothat.</span><span class="sxs-lookup"><span data-stu-id="d881c-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="d881c-116">Directiva de Hello no se establece directamente en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="d881c-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="d881c-117">En su lugar, se aplica cuando un cliente llama a un servicio.</span><span class="sxs-lookup"><span data-stu-id="d881c-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="d881c-118">Por ejemplo, una directiva establecida en SharePoint aplica tooclients llamando a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d881c-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="d881c-119">Una directiva establecida en Exchange aplica tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="d881c-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="d881c-120">¿Aplica una directiva de acceso condicional tooservice cuentas?</span><span class="sxs-lookup"><span data-stu-id="d881c-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="d881c-121">Las directivas de acceso condicional aplican las cuentas de usuario de tooall.</span><span class="sxs-lookup"><span data-stu-id="d881c-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="d881c-122">Aquí se incluyen las cuentas de usuario que se usan como cuentas de servicio.</span><span class="sxs-lookup"><span data-stu-id="d881c-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="d881c-123">A menudo, una cuenta de servicio que se ejecuta desatendida no puede satisfacer los requisitos de Hola de una directiva de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="d881c-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="d881c-124">Por ejemplo, se podría requerir una autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="d881c-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="d881c-125">Las cuentas de servicio se pueden excluir de una directiva mediante la configuración de administración de directivas de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="d881c-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="d881c-126">¿Están disponibles las API Graph para configurar directivas de acceso condicional?</span><span class="sxs-lookup"><span data-stu-id="d881c-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="d881c-127">Actualmente no.</span><span class="sxs-lookup"><span data-stu-id="d881c-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="d881c-128">¿Qué es la directiva de exclusión predeterminada de Hola para plataformas de dispositivos no compatibles?</span><span class="sxs-lookup"><span data-stu-id="d881c-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="d881c-129">Actualmente, las directivas de acceso condicional se aplican de forma selectiva a los usuarios de dispositivos iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="d881c-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="d881c-130">Las aplicaciones en otras plataformas de dispositivo, de forma predeterminada, no se ven afectadas por la directiva de acceso condicional de Hola para dispositivos iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="d881c-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="d881c-131">Un administrador de inquilinos puede elegir toooverride Hola directiva global toodisallow acceso toousers en plataformas que no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="d881c-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="d881c-132">¿Cómo funcionan las directivas de acceso condicional para Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="d881c-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="d881c-133">Microsoft Teams se basa principalmente en Exchange Online y SharePoint Online para los principales escenarios de productividad, como las reuniones, los calendarios y el uso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="d881c-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="d881c-134">Directivas de acceso condicional que se establecen para estas aplicaciones de nube aplican los equipos de tooMicrosoft cuando un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="d881c-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="d881c-135">Microsoft Teams también se admite por separado como aplicación de nube en las directivas de acceso condicional de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d881c-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="d881c-136">Las directivas de entidad emisora de certificados que están establecidas para una aplicación de nube aplican los equipos de tooMicrosoft cuando un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="d881c-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="d881c-137">Los clientes de escritorio de Microsoft Teams para Windows y Mac admiten la autenticación moderna.</span><span class="sxs-lookup"><span data-stu-id="d881c-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="d881c-138">La autenticación moderna aporta en función de las aplicaciones cliente de Office de hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft en plataformas de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d881c-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
