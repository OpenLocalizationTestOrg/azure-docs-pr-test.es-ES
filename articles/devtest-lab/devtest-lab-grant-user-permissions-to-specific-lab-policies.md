---
title: "Concesión de permisos de usuario a directivas específicas de laboratorio | Microsoft Docs"
description: "Obtenga información acerca de cómo conceder permisos de usuario para las directivas específicas de laboratorio en DevTest Labs según las necesidades de cada usuario"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="35447-103">Concesión de permisos de usuario a directivas específicas de laboratorio</span><span class="sxs-lookup"><span data-stu-id="35447-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="35447-104">Información general</span><span class="sxs-lookup"><span data-stu-id="35447-104">Overview</span></span>
<span data-ttu-id="35447-105">Este artículo muestra cómo usar PowerShell para conceder permisos de usuario a una directiva concreta de laboratorio.</span><span class="sxs-lookup"><span data-stu-id="35447-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="35447-106">De este modo, se pueden aplicar permisos en función de las necesidades de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="35447-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="35447-107">Por ejemplo, quizá prefiera conceder a un usuario determinado la posibilidad de cambiar la configuración de directiva de máquina virtual, pero no las directivas de costos.</span><span class="sxs-lookup"><span data-stu-id="35447-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="35447-108">Directivas como recursos</span><span class="sxs-lookup"><span data-stu-id="35447-108">Policies as resources</span></span>
<span data-ttu-id="35447-109">Tal y como se describe en el artículo [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md) , RBAC permite la administración de acceso específica de recursos para Azure.</span><span class="sxs-lookup"><span data-stu-id="35447-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="35447-110">Gracias a RBAC puede dividir las tareas entre el equipo de DevOps, y conceder a los usuarios únicamente el nivel de acceso que necesitan para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="35447-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="35447-111">En DevTest Labs, una directiva es un tipo de recurso que permite la acción de RBAC **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="35447-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="35447-112">Cada directiva de laboratorio es un recurso en el tipo de recurso Directiva, y se puede asignar como ámbito a un rol RBAC.</span><span class="sxs-lookup"><span data-stu-id="35447-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="35447-113">Por ejemplo, para conceder permiso de lectura/escritura de los usuarios para el **tamaños de máquina virtual permite** directiva, debe crear un rol personalizado que funcione con el **Microsoft.DevTestLab/labs/policySets/policies/*** acción y, a continuación, asignar los usuarios adecuados a este rol de seguridad en el ámbito de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="35447-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="35447-114">Para obtener más información sobre los roles personalizados de RBAC, consulte [Control de acceso de los roles personalizados](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="35447-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="35447-115">Creación de un rol personalizado de laboratorio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="35447-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="35447-116">Para empezar, debe leer el artículo siguiente, donde se explica cómo instalar y configurar los cmdlets de Azure PowerShell: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="35447-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="35447-117">Una vez haya configurado los cmdlets de Azure PowerShell, podrá realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="35447-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="35447-118">Enumerar todas las operaciones y acciones para un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="35447-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="35447-119">Enumerar las acciones de un rol determinado</span><span class="sxs-lookup"><span data-stu-id="35447-119">List actions in a particular role:</span></span>
* <span data-ttu-id="35447-120">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="35447-120">Create a custom role</span></span>

<span data-ttu-id="35447-121">El siguiente script de PowerShell muestra ejemplos de cómo realizar estas tareas:</span><span class="sxs-lookup"><span data-stu-id="35447-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="35447-122">Asignación de permisos a un usuario para una directiva determinada utilizando roles personalizados</span><span class="sxs-lookup"><span data-stu-id="35447-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="35447-123">Una vez haya definido los roles personalizados, puede asignárselos a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="35447-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="35447-124">A fin de asignar un rol personalizado a un usuario, primero debe obtener el **ObjectId** que representa a ese usuario.</span><span class="sxs-lookup"><span data-stu-id="35447-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="35447-125">Para ello, utilice el cmdlet **Get-AzureRmADUser** .</span><span class="sxs-lookup"><span data-stu-id="35447-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="35447-126">En el ejemplo siguiente, el valor **ObjectId** del usuario *SomeUser* es 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="35447-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="35447-127">Una vez que tenga el **ObjectId** para el usuario y un nombre de rol personalizado, puede asignar ese rol al usuario con el cmdlet **New-AzureRmRoleAssignment**:</span><span class="sxs-lookup"><span data-stu-id="35447-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="35447-128">En el ejemplo anterior, se utiliza la directiva **AllowedVmSizesInLab** .</span><span class="sxs-lookup"><span data-stu-id="35447-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="35447-129">Puede utilizar cualquiera de las directivas siguientes:</span><span class="sxs-lookup"><span data-stu-id="35447-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="35447-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="35447-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="35447-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="35447-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="35447-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="35447-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="35447-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="35447-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="35447-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35447-134">Next steps</span></span>
<span data-ttu-id="35447-135">Una vez que haya concedido permisos de usuario a las directivas específicas del laboratorio, estos son algunos de los siguientes pasos que debe considerar:</span><span class="sxs-lookup"><span data-stu-id="35447-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="35447-136">[Acceso seguro a un laboratorio](devtest-lab-add-devtest-user.md)</span><span class="sxs-lookup"><span data-stu-id="35447-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="35447-137">[Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)</span><span class="sxs-lookup"><span data-stu-id="35447-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="35447-138">[Creación de una plantilla de laboratorio](devtest-lab-create-template.md)</span><span class="sxs-lookup"><span data-stu-id="35447-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="35447-139">[Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)</span><span class="sxs-lookup"><span data-stu-id="35447-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="35447-140">[Incorporación de una máquina virtual con artefactos a un laboratorio](devtest-lab-add-vm-with-artifacts.md)</span><span class="sxs-lookup"><span data-stu-id="35447-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

