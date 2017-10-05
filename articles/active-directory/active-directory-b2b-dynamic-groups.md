---
title: "Grupos dinámicos y colaboración B2B de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="9688d-103">Grupos dinámicos y colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9688d-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="9688d-104">¿Qué son los grupos dinámicos?</span><span class="sxs-lookup"><span data-stu-id="9688d-104">What are dynamic groups?</span></span>
<span data-ttu-id="9688d-105">La configuración dinámica de pertenencia a grupos de seguridad de Azure Active Directory (Azure AD) está disponible en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9688d-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9688d-106">Los administradores pueden establecer reglas para rellenar los grupos que se crean en Azure Active Directory en función de los atributos de usuario (por ejemplo, userType, department o country).</span><span class="sxs-lookup"><span data-stu-id="9688d-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="9688d-107">Los miembros se agregan automáticamente a un grupo de seguridad, o se quitan de este, según sus atributos.</span><span class="sxs-lookup"><span data-stu-id="9688d-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="9688d-108">Estos grupos pueden proporcionar acceso a aplicaciones o recursos en la nube (documentos y sitios de SharePoint) y para asignar licencias a miembros.</span><span class="sxs-lookup"><span data-stu-id="9688d-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="9688d-109">Obtenga más información sobre los grupos dinámicos en [Grupos dedicados en Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="9688d-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="9688d-110">La [licencia Azure AD Premium P1 o P2](https://azure.microsoft.com/pricing/details/active-directory/) apropiada se necesita para crear y usar grupos dinámicos.</span><span class="sxs-lookup"><span data-stu-id="9688d-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="9688d-111">Obtenga más información en el artículo [Creación de reglas de pertenencia dinámica a grupos basadas en atributos en Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9688d-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="9688d-112">¿Cuáles son los grupos dinámicos integrados?</span><span class="sxs-lookup"><span data-stu-id="9688d-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="9688d-113">El grupo dinámico **Todos los usuarios** permite a los administradores de inquilinos crear un grupo que contenga todos los usuarios del inquilino con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="9688d-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="9688d-114">De forma predeterminada, el grupo **Todos los usuarios** incluye todos los usuarios del directorio, incluidos los miembros y los invitados.</span><span class="sxs-lookup"><span data-stu-id="9688d-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="9688d-115">En el nuevo portal de administración de Azure Active Directory, puede optar por habilitar el grupo **Todos los usuarios** en la vista de configuración del grupo.</span><span class="sxs-lookup"><span data-stu-id="9688d-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![Grupos integrados](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="9688d-117">Protección del grupo dinámico Todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="9688d-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="9688d-118">De manera predeterminada, el grupo **Todos los usuarios** contendrá también los usuarios de colaboración de B2B (invitados).</span><span class="sxs-lookup"><span data-stu-id="9688d-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="9688d-119">Puede proteger más su grupo **Todos los usuarios** con una regla para quitar los usuarios invitados.</span><span class="sxs-lookup"><span data-stu-id="9688d-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="9688d-120">La ilustración siguiente muestra el grupo **Todos los usuarios** modificado para excluir a los invitados.</span><span class="sxs-lookup"><span data-stu-id="9688d-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![Habilitación de todos los grupos de usuarios](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="9688d-122">Puede que también encuentre esto útil para crear un grupo dinámico que contenga solo usuarios invitados, de manera que pueda aplicar directivas (como directivas de acceso condicional de Azure AD) para ellos.</span><span class="sxs-lookup"><span data-stu-id="9688d-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="9688d-123">Este el aspecto que tendría ese grupo:</span><span class="sxs-lookup"><span data-stu-id="9688d-123">What such a group might look like:</span></span>

![Exclusión de usuarios invitados](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="9688d-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9688d-125">Next steps</span></span>

<span data-ttu-id="9688d-126">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9688d-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="9688d-127">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="9688d-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="9688d-128">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="9688d-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="9688d-129">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="9688d-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="9688d-130">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="9688d-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="9688d-131">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="9688d-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="9688d-132">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="9688d-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="9688d-133">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="9688d-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="9688d-134">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="9688d-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="9688d-135">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="9688d-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="9688d-136">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="9688d-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
