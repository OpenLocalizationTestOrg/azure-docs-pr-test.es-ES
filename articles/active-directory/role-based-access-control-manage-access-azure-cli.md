---
title: aaaManage Role-Based Access Control (RBAC) con CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage Role-Based Control de acceso (RBAC) con hello Azure de línea de comandos de la interfaz por la lista de roles y roles acciones y mediante la asignación de roles toohello ámbitos de suscripción y la aplicación."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Administrar el Control de acceso basado en roles con hello Azure interfaz de línea de comandos
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [CLI de Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API DE REST](role-based-access-control-manage-access-rest.md)


Puede usar el Control de acceso basado en roles (RBAC) en hello portal de Azure y suscripción de tooyour de acceso de API de Azure Resource Manager toomanage y recursos en un nivel específico. Con esta característica, puede conceder acceso a los usuarios, grupos o entidades de servicio de Active Directory mediante la asignación de algunos toothem de roles en un ámbito determinado.

Para poder usar Azure interfaz de línea de comandos (CLI) de hello toomanage RBAC, debe tener Hola siguiendo los requisitos previos:

* CLI de Azure versión 0.8.8 o posterior. versión más reciente de tooinstall hello y asócielo con su suscripción de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager en la CLI de Azure Vaya demasiado[Using Hola CLI de Azure con el Administrador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obtener más detalles.

## <a name="list-roles"></a>Lista de roles
### <a name="list-all-available-roles"></a>Lista de todos los roles disponibles
toolist todos los roles disponibles, use:

        azure role list

Hello en el ejemplo siguiente se muestra lista Hola de *todos los roles disponibles*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Lista de las acciones de un rol
acciones de hello toolist de un rol, use:

    azure role show "<role name>"

Hello en el ejemplo siguiente se muestra acciones de Hola de hello *colaborador* y *colaborador de la máquina Virtual* roles.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Línea de comandos de Azure RBAC: vista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Lista de acceso
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Lista de las asignaciones de rol vigentes en un grupo de recursos
toolist hello las asignaciones de roles que existen en un grupo de recursos, use:

    azure role assignment list --resource-group <resource group name>

Hello en el ejemplo siguiente se muestra las asignaciones de roles de Hola Hola *projecforcast de ventas de pharma* grupo.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Línea de comandos de Azure RBAC: lista de asignación de roles de Azure por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Lista de las asignaciones de rol de un usuario
asignaciones de roles de hello toolist para un usuario específico y asignaciones de Hola que están asignados a grupos del usuario tooa, use:

    azure role assignment list --signInName <user email>

También puede ver las asignaciones de roles que se heredan de grupos mediante la modificación de comando hello:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Hello en el ejemplo siguiente se muestra las asignaciones de roles de Hola que se conceden toohello  *sameert@aaddemo.com*  usuario. Esto incluye los roles que se heredan los grupos y roles que se asignan directamente toohello usuario.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Línea de comandos de Azure RBAC: lista de asignación de roles de Azure por usuario (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Conceder acceso
acceso de toogrant después de haber identificado el rol de Hola que desea tooassign, use:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Asignar un toogroup de rol en el ámbito de la suscripción de Hola
tooassign un grupo de tooa de rol en el ámbito de la suscripción de hello, use:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hello en el ejemplo siguiente se asigna hello *lector* rol demasiado*equipo de Christine Koch* en hello *suscripción* ámbito.

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Asignación de una aplicación de tooan de rol en el ámbito de la suscripción de Hola
tooassign una aplicación de tooan de rol en el ámbito de la suscripción de hello, use:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hello en el ejemplo siguiente se concede hello *colaborador* rol tooan *Azure AD* aplicación Hola seleccionado la suscripción.

 ![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por aplicación (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Asignar a un usuario de tooa de rol en el ámbito de grupo de recursos de Hola
tooassign un usuario de tooa de rol en el ámbito de grupo de recursos de hello, use:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Hello en el ejemplo siguiente se concede hello *colaborador de la máquina Virtual* rol demasiado *samert@aaddemo.com*  usuario en hello *ProjectForcast de ventas de Pharma* ámbito de grupo de recursos.

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por usuario (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Asignar a un grupo de tooa de rol en el ámbito de recursos de Hola
tooassign un grupo de tooa de rol en el ámbito de recursos de hello, use:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Hello en el ejemplo siguiente se concede hello *colaborador de la máquina Virtual* rol tooan *Azure AD* grupo un *subred*.

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Quitar acceso
tooremove una asignación de roles, use:

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

Hello en el ejemplo siguiente se quita hello *colaborador de la máquina Virtual* asignación de roles de hello  *sammert@aaddemo.com*  usuario en hello *ProjectForcast de ventas de Pharma* grupo de recursos.
ejemplo de Hola, a continuación, quita asignación de roles de Hola de un grupo de suscripción de Hola.

![Línea de comandos de Azure RBAC: asignación de roles de Azure eliminada (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Crear un rol personalizado
toocreate un rol personalizado, use:

    azure role create --inputfile <file path>

Hello en el ejemplo siguiente se crea un rol personalizado denominado *operador de máquina Virtual*. Este rol de seguridad concede acceso tooall lee las operaciones de *Microsoft.Compute*, *almacenamiento de Microsoft*, y *Microsoft.Network* acceso a los proveedores y concede recursos toostart, reiniciar y supervisar las máquinas virtuales. El rol personalizado se puede usar en dos suscripciones. En este ejemplo, se usa un archivo JSON como entrada.

![JSON: definición de roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Línea de comandos de Azure RBAC: creación de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Modificación de un rol personalizado
toomodify un rol personalizado, utilice primero hello `azure role show` comando tooretrieve definición de roles. En segundo lugar, asegúrese de archivo de definición de rol toohello de hello cambios deseados. Por último, utilice `azure role set` toosave Hola modificó la definición de rol.

    azure role set --inputfile <file path>

Hello en el ejemplo siguiente se agrega hello *Microsoft.Insights/diagnosticSettings/* operación toohello **acciones**y una suscripción de Azure toohello **AssignableScopes**de roles personalizados de hello operador de máquina Virtual.

![JSON: modificación de definición de roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Línea de comandos de Azure RBAC: establecimiento de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Eliminación de un rol personalizado
toodelete un rol personalizado, utilice primero hello `azure role show` comando toodetermine hello **identificador** del rol de Hola. A continuación, usar hello `azure role delete` rol de hello toodelete de comando mediante la especificación de hello **identificador**.

Hello en el ejemplo siguiente se quita hello *operador de máquina Virtual* roles personalizados.

![Línea de comandos de Azure RBAC: eliminación de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Lista de roles personalizados
roles de hello toolist que están disponibles para la asignación en un ámbito, usar hello `azure role list` comando.

Hola siguiente comando enumera todos los roles que están disponibles para la asignación de la suscripción de hello seleccionado.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

En el siguiente ejemplo de Hola Hola *operador de máquina Virtual* roles personalizados no está disponible en hello *Production4* suscripción porque esa suscripción no está en hello  **AssignableScopes** del rol de Hola.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure para roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

