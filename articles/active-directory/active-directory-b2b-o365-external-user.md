---
title: "aaaOffice 365 uso compartido externo y la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
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
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="8d54f-103">Uso compartido externo de Office 365 y colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d54f-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="8d54f-104">Externo de uso compartido de Office 365 (OneDrive, SharePoint Online, grupos unificados, etc.) y B2B de Azure Active Directory (Azure AD) colaboración son técnicamente Hola mismo lo.</span><span class="sxs-lookup"><span data-stu-id="8d54f-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="8d54f-105">Todas las externas compartir (excepto OneDrive y SharePoint Online), incluidos los invitados en grupos de Office 365, ya usa invitación de colaboración B2B de Azure AD hello las API para el uso compartido.</span><span class="sxs-lookup"><span data-stu-id="8d54f-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="8d54f-106">OneDrive y SharePoint Online tiene un administrador de invitaciones independiente.</span><span class="sxs-lookup"><span data-stu-id="8d54f-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="8d54f-107">La compatibilidad con el uso compartido externo en OneDrive o SharePoint Online comenzó antes que Azure AD desarrollara su compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="8d54f-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="8d54f-108">Con el tiempo, compartir externo OneDrive y SharePoint Online ha acumulado varias características y muchos millones de usuarios que usan productos de hello en-integrada patrón de uso compartido.</span><span class="sxs-lookup"><span data-stu-id="8d54f-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="8d54f-109">Sin embargo, existen algunas diferencias sutiles entre cómo funciona el uso compartido externo de OneDrive y SharePoint Online y la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8d54f-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="8d54f-110">OneDrive y SharePoint Online agrega directorio toohello de los usuarios después de que los usuarios han canjear sus invitaciones.</span><span class="sxs-lookup"><span data-stu-id="8d54f-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="8d54f-111">Por lo tanto, antes de canje, no ve el usuario de hello en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d54f-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="8d54f-112">Si otro sitio invita a un usuario en hello mientras tanto, se genera una nueva invitación.</span><span class="sxs-lookup"><span data-stu-id="8d54f-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="8d54f-113">Sin embargo, cuando se usa la colaboración B2B de Azure AD, los usuarios se agregan inmediatamente cuando se les invita por lo que se muestran en todas partes.</span><span class="sxs-lookup"><span data-stu-id="8d54f-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="8d54f-114">Hola canje experiencia en OneDrive o SharePoint Online tiene un aspecto diferente de la experiencia de hello en colaboración B2B de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d54f-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="8d54f-115">Después de que un usuario los canjea una invitación, experiencias de hello son similares.</span><span class="sxs-lookup"><span data-stu-id="8d54f-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="8d54f-116">Los usuarios invitados a la colaboración B2B de Azure AD se pueden seleccionar en los cuadros de diálogo de uso compartido de OneDrive y SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8d54f-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="8d54f-117">Los usuarios invitados a OneDrive y SharePoint Online también se muestran en Azure AD después de que canjean sus invitaciones.</span><span class="sxs-lookup"><span data-stu-id="8d54f-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="8d54f-118">toomanage externo compartida en OneDrive o SharePoint Online con la colaboración B2B de Azure AD, establezca hello OneDrive y SharePoint Online externo compartir configuración demasiado**sólo Permitir uso compartido con usuarios externos ya en el directorio de hello**.</span><span class="sxs-lookup"><span data-stu-id="8d54f-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="8d54f-119">Los usuarios pueden ir tooexternally compartido sitios y selección de colaboradores externos que Hola administrador ha agregado.</span><span class="sxs-lookup"><span data-stu-id="8d54f-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="8d54f-120">Hola, administrador puede agregar colaboradores externos de Hola a través de hello invitación de colaboración B2B API.</span><span class="sxs-lookup"><span data-stu-id="8d54f-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Hola OneDrive y SharePoint Online configuración del uso compartido externo](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="8d54f-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8d54f-122">Next steps</span></span>

<span data-ttu-id="8d54f-123">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8d54f-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8d54f-124">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="8d54f-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8d54f-125">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="8d54f-126">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="8d54f-127">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="8d54f-128">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="8d54f-129">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d54f-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="8d54f-130">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="8d54f-131">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="8d54f-132">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="8d54f-133">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="8d54f-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
