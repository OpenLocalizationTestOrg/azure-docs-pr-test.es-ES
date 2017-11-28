---
title: asignaciones de acceso de recursos de Azure aaaView | Documentos de Microsoft
description: Ver y administrar todas las asignaciones de Control de acceso basado en roles de Hola para cualquier usuario o grupo en hello portal de Azure
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
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="ebc24-103">Ver las asignaciones de acceso para usuarios y grupos en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ebc24-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebc24-104">Administración del acceso por usuario o grupo</span><span class="sxs-lookup"><span data-stu-id="ebc24-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="ebc24-105">Administración del acceso por recurso</span><span class="sxs-lookup"><span data-stu-id="ebc24-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="ebc24-106">Con control de acceso basado en roles (RBAC) en hello Azure Active Directory (Azure AD), puede administrar el acceso tooyour Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="ebc24-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="ebc24-107">Acceso asignado con RBAC es específica porque hay dos maneras puede limitar los permisos de hello:</span><span class="sxs-lookup"><span data-stu-id="ebc24-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="ebc24-108">**Ámbito:** las asignaciones de roles RBAC son suscripción específica de tooa con ámbito, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="ebc24-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="ebc24-109">Un usuario tiene acceso tooa único recurso no puede tener acceso a otros recursos en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="ebc24-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="ebc24-110">**Rol:** en el ámbito de Hola de asignación de hello, se restringe el acceso aún más mediante la asignación de un rol.</span><span class="sxs-lookup"><span data-stu-id="ebc24-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="ebc24-111">Los roles pueden ser generales, como propietarios, o específicos, como lectores de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ebc24-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="ebc24-112">Roles solo pueden asignarse desde dentro de la suscripción de hello, el grupo de recursos o el recurso que es el ámbito de hello para la asignación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebc24-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="ebc24-113">Pero puede ver todas las asignaciones de acceso de Hola para un usuario determinado o un grupo en un único lugar.</span><span class="sxs-lookup"><span data-stu-id="ebc24-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="ebc24-114">Puede tener hasta las asignaciones de roles de too2000 en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="ebc24-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="ebc24-115">Obtener más información acerca de cómo demasiado[usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ebc24-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="ebc24-116">Visualización de asignaciones de acceso</span><span class="sxs-lookup"><span data-stu-id="ebc24-116">View access assignments</span></span>
<span data-ttu-id="ebc24-117">toolook asignaciones de acceso de Hola para un único usuario o grupo, iniciar en Azure Active Directory en hello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebc24-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="ebc24-118">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ebc24-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="ebc24-119">Si esta opción no está visible en la lista de navegación, seleccione **más servicios** y, a continuación, desplácese hacia abajo toofind **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ebc24-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="ebc24-120">Seleccione **Usuarios y grupos** y luego **Todos los usuarios** o **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="ebc24-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="ebc24-121">En este ejemplo, nos centramos en los usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="ebc24-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="ebc24-122">![Captura de pantalla de administración de usuarios y grupos en Azure Active Directory](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="ebc24-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="ebc24-123">Buscar usuario Hola por nombre o nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="ebc24-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="ebc24-124">Seleccione **recursos de Azure** en la hoja de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebc24-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="ebc24-125">Aparecen todas las asignaciones de acceso de Hola para dicho usuario.</span><span class="sxs-lookup"><span data-stu-id="ebc24-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="ebc24-126">Asignaciones de tooview de permisos de lectura</span><span class="sxs-lookup"><span data-stu-id="ebc24-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="ebc24-127">Esta página solo muestra las asignaciones de acceso de Hola que dispone de permiso tooread.</span><span class="sxs-lookup"><span data-stu-id="ebc24-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="ebc24-128">Por ejemplo, puede tener acceso de lectura toosubscription A y seguir toocheck de hoja de recursos de Azure toohello las asignaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="ebc24-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="ebc24-129">Puede ver sus asignaciones de acceso de la suscripción A, pero no verá que también tiene asignaciones de acceso de la B.</span><span class="sxs-lookup"><span data-stu-id="ebc24-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="ebc24-130">Eliminación de asignaciones de acceso</span><span class="sxs-lookup"><span data-stu-id="ebc24-130">Delete access assignments</span></span>
<span data-ttu-id="ebc24-131">En esta hoja, puede eliminar asignaciones de acceso que se asignaron directamente tooa usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="ebc24-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="ebc24-132">Si la asignación de acceso de Hola se heredó de un grupo primario, es necesario toogo toohello recursos o suscripción y administrar una asignación de hello no existe.</span><span class="sxs-lookup"><span data-stu-id="ebc24-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="ebc24-133">En lista de Hola de todas las asignaciones de acceso de Hola para un usuario o grupo, seleccione Hola uno desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="ebc24-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="ebc24-134">Seleccione **quitar** y, a continuación, **Sí** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ebc24-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="ebc24-135">![Captura de pantalla de eliminación de asignación de acceso](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="ebc24-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebc24-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebc24-136">Next steps</span></span>

* <span data-ttu-id="ebc24-137">Empezar a trabajar con el Control de acceso basado en roles demasiado[usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ebc24-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="ebc24-138">Vea hello [funciones integradas de RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="ebc24-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

