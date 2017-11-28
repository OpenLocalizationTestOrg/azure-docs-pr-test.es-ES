---
title: "Adición de un usuario de colaboración B2B de Azure Active Directory a un rol | Microsoft Docs"
description: "Adición de un usuario invitado a un rol en Azure Active Directory"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="e360b-103">Conceda permisos a los usuarios de organizaciones asociadas en el inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e360b-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="e360b-104">Los usuarios de colaboración B2B de Azure Active Directory (Azure AD) se agregan como usuarios invitados al directorio y los permisos de invitado del directorio están restringidos de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e360b-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="e360b-105">Asimismo, su empresa puede necesitar algunos usuarios invitados para cubrir más roles con privilegios en su organización.</span><span class="sxs-lookup"><span data-stu-id="e360b-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="e360b-106">Para respaldar la definición de roles de privilegios más elevados, se pueden agregar usuarios invitados a los roles que desee, según las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="e360b-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="e360b-107">Rol predeterminado</span><span class="sxs-lookup"><span data-stu-id="e360b-107">Default role</span></span>

![Rol predeterminado](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="e360b-109">Rol de administrador global</span><span class="sxs-lookup"><span data-stu-id="e360b-109">Global Administrator Role</span></span>

![Rol de administrador global](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="e360b-111">Rol de administrador limitado</span><span class="sxs-lookup"><span data-stu-id="e360b-111">Limited Administrator Role</span></span>

![Rol de administrador limitado](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="e360b-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e360b-113">Next steps</span></span>

<span data-ttu-id="e360b-114">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e360b-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e360b-115">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e360b-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e360b-116">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="e360b-117">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="e360b-118">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="e360b-119">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e360b-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="e360b-120">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="e360b-121">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="e360b-122">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="e360b-123">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="e360b-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="e360b-124">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e360b-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
