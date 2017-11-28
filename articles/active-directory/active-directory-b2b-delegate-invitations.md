---
title: "Delegación de invitaciones de la colaboración B2B de Azure Active Directory | Microsoft Docs"
description: "Las propiedades de un usuario de colaboración B2B de Azure Active Directory son configurables."
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d2977-103">Delegación de invitaciones de la colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2977-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="d2977-104">Con la colaboración negocio a negocio (B2B) de Azure Active Directory (Azure AD), no tiene que ser un administrador global para enviar invitaciones.</span><span class="sxs-lookup"><span data-stu-id="d2977-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="d2977-105">Puede usar directivas y delegar invitaciones en usuarios cuyos roles les permitan enviar invitaciones.</span><span class="sxs-lookup"><span data-stu-id="d2977-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="d2977-106">Una nueva forma importante de delegar las invitaciones de usuarios invitados es a través del rol de invitador invitado.</span><span class="sxs-lookup"><span data-stu-id="d2977-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="d2977-107">Rol de invitador de personas</span><span class="sxs-lookup"><span data-stu-id="d2977-107">Guest Inviter role</span></span>
<span data-ttu-id="d2977-108">Podemos asignamos al usuario el rol de invitador invitado para enviar invitaciones.</span><span class="sxs-lookup"><span data-stu-id="d2977-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="d2977-109">No tiene que ser miembro del rol administrador global para enviar invitaciones.</span><span class="sxs-lookup"><span data-stu-id="d2977-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="d2977-110">De forma predeterminada, los usuarios normales también pueden invocar la API de invitación, a menos que un administrador global haya deshabilitado las invitaciones para los usuarios normales.</span><span class="sxs-lookup"><span data-stu-id="d2977-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="d2977-111">Un usuario también puede invocar la API mediante Azure Portal o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2977-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="d2977-112">Este es un ejemplo que muestra cómo usar PowerShell para agregar un usuario al rol Invitador de personas:</span><span class="sxs-lookup"><span data-stu-id="d2977-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="d2977-113">Controlar quién puede invitar</span><span class="sxs-lookup"><span data-stu-id="d2977-113">Control who can invite</span></span>

![Controlar el procedimiento de invitación](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="d2977-115">Gracias a la colaboración B2B de Azure AD, el administrador de inquilinos puede establecer las siguientes directivas de invitación:</span><span class="sxs-lookup"><span data-stu-id="d2977-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="d2977-116">Desactivar invitaciones</span><span class="sxs-lookup"><span data-stu-id="d2977-116">Turn off invitations</span></span>
- <span data-ttu-id="d2977-117">Solo los administradores y usuarios del rol Invitador de personas pueden invitar</span><span class="sxs-lookup"><span data-stu-id="d2977-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="d2977-118">Los administradores, el rol Invitador de personas y los miembros pueden invitar</span><span class="sxs-lookup"><span data-stu-id="d2977-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="d2977-119">Todos los usuarios, incluidos los invitados, pueden invitar</span><span class="sxs-lookup"><span data-stu-id="d2977-119">All users, including guests, can invite</span></span>

<span data-ttu-id="d2977-120">De forma predeterminada, los inquilinos se establecen en #4.</span><span class="sxs-lookup"><span data-stu-id="d2977-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="d2977-121">(Todos los usuarios, incluidos los invitados, pueden invitar a usuarios B2B).</span><span class="sxs-lookup"><span data-stu-id="d2977-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2977-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2977-122">Next steps</span></span>

<span data-ttu-id="d2977-123">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d2977-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d2977-124">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="d2977-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d2977-125">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="d2977-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d2977-126">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="d2977-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d2977-127">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="d2977-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="d2977-128">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2977-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d2977-129">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="d2977-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d2977-130">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="d2977-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d2977-131">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="d2977-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d2977-132">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="d2977-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d2977-133">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="d2977-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
