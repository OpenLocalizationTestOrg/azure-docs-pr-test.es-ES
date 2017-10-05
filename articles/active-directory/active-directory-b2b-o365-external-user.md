---
title: "Uso compartido externo de Office 365 y colaboración B2B de Azure Active Directory | Microsoft Docs"
description: "referencia de asignación de notificaciones para la colaboración B2B de Azure Active Directory"
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
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="1197a-103">Uso compartido externo de Office 365 y colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1197a-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="1197a-104">Técnicamente, es lo mismo utilizar el uso compartido externo de Office 365 (OneDrive, SharePoint Online, grupos unificados, etc.) y la colaboración B2B de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1197a-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="1197a-105">Todos los usos compartidos externos (excepto OneDrive o SharePoint Online), incluidos los invitados de grupos de Office 365, ya utilizan las API de invitación de colaboración B2B de Azure AD para el uso compartido.</span><span class="sxs-lookup"><span data-stu-id="1197a-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="1197a-106">OneDrive y SharePoint Online tiene un administrador de invitaciones independiente.</span><span class="sxs-lookup"><span data-stu-id="1197a-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="1197a-107">La compatibilidad con el uso compartido externo en OneDrive o SharePoint Online comenzó antes que Azure AD desarrollara su compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="1197a-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="1197a-108">Con el tiempo, el uso compartido externo de OneDrive o SharePoint Online ha acumulado varias características y muchos millones de usuarios que usan el patrón de uso compartido integrado del producto.</span><span class="sxs-lookup"><span data-stu-id="1197a-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="1197a-109">Sin embargo, existen algunas diferencias sutiles entre cómo funciona el uso compartido externo de OneDrive y SharePoint Online y la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1197a-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="1197a-110">OneDrive y SharePoint Online agregan usuarios al directorio después de que los usuarios han canjeado sus invitaciones.</span><span class="sxs-lookup"><span data-stu-id="1197a-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="1197a-111">Por lo tanto, antes del canje, el usuario no se muestra en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1197a-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="1197a-112">Si, mientras tanto, un usuario recibe una invitación de otro sitio, se genera una nueva invitación.</span><span class="sxs-lookup"><span data-stu-id="1197a-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="1197a-113">Sin embargo, cuando se usa la colaboración B2B de Azure AD, los usuarios se agregan inmediatamente cuando se les invita por lo que se muestran en todas partes.</span><span class="sxs-lookup"><span data-stu-id="1197a-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="1197a-114">La experiencia de canje en OneDrive y SharePoint Online parece diferente de la experiencia de colaboración B2B de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1197a-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="1197a-115">Después de que un usuario canjea una invitación, las experiencias se asemejan.</span><span class="sxs-lookup"><span data-stu-id="1197a-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="1197a-116">Los usuarios invitados a la colaboración B2B de Azure AD se pueden seleccionar en los cuadros de diálogo de uso compartido de OneDrive y SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1197a-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="1197a-117">Los usuarios invitados a OneDrive y SharePoint Online también se muestran en Azure AD después de que canjean sus invitaciones.</span><span class="sxs-lookup"><span data-stu-id="1197a-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="1197a-118">Para administrar el uso compartido externo en OneDrive o SharePoint Online con la colaboración B2B de Azure AD, establezca la configuración de uso compartido externo de OneDrive o SharePoint Online en **Only allow sharing with external users already in the directory** (Solo permitir uso compartido con usuarios externos que ya se encuentren en el directorio).</span><span class="sxs-lookup"><span data-stu-id="1197a-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="1197a-119">Los usuarios pueden acceder a los sitios compartidos externamente y elegir entre colaboradores externos que haya agregado el administrador.</span><span class="sxs-lookup"><span data-stu-id="1197a-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="1197a-120">El administrador puede agregar los colaboradores externos a través de la API de invitación de colaboración B2B.</span><span class="sxs-lookup"><span data-stu-id="1197a-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![La configuración de uso compartido externo de OneDrive y SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="1197a-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1197a-122">Next steps</span></span>

<span data-ttu-id="1197a-123">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1197a-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1197a-124">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="1197a-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1197a-125">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1197a-126">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="1197a-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1197a-127">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1197a-128">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1197a-129">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1197a-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1197a-130">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1197a-131">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1197a-132">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1197a-133">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1197a-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
