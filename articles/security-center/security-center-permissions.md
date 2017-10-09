---
title: aaaPermissions en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este artículo se explica cómo el centro de seguridad de Azure usa toousers de permisos de tooassign de control de acceso basado en roles e identifica Hola permitida acciones para cada rol."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="fbdbb-103">Permisos en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="fbdbb-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="fbdbb-104">Centro de seguridad de Azure usa [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md), lo que proporciona [roles integrados](../active-directory/role-based-access-built-in-roles.md) que se puede asignar toousers, grupos y servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="fbdbb-105">Centro de seguridad evalúa la configuración de Hola de los problemas de seguridad de recursos tooidentify y vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="fbdbb-106">En el centro de seguridad, sólo verá información relacionada con recursos tooa cuando se le asigna Hola rol de propietario, Colaborador o lector de hello suscripción o grupo de recursos que pertenece el recurso.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="fbdbb-107">En los roles de toothese adición, hay dos funciones específicas de centro de seguridad:</span><span class="sxs-lookup"><span data-stu-id="fbdbb-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="fbdbb-108">**Lector de seguridad**: un usuario que pertenece el rol de toothis tiene ver derechos tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="fbdbb-109">usuario de Hello puede ver las recomendaciones, alertas, una directiva de seguridad y los Estados de seguridad, pero no puede realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="fbdbb-110">**Administrador de seguridad**: un usuario que pertenece el rol de toothis tiene Hola mismo derechos como Hola lector de seguridad y puede actualizar también la directiva de seguridad de Hola y descartar las alertas y las recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="fbdbb-111">roles de seguridad de Hello, lector de seguridad y el Administrador de seguridad, tienen acceso sólo en el centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="fbdbb-112">roles de seguridad de Hello no tiene acceso a las áreas de servicio de tooother de Azure como almacenamiento, Web y móviles o Internet de las cosas.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="fbdbb-113">Roles y acciones permitidas</span><span class="sxs-lookup"><span data-stu-id="fbdbb-113">Roles and allowed actions</span></span>

<span data-ttu-id="fbdbb-114">Hello siguiente tabla muestra los roles y las acciones permitidas en el centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="fbdbb-115">Una X indica que se permite la acción de Hola para ese rol.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="fbdbb-116">Rol</span><span class="sxs-lookup"><span data-stu-id="fbdbb-116">Role</span></span> | <span data-ttu-id="fbdbb-117">Editar directivas de seguridad</span><span class="sxs-lookup"><span data-stu-id="fbdbb-117">Edit security policy</span></span> | <span data-ttu-id="fbdbb-118">Aplicar recomendaciones de seguridad en un recurso</span><span class="sxs-lookup"><span data-stu-id="fbdbb-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="fbdbb-119">Descartar alertas y recomendaciones</span><span class="sxs-lookup"><span data-stu-id="fbdbb-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="fbdbb-120">Ver alertas y recomendaciones</span><span class="sxs-lookup"><span data-stu-id="fbdbb-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="fbdbb-121">Propietario de la suscripción</span><span class="sxs-lookup"><span data-stu-id="fbdbb-121">Subscription Owner</span></span> | <span data-ttu-id="fbdbb-122">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-122">X</span></span> | <span data-ttu-id="fbdbb-123">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-123">X</span></span> | <span data-ttu-id="fbdbb-124">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-124">X</span></span> | <span data-ttu-id="fbdbb-125">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-125">X</span></span> |
| <span data-ttu-id="fbdbb-126">Colaborador de la suscripción</span><span class="sxs-lookup"><span data-stu-id="fbdbb-126">Subscription Contributor</span></span> | <span data-ttu-id="fbdbb-127">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-127">X</span></span> | <span data-ttu-id="fbdbb-128">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-128">X</span></span> | <span data-ttu-id="fbdbb-129">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-129">X</span></span> | <span data-ttu-id="fbdbb-130">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-130">X</span></span> |
| <span data-ttu-id="fbdbb-131">Propietario del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fbdbb-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="fbdbb-132">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-132">X</span></span> | -- | <span data-ttu-id="fbdbb-133">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-133">X</span></span> |
| <span data-ttu-id="fbdbb-134">Colaborador del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fbdbb-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="fbdbb-135">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-135">X</span></span> | -- | <span data-ttu-id="fbdbb-136">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-136">X</span></span> |
| <span data-ttu-id="fbdbb-137">Lector</span><span class="sxs-lookup"><span data-stu-id="fbdbb-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="fbdbb-138">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-138">X</span></span> |
| <span data-ttu-id="fbdbb-139">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="fbdbb-139">Security Administrator</span></span> | <span data-ttu-id="fbdbb-140">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-140">X</span></span> | -- | <span data-ttu-id="fbdbb-141">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-141">X</span></span> | <span data-ttu-id="fbdbb-142">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-142">X</span></span> |
| <span data-ttu-id="fbdbb-143">Lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="fbdbb-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="fbdbb-144">X</span><span class="sxs-lookup"><span data-stu-id="fbdbb-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="fbdbb-145">Se recomienda que se definan Hola rol menos permisivo necesarios para los usuarios toocomplete sus tareas.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="fbdbb-146">Por ejemplo, asigne toousers de rol de lector de Hola que solo necesita tooview información sobre el estado de seguridad de Hola de un recurso pero no realizar acciones como aplicar recomendaciones o editar directivas.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fbdbb-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbdbb-147">Next steps</span></span>
<span data-ttu-id="fbdbb-148">Este artículo explica cómo el centro de seguridad utiliza RBAC tooassign permisos toousers e identificado Hola permitida acciones para cada rol.</span><span class="sxs-lookup"><span data-stu-id="fbdbb-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="fbdbb-149">Ahora que está familiarizado con las asignaciones de roles de hello necesarios toomonitor Hola estado de seguridad de su suscripción, editar las directivas de seguridad y aplicar las recomendaciones, obtenga información acerca de cómo:</span><span class="sxs-lookup"><span data-stu-id="fbdbb-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="fbdbb-150">Establecer directivas de seguridad en Security Center</span><span class="sxs-lookup"><span data-stu-id="fbdbb-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="fbdbb-151">Administrar recomendaciones de seguridad en Security Center</span><span class="sxs-lookup"><span data-stu-id="fbdbb-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="fbdbb-152">Supervisar el estado de seguridad de Hola de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="fbdbb-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="fbdbb-153">Administrar y responder a alertas de toosecurity en el centro de seguridad</span><span class="sxs-lookup"><span data-stu-id="fbdbb-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="fbdbb-154">Supervisar soluciones de seguridad de asociados</span><span class="sxs-lookup"><span data-stu-id="fbdbb-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
