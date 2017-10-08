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
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Administración del control de acceso basado en rol con Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [CLI de Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API DE REST](role-based-access-control-manage-access-rest.md)

Puede usar el Control de acceso basado en roles (RBAC) de hello portal de Azure y la suscripción de tooyour de acceso de API de administración de recursos de Azure toomanage en un nivel específico. Con esta característica, puede conceder acceso a los usuarios, grupos o entidades de servicio de Active Directory mediante la asignación de algunos toothem de roles en un ámbito determinado.

Para poder usar PowerShell toomanage RBAC, necesita Hola siguiendo los requisitos previos:

* La versión 0.8.8 o posterior de Azure PowerShell. versión más reciente de tooinstall hello y asócielo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* Cmdlets de Azure Resource Manager. Instalar hello [cmdlets de Azure Resource Manager](/powershell/azure/overview) en PowerShell.

## <a name="list-roles"></a>Lista de roles
### <a name="list-all-available-roles"></a>Lista de todos los roles disponibles
roles RBAC toolist que están disponibles para la asignación y tooinspect Hola operaciones toowhich que permita el acceso, utilice `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Lista de las acciones de un rol
acciones de hello toolist para un rol específico, use `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition para un rol específico - captura de pantalla](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Consulta de quién ha accedido
usar asignaciones de acceso de toolist RBAC, `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Lista de asignaciones de roles en un ámbito específico
Puede ver todas las asignaciones de acceso de Hola para una suscripción especificada, el grupo de recursos o el recurso. Por ejemplo, toosee Hola todas las asignaciones de hello activo para un grupo de recursos, utilice `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para un grupo de recursos - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Lista de roles tooa usuario asignado
toolist todos los roles de Hola que se asignan tooa especifican usuarios y roles de Hola que se asignan grupos de toohello toowhich Hola usuario pertenece, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment para un usuario - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Lista de asignaciones de roles de administrador y coadministrador de servicio básico
las asignaciones de acceso de toolist para Administrador de la suscripción clásico de Hola y coadministrators, use:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Conceder acceso
### <a name="search-for-object-ids"></a>Búsqueda de identificadores de objetos
tooassign un rol, deberá tooidentify Hola objetos (usuario, grupo o aplicación) y ámbito de Hola.

Si no conoce el identificador de la suscripción de hello, encontrará en hello **suscripciones** hoja en hello portal de Azure. toolearn tooquery Hola Id. de suscripción, vea [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) en MSDN.

Id. de objeto de hello tooget para un grupo de Azure AD, use:

    Get-AzureRmADGroup -SearchString <group name in quotes>

Id. de objeto de hello tooget para una entidad de servicio de Azure AD o una aplicación, use:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Asignación de una aplicación de tooan de rol en el ámbito de la suscripción de Hola
aplicación de tooan toogrant access en el ámbito de la suscripción de hello, use:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Asignar a un usuario de tooa de rol en el ámbito de grupo de recursos de Hola
toogrant acceso tooa de usuario en el ámbito de grupo de recursos de hello, use:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Asignar a un grupo de tooa de rol en el ámbito de recursos de Hola
grupo de tooa toogrant acceso en el ámbito de recursos de hello, use:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Quitar acceso
tooremove el acceso para usuarios, grupos y aplicaciones, use:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Crear un rol personalizado
toocreate un rol personalizado, use hello ```New-AzureRmRoleDefinition``` comando. Existen dos métodos de estructurar el rol de hello, con PSRoleDefinitionObject o una plantilla JSON. 

## <a name="get-actions-for-a-resource-provider"></a>Acciones Get para un proveedor de recursos
Al crear roles personalizados desde el principio, es importante tooknow todos hello las posibles operaciones de proveedores de recursos de Hola.
Hola de uso ```Get-AzureRMProviderOperation``` comando tooget esta información.
Por ejemplo, si desea que toocheck todas las operaciones disponibles hello para la máquina virtual use este comando:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Creación de rol con PSRoleDefinitionObject
Cuando se usa PowerShell toocreate un rol personalizado, puede empezar desde cero o usar uno de hello [roles integrados](role-based-access-built-in-roles.md) como punto de partida. ejemplo de Hola en esta sección comienza con un rol integrado y, a continuación, personaliza con más privilegios. Editar Hola de hello atributos tooadd *acciones*, *notActions*, o *ámbitos* que desee y, a continuación, guardar los cambios de Hola como un nuevo rol.

Hello en el ejemplo siguiente se inicia con hello *colaborador de la máquina Virtual* rol y se utiliza ese toocreate un rol personalizado denominado *operador de máquina Virtual*. nuevo rol de Hello concede acceso tooall lee las operaciones de *Microsoft.Compute*, *almacenamiento de Microsoft*, y *Microsoft.Network* acceso a los proveedores y concede recursos toostart, reiniciar y supervisar las máquinas virtuales. roles personalizados de Hello pueden usarse en dos suscripciones.

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

### <a name="create-role-with-json-template"></a>Creación de rol con plantilla JSON
Una plantilla JSON puede utilizarse como definición de origen de Hola para roles personalizados de Hola. Hello en el ejemplo siguiente se crea un rol personalizado que permite el acceso de lectura toostorage y recursos de proceso, tener acceso a toosupport y agrega ese rol tootwo suscripciones. Crear un nuevo archivo `C:\CustomRoles\customrole1.json` con el siguiente ejemplo de Hola. Hello Id. debe establecerse demasiado`null` durante la creación de rol inicial como un nuevo identificador se genera automáticamente. 

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
tooadd Hola rol toohello suscripciones, ejecute el siguiente comando de PowerShell de hello:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Modificación de un rol personalizado
Toocreating similar un rol personalizado, puede modificar un rol personalizado existente con hello PSRoleDefinitionObject o una plantilla JSON.

### <a name="modify-role-with-psroledefinitionobject"></a>Modificación de rol con PSRoleDefinitionObject
toomodify un rol personalizado, en primer lugar, utilice hello `Get-AzureRmRoleDefinition` comando definición de roles de tooretrieve Hola. En segundo lugar, realice los cambios de hello deseado toohello definición de roles. Por último, utilice hello `Set-AzureRmRoleDefinition` comando toosave hello modificó la definición de rol.

Hello en el ejemplo siguiente se agrega hello `Microsoft.Insights/diagnosticSettings/*` operación toohello *operador de máquina Virtual* roles personalizados.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Hello en el ejemplo siguiente se agrega una suscripción de Azure toohello puede asignar los ámbitos de hello *operador de máquina Virtual* roles personalizados.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Modificación de rol con plantilla JSON
Mediante la plantilla de hello anterior JSON, puede modificar una existente tooadd roles personalizados fácilmente o quitar acciones. Actualizar plantilla JSON de Hola y agregar acción de lectura de Hola para funciones de red tal y como se muestra en el siguiente ejemplo de Hola. las definiciones de Hello aparecen en la plantilla de hello no son aplicados de manera acumulativa tooan definición existente, lo que significa que esa función hello aparece exactamente tal y como se especifica en la plantilla de Hola. También debe campo de Id. de hello tooupdate con Id. de hello del rol de Hola. Si no está seguro de qué es este valor, puede usar hello `Get-AzureRmRoleDefinition` cmdlet tooget esta información.

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

tooupdate Hola rol existente, ejecute el siguiente comando de PowerShell de hello:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Eliminación de un rol personalizado
toodelete un rol personalizado, use hello `Remove-AzureRmRoleDefinition` comando.

Hello en el ejemplo siguiente se quita hello *operador de máquina Virtual* roles personalizados.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Lista de roles personalizados
roles de hello toolist que están disponibles para la asignación en un ámbito, usar hello `Get-AzureRmRoleDefinition` comando.

Hola siguiente ejemplo enumera todos los roles que están disponibles para la asignación de la suscripción de hello seleccionado.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

En el siguiente ejemplo de Hola Hola *operador de máquina Virtual* roles personalizados no está disponible en hello *Production4* suscripción porque esa suscripción no está en hello  **AssignableScopes** del rol de Hola.

![RBAC PowerShell - Get-AzureRmRoleDefinition - captura de pantalla](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Consulte también
* [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

