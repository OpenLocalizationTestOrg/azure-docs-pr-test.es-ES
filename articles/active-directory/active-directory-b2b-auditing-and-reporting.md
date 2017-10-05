---
title: "Auditoría y generación de informes para usuarios de colaboración B2B de Azure Active Directory | Microsoft Docs"
description: "Las propiedades de un usuario invitado son configurables en la colaboración B2B de Azure Active Directory."
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
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: ba782270f3280e52235bc13148d232284b55762a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a><span data-ttu-id="10475-103">Auditoría y generación de informes para usuarios de colaboración 2B</span><span class="sxs-lookup"><span data-stu-id="10475-103">Auditing and reporting a B2B collaboration user</span></span>
<span data-ttu-id="10475-104">Con usuarios invitados, cuenta con funcionalidades de auditoría similares a las que tiene con los usuarios miembros.</span><span class="sxs-lookup"><span data-stu-id="10475-104">With guest users, you have auditing capabilities similar to with member users.</span></span> <span data-ttu-id="10475-105">A continuación, se muestra un ejemplo del historial de canje e invitación de los usuario Sam Oogle al que se acaba de invitar:</span><span class="sxs-lookup"><span data-stu-id="10475-105">Here's an example of the invitation and redemption history of invitee Sam Oogle:</span></span>

![Registro de auditoría](./media/active-directory-b2b-auditing-and-reporting/audit-log.png)

<span data-ttu-id="10475-107">Puede profundizar en cada uno de estos eventos para obtener los detalles.</span><span class="sxs-lookup"><span data-stu-id="10475-107">You can dive into each of these events to get the details.</span></span> <span data-ttu-id="10475-108">Por ejemplo, echemos un vistazo a los detalles de aceptación.</span><span class="sxs-lookup"><span data-stu-id="10475-108">For example, let's look at the acceptance details.</span></span>

![Detalles de actividad](./media/active-directory-b2b-auditing-and-reporting/activity-details.png)

<span data-ttu-id="10475-110">También puede exportar estos registros de Azure AD y utilizar la herramienta de informes que prefiera para obtener informes personalizados.</span><span class="sxs-lookup"><span data-stu-id="10475-110">You can also export these logs from Azure AD and use the reporting tool of your choice to get customized reports.</span></span>

### <a name="next-steps"></a><span data-ttu-id="10475-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10475-111">Next steps</span></span>

<span data-ttu-id="10475-112">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="10475-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="10475-113">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="10475-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="10475-114">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-114">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="10475-115">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="10475-115">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="10475-116">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-116">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="10475-117">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-117">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="10475-118">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="10475-118">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="10475-119">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-119">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="10475-120">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-120">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="10475-121">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-121">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="10475-122">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="10475-122">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="10475-123">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="10475-123">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
