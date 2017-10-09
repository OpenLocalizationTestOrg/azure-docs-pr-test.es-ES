---
title: "función de aaaAdd un B2B de Azure Active Directory colaboración usuario tooa | Documentos de Microsoft"
description: Agregar un rol de tooa de usuario de invitado de Azure Active Directory
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
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="1f764-103">Conceder permisos toousers de organizaciones de socios comerciales en el inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f764-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="1f764-104">Los usuarios de colaboración B2B de Active Directory (Azure AD) Azure se agregan como directorio de toohello de invitado a los usuarios y permisos de invitado en el directorio de hello están restringidos de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1f764-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="1f764-105">Su empresa necesite algunos roles de privilegio mayor invitado toofill de los usuarios de su organización.</span><span class="sxs-lookup"><span data-stu-id="1f764-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="1f764-106">toosupport definir roles de privilegio mayor, los usuarios invitados pueden ser funciones de agregado tooany que desee, en función de las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="1f764-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="1f764-107">Rol predeterminado</span><span class="sxs-lookup"><span data-stu-id="1f764-107">Default role</span></span>

![Rol predeterminado](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="1f764-109">Rol de administrador global</span><span class="sxs-lookup"><span data-stu-id="1f764-109">Global Administrator Role</span></span>

![Rol de administrador global](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="1f764-111">Rol de administrador limitado</span><span class="sxs-lookup"><span data-stu-id="1f764-111">Limited Administrator Role</span></span>

![Rol de administrador limitado](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="1f764-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f764-113">Next steps</span></span>

<span data-ttu-id="1f764-114">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1f764-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1f764-115">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="1f764-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1f764-116">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1f764-117">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1f764-118">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1f764-119">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f764-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1f764-120">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1f764-121">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1f764-122">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1f764-123">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="1f764-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="1f764-124">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="1f764-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
