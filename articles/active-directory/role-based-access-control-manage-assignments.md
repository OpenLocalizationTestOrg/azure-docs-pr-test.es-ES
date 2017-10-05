---
title: "Visualización de asignaciones de acceso a recursos de Azure | Microsoft Docs"
description: "Visualización y administración de todas las asignaciones de control de acceso basado en rol de cualquier usuario o grupo en Azure Portal"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="5db87-103">Visualización de asignaciones de acceso para usuarios y grupos en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5db87-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5db87-104">Administración del acceso por usuario o grupo</span><span class="sxs-lookup"><span data-stu-id="5db87-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="5db87-105">Administración del acceso por recurso</span><span class="sxs-lookup"><span data-stu-id="5db87-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="5db87-106">Gracias al control de acceso basado en rol (RBAC) de Azure Active Directory (Azure AD), puede administrar el acceso a los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db87-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="5db87-107">El acceso que se asigna con RBAC es específico porque se pueden restringir los permisos de dos formas:</span><span class="sxs-lookup"><span data-stu-id="5db87-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="5db87-108">**Ámbito** : las asignaciones de roles RBAC se limitan a una suscripción, un grupo de recursos o un recurso específicos.</span><span class="sxs-lookup"><span data-stu-id="5db87-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="5db87-109">Un usuario con acceso a un único recurso no puede tener acceso a otros recursos de la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="5db87-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="5db87-110">**Rol** : dentro del ámbito de la asignación, se limita el acceso aún más mediante la asignación de un rol.</span><span class="sxs-lookup"><span data-stu-id="5db87-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="5db87-111">Los roles pueden ser generales, como propietarios, o específicos, como lectores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5db87-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="5db87-112">Asimismo, solo pueden asignarse desde dentro de la suscripción, el grupo de recursos o el recurso que esté en el ámbito de la asignación.</span><span class="sxs-lookup"><span data-stu-id="5db87-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="5db87-113">No obstante, puede ver todas las asignaciones de acceso de un usuario o grupo determinado en un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="5db87-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="5db87-114">Puede tener hasta 2000 asignaciones de roles en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="5db87-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="5db87-115">Para administrar el acceso a los recursos, consulte [Uso de asignaciones de roles para administrar el acceso a los recursos de la suscripción de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5db87-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="5db87-116">Visualización de asignaciones de acceso</span><span class="sxs-lookup"><span data-stu-id="5db87-116">View access assignments</span></span>
<span data-ttu-id="5db87-117">Para buscar las asignaciones de acceso de un único usuario o grupo, empiece en [Azure Portal](http://portal.azure.com)de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5db87-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="5db87-118">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5db87-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="5db87-119">Si esta opción no está visible en la lista de navegación, seleccione **More Services** (Más servicios) y luego desplácese hacia abajo hasta encontrar **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5db87-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="5db87-120">Seleccione **Usuarios y grupos** y luego **Todos los usuarios** o **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="5db87-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="5db87-121">En este ejemplo, nos centramos en los usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="5db87-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="5db87-122">![Captura de pantalla de administración de usuarios y grupos en Azure Active Directory](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="5db87-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="5db87-123">Busque el usuario por nombre o nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="5db87-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="5db87-124">Seleccione **Recursos de Azure** en la hoja de usuario.</span><span class="sxs-lookup"><span data-stu-id="5db87-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="5db87-125">Aparecen todas las asignaciones de dicho usuario.</span><span class="sxs-lookup"><span data-stu-id="5db87-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="5db87-126">Permisos de lectura para ver las asignaciones</span><span class="sxs-lookup"><span data-stu-id="5db87-126">Read permissions to view assignments</span></span>
<span data-ttu-id="5db87-127">Esta página solo muestra las asignaciones de acceso que tiene permiso para leer.</span><span class="sxs-lookup"><span data-stu-id="5db87-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="5db87-128">Por ejemplo, tiene acceso de lectura a la suscripción A y va a la hoja de recursos de Azure para comprobar las asignaciones de un usuario.</span><span class="sxs-lookup"><span data-stu-id="5db87-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="5db87-129">Puede ver sus asignaciones de acceso de la suscripción A, pero no verá que también tiene asignaciones de acceso de la B.</span><span class="sxs-lookup"><span data-stu-id="5db87-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="5db87-130">Eliminación de asignaciones de acceso</span><span class="sxs-lookup"><span data-stu-id="5db87-130">Delete access assignments</span></span>
<span data-ttu-id="5db87-131">En esta hoja, puede eliminar las asignaciones de acceso que se asignaron directamente a un usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="5db87-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="5db87-132">Si la asignación de acceso se hereda de un grupo primario, debe ir a la suscripción o al recurso y administrarla allí.</span><span class="sxs-lookup"><span data-stu-id="5db87-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="5db87-133">En la lista de todas las asignaciones de acceso de un usuario o grupo, seleccione la que quiera eliminar.</span><span class="sxs-lookup"><span data-stu-id="5db87-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="5db87-134">Seleccione **Quitar** y después **Sí** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="5db87-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="5db87-135">![Captura de pantalla de eliminación de asignación de acceso](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="5db87-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5db87-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5db87-136">Next steps</span></span>

* <span data-ttu-id="5db87-137">Vea una introducción al control de acceso basado en rol en [Uso de asignaciones de roles para administrar el acceso a los recursos de la suscripción de Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5db87-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="5db87-138">Consulte los [roles integrados en RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5db87-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

