---
title: "Limitaciones de colaboración B2B de Azure Active Directory | Microsoft Docs"
description: "Limitaciones actuales de la colaboración B2B de Azure Active Directory"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="3b6c2-103">Limitaciones de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6c2-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="3b6c2-104">La colaboración B2B de Active Directory (Azure AD) de Azure está sujeta actualmente a las limitaciones descritas en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="3b6c2-105">Posibilidad de doble autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="3b6c2-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="3b6c2-106">Con B2B de Azure AD, puede aplicar la autenticación multifactor en la organización del recurso (la organización que invita).</span><span class="sxs-lookup"><span data-stu-id="3b6c2-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="3b6c2-107">Los motivos de este enfoque se detallan en [Acceso condicional para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="3b6c2-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="3b6c2-108">Si un asociado ya tiene instalada la autenticación multifactor y la exige, los usuarios del asociado podrían tener que realizar la autenticación una vez en su organización principal y otra vez en la suya.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="3b6c2-109">Activación instantánea</span><span class="sxs-lookup"><span data-stu-id="3b6c2-109">Instant-on</span></span>
<span data-ttu-id="3b6c2-110">En los flujos de colaboración B2B, hemos agregado usuarios al directorio y los hemos actualizado dinámicamente durante el canje de invitación, la asignación de aplicaciones y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="3b6c2-111">Las actualizaciones y escrituras se producen normalmente en una instancia de directorio y se deben replicar en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="3b6c2-112">La replicación se completa una vez que se actualicen todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="3b6c2-113">En ocasiones, cuando el objeto se escribe o se actualiza en una instancia y la llamada para recuperar este objeto es a otra instancia, pueden producirse latencias en la replicación.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="3b6c2-114">Si esto sucede, actualice o vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="3b6c2-115">Si está escribiendo una aplicación mediante la API, los reintentos con algún retroceso es una buena práctica defensiva para mitigar este problema.</span><span class="sxs-lookup"><span data-stu-id="3b6c2-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b6c2-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b6c2-116">Next steps</span></span>

<span data-ttu-id="3b6c2-117">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3b6c2-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="3b6c2-118">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="3b6c2-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="3b6c2-119">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="3b6c2-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="3b6c2-120">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="3b6c2-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="3b6c2-121">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="3b6c2-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="3b6c2-122">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="3b6c2-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="3b6c2-123">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b6c2-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="3b6c2-124">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="3b6c2-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="3b6c2-125">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="3b6c2-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="3b6c2-126">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="3b6c2-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="3b6c2-127">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="3b6c2-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
