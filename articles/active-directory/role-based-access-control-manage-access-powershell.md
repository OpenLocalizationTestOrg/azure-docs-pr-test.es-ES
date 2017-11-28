---
title: aaaManage Role-Based Access Control (RBAC) con Azure PowerShell | Documentos de Microsoft
description: "¿Cómo toomanage RBAC con Azure PowerShell, incluidas la lista de roles, asignación de roles y eliminar asignaciones de roles."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="f3474-103">Administración del control de acceso basado en rol con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3474-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3474-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3474-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="f3474-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f3474-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="f3474-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="f3474-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="f3474-107">Puede usar el Control de acceso basado en roles (RBAC) de hello portal de Azure y la suscripción de tooyour de acceso de API de administración de recursos de Azure toomanage en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="f3474-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="f3474-108">Con esta característica, puede conceder acceso a los usuarios, grupos o entidades de servicio de Active Directory mediante la asignación de algunos toothem de roles en un ámbito determinado.</span><span class="sxs-lookup"><span data-stu-id="f3474-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="f3474-109">Para poder usar PowerShell toomanage RBAC, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="f3474-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="f3474-110">La versión 0.8.8 o posterior de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3474-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="f3474-111">versión más reciente de tooinstall hello y asócielo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f3474-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f3474-112">Cmdlets de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f3474-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="f3474-113">Instalar hello [cmdlets de Azure Resource Manager](/powershell/azure/overview) en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3474-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="f3474-114">Lista de roles</span><span class="sxs-lookup"><span data-stu-id="f3474-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="f3474-115">Lista de todos los roles disponibles</span><span class="sxs-lookup"><span data-stu-id="f3474-115">List all available roles</span></span>
<span data-ttu-id="f3474-116">roles RBAC toolist que están disponibles para la asignación y tooinspect Hola operaciones toowhich que permita el acceso, utilice `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="f3474-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="f3474-118">Lista de las acciones de un rol</span><span class="sxs-lookup"><span data-stu-id="f3474-118">List actions of a role</span></span>
<span data-ttu-id="f3474-119">acciones de hello toolist para un rol específico, use `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="f3474-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition para un rol específico - captura de pantalla](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="f3474-121">Consulta de quién ha accedido</span><span class="sxs-lookup"><span data-stu-id="f3474-121">See who has access</span></span>
<span data-ttu-id="f3474-122">usar asignaciones de acceso de toolist RBAC, `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="f3474-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="f3474-123">Lista de asignaciones de roles en un ámbito específico</span><span class="sxs-lookup"><span data-stu-id="f3474-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="f3474-124">Puede ver todas las asignaciones de acceso de Hola para una suscripción especificada, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="f3474-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="f3474-125">Por ejemplo, toosee Hola todas las asignaciones de hello activo para un grupo de recursos, utilice `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="f3474-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para un grupo de recursos - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="f3474-127">Lista de roles tooa usuario asignado</span><span class="sxs-lookup"><span data-stu-id="f3474-127">List roles assigned tooa user</span></span>
<span data-ttu-id="f3474-128">toolist todos los roles de Hola que se asignan tooa especifican usuarios y roles de Hola que se asignan grupos de toohello toowhich Hola usuario pertenece, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="f3474-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para un usuario - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="f3474-130">Lista de asignaciones de roles de administrador y coadministrador de servicio básico</span><span class="sxs-lookup"><span data-stu-id="f3474-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="f3474-131">las asignaciones de acceso de toolist para Administrador de la suscripción clásico de Hola y coadministrators, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="f3474-132">Conceder acceso</span><span class="sxs-lookup"><span data-stu-id="f3474-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="f3474-133">Búsqueda de identificadores de objetos</span><span class="sxs-lookup"><span data-stu-id="f3474-133">Search for object IDs</span></span>
<span data-ttu-id="f3474-134">tooassign un rol, deberá tooidentify Hola objetos (usuario, grupo o aplicación) y ámbito de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="f3474-135">Si no conoce el identificador de la suscripción de hello, encontrará en hello **suscripciones** hoja en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3474-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="f3474-136">toolearn tooquery Hola Id. de suscripción, vea [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="f3474-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="f3474-137">Id. de objeto de hello tooget para un grupo de Azure AD, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="f3474-138">Id. de objeto de hello tooget para una entidad de servicio de Azure AD o una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="f3474-139">Asignación de una aplicación de tooan de rol en el ámbito de la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="f3474-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="f3474-140">aplicación de tooan toogrant access en el ámbito de la suscripción de hello, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="f3474-142">Asignar a un usuario de tooa de rol en el ámbito de grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f3474-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="f3474-143">toogrant acceso tooa de usuario en el ámbito de grupo de recursos de hello, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="f3474-145">Asignar a un grupo de tooa de rol en el ámbito de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f3474-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="f3474-146">grupo de tooa toogrant acceso en el ámbito de recursos de hello, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="f3474-148">Quitar acceso</span><span class="sxs-lookup"><span data-stu-id="f3474-148">Remove access</span></span>
<span data-ttu-id="f3474-149">tooremove el acceso para usuarios, grupos y aplicaciones, use:</span><span class="sxs-lookup"><span data-stu-id="f3474-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="f3474-151">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="f3474-151">Create a custom role</span></span>
<span data-ttu-id="f3474-152">toocreate un rol personalizado, use hello ```New-AzureRmRoleDefinition``` comando.</span><span class="sxs-lookup"><span data-stu-id="f3474-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="f3474-153">Existen dos métodos de estructurar el rol de hello, con PSRoleDefinitionObject o una plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="f3474-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="f3474-154">Acciones Get para un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="f3474-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="f3474-155">Al crear roles personalizados desde el principio, es importante tooknow todos hello las posibles operaciones de proveedores de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="f3474-156">Hola de uso ```Get-AzureRMProviderOperation``` comando tooget esta información.</span><span class="sxs-lookup"><span data-stu-id="f3474-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="f3474-157">Por ejemplo, si desea que toocheck todas las operaciones disponibles hello para la máquina virtual use este comando:</span><span class="sxs-lookup"><span data-stu-id="f3474-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="f3474-158">Creación de rol con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="f3474-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="f3474-159">Cuando se usa PowerShell toocreate un rol personalizado, puede empezar desde cero o usar uno de hello [roles integrados](role-based-access-built-in-roles.md) como punto de partida.</span><span class="sxs-lookup"><span data-stu-id="f3474-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="f3474-160">ejemplo de Hola en esta sección comienza con un rol integrado y, a continuación, personaliza con más privilegios.</span><span class="sxs-lookup"><span data-stu-id="f3474-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="f3474-161">Editar Hola de hello atributos tooadd *acciones*, *notActions*, o *ámbitos* que desee y, a continuación, guardar los cambios de Hola como un nuevo rol.</span><span class="sxs-lookup"><span data-stu-id="f3474-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="f3474-162">Hello en el ejemplo siguiente se inicia con hello *colaborador de la máquina Virtual* rol y se utiliza ese toocreate un rol personalizado denominado *operador de máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="f3474-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="f3474-163">nuevo rol de Hello concede acceso tooall lee las operaciones de *Microsoft.Compute*, *almacenamiento de Microsoft*, y *Microsoft.Network* acceso a los proveedores y concede recursos toostart, reiniciar y supervisar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f3474-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="f3474-164">roles personalizados de Hello pueden usarse en dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="f3474-164">hello custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="f3474-166">Creación de rol con plantilla JSON</span><span class="sxs-lookup"><span data-stu-id="f3474-166">Create role with JSON template</span></span>
<span data-ttu-id="f3474-167">Una plantilla JSON puede utilizarse como definición de origen de Hola para roles personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="f3474-168">Hello en el ejemplo siguiente se crea un rol personalizado que permite el acceso de lectura toostorage y recursos de proceso, tener acceso a toosupport y agrega ese rol tootwo suscripciones.</span><span class="sxs-lookup"><span data-stu-id="f3474-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="f3474-169">Crear un nuevo archivo `C:\CustomRoles\customrole1.json` con el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="f3474-170">Hello Id. debe establecerse demasiado`null` durante la creación de rol inicial como un nuevo identificador se genera automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f3474-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="f3474-171">tooadd Hola rol toohello suscripciones, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="f3474-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="f3474-172">Modificación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="f3474-172">Modify a custom role</span></span>
<span data-ttu-id="f3474-173">Toocreating similar un rol personalizado, puede modificar un rol personalizado existente con hello PSRoleDefinitionObject o una plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="f3474-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="f3474-174">Modificación de rol con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="f3474-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="f3474-175">toomodify un rol personalizado, en primer lugar, utilice hello `Get-AzureRmRoleDefinition` comando definición de roles de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="f3474-176">En segundo lugar, realice los cambios de hello deseado toohello definición de roles.</span><span class="sxs-lookup"><span data-stu-id="f3474-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="f3474-177">Por último, utilice hello `Set-AzureRmRoleDefinition` comando toosave hello modificó la definición de rol.</span><span class="sxs-lookup"><span data-stu-id="f3474-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="f3474-178">Hello en el ejemplo siguiente se agrega hello `Microsoft.Insights/diagnosticSettings/*` operación toohello *operador de máquina Virtual* roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="f3474-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="f3474-180">Hello en el ejemplo siguiente se agrega una suscripción de Azure toohello puede asignar los ámbitos de hello *operador de máquina Virtual* roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="f3474-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="f3474-182">Modificación de rol con plantilla JSON</span><span class="sxs-lookup"><span data-stu-id="f3474-182">Modify role with JSON template</span></span>
<span data-ttu-id="f3474-183">Mediante la plantilla de hello anterior JSON, puede modificar una existente tooadd roles personalizados fácilmente o quitar acciones.</span><span class="sxs-lookup"><span data-stu-id="f3474-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="f3474-184">Actualizar plantilla JSON de Hola y agregar acción de lectura de Hola para funciones de red tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="f3474-185">las definiciones de Hello aparecen en la plantilla de hello no son aplicados de manera acumulativa tooan definición existente, lo que significa que esa función hello aparece exactamente tal y como se especifica en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="f3474-186">También debe campo de Id. de hello tooupdate con Id. de hello del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="f3474-187">Si no está seguro de qué es este valor, puede usar hello `Get-AzureRmRoleDefinition` cmdlet tooget esta información.</span><span class="sxs-lookup"><span data-stu-id="f3474-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="f3474-188">tooupdate Hola rol existente, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="f3474-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="f3474-189">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="f3474-189">Delete a custom role</span></span>
<span data-ttu-id="f3474-190">toodelete un rol personalizado, use hello `Remove-AzureRmRoleDefinition` comando.</span><span class="sxs-lookup"><span data-stu-id="f3474-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="f3474-191">Hello en el ejemplo siguiente se quita hello *operador de máquina Virtual* roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="f3474-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="f3474-193">Lista de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="f3474-193">List custom roles</span></span>
<span data-ttu-id="f3474-194">roles de hello toolist que están disponibles para la asignación en un ámbito, usar hello `Get-AzureRmRoleDefinition` comando.</span><span class="sxs-lookup"><span data-stu-id="f3474-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="f3474-195">Hola siguiente ejemplo enumera todos los roles que están disponibles para la asignación de la suscripción de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="f3474-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="f3474-197">En el siguiente ejemplo de Hola Hola *operador de máquina Virtual* roles personalizados no está disponible en hello *Production4* suscripción porque esa suscripción no está en hello  **AssignableScopes** del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3474-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="f3474-199">Consulte también</span><span class="sxs-lookup"><span data-stu-id="f3474-199">See also</span></span>
* <span data-ttu-id="f3474-200">[Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="f3474-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

