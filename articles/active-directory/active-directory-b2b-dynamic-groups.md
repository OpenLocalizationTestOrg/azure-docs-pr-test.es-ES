---
title: "aaaDynamic grupos y la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "La colaboración B2B de Active Directory de Azure puede utilizarse con grupos dinámicos de Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="15512-103">Grupos dinámicos y colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15512-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="15512-104">¿Qué son los grupos dinámicos?</span><span class="sxs-lookup"><span data-stu-id="15512-104">What are dynamic groups?</span></span>
<span data-ttu-id="15512-105">Configuración dinámica de pertenencia a grupos de seguridad de Azure Active Directory (Azure AD) está disponible en [Hola portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15512-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="15512-106">Los administradores pueden configurar reglas de grupos de toopopulate que se crean en Azure Active Directory en función de atributos de usuario (por ejemplo, userType, departamento o país).</span><span class="sxs-lookup"><span data-stu-id="15512-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="15512-107">Los miembros se pueden agregar automáticamente tooor quita de un grupo de seguridad en función de sus atributos.</span><span class="sxs-lookup"><span data-stu-id="15512-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="15512-108">Estos grupos pueden proporcionar acceso a recursos tooapplications o en la nube (los sitios de SharePoint, documentos) y tooassign licencias toomembers.</span><span class="sxs-lookup"><span data-stu-id="15512-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="15512-109">Obtenga más información sobre los grupos dinámicos en [Grupos dedicados en Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="15512-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="15512-110">Hola adecuado [P1 de Azure AD Premium o P2 con licencias](https://azure.microsoft.com/pricing/details/active-directory/) es grupos dinámicos necesarios toocreate y uso.</span><span class="sxs-lookup"><span data-stu-id="15512-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="15512-111">Obtenga más información en el artículo de hello [crear reglas basadas en atributos de pertenencia dinámica a grupos en Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15512-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="15512-112">¿Qué grupos dinámicos integrados de hello?</span><span class="sxs-lookup"><span data-stu-id="15512-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="15512-113">Hola **todos los usuarios** grupo dinámico permite toocreate de administradores de inquilinos un grupo que contiene todos los usuarios de inquilinos de hello con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="15512-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="15512-114">De forma predeterminada, Hola **todos los usuarios** grupo incluye a todos los usuarios de directorio de hello, incluidos los miembros y los invitados.</span><span class="sxs-lookup"><span data-stu-id="15512-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="15512-115">En el portal de administración de Azure Active Directory nuevo hello, puede elegir hello tooenable **todos los usuarios** grupo Hola ver configuración de grupo.</span><span class="sxs-lookup"><span data-stu-id="15512-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![Grupos integrados](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="15512-117">La protección de Hola a todos los grupos de usuarios dinámica</span><span class="sxs-lookup"><span data-stu-id="15512-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="15512-118">De forma predeterminada, Hola **todos los usuarios** grupo contiene los usuarios de colaboración (invitado) de B2B.</span><span class="sxs-lookup"><span data-stu-id="15512-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="15512-119">Puede proteger aún más su **todos los usuarios** grupo mediante el uso de un usuario de invitado de tooremove de regla.</span><span class="sxs-lookup"><span data-stu-id="15512-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="15512-120">Hello en la ilustración siguiente se muestra hello **todos los usuarios** grupo Modificar tooexclude invitados.</span><span class="sxs-lookup"><span data-stu-id="15512-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![Habilitación de todos los grupos de usuarios](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="15512-122">Es posible que también resulte útil toocreate un nuevo grupo dinámico que contiene solo los usuarios invitados, para que pueda aplicar directivas (por ejemplo, las directivas de acceso condicional de Azure AD) toothem.</span><span class="sxs-lookup"><span data-stu-id="15512-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="15512-123">Este el aspecto que tendría ese grupo:</span><span class="sxs-lookup"><span data-stu-id="15512-123">What such a group might look like:</span></span>

![Exclusión de usuarios invitados](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="15512-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15512-125">Next steps</span></span>

<span data-ttu-id="15512-126">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="15512-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="15512-127">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="15512-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="15512-128">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="15512-129">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="15512-130">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="15512-131">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="15512-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="15512-132">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="15512-133">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="15512-134">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="15512-135">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="15512-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="15512-136">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="15512-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
