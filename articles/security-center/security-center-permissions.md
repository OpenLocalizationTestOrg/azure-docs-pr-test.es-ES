---
title: Permisos en Azure Security Center | Microsoft Docs
description: "En este artículo se explica cómo Azure Security Center usa el control de acceso basado en roles para asignar permisos a los usuarios e identifica las acciones permitidas para cada rol."
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
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="78135-103">Permisos en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="78135-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="78135-104">Azure Security Center usa el [control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md), que proporciona [roles integrados](../active-directory/role-based-access-built-in-roles.md) que se pueden asignar a usuarios, grupos y servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="78135-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="78135-105">Security Center evalúa la configuración de los recursos para identificar problemas de seguridad y vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="78135-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="78135-106">En Security Center, solo se muestra información relacionada con un recurso cuando tiene asignado el rol de Propietario, Colaborador o Lector a la suscripción o grupo de recursos al que pertenece un recurso.</span><span class="sxs-lookup"><span data-stu-id="78135-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="78135-107">Además de estos roles, hay dos roles específicos de Security Center:</span><span class="sxs-lookup"><span data-stu-id="78135-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="78135-108">**Lector de seguridad**: un usuario que pertenece a este rol tiene derechos de visualización en Security Center.</span><span class="sxs-lookup"><span data-stu-id="78135-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="78135-109">El usuario puede ver las recomendaciones, las alertas, una directiva de seguridad y los estados de seguridad, pero no puede realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="78135-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="78135-110">**Administrador de seguridad**: un usuario que pertenece a este rol tiene los mismos derechos que el lector de seguridad, y puede actualizar la directiva de seguridad y descartar las alertas y las recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="78135-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="78135-111">Los roles de seguridad Lector de seguridad y Administrador de seguridad solo tienen acceso a Security Center.</span><span class="sxs-lookup"><span data-stu-id="78135-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="78135-112">Los roles de seguridad descritos no tienen acceso a otras áreas de servicio de Azure, como Storage, Web y móvil o Internet de las cosas.</span><span class="sxs-lookup"><span data-stu-id="78135-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="78135-113">Roles y acciones permitidas</span><span class="sxs-lookup"><span data-stu-id="78135-113">Roles and allowed actions</span></span>

<span data-ttu-id="78135-114">En la siguiente tabla se muestran los roles y las acciones permitidas en Security Center.</span><span class="sxs-lookup"><span data-stu-id="78135-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="78135-115">Una X indica que la acción se permite para ese rol.</span><span class="sxs-lookup"><span data-stu-id="78135-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="78135-116">Rol</span><span class="sxs-lookup"><span data-stu-id="78135-116">Role</span></span> | <span data-ttu-id="78135-117">Editar directivas de seguridad</span><span class="sxs-lookup"><span data-stu-id="78135-117">Edit security policy</span></span> | <span data-ttu-id="78135-118">Aplicar recomendaciones de seguridad en un recurso</span><span class="sxs-lookup"><span data-stu-id="78135-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="78135-119">Descartar alertas y recomendaciones</span><span class="sxs-lookup"><span data-stu-id="78135-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="78135-120">Ver alertas y recomendaciones</span><span class="sxs-lookup"><span data-stu-id="78135-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="78135-121">Propietario de la suscripción</span><span class="sxs-lookup"><span data-stu-id="78135-121">Subscription Owner</span></span> | <span data-ttu-id="78135-122">X</span><span class="sxs-lookup"><span data-stu-id="78135-122">X</span></span> | <span data-ttu-id="78135-123">X</span><span class="sxs-lookup"><span data-stu-id="78135-123">X</span></span> | <span data-ttu-id="78135-124">X</span><span class="sxs-lookup"><span data-stu-id="78135-124">X</span></span> | <span data-ttu-id="78135-125">X</span><span class="sxs-lookup"><span data-stu-id="78135-125">X</span></span> |
| <span data-ttu-id="78135-126">Colaborador de la suscripción</span><span class="sxs-lookup"><span data-stu-id="78135-126">Subscription Contributor</span></span> | <span data-ttu-id="78135-127">X</span><span class="sxs-lookup"><span data-stu-id="78135-127">X</span></span> | <span data-ttu-id="78135-128">X</span><span class="sxs-lookup"><span data-stu-id="78135-128">X</span></span> | <span data-ttu-id="78135-129">X</span><span class="sxs-lookup"><span data-stu-id="78135-129">X</span></span> | <span data-ttu-id="78135-130">X</span><span class="sxs-lookup"><span data-stu-id="78135-130">X</span></span> |
| <span data-ttu-id="78135-131">Propietario del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="78135-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="78135-132">X</span><span class="sxs-lookup"><span data-stu-id="78135-132">X</span></span> | -- | <span data-ttu-id="78135-133">X</span><span class="sxs-lookup"><span data-stu-id="78135-133">X</span></span> |
| <span data-ttu-id="78135-134">Colaborador del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="78135-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="78135-135">X</span><span class="sxs-lookup"><span data-stu-id="78135-135">X</span></span> | -- | <span data-ttu-id="78135-136">X</span><span class="sxs-lookup"><span data-stu-id="78135-136">X</span></span> |
| <span data-ttu-id="78135-137">Lector</span><span class="sxs-lookup"><span data-stu-id="78135-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="78135-138">X</span><span class="sxs-lookup"><span data-stu-id="78135-138">X</span></span> |
| <span data-ttu-id="78135-139">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="78135-139">Security Administrator</span></span> | <span data-ttu-id="78135-140">X</span><span class="sxs-lookup"><span data-stu-id="78135-140">X</span></span> | -- | <span data-ttu-id="78135-141">X</span><span class="sxs-lookup"><span data-stu-id="78135-141">X</span></span> | <span data-ttu-id="78135-142">X</span><span class="sxs-lookup"><span data-stu-id="78135-142">X</span></span> |
| <span data-ttu-id="78135-143">Lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="78135-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="78135-144">X</span><span class="sxs-lookup"><span data-stu-id="78135-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="78135-145">Es recomendable que asigne el rol de menos permisos que los usuarios necesiten para realizar sus tareas.</span><span class="sxs-lookup"><span data-stu-id="78135-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="78135-146">Por ejemplo, asigne el rol Lector a los usuarios que solo necesiten ver información sobre el estado de seguridad de los recursos, pero no llevar a cabo acciones como aplicar recomendaciones o editar directivas.</span><span class="sxs-lookup"><span data-stu-id="78135-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="78135-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78135-147">Next steps</span></span>
<span data-ttu-id="78135-148">En este artículo se ha explicado cómo Security Center usa RBAC para asignar permisos a los usuarios e identifica las acciones permitidas para cada rol.</span><span class="sxs-lookup"><span data-stu-id="78135-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="78135-149">Ahora que ya está familiarizado con las asignaciones de roles necesarios para supervisar el estado de seguridad de su suscripción, editar directivas de seguridad y aplicar recomendaciones, aprenderá los siguientes conceptos:</span><span class="sxs-lookup"><span data-stu-id="78135-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="78135-150">Establecer directivas de seguridad en Security Center</span><span class="sxs-lookup"><span data-stu-id="78135-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="78135-151">Administrar recomendaciones de seguridad en Security Center</span><span class="sxs-lookup"><span data-stu-id="78135-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="78135-152">Supervisar el estado de seguridad de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="78135-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="78135-153">Responder a alertas de seguridad en Security Center</span><span class="sxs-lookup"><span data-stu-id="78135-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="78135-154">Supervisar soluciones de seguridad de asociados</span><span class="sxs-lookup"><span data-stu-id="78135-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
