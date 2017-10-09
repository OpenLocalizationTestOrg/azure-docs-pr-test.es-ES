---
title: aaaAdd los propietarios y los usuarios en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: Agregar propietarios y usuarios en los laboratorios de desarrollo y pruebas de Azure mediante el portal de Azure de Hola o PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="f05ed-103">Adición de propietarios y usuarios en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f05ed-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="f05ed-104">El acceso a Azure DevTest Labs se controla mediante el [control de acceso basado en rol (RBAC) de Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f05ed-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="f05ed-105">Usar RBAC, puede separar los derechos en el equipo en *roles* que se le concede únicamente cantidad de Hola de acceso necesarios toousers tooperform sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="f05ed-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="f05ed-106">Tres de estos roles RBAC son *Propietario*, *Usuario de DevTest Labs* y *Colaborador*.</span><span class="sxs-lookup"><span data-stu-id="f05ed-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="f05ed-107">En este artículo, aprenderá qué acciones pueden realizarse en cada una de estas tres funciones principales RBAC Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="f05ed-108">Desde allí, aprenderá cómo práctica de tooadd usuarios tooa: tanto a través de Hola portal y a través de un script de PowerShell y cómo los usuarios de tooadd de Hola a nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="f05ed-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="f05ed-109">Acciones que se pueden realizar en cada rol</span><span class="sxs-lookup"><span data-stu-id="f05ed-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="f05ed-110">Hay tres roles principales que puede asignar a un usuario:</span><span class="sxs-lookup"><span data-stu-id="f05ed-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="f05ed-111">Propietario</span><span class="sxs-lookup"><span data-stu-id="f05ed-111">Owner</span></span>
* <span data-ttu-id="f05ed-112">Usuario de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f05ed-112">DevTest Labs User</span></span>
* <span data-ttu-id="f05ed-113">Colaborador</span><span class="sxs-lookup"><span data-stu-id="f05ed-113">Contributor</span></span>

<span data-ttu-id="f05ed-114">Hello tabla siguiente muestra las acciones de Hola que se pueden realizar los usuarios en cada uno de estos roles:</span><span class="sxs-lookup"><span data-stu-id="f05ed-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="f05ed-115">**Acciones que pueden realizar los usuarios de este rol**</span><span class="sxs-lookup"><span data-stu-id="f05ed-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="f05ed-116">**Usuario de DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="f05ed-116">**DevTest Labs User**</span></span> | <span data-ttu-id="f05ed-117">**Propietario**</span><span class="sxs-lookup"><span data-stu-id="f05ed-117">**Owner**</span></span> | <span data-ttu-id="f05ed-118">**Colaborador**</span><span class="sxs-lookup"><span data-stu-id="f05ed-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f05ed-119">**Tareas de laboratorio**</span><span class="sxs-lookup"><span data-stu-id="f05ed-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="f05ed-120">Agregar laboratorio tooa de usuarios</span><span class="sxs-lookup"><span data-stu-id="f05ed-120">Add users tooa lab</span></span> |<span data-ttu-id="f05ed-121">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-121">No</span></span> |<span data-ttu-id="f05ed-122">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-122">Yes</span></span> |<span data-ttu-id="f05ed-123">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-123">No</span></span> |
| <span data-ttu-id="f05ed-124">Actualizar la configuración de costo</span><span class="sxs-lookup"><span data-stu-id="f05ed-124">Update cost settings</span></span> |<span data-ttu-id="f05ed-125">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-125">No</span></span> |<span data-ttu-id="f05ed-126">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-126">Yes</span></span> |<span data-ttu-id="f05ed-127">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-127">Yes</span></span> |
| <span data-ttu-id="f05ed-128">**Tareas base de máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="f05ed-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="f05ed-129">Agregar y quitar imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="f05ed-129">Add and remove custom images</span></span> |<span data-ttu-id="f05ed-130">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-130">No</span></span> |<span data-ttu-id="f05ed-131">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-131">Yes</span></span> |<span data-ttu-id="f05ed-132">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-132">Yes</span></span> |
| <span data-ttu-id="f05ed-133">Agregar, actualizar y eliminar las fórmulas</span><span class="sxs-lookup"><span data-stu-id="f05ed-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="f05ed-134">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-134">Yes</span></span> |<span data-ttu-id="f05ed-135">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-135">Yes</span></span> |<span data-ttu-id="f05ed-136">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-136">Yes</span></span> |
| <span data-ttu-id="f05ed-137">Incluir en la lista de permitidos imágenes de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f05ed-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="f05ed-138">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-138">No</span></span> |<span data-ttu-id="f05ed-139">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-139">Yes</span></span> |<span data-ttu-id="f05ed-140">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-140">Yes</span></span> |
| <span data-ttu-id="f05ed-141">**Tareas de la máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="f05ed-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="f05ed-142">Crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f05ed-142">Create VMs</span></span> |<span data-ttu-id="f05ed-143">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-143">Yes</span></span> |<span data-ttu-id="f05ed-144">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-144">Yes</span></span> |<span data-ttu-id="f05ed-145">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-145">Yes</span></span> |
| <span data-ttu-id="f05ed-146">Iniciar, detener y eliminar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f05ed-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="f05ed-147">Solo las máquinas virtuales creadas por el usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="f05ed-147">Only VMs created by hello user</span></span> |<span data-ttu-id="f05ed-148">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-148">Yes</span></span> |<span data-ttu-id="f05ed-149">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-149">Yes</span></span> |
| <span data-ttu-id="f05ed-150">Actualizar directivas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f05ed-150">Update VM policies</span></span> |<span data-ttu-id="f05ed-151">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-151">No</span></span> |<span data-ttu-id="f05ed-152">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-152">Yes</span></span> |<span data-ttu-id="f05ed-153">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-153">Yes</span></span> |
| <span data-ttu-id="f05ed-154">Agregar discos de datos o quitarlos en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f05ed-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="f05ed-155">Solo las máquinas virtuales creadas por el usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="f05ed-155">Only VMs created by hello user</span></span> |<span data-ttu-id="f05ed-156">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-156">Yes</span></span> |<span data-ttu-id="f05ed-157">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-157">Yes</span></span> |
| <span data-ttu-id="f05ed-158">**Tareas de artefacto**</span><span class="sxs-lookup"><span data-stu-id="f05ed-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="f05ed-159">Agregar y quitar repositorios de artefacto</span><span class="sxs-lookup"><span data-stu-id="f05ed-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="f05ed-160">No</span><span class="sxs-lookup"><span data-stu-id="f05ed-160">No</span></span> |<span data-ttu-id="f05ed-161">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-161">Yes</span></span> |<span data-ttu-id="f05ed-162">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-162">Yes</span></span> |
| <span data-ttu-id="f05ed-163">Aplicar artefactos</span><span class="sxs-lookup"><span data-stu-id="f05ed-163">Apply artifacts</span></span> |<span data-ttu-id="f05ed-164">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-164">Yes</span></span> |<span data-ttu-id="f05ed-165">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-165">Yes</span></span> |<span data-ttu-id="f05ed-166">Sí</span><span class="sxs-lookup"><span data-stu-id="f05ed-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="f05ed-167">Cuando un usuario crea una máquina virtual, ese usuario se le asigna automáticamente toohello **propietario** rol de hello creado máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f05ed-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="f05ed-168">Agregar un usuario o propietario en nivel de laboratorio de Hola</span><span class="sxs-lookup"><span data-stu-id="f05ed-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="f05ed-169">Los propietarios y los usuarios pueden agregarse en nivel de laboratorio de Hola a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f05ed-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="f05ed-170">Esto incluye a los usuarios externos con una [cuenta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)válida.</span><span class="sxs-lookup"><span data-stu-id="f05ed-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="f05ed-171">Hola pasos guiarle por proceso Hola para agregar un laboratorio de tooa propietario o usuario en los laboratorios de desarrollo y pruebas de Azure:</span><span class="sxs-lookup"><span data-stu-id="f05ed-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="f05ed-172">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f05ed-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f05ed-173">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f05ed-174">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="f05ed-175">En la hoja del laboratorio de hello, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="f05ed-176">En hello **configuración** hoja, seleccione **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="f05ed-177">En hello **usuarios** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Agregar usuario](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="f05ed-179">En hello **seleccione un rol** hoja, seleccione Hola un rol deseado.</span><span class="sxs-lookup"><span data-stu-id="f05ed-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="f05ed-180">Hola sección [acciones que pueden realizarse en cada rol](#actions-that-can-be-performed-in-each-role) listas Hola varias acciones que se pueden realizar los usuarios en roles de propietario, el usuario de desarrollo y pruebas y el colaborador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="f05ed-181">En hello **agregar usuarios** hoja, escriba la dirección de correo electrónico de Hola o nombre de usuario de hello desea tooadd en función de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="f05ed-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="f05ed-182">Si no se encuentra el usuario hello, un mensaje de error explica el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="f05ed-183">Si se encuentra el usuario hello, ese usuario se muestran y seleccionado.</span><span class="sxs-lookup"><span data-stu-id="f05ed-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="f05ed-184">Elija **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-184">Select **Select**.</span></span>
10. <span data-ttu-id="f05ed-185">Seleccione **Aceptar** tooclose hello **agregar acceso** hoja.</span><span class="sxs-lookup"><span data-stu-id="f05ed-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="f05ed-186">Cuando vuelva toohello **usuarios** hoja, se ha agregado el usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="f05ed-187">Agregar un laboratorio de tooa de usuario externo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f05ed-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="f05ed-188">Además los usuarios de tooadding Hola portal de Azure, puede agregar un laboratorio de tooyour de usuario externo mediante un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f05ed-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="f05ed-189">Hola siguiente ejemplo, basta con modificar valores de parámetro de hello en hello **toochange valores** comentario.</span><span class="sxs-lookup"><span data-stu-id="f05ed-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="f05ed-190">Puede recuperar hello `subscriptionId`, `labResourceGroup`, y `labName` valores de hoja de laboratorio Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f05ed-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f05ed-191">script de ejemplo de Hola se da por supuesto que Hola especifica el usuario se ha agregado como un toohello invitado Active Directory y se producirá un error si no es el caso de hello.</span><span class="sxs-lookup"><span data-stu-id="f05ed-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="f05ed-192">tooadd un usuario no está en hello laboratorio tooa de Active Directory, utilice el rol de tooa de usuario de hello tooassign portal Azure Hola tal y como se muestra en la sección de hello, [agregar un usuario o propietario en nivel de laboratorio de hello](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="f05ed-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="f05ed-193">Agregar un propietario o usuario en el nivel de suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="f05ed-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="f05ed-194">Permisos de Azure se propagan de ámbito de toochild ámbito principal en Azure.</span><span class="sxs-lookup"><span data-stu-id="f05ed-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="f05ed-195">Por lo tanto, los propietarios de una suscripción de Azure que contiene laboratorios, automáticamente son propietarios de estos.</span><span class="sxs-lookup"><span data-stu-id="f05ed-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="f05ed-196">También poseen hello las máquinas virtuales y otros recursos creados por los usuarios del laboratorio de Hola y Hola servicio laboratorios de desarrollo y pruebas de Azure.</span><span class="sxs-lookup"><span data-stu-id="f05ed-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="f05ed-197">Puede agregar laboratorio de tooa más propietarios a través de la hoja del laboratorio de Hola Hola [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f05ed-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="f05ed-198">Sin embargo, Hola agrega ámbito del propietario de la administración es más estrecha que el ámbito del propietario de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="f05ed-199">Por ejemplo, hello agrega propietarios no tiene acceso completo toosome de recursos de Hola que se crean en la suscripción de Hola Hola servicio laboratorios de desarrollo y pruebas.</span><span class="sxs-lookup"><span data-stu-id="f05ed-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="f05ed-200">tooadd un tooan de propietario de la suscripción de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f05ed-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="f05ed-201">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f05ed-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f05ed-202">Seleccione **más servicios**y, a continuación, seleccione **suscripciones** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="f05ed-203">Seleccione la suscripción de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="f05ed-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="f05ed-204">Seleccione el icono **Acceder** .</span><span class="sxs-lookup"><span data-stu-id="f05ed-204">Select **Access** icon.</span></span> 
   
    ![Usuarios de acceso](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="f05ed-206">En hello **usuarios** hoja, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Agregar usuario](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="f05ed-208">En hello **seleccione un rol** hoja, seleccione **propietario**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="f05ed-209">En hello **agregar usuarios** hoja, escriba la dirección de correo electrónico de Hola o el nombre de usuario de hello desea tooadd como propietario.</span><span class="sxs-lookup"><span data-stu-id="f05ed-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="f05ed-210">Si no se encuentra el usuario hello, obtendrá un mensaje de error que explica el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="f05ed-211">Si se encuentra el usuario hello, ese usuario aparece en hello **usuario** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="f05ed-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="f05ed-212">Seleccione el nombre de usuario ubicada de Hola.</span><span class="sxs-lookup"><span data-stu-id="f05ed-212">Select hello located user name.</span></span>
9. <span data-ttu-id="f05ed-213">Elija **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="f05ed-213">Select **Select**.</span></span>
10. <span data-ttu-id="f05ed-214">Seleccione **Aceptar** tooclose hello **agregar acceso** hoja.</span><span class="sxs-lookup"><span data-stu-id="f05ed-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="f05ed-215">Cuando vuelva toohello **usuarios** hoja, usuario Hola se ha agregado como un propietario.</span><span class="sxs-lookup"><span data-stu-id="f05ed-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="f05ed-216">Este usuario es ahora un propietario de los laboratorios creada con esta suscripción y, por tanto, ser capaz de tooperform tareas de propietario.</span><span class="sxs-lookup"><span data-stu-id="f05ed-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

