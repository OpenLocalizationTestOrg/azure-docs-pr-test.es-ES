---
title: las directivas de laboratorio de aaaGrant usuario permisos toospecific | Documentos de Microsoft
description: "Obtenga información acerca de cómo toogrant permisos toospecific laboratorio las directivas de usuario en los laboratorios de desarrollo y pruebas según las necesidades de cada usuario"
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
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="c2ecb-103">Conceder permisos de usuario toospecific directivas de laboratorio</span><span class="sxs-lookup"><span data-stu-id="c2ecb-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="c2ecb-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c2ecb-104">Overview</span></span>
<span data-ttu-id="c2ecb-105">Este artículo se explica cómo toouse directiva de PowerShell toogrant a los usuarios permisos tooa laboratorio determinado.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="c2ecb-106">De este modo, se pueden aplicar permisos en función de las necesidades de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="c2ecb-107">Por ejemplo, puede toogrant una configuración de directiva de usuario determinado Hola capacidad toochange Hola VM, pero no Hola costo directivas.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="c2ecb-108">Directivas como recursos</span><span class="sxs-lookup"><span data-stu-id="c2ecb-108">Policies as resources</span></span>
<span data-ttu-id="c2ecb-109">Según lo descrito en hello [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md) artículo, RBAC permite la administración de acceso específico de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="c2ecb-110">Usar RBAC, puede separar los derechos en el equipo de DevOps y conceder únicamente una cantidad Hola de toousers de acceso que necesitan tooperform sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="c2ecb-111">En los laboratorios de desarrollo y pruebas, una directiva es un tipo de recurso que permite la acción de RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="c2ecb-112">Cada directiva de laboratorio es un recurso en el tipo de recurso de directiva de Hola y puede asignarse como un ámbito de la función de RBAC tooan.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="c2ecb-113">Por ejemplo, en toohello de permiso de lectura/escritura de orden toogrant usuarios **tamaños de máquina virtual permite** directiva, debe crear un rol personalizado que funcione con hello **Microsoft.DevTestLab/labs/policySets/policies/** * acción y, a continuación, asignar Hola usuarios adecuados toothis rol personalizado en el ámbito de Hola de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="c2ecb-114">toolearn más información acerca de las funciones personalizadas en RBAC, vea hello [control de acceso de roles personalizados](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c2ecb-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="c2ecb-115">Creación de un rol personalizado de laboratorio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2ecb-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="c2ecb-116">En orden tooget iniciado, necesitará hello tooread después de artículo, que se explicará cómo tooinstall y configurar los cmdlets de PowerShell de Azure de hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="c2ecb-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="c2ecb-117">Una vez haya configurado Hola cmdlets de PowerShell de Azure, puede realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="c2ecb-118">Lista de todas las operaciones de Hola/acciones para un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="c2ecb-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="c2ecb-119">Enumerar las acciones de un rol determinado</span><span class="sxs-lookup"><span data-stu-id="c2ecb-119">List actions in a particular role:</span></span>
* <span data-ttu-id="c2ecb-120">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="c2ecb-120">Create a custom role</span></span>

<span data-ttu-id="c2ecb-121">Hola siguiente script de PowerShell muestra ejemplos de cómo tooperform estas tareas:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="c2ecb-122">Asignar permisos de usuario de tooa para una directiva determinada utilizando roles personalizados</span><span class="sxs-lookup"><span data-stu-id="c2ecb-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="c2ecb-123">Una vez que haya definido sus funciones personalizadas, puede asignarlos toousers.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="c2ecb-124">En orden tooassign un usuario de tooa roles personalizados, primero debe obtener hello **ObjectId** que representa ese usuario.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="c2ecb-125">toodo que usar hello **AzureRmADUser Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="c2ecb-126">En el siguiente ejemplo de Hola Hola **ObjectId** de hello *SomeUser* usuario es 05DEFF7B 0AC3 4ABF B74D 6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="c2ecb-127">Una vez que tenga hello **ObjectId** de usuario de Hola y el nombre de rol personalizado, puede asignar ese usuario toohello de rol con hello **AzureRmRoleAssignment New** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="c2ecb-128">En el ejemplo anterior de hello, Hola **AllowedVmSizesInLab** se utiliza la directiva.</span><span class="sxs-lookup"><span data-stu-id="c2ecb-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="c2ecb-129">Puede usar cualquiera de hello las directivas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="c2ecb-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="c2ecb-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="c2ecb-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="c2ecb-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="c2ecb-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="c2ecb-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="c2ecb-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="c2ecb-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="c2ecb-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2ecb-134">Next steps</span></span>
<span data-ttu-id="c2ecb-135">Una vez haya concedido directivas de laboratorio de toospecific de permisos de usuario, estas son algunas tooconsider de pasos siguiente:</span><span class="sxs-lookup"><span data-stu-id="c2ecb-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="c2ecb-136">[Laboratorio de acceso seguro tooa](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="c2ecb-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="c2ecb-137">[Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)</span><span class="sxs-lookup"><span data-stu-id="c2ecb-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="c2ecb-138">[Creación de una plantilla de laboratorio](devtest-lab-create-template.md)</span><span class="sxs-lookup"><span data-stu-id="c2ecb-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="c2ecb-139">[Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)</span><span class="sxs-lookup"><span data-stu-id="c2ecb-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="c2ecb-140">[Agregar una máquina virtual con el laboratorio de artefactos tooa](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="c2ecb-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

