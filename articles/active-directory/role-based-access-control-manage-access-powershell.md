---
title: "Administración del control de acceso basado en roles (RBAC) con Azure PowerShell | Microsoft Docs"
description: "Cómo administrar RBAC con Azure PowerShell, incluida la enumeración y asignación de roles, y la eliminación de asignaciones de roles."
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
ms.openlocfilehash: d7b11df21650b5cb27f9c3dd8306f8d12664185e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="8498c-103">Administración del control de acceso basado en rol con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8498c-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8498c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8498c-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="8498c-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8498c-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="8498c-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="8498c-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="8498c-107">Puede usar el control de acceso basado en rol (RBAC) del Portal de Azure y la API de Administración de recursos de Azure para administrar el acceso a su suscripción en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="8498c-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="8498c-108">Con esta característica, puede conceder acceso a usuarios, grupos o entidades de seguridad de servicio de Active Directory asignándoles roles en un ámbito determinado.</span><span class="sxs-lookup"><span data-stu-id="8498c-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="8498c-109">Para poder usar Windows PowerShell con el fin de administrar RBAC, necesita cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="8498c-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="8498c-110">La versión 0.8.8 o posterior de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8498c-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="8498c-111">Para instalar la última versión y asociarla a la suscripción de Azure, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8498c-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="8498c-112">Cmdlets de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8498c-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="8498c-113">Instale los [cmdlets de Azure Resource Manager](/powershell/azure/overview) en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8498c-113">Install the [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="8498c-114">Lista de roles</span><span class="sxs-lookup"><span data-stu-id="8498c-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="8498c-115">Lista de todos los roles disponibles</span><span class="sxs-lookup"><span data-stu-id="8498c-115">List all available roles</span></span>
<span data-ttu-id="8498c-116">Para enumerar los roles de RBAC disponibles para asignación y para inspeccionar las operaciones a las que conceden acceso, use `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="8498c-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="8498c-118">Lista de las acciones de un rol</span><span class="sxs-lookup"><span data-stu-id="8498c-118">List actions of a role</span></span>
<span data-ttu-id="8498c-119">Para enumerar las acciones de un rol específico, use `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="8498c-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition para un rol específico - captura de pantalla](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="8498c-121">Consulta de quién ha accedido</span><span class="sxs-lookup"><span data-stu-id="8498c-121">See who has access</span></span>
<span data-ttu-id="8498c-122">Para mostrar las asignaciones de acceso RBAC, use `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="8498c-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="8498c-123">Lista de asignaciones de roles en un ámbito específico</span><span class="sxs-lookup"><span data-stu-id="8498c-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="8498c-124">Puede ver todas las asignaciones de acceso de una suscripción, un grupo de recursos o un recurso determinados.</span><span class="sxs-lookup"><span data-stu-id="8498c-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="8498c-125">Por ejemplo, para ver todas las asignaciones activas de un grupo de recursos, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="8498c-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para un grupo de recursos - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="8498c-127">Lista de roles asignados a un usuario</span><span class="sxs-lookup"><span data-stu-id="8498c-127">List roles assigned to a user</span></span>
<span data-ttu-id="8498c-128">Para enumerar todos los roles asignados a un usuario especificado y los roles que se asignan a los grupos a los que pertenece el usuario, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="8498c-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para un usuario - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="8498c-130">Lista de asignaciones de roles de administrador y coadministrador de servicio básico</span><span class="sxs-lookup"><span data-stu-id="8498c-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="8498c-131">Para enumerar las asignaciones de acceso para el administrador y los coadministradores de suscripción clásica, use:</span><span class="sxs-lookup"><span data-stu-id="8498c-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="8498c-132">Conceder acceso</span><span class="sxs-lookup"><span data-stu-id="8498c-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="8498c-133">Búsqueda de identificadores de objetos</span><span class="sxs-lookup"><span data-stu-id="8498c-133">Search for object IDs</span></span>
<span data-ttu-id="8498c-134">Para asignar un rol, debe identificar el objeto (usuario, grupo o aplicación) y el ámbito.</span><span class="sxs-lookup"><span data-stu-id="8498c-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="8498c-135">Si no conoce el id. de suscripción, lo encontrará en la hoja **Suscripciones** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8498c-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="8498c-136">Para obtener información sobre cómo obtener el id. de suscripción, vea [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="8498c-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="8498c-137">Para obtener el id. del objeto de un grupo de Azure AD, use:</span><span class="sxs-lookup"><span data-stu-id="8498c-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="8498c-138">Para obtener el id. de objeto de una entidad principal de servicio de Azure AD o aplicación, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8498c-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="8498c-139">Asignación de un rol a una aplicación en el ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="8498c-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="8498c-140">Para conceder acceso a una aplicación en el ámbito de la suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="8498c-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="8498c-142">Asignación de un rol a un usuario en el ámbito del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8498c-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="8498c-143">Para conceder acceso a un usuario en el ámbito del grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="8498c-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="8498c-145">Asignación de un rol a un grupo en el ámbito del recurso</span><span class="sxs-lookup"><span data-stu-id="8498c-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="8498c-146">Para conceder acceso a un grupo en el ámbito del recurso, use:</span><span class="sxs-lookup"><span data-stu-id="8498c-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="8498c-148">Quitar acceso</span><span class="sxs-lookup"><span data-stu-id="8498c-148">Remove access</span></span>
<span data-ttu-id="8498c-149">Para quitar el acceso de usuarios, grupos y aplicaciones, use:</span><span class="sxs-lookup"><span data-stu-id="8498c-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="8498c-151">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="8498c-151">Create a custom role</span></span>
<span data-ttu-id="8498c-152">Para crear un rol personalizado, use el comando ```New-AzureRmRoleDefinition``` .</span><span class="sxs-lookup"><span data-stu-id="8498c-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="8498c-153">Existen dos métodos para estructurar el rol: por medio de PSRoleDefinitionObject o una plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="8498c-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="8498c-154">Acciones Get para un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="8498c-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="8498c-155">A la hora de crear roles personalizados desde el principio, es importante conocer todas las operaciones posibles de los proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="8498c-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="8498c-156">Use el comando ```Get-AzureRMProviderOperation``` para obtener esta información.</span><span class="sxs-lookup"><span data-stu-id="8498c-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="8498c-157">Por ejemplo, si quiere comprobar todas las operaciones disponibles para la máquina virtual, use este comando:</span><span class="sxs-lookup"><span data-stu-id="8498c-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="8498c-158">Creación de rol con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="8498c-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="8498c-159">Al usar PowerShell para crear un rol personalizado, puede empezar desde cero o usar uno de los [roles integrados](role-based-access-built-in-roles.md) como punto de partida.</span><span class="sxs-lookup"><span data-stu-id="8498c-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="8498c-160">En el ejemplo de esta sección se empieza con un rol integrado y, luego, se personaliza con más privilegios.</span><span class="sxs-lookup"><span data-stu-id="8498c-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="8498c-161">Edite los atributos para agregar cualquier elemento *Actions*, *notActions* o *scopes* que quiera y guarde los cambios como un nuevo rol.</span><span class="sxs-lookup"><span data-stu-id="8498c-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="8498c-162">El ejemplo siguiente se inicia con el rol *Colaborador de la máquina virtual* y lo usa para crear un rol personalizado denominado *Operador de máquina virtual*.</span><span class="sxs-lookup"><span data-stu-id="8498c-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="8498c-163">El nuevo rol concede acceso a todas las operaciones de lectura de los proveedores de recursos *Microsoft.Compute*, *Microsoft.Storage* y *Microsoft.Network*, y concede acceso para iniciar, reiniciar y supervisar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8498c-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="8498c-164">El rol personalizado se puede usar en dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="8498c-164">The custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="8498c-166">Creación de rol con plantilla JSON</span><span class="sxs-lookup"><span data-stu-id="8498c-166">Create role with JSON template</span></span>
<span data-ttu-id="8498c-167">Se puede usar una plantilla JSON como definición de origen para el rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="8498c-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="8498c-168">En el ejemplo siguiente se crea un rol personalizado que permite el acceso de lectura a recursos de almacenamiento y proceso y el acceso a la asistencia técnica, y además agrega ese rol a dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="8498c-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="8498c-169">Cree un archivo `C:\CustomRoles\customrole1.json` con el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8498c-169">Create a new file `C:\CustomRoles\customrole1.json` with the following example.</span></span> <span data-ttu-id="8498c-170">El identificador se debe establecer en `null` durante la creación de rol inicial ya que se generará un nuevo identificador automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8498c-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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
<span data-ttu-id="8498c-171">Para agregar el rol a las suscripciones, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8498c-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="8498c-172">Modificación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="8498c-172">Modify a custom role</span></span>
<span data-ttu-id="8498c-173">De modo similar a la creación de un rol personalizado, puede modificar un rol personalizado existente por medio de PSRoleDefinitionObject o una plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="8498c-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="8498c-174">Modificación de rol con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="8498c-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="8498c-175">Para modificar un rol personalizado, use en primer lugar el comando `Get-AzureRmRoleDefinition` para recuperar la definición de rol.</span><span class="sxs-lookup"><span data-stu-id="8498c-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="8498c-176">Después, haga los cambios que desee en la definición de rol.</span><span class="sxs-lookup"><span data-stu-id="8498c-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="8498c-177">Por último, use el comando `Set-AzureRmRoleDefinition` para guardar la definición de rol modificada.</span><span class="sxs-lookup"><span data-stu-id="8498c-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="8498c-178">En el ejemplo siguiente se agrega la operación `Microsoft.Insights/diagnosticSettings/*` al rol personalizado *Operador de máquina virtual* .</span><span class="sxs-lookup"><span data-stu-id="8498c-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="8498c-180">En el ejemplo siguiente se agrega una suscripción de Azure a los ámbitos asignables del rol personalizado *Operador de máquina virtual* .</span><span class="sxs-lookup"><span data-stu-id="8498c-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="8498c-182">Modificación de rol con plantilla JSON</span><span class="sxs-lookup"><span data-stu-id="8498c-182">Modify role with JSON template</span></span>
<span data-ttu-id="8498c-183">Con la anterior plantilla JSON, puede modificar fácilmente un rol personalizado existente para agregar o quitar acciones.</span><span class="sxs-lookup"><span data-stu-id="8498c-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="8498c-184">Actualice la plantilla JSON y agregue la acción de lectura para las redes tal y como se muestra en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8498c-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="8498c-185">Las definiciones que aparecen en la plantilla no se aplican de manera acumulativa a una definición existente, lo que significa que el rol aparecerá exactamente como lo especifique en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="8498c-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="8498c-186">También que necesita actualizar el identificador con el identificador del rol.</span><span class="sxs-lookup"><span data-stu-id="8498c-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="8498c-187">Si no está seguro de cuál es este valor, puede usar el cmdlet `Get-AzureRmRoleDefinition` para obtener esta información.</span><span class="sxs-lookup"><span data-stu-id="8498c-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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

<span data-ttu-id="8498c-188">Para actualizar el rol existente, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8498c-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="8498c-189">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="8498c-189">Delete a custom role</span></span>
<span data-ttu-id="8498c-190">Para eliminar un rol personalizado, use el comando `Remove-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="8498c-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="8498c-191">En el ejemplo siguiente se quita el rol personalizado *Operador de máquina virtual* .</span><span class="sxs-lookup"><span data-stu-id="8498c-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="8498c-193">Lista de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="8498c-193">List custom roles</span></span>
<span data-ttu-id="8498c-194">Para enumerar los roles que están disponibles para la asignación en un ámbito, use el comando `Get-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="8498c-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="8498c-195">En el ejemplo siguiente se enumeran todos los roles disponibles para la asignación en la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="8498c-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="8498c-197">En el ejemplo siguiente, el rol personalizado *Operador de máquina virtual* no está disponible en la suscripción *Production4*, ya que la suscripción no se encuentra entre los elementos **AssignableScopes** del rol.</span><span class="sxs-lookup"><span data-stu-id="8498c-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="8498c-199">Consulte también</span><span class="sxs-lookup"><span data-stu-id="8498c-199">See also</span></span>
* <span data-ttu-id="8498c-200">[Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="8498c-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

