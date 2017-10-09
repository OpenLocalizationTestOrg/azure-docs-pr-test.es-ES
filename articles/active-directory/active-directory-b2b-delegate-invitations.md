---
title: "aaaDelegate invitaciones para la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
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
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="e2a1d-103">Delegación de invitaciones de la colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2a1d-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="e2a1d-104">Con la colaboración de negocio a negocio (B2B) de Azure Active Directory (Azure AD), no es necesario toobe un invitaciones de toosend administrador global.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="e2a1d-105">En su lugar, puede usar las directivas y delegar toousers invitaciones cuyas funciones permitan toosend invitaciones.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="e2a1d-106">Un importante nueva manera toodelegate invitado usuario invitaciones es a través de rol de autor de la invitación invitado Hola.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="e2a1d-107">Rol de invitador de personas</span><span class="sxs-lookup"><span data-stu-id="e2a1d-107">Guest Inviter role</span></span>
<span data-ttu-id="e2a1d-108">Podemos asignar Hola usuario tooGuest invitaciones de toosend de rol de autor de la invitación.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="e2a1d-109">No tiene miembros toobe de invitaciones de toosend de rol de administrador global de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="e2a1d-110">De forma predeterminada, los usuarios regulares también pueden invocar API de invitación de Hola a menos que un administrador global deshabilitado invitaciones para que los usuarios normales.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="e2a1d-111">Un usuario también puede invocar la API de hello usando Hola portal de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="e2a1d-112">Este es un ejemplo que muestra cómo toouse PowerShell tooadd un rol de usuario toohello Invitador invitado:</span><span class="sxs-lookup"><span data-stu-id="e2a1d-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="e2a1d-113">Controlar quién puede invitar</span><span class="sxs-lookup"><span data-stu-id="e2a1d-113">Control who can invite</span></span>

![Control cómo tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="e2a1d-115">Con la colaboración B2B de Azure AD, un administrador de inquilinos puede establecer las siguientes directivas de invitación de hello:</span><span class="sxs-lookup"><span data-stu-id="e2a1d-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="e2a1d-116">Desactivar invitaciones</span><span class="sxs-lookup"><span data-stu-id="e2a1d-116">Turn off invitations</span></span>
- <span data-ttu-id="e2a1d-117">Pueden invitar solo los administradores y usuarios en función de invitado Invitador Hola</span><span class="sxs-lookup"><span data-stu-id="e2a1d-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="e2a1d-118">Pueden invitar administradores, rol de autor de la invitación invitado hello y miembros</span><span class="sxs-lookup"><span data-stu-id="e2a1d-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="e2a1d-119">Todos los usuarios, incluidos los invitados, pueden invitar</span><span class="sxs-lookup"><span data-stu-id="e2a1d-119">All users, including guests, can invite</span></span>

<span data-ttu-id="e2a1d-120">De forma predeterminada, los inquilinos se establecen demasiado n.º 4.</span><span class="sxs-lookup"><span data-stu-id="e2a1d-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="e2a1d-121">(Todos los usuarios, incluidos los invitados, pueden invitar a usuarios B2B).</span><span class="sxs-lookup"><span data-stu-id="e2a1d-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2a1d-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2a1d-122">Next steps</span></span>

<span data-ttu-id="e2a1d-123">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e2a1d-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e2a1d-124">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e2a1d-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e2a1d-125">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="e2a1d-126">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="e2a1d-127">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="e2a1d-128">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2a1d-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="e2a1d-129">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="e2a1d-130">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="e2a1d-131">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="e2a1d-132">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="e2a1d-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="e2a1d-133">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e2a1d-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
