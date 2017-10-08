---
title: "aaaLimitations de colaboración B2B de Azure Active Directory | Documentos de Microsoft"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="2a570-103">Limitaciones de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a570-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="2a570-104">Colaboración B2B de Active Directory (Azure AD) de Azure está actualmente limitaciones de toohello asunto descritas en este artículo.</span><span class="sxs-lookup"><span data-stu-id="2a570-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="2a570-105">Posibilidad de doble autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="2a570-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="2a570-106">Con Azure AD B2B, se puede aplicar la autenticación multifactor en la organización de recursos de hello (Hola invitar a la organización).</span><span class="sxs-lookup"><span data-stu-id="2a570-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="2a570-107">motivos de Hola de este enfoque se detallan en [acceso condicional para los usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="2a570-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="2a570-108">Si un socio ya tiene la autenticación multifactor configurar y aplicar, sus usuarios podrían tener la autenticación de hello tooperform una vez en su organización principal y, a continuación, nuevo en suyo.</span><span class="sxs-lookup"><span data-stu-id="2a570-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="2a570-109">Activación instantánea</span><span class="sxs-lookup"><span data-stu-id="2a570-109">Instant-on</span></span>
<span data-ttu-id="2a570-110">En los flujos de colaboración de hello B2B, se agregue usuarios toohello directorio y actualizarlos dinámicamente durante el canje de invitación, asignación de aplicación y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="2a570-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="2a570-111">actualizaciones de Hola y escrituras normalmente se producen en la instancia de un directorio y se deben replicar a través de todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="2a570-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="2a570-112">La replicación se completa una vez que se actualicen todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="2a570-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="2a570-113">A veces cuando es escribir o actualizar en una instancia de objeto de Hola y Hola llamar tooretrieve este objeto es instancia tooanother, pueden producirse las latencias de replicación.</span><span class="sxs-lookup"><span data-stu-id="2a570-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="2a570-114">Si esto sucede, actualice o vuelva a intentar toohelp.</span><span class="sxs-lookup"><span data-stu-id="2a570-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="2a570-115">Si está escribiendo una aplicación con nuestra API, a continuación, reintentos con un retroceso es un tooalleviate estable, buena práctica este problema.</span><span class="sxs-lookup"><span data-stu-id="2a570-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a570-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a570-116">Next steps</span></span>

<span data-ttu-id="2a570-117">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="2a570-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="2a570-118">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="2a570-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2a570-119">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="2a570-120">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="2a570-121">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="2a570-122">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="2a570-123">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a570-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="2a570-124">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="2a570-125">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="2a570-126">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="2a570-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="2a570-127">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="2a570-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
