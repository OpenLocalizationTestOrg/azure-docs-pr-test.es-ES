---
title: Control de acceso basado en aaaRole Hola portal de Azure | Documentos de Microsoft
description: "Introducción a administración de acceso con Control de acceso basado en roles en hello Portal de Azure. Usar los recursos de rol asignaciones tooassign permisos tooyour."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="2a6c9-104">Usar recursos de suscripción de Azure de Role-Based Access Control toomanage acceso tooyour</span><span class="sxs-lookup"><span data-stu-id="2a6c9-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a6c9-105">Administración del acceso por usuario o grupo</span><span class="sxs-lookup"><span data-stu-id="2a6c9-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="2a6c9-106">Administrar el acceso por recurso</span><span class="sxs-lookup"><span data-stu-id="2a6c9-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="2a6c9-107">El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso para Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="2a6c9-108">Usar RBAC, puede conceder únicamente cantidad de Hola de acceso que los usuarios necesitan tooperform sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="2a6c9-109">En este artículo le ayuda a ponerse en marcha con RBAC en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="2a6c9-110">Si desea más detalles sobre cómo RBAC ayuda a administrar el acceso, consulte [¿Qué es el control de acceso basado en rol?](role-based-access-control-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="2a6c9-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="2a6c9-111">Dentro de cada suscripción, puede conceder too2000 asignaciones de rol.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="2a6c9-112">Vista de acceso</span><span class="sxs-lookup"><span data-stu-id="2a6c9-112">View access</span></span>
<span data-ttu-id="2a6c9-113">Puede ver quién tiene acceso tooa recursos, grupo de recursos o suscripción de su hoja principal en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2a6c9-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2a6c9-114">Por ejemplo, queremos toosee que tenga acceso tooone nuestro de grupos de recursos:</span><span class="sxs-lookup"><span data-stu-id="2a6c9-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="2a6c9-115">Seleccione **grupos de recursos** en barra de navegación de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="2a6c9-116">![Grupos de recursos - icono](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="2a6c9-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="2a6c9-117">Nombre seleccione Hola Hola del grupo de recursos de hello **grupos de recursos** hoja.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="2a6c9-118">Seleccione **(de índices IAM) de control de acceso** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="2a6c9-119">hoja de control de acceso de Hello enumera todos los usuarios, grupos y las aplicaciones que se han concedido el grupo de recursos de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Hoja de usuarios: acceso heredado frente a asignado (captura de pantalla)](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="2a6c9-121">Tenga en cuenta que algunos roles tienen como ámbito demasiado**este recurso** mientras que otras son **Inherited** desde otro ámbito.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="2a6c9-122">Acceso se asigna a específicamente el grupo de recursos toohello o se hereda de una suscripción de asignación toohello primario.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="2a6c9-123">Los administradores de suscripciones clásico y coadministradores se consideran los propietarios de suscripción de hello en el nuevo modelo de RBAC Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="2a6c9-124">Agregación de acceso</span><span class="sxs-lookup"><span data-stu-id="2a6c9-124">Add Access</span></span>
<span data-ttu-id="2a6c9-125">Conceder acceso desde dentro de recurso de hello, grupo de recursos o suscripción de ámbito de Hola Hola de asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="2a6c9-126">Seleccione **agregar** en el módulo de control de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="2a6c9-127">Rol de hello SELECT que desea tooassign de hello **seleccione un rol** hoja.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="2a6c9-128">Seleccione usuario hello, grupo o aplicación en el directorio que desee toogrant acceso a.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="2a6c9-129">Puede buscar directorio de hello con nombres para mostrar, direcciones de correo electrónico y los identificadores de objeto.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Hoja Agregar usuarios: búsqueda (captura de pantalla)](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="2a6c9-131">Seleccione **Aceptar** asignación de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="2a6c9-132">Hola **Agregar usuario** emergente realiza un seguimiento de progreso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="2a6c9-133">![Barra de progreso Agregando usuario: captura de pantalla](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="2a6c9-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="2a6c9-134">Después de agregar correctamente una asignación de roles, que aparecerá en hello **usuarios** hoja.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="2a6c9-135">Eliminación de acceso</span><span class="sxs-lookup"><span data-stu-id="2a6c9-135">Remove Access</span></span>
1. <span data-ttu-id="2a6c9-136">Mantenga el cursor sobre el nombre de asignación de Hola que desea tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="2a6c9-137">Nombre de toohello siguiente aparece una casilla.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="2a6c9-138">Usar Hola casillas tooselect uno o más asignaciones de roles.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="2a6c9-139">Seleccione **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="2a6c9-140">Seleccione **Sí** eliminación de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="2a6c9-141">Las asignaciones heredadas no se pueden quitar.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="2a6c9-142">Si necesita tooremove una asignación heredada, deberá toodo en hello ámbito donde se creó la asignación de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="2a6c9-143">Hola **ámbito** columna, junto demasiado**Inherited** hay un vínculo que le guíe toohello recursos que se asignó este rol.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="2a6c9-144">Vaya a la lista de recursos de toohello asignación de roles de tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Hoja de usuario: acceso heredado deshabilita el botón de eliminación (captura de pantalla)](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="2a6c9-146">Acceso a toomanage de otra herramientas</span><span class="sxs-lookup"><span data-stu-id="2a6c9-146">Other tools toomanage access</span></span>
<span data-ttu-id="2a6c9-147">Puede asignar roles y administrar el acceso con comandos de RBAC de Azure en herramientas distintas Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="2a6c9-148">Siga Hola vínculos toolearn más información acerca de los requisitos previos de Hola y empezar a trabajar con comandos de hello RBAC de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6c9-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="2a6c9-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a6c9-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="2a6c9-150">Interfaz de la línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="2a6c9-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="2a6c9-151">API DE REST</span><span class="sxs-lookup"><span data-stu-id="2a6c9-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="2a6c9-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a6c9-152">Next Steps</span></span>
* [<span data-ttu-id="2a6c9-153">Creación de un informe del historial de cambios de acceso</span><span class="sxs-lookup"><span data-stu-id="2a6c9-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="2a6c9-154">Vea hello [funciones integradas de RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="2a6c9-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="2a6c9-155">Defina sus propios [Custom Roles in Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="2a6c9-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

