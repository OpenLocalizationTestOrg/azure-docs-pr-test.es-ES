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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="dd9ba-103">Administrar el Control de acceso basado en roles con hello Azure interfaz de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="dd9ba-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd9ba-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd9ba-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="dd9ba-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dd9ba-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="dd9ba-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="dd9ba-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="dd9ba-107">Puede usar el Control de acceso basado en roles (RBAC) en hello portal de Azure y suscripción de tooyour de acceso de API de Azure Resource Manager toomanage y recursos en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="dd9ba-108">Con esta característica, puede conceder acceso a los usuarios, grupos o entidades de servicio de Active Directory mediante la asignación de algunos toothem de roles en un ámbito determinado.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="dd9ba-109">Para poder usar Azure interfaz de línea de comandos (CLI) de hello toomanage RBAC, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="dd9ba-110">CLI de Azure versión 0.8.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="dd9ba-111">versión más reciente de tooinstall hello y asócielo con su suscripción de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dd9ba-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="dd9ba-112">Azure Resource Manager en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dd9ba-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="dd9ba-113">Vaya demasiado[Using Hola CLI de Azure con el Administrador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="dd9ba-114">Lista de roles</span><span class="sxs-lookup"><span data-stu-id="dd9ba-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="dd9ba-115">Lista de todos los roles disponibles</span><span class="sxs-lookup"><span data-stu-id="dd9ba-115">List all available roles</span></span>
<span data-ttu-id="dd9ba-116">toolist todos los roles disponibles, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="dd9ba-117">Hello en el ejemplo siguiente se muestra lista Hola de *todos los roles disponibles*.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="dd9ba-119">Lista de las acciones de un rol</span><span class="sxs-lookup"><span data-stu-id="dd9ba-119">List actions of a role</span></span>
<span data-ttu-id="dd9ba-120">acciones de hello toolist de un rol, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="dd9ba-121">Hello en el ejemplo siguiente se muestra acciones de Hola de hello *colaborador* y *colaborador de la máquina Virtual* roles.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Línea de comandos de Azure RBAC: vista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="dd9ba-123">Lista de acceso</span><span class="sxs-lookup"><span data-stu-id="dd9ba-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="dd9ba-124">Lista de las asignaciones de rol vigentes en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dd9ba-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="dd9ba-125">toolist hello las asignaciones de roles que existen en un grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="dd9ba-126">Hello en el ejemplo siguiente se muestra las asignaciones de roles de Hola Hola *projecforcast de ventas de pharma* grupo.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Línea de comandos de Azure RBAC: lista de asignación de roles de Azure por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="dd9ba-128">Lista de las asignaciones de rol de un usuario</span><span class="sxs-lookup"><span data-stu-id="dd9ba-128">List role assignments for a user</span></span>
<span data-ttu-id="dd9ba-129">asignaciones de roles de hello toolist para un usuario específico y asignaciones de Hola que están asignados a grupos del usuario tooa, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="dd9ba-130">También puede ver las asignaciones de roles que se heredan de grupos mediante la modificación de comando hello:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="dd9ba-131">Hello en el ejemplo siguiente se muestra las asignaciones de roles de Hola que se conceden toohello  *sameert@aaddemo.com*  usuario.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="dd9ba-132">Esto incluye los roles que se heredan los grupos y roles que se asignan directamente toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Línea de comandos de Azure RBAC: lista de asignación de roles de Azure por usuario (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="dd9ba-134">Conceder acceso</span><span class="sxs-lookup"><span data-stu-id="dd9ba-134">Grant access</span></span>
<span data-ttu-id="dd9ba-135">acceso de toogrant después de haber identificado el rol de Hola que desea tooassign, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="dd9ba-136">Asignar un toogroup de rol en el ámbito de la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="dd9ba-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="dd9ba-137">tooassign un grupo de tooa de rol en el ámbito de la suscripción de hello, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="dd9ba-138">Hello en el ejemplo siguiente se asigna hello *lector* rol demasiado*equipo de Christine Koch* en hello *suscripción* ámbito.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="dd9ba-140">Asignación de una aplicación de tooan de rol en el ámbito de la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="dd9ba-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="dd9ba-141">tooassign una aplicación de tooan de rol en el ámbito de la suscripción de hello, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="dd9ba-142">Hello en el ejemplo siguiente se concede hello *colaborador* rol tooan *Azure AD* aplicación Hola seleccionado la suscripción.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por aplicación (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="dd9ba-144">Asignar a un usuario de tooa de rol en el ámbito de grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="dd9ba-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="dd9ba-145">tooassign un usuario de tooa de rol en el ámbito de grupo de recursos de hello, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="dd9ba-146">Hello en el ejemplo siguiente se concede hello *colaborador de la máquina Virtual* rol demasiado *samert@aaddemo.com*  usuario en hello *ProjectForcast de ventas de Pharma* ámbito de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por usuario (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="dd9ba-148">Asignar a un grupo de tooa de rol en el ámbito de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="dd9ba-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="dd9ba-149">tooassign un grupo de tooa de rol en el ámbito de recursos de hello, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="dd9ba-150">Hello en el ejemplo siguiente se concede hello *colaborador de la máquina Virtual* rol tooan *Azure AD* grupo un *subred*.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="dd9ba-152">Quitar acceso</span><span class="sxs-lookup"><span data-stu-id="dd9ba-152">Remove access</span></span>
<span data-ttu-id="dd9ba-153">tooremove una asignación de roles, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="dd9ba-154">Hello en el ejemplo siguiente se quita hello *colaborador de la máquina Virtual* asignación de roles de hello  *sammert@aaddemo.com*  usuario en hello *ProjectForcast de ventas de Pharma* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="dd9ba-155">ejemplo de Hola, a continuación, quita asignación de roles de Hola de un grupo de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure eliminada (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="dd9ba-157">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="dd9ba-157">Create a custom role</span></span>
<span data-ttu-id="dd9ba-158">toocreate un rol personalizado, use:</span><span class="sxs-lookup"><span data-stu-id="dd9ba-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="dd9ba-159">Hello en el ejemplo siguiente se crea un rol personalizado denominado *operador de máquina Virtual*.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="dd9ba-160">Este rol de seguridad concede acceso tooall lee las operaciones de *Microsoft.Compute*, *almacenamiento de Microsoft*, y *Microsoft.Network* acceso a los proveedores y concede recursos toostart, reiniciar y supervisar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="dd9ba-161">El rol personalizado se puede usar en dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="dd9ba-162">En este ejemplo, se usa un archivo JSON como entrada.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-162">This example uses a JSON file as an input.</span></span>

![JSON: definición de roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Línea de comandos de Azure RBAC: creación de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="dd9ba-165">Modificación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="dd9ba-165">Modify a custom role</span></span>
<span data-ttu-id="dd9ba-166">toomodify un rol personalizado, utilice primero hello `azure role show` comando tooretrieve definición de roles.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="dd9ba-167">En segundo lugar, asegúrese de archivo de definición de rol toohello de hello cambios deseados.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="dd9ba-168">Por último, utilice `azure role set` toosave Hola modificó la definición de rol.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="dd9ba-169">Hello en el ejemplo siguiente se agrega hello *Microsoft.Insights/diagnosticSettings/* operación toohello **acciones**y una suscripción de Azure toohello **AssignableScopes**de roles personalizados de hello operador de máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON: modificación de definición de roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Línea de comandos de Azure RBAC: establecimiento de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="dd9ba-172">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="dd9ba-172">Delete a custom role</span></span>
<span data-ttu-id="dd9ba-173">toodelete un rol personalizado, utilice primero hello `azure role show` comando toodetermine hello **identificador** del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="dd9ba-174">A continuación, usar hello `azure role delete` rol de hello toodelete de comando mediante la especificación de hello **identificador**.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="dd9ba-175">Hello en el ejemplo siguiente se quita hello *operador de máquina Virtual* roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Línea de comandos de Azure RBAC: eliminación de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="dd9ba-177">Lista de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="dd9ba-177">List custom roles</span></span>
<span data-ttu-id="dd9ba-178">roles de hello toolist que están disponibles para la asignación en un ámbito, usar hello `azure role list` comando.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="dd9ba-179">Hola siguiente comando enumera todos los roles que están disponibles para la asignación de la suscripción de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="dd9ba-181">En el siguiente ejemplo de Hola Hola *operador de máquina Virtual* roles personalizados no está disponible en hello *Production4* suscripción porque esa suscripción no está en hello  **AssignableScopes** del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd9ba-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure para roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="dd9ba-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd9ba-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

