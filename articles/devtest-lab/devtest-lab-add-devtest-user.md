---
title: "Adición de propietarios y usuarios en Azure DevTest Labs | Microsoft Docs"
description: Agregar propietarios y usuarios en Azure DevTest Labs mediante Azure Portal o PowerShell
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
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="e7f05-103">Adición de propietarios y usuarios en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e7f05-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="e7f05-104">El acceso a Azure DevTest Labs se controla mediante el [control de acceso basado en rol (RBAC) de Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e7f05-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="e7f05-105">Mediante RBAC, puede repartir las tareas del equipo en *roles* y conceder a los usuarios únicamente el nivel de acceso que necesitan para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7f05-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="e7f05-106">Tres de estos roles RBAC son *Propietario*, *Usuario de DevTest Labs* y *Colaborador*.</span><span class="sxs-lookup"><span data-stu-id="e7f05-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="e7f05-107">En este artículo, aprenderá qué acciones se pueden realizar en cada uno de los tres roles principales de RBAC.</span><span class="sxs-lookup"><span data-stu-id="e7f05-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="e7f05-108">A partir de ahí, aprenderá cómo agregar usuarios a un laboratorio a través del portal o a través de un script de PowerShell y cómo agregar los usuarios en el nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="e7f05-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="e7f05-109">Acciones que se pueden realizar en cada rol</span><span class="sxs-lookup"><span data-stu-id="e7f05-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="e7f05-110">Hay tres roles principales que puede asignar a un usuario:</span><span class="sxs-lookup"><span data-stu-id="e7f05-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="e7f05-111">Propietario</span><span class="sxs-lookup"><span data-stu-id="e7f05-111">Owner</span></span>
* <span data-ttu-id="e7f05-112">Usuario de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e7f05-112">DevTest Labs User</span></span>
* <span data-ttu-id="e7f05-113">Colaborador</span><span class="sxs-lookup"><span data-stu-id="e7f05-113">Contributor</span></span>

<span data-ttu-id="e7f05-114">En la tabla siguiente se muestran las acciones que pueden realizar los usuarios pertenecientes a cada uno de estos roles:</span><span class="sxs-lookup"><span data-stu-id="e7f05-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="e7f05-115">**Acciones que pueden realizar los usuarios de este rol**</span><span class="sxs-lookup"><span data-stu-id="e7f05-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="e7f05-116">**Usuario de DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="e7f05-116">**DevTest Labs User**</span></span> | <span data-ttu-id="e7f05-117">**Propietario**</span><span class="sxs-lookup"><span data-stu-id="e7f05-117">**Owner**</span></span> | <span data-ttu-id="e7f05-118">**Colaborador**</span><span class="sxs-lookup"><span data-stu-id="e7f05-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e7f05-119">**Tareas de laboratorio**</span><span class="sxs-lookup"><span data-stu-id="e7f05-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="e7f05-120">Agregar usuarios a un laboratorio</span><span class="sxs-lookup"><span data-stu-id="e7f05-120">Add users to a lab</span></span> |<span data-ttu-id="e7f05-121">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-121">No</span></span> |<span data-ttu-id="e7f05-122">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-122">Yes</span></span> |<span data-ttu-id="e7f05-123">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-123">No</span></span> |
| <span data-ttu-id="e7f05-124">Actualizar la configuración de costo</span><span class="sxs-lookup"><span data-stu-id="e7f05-124">Update cost settings</span></span> |<span data-ttu-id="e7f05-125">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-125">No</span></span> |<span data-ttu-id="e7f05-126">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-126">Yes</span></span> |<span data-ttu-id="e7f05-127">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-127">Yes</span></span> |
| <span data-ttu-id="e7f05-128">**Tareas base de máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="e7f05-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="e7f05-129">Agregar y quitar imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="e7f05-129">Add and remove custom images</span></span> |<span data-ttu-id="e7f05-130">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-130">No</span></span> |<span data-ttu-id="e7f05-131">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-131">Yes</span></span> |<span data-ttu-id="e7f05-132">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-132">Yes</span></span> |
| <span data-ttu-id="e7f05-133">Agregar, actualizar y eliminar las fórmulas</span><span class="sxs-lookup"><span data-stu-id="e7f05-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="e7f05-134">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-134">Yes</span></span> |<span data-ttu-id="e7f05-135">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-135">Yes</span></span> |<span data-ttu-id="e7f05-136">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-136">Yes</span></span> |
| <span data-ttu-id="e7f05-137">Incluir en la lista de permitidos imágenes de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e7f05-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="e7f05-138">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-138">No</span></span> |<span data-ttu-id="e7f05-139">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-139">Yes</span></span> |<span data-ttu-id="e7f05-140">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-140">Yes</span></span> |
| <span data-ttu-id="e7f05-141">**Tareas de la máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="e7f05-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="e7f05-142">Crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e7f05-142">Create VMs</span></span> |<span data-ttu-id="e7f05-143">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-143">Yes</span></span> |<span data-ttu-id="e7f05-144">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-144">Yes</span></span> |<span data-ttu-id="e7f05-145">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-145">Yes</span></span> |
| <span data-ttu-id="e7f05-146">Iniciar, detener y eliminar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e7f05-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="e7f05-147">Solo las máquinas virtuales creadas por el usuario</span><span class="sxs-lookup"><span data-stu-id="e7f05-147">Only VMs created by the user</span></span> |<span data-ttu-id="e7f05-148">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-148">Yes</span></span> |<span data-ttu-id="e7f05-149">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-149">Yes</span></span> |
| <span data-ttu-id="e7f05-150">Actualizar directivas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e7f05-150">Update VM policies</span></span> |<span data-ttu-id="e7f05-151">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-151">No</span></span> |<span data-ttu-id="e7f05-152">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-152">Yes</span></span> |<span data-ttu-id="e7f05-153">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-153">Yes</span></span> |
| <span data-ttu-id="e7f05-154">Agregar discos de datos o quitarlos en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e7f05-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="e7f05-155">Solo las máquinas virtuales creadas por el usuario</span><span class="sxs-lookup"><span data-stu-id="e7f05-155">Only VMs created by the user</span></span> |<span data-ttu-id="e7f05-156">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-156">Yes</span></span> |<span data-ttu-id="e7f05-157">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-157">Yes</span></span> |
| <span data-ttu-id="e7f05-158">**Tareas de artefacto**</span><span class="sxs-lookup"><span data-stu-id="e7f05-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="e7f05-159">Agregar y quitar repositorios de artefacto</span><span class="sxs-lookup"><span data-stu-id="e7f05-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="e7f05-160">No</span><span class="sxs-lookup"><span data-stu-id="e7f05-160">No</span></span> |<span data-ttu-id="e7f05-161">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-161">Yes</span></span> |<span data-ttu-id="e7f05-162">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-162">Yes</span></span> |
| <span data-ttu-id="e7f05-163">Aplicar artefactos</span><span class="sxs-lookup"><span data-stu-id="e7f05-163">Apply artifacts</span></span> |<span data-ttu-id="e7f05-164">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-164">Yes</span></span> |<span data-ttu-id="e7f05-165">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-165">Yes</span></span> |<span data-ttu-id="e7f05-166">Sí</span><span class="sxs-lookup"><span data-stu-id="e7f05-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="e7f05-167">Cuando un usuario crea una máquina virtual, a ese usuario se le asigna automáticamente el rol **Propietario** de la máquina virtual creada.</span><span class="sxs-lookup"><span data-stu-id="e7f05-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="e7f05-168">Agregar un propietario o usuario en el nivel de laboratorio</span><span class="sxs-lookup"><span data-stu-id="e7f05-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="e7f05-169">Los propietarios y los usuarios se pueden agregar en el nivel de laboratorio a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e7f05-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="e7f05-170">Esto incluye a los usuarios externos con una [cuenta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)válida.</span><span class="sxs-lookup"><span data-stu-id="e7f05-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="e7f05-171">Los siguientes pasos le guiarán a través del proceso de agregación de un propietario o usuario a un laboratorio de Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="e7f05-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="e7f05-172">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e7f05-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e7f05-173">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="e7f05-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="e7f05-174">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="e7f05-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="e7f05-175">En la hoja del laboratorio, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="e7f05-176">En la hoja **Configuración**, seleccione **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="e7f05-177">En la hoja **Usuarios**, seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![Agregar usuario](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="e7f05-179">En la hoja **Seleccionar un rol** , seleccione el rol que desee.</span><span class="sxs-lookup"><span data-stu-id="e7f05-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="e7f05-180">En la sección [Acciones que se pueden realizar en cada rol](#actions-that-can-be-performed-in-each-role) se enumeran las distintas acciones que pueden realizar los usuarios de los roles de Propietario, Usuario de DevTest y Colaborador.</span><span class="sxs-lookup"><span data-stu-id="e7f05-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="e7f05-181">En la hoja **Agregar usuarios** , escriba la dirección de correo electrónico o el nombre del usuario que desea agregar en el rol especificado.</span><span class="sxs-lookup"><span data-stu-id="e7f05-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="e7f05-182">Si no se encuentra el usuario, aparecerá un mensaje de error que explica el problema.</span><span class="sxs-lookup"><span data-stu-id="e7f05-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="e7f05-183">Si se encuentra el usuario, ese usuario se muestra y se selecciona.</span><span class="sxs-lookup"><span data-stu-id="e7f05-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="e7f05-184">Elija **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-184">Select **Select**.</span></span>
10. <span data-ttu-id="e7f05-185">Seleccione **Aceptar** para cerrar la hoja **Agregar acceso**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="e7f05-186">Cuando vuelva a la hoja **Usuarios** , el usuario ya se habrá agregado.</span><span class="sxs-lookup"><span data-stu-id="e7f05-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="e7f05-187">Incorporación de un usuario externo a un laboratorio mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f05-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="e7f05-188">Además de agregar usuarios en Azure Portal, puede agregar un usuario externo al laboratorio mediante un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7f05-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="e7f05-189">En el ejemplo siguiente, basta con modificar los valores de parámetro en el comentario **Values to change** (Valores para cambiar).</span><span class="sxs-lookup"><span data-stu-id="e7f05-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="e7f05-190">Puede recuperar los valores `subscriptionId`, `labResourceGroup` y `labName` de la hoja de laboratorio en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e7f05-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e7f05-191">El script de ejemplo supone que el usuario especificado se ha agregado como invitado a Active Directory y se producirá un error si este no es el caso.</span><span class="sxs-lookup"><span data-stu-id="e7f05-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="e7f05-192">Para agregar un usuario que no está en Active Directory a un laboratorio, use Azure Portal para asignar el usuario a un rol, tal como se muestra en la sección [Agregar un propietario o usuario en el nivel de laboratorio](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="e7f05-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="e7f05-193">Agregar un propietario o usuario en el nivel de suscripción</span><span class="sxs-lookup"><span data-stu-id="e7f05-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="e7f05-194">Los permisos de Azure se propagan desde el ámbito primario al secundario en Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f05-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="e7f05-195">Por lo tanto, los propietarios de una suscripción de Azure que contiene laboratorios, automáticamente son propietarios de estos.</span><span class="sxs-lookup"><span data-stu-id="e7f05-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="e7f05-196">También serán propietarios de las máquinas virtuales y de los demás recursos creados por los usuarios del laboratorio y el servicio Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="e7f05-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="e7f05-197">Puede agregar propietarios adicionales a un laboratorio a través de la hoja del laboratorio en [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e7f05-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="e7f05-198">Sin embargo, el ámbito de administración del propietario agregado será más limitado que el ámbito del propietario de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="e7f05-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="e7f05-199">Por ejemplo, los propietarios agregados no tienen acceso completo a algunos de los recursos que el servicio DevTest Labs crea en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="e7f05-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="e7f05-200">Para agregar un propietario a una suscripción de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e7f05-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="e7f05-201">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e7f05-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e7f05-202">Seleccione **Más servicios** y, después, seleccione **Suscripciones** en la lista.</span><span class="sxs-lookup"><span data-stu-id="e7f05-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="e7f05-203">Seleccione la suscripción deseada.</span><span class="sxs-lookup"><span data-stu-id="e7f05-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="e7f05-204">Seleccione el icono **Acceder** .</span><span class="sxs-lookup"><span data-stu-id="e7f05-204">Select **Access** icon.</span></span> 
   
    ![Usuarios de acceso](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="e7f05-206">En la hoja **Usuarios**, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-206">On the **Users** blade, select **Add**.</span></span>
   
    ![Agregar usuario](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="e7f05-208">En la hoja **Seleccionar rol**, seleccione **Propietario**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="e7f05-209">En la hoja **Agregar usuarios** , escriba la dirección de correo electrónico o el nombre del usuario que desea agregar como propietario.</span><span class="sxs-lookup"><span data-stu-id="e7f05-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="e7f05-210">Si no se encuentra el usuario, aparecerá un mensaje de error que explica el problema.</span><span class="sxs-lookup"><span data-stu-id="e7f05-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="e7f05-211">Si se encuentra el usuario, dicho usuario se mostrará en el cuadro de texto **Usuario** .</span><span class="sxs-lookup"><span data-stu-id="e7f05-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="e7f05-212">Seleccione el nombre de usuario encontrado.</span><span class="sxs-lookup"><span data-stu-id="e7f05-212">Select the located user name.</span></span>
9. <span data-ttu-id="e7f05-213">Elija **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-213">Select **Select**.</span></span>
10. <span data-ttu-id="e7f05-214">Seleccione **Aceptar** para cerrar la hoja **Agregar acceso**.</span><span class="sxs-lookup"><span data-stu-id="e7f05-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="e7f05-215">Cuando vuelva a la hoja **Usuarios** , el usuario ya se habrá agregado como propietario.</span><span class="sxs-lookup"><span data-stu-id="e7f05-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="e7f05-216">Este usuario será ya propietario de cualquier laboratorio creado con esta suscripción y, por lo tanto, podrá realizar tareas de propietario.</span><span class="sxs-lookup"><span data-stu-id="e7f05-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

