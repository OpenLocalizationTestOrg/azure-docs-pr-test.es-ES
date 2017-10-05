---
title: "Administración del control de acceso basado en rol (RBAC) con la CLI de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo administrar el control de acceso basado en rol (RBAC) con la interfaz de la línea de comandos de Azure a través de la enumeración de roles y acciones de roles y de la asignación de roles a los ámbitos de aplicación y suscripción."
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
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="749bf-103">Administración del control de acceso basado en rol con la interfaz de la línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="749bf-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="749bf-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="749bf-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="749bf-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="749bf-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="749bf-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="749bf-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="749bf-107">Puede usar el control de acceso basado en rol (RBAC) del Portal de Azure y la API de Azure Resource Manager para administrar el acceso a su suscripción y sus recursos en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="749bf-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="749bf-108">Con esta característica, puede conceder acceso a usuarios, grupos o entidades de seguridad de servicio de Active Directory asignándoles roles en un ámbito determinado.</span><span class="sxs-lookup"><span data-stu-id="749bf-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="749bf-109">Para poder usar la interfaz de la línea de comandos (CLI) de Azure y administrar RBAC, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="749bf-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="749bf-110">CLI de Azure versión 0.8.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="749bf-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="749bf-111">Para instalar la última versión y asociarla a la suscripción de Azure, consulte [Instalación y configuración de la interfaz de la línea de comandos de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="749bf-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="749bf-112">Azure Resource Manager en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="749bf-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="749bf-113">Para más información, consulte [Uso de la CLI de Azure con Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="749bf-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="749bf-114">Lista de roles</span><span class="sxs-lookup"><span data-stu-id="749bf-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="749bf-115">Lista de todos los roles disponibles</span><span class="sxs-lookup"><span data-stu-id="749bf-115">List all available roles</span></span>
<span data-ttu-id="749bf-116">Para enumerar todos los roles disponibles, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="749bf-117">El ejemplo siguiente muestra la lista de *todos los roles disponibles*.</span><span class="sxs-lookup"><span data-stu-id="749bf-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="749bf-119">Lista de las acciones de un rol</span><span class="sxs-lookup"><span data-stu-id="749bf-119">List actions of a role</span></span>
<span data-ttu-id="749bf-120">Para enumerar las acciones de un rol, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="749bf-121">El ejemplo siguiente muestra las acciones del rol *Colaborador* y del rol *Colaborador de la máquina virtual*.</span><span class="sxs-lookup"><span data-stu-id="749bf-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Línea de comandos de Azure RBAC: vista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="749bf-123">Lista de acceso</span><span class="sxs-lookup"><span data-stu-id="749bf-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="749bf-124">Lista de las asignaciones de rol vigentes en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="749bf-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="749bf-125">Para mostrar las asignaciones de roles de un grupo de recursos, utilice:</span><span class="sxs-lookup"><span data-stu-id="749bf-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="749bf-126">En el ejemplo siguiente, se muestran las asignaciones de roles del grupo *pharma-sales-projecforcast* .</span><span class="sxs-lookup"><span data-stu-id="749bf-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Línea de comandos de Azure RBAC: lista de asignación de roles de Azure por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="749bf-128">Lista de las asignaciones de rol de un usuario</span><span class="sxs-lookup"><span data-stu-id="749bf-128">List role assignments for a user</span></span>
<span data-ttu-id="749bf-129">Para enumerar las asignaciones de rol de un usuario específico y las asignaciones de los grupos de un usuario, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="749bf-130">También puede ver las asignaciones de roles que se heredan de grupos modificando el comando:</span><span class="sxs-lookup"><span data-stu-id="749bf-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="749bf-131">En el ejemplo siguiente, se muestran las asignaciones de rol concedidas al usuario *sameert@aaddemo.com* .</span><span class="sxs-lookup"><span data-stu-id="749bf-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="749bf-132">Entre ellas, los roles asignados directamente al usuario y los roles que se heredan de los grupos.</span><span class="sxs-lookup"><span data-stu-id="749bf-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Línea de comandos de Azure RBAC: lista de asignación de roles de Azure por usuario (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="749bf-134">Conceder acceso</span><span class="sxs-lookup"><span data-stu-id="749bf-134">Grant access</span></span>
<span data-ttu-id="749bf-135">Para conceder acceso después de haber identificado el rol que desea asignar, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="749bf-136">Asignación de un rol a un grupo en el ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="749bf-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="749bf-137">Para asignar un rol a un grupo en el ámbito de la suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="749bf-138">En el ejemplo siguiente se asigna el rol *Lector* al *equipo de Christine Koch* en el ámbito de la *suscripción*.</span><span class="sxs-lookup"><span data-stu-id="749bf-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="749bf-140">Asignación de un rol a una aplicación en el ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="749bf-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="749bf-141">Para asignar un rol a una aplicación en el ámbito de la suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="749bf-142">En el ejemplo siguiente, se concede el rol *Colaborador* a una aplicación de *Azure AD* en la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="749bf-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por aplicación (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="749bf-144">Asignación de un rol a un usuario en el ámbito del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="749bf-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="749bf-145">Para asignar un rol a un usuario en el ámbito del grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="749bf-146">En el ejemplo siguiente, se concede el rol *Colaborador de la máquina virtual* al usuario *samert@aaddemo.com* en el ámbito del grupo de recursos *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="749bf-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por usuario (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="749bf-148">Asignación de un rol a un grupo en el ámbito del recurso</span><span class="sxs-lookup"><span data-stu-id="749bf-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="749bf-149">Para asignar un rol a un grupo en el ámbito del recurso, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="749bf-150">En el ejemplo siguiente, se concede el rol *Colaborador de la máquina virtual* a un grupo de *Azure AD* en una *subred*.</span><span class="sxs-lookup"><span data-stu-id="749bf-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure creada por grupo (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="749bf-152">Quitar acceso</span><span class="sxs-lookup"><span data-stu-id="749bf-152">Remove access</span></span>
<span data-ttu-id="749bf-153">Para quitar una asignación de rol, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="749bf-154">En el ejemplo siguiente, se quita la asignación de rol *Colaborador de la máquina virtual* del usuario *sammert@aaddemo.com* en el grupo de recursos *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="749bf-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="749bf-155">Luego, se quita la asignación de rol de un grupo de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="749bf-155">The example then removes the role assignment from a group on the subscription.</span></span>

![Línea de comandos de Azure RBAC: asignación de roles de Azure eliminada (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="749bf-157">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="749bf-157">Create a custom role</span></span>
<span data-ttu-id="749bf-158">Para crear un rol personalizado, use:</span><span class="sxs-lookup"><span data-stu-id="749bf-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="749bf-159">En el ejemplo siguiente, se crea un rol personalizado llamado *Operador de máquina virtual*.</span><span class="sxs-lookup"><span data-stu-id="749bf-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="749bf-160">El rol personalizado concede acceso a todas las operaciones de lectura de los proveedores de recursos *Microsoft.Compute*, *Microsoft.Storage* y *Microsoft.Network*, y concede acceso para iniciar, reiniciar y supervisar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="749bf-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="749bf-161">El rol personalizado se puede usar en dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="749bf-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="749bf-162">En este ejemplo, se usa un archivo JSON como entrada.</span><span class="sxs-lookup"><span data-stu-id="749bf-162">This example uses a JSON file as an input.</span></span>

![JSON: definición de roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Línea de comandos de Azure RBAC: creación de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="749bf-165">Modificación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="749bf-165">Modify a custom role</span></span>
<span data-ttu-id="749bf-166">Para modificar un rol personalizado, use en primer lugar el comando `azure role show` para recuperar la definición de rol.</span><span class="sxs-lookup"><span data-stu-id="749bf-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="749bf-167">Después, haga los cambios que desee en el archivo de definición de rol.</span><span class="sxs-lookup"><span data-stu-id="749bf-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="749bf-168">Por último, use `azure role set` para guardar la definición de rol modificada.</span><span class="sxs-lookup"><span data-stu-id="749bf-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="749bf-169">En el ejemplo siguiente, se agrega la operación *Microsoft.Insights/diagnosticSettings/* a **Acciones** y una suscripción de Azure al valor de **AssignableScopes** del rol personalizado de operador de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="749bf-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON: modificación de definición de roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Línea de comandos de Azure RBAC: establecimiento de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="749bf-172">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="749bf-172">Delete a custom role</span></span>
<span data-ttu-id="749bf-173">Para eliminar un rol personalizado, use primero el comando `azure role show` para determinar el **id.** del rol.</span><span class="sxs-lookup"><span data-stu-id="749bf-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="749bf-174">Luego, use el comando `azure role delete` para eliminar el rol especificando el **id**.</span><span class="sxs-lookup"><span data-stu-id="749bf-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="749bf-175">En el ejemplo siguiente se quita el rol personalizado *Operador de máquina virtual* .</span><span class="sxs-lookup"><span data-stu-id="749bf-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![Línea de comandos de Azure RBAC: eliminación de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="749bf-177">Lista de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="749bf-177">List custom roles</span></span>
<span data-ttu-id="749bf-178">Para enumerar los roles que están disponibles para la asignación en un ámbito, use el comando `azure role list` .</span><span class="sxs-lookup"><span data-stu-id="749bf-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="749bf-179">En el comando siguiente se enumeran todos los roles disponibles para la asignación en la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="749bf-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="749bf-181">En el ejemplo siguiente, el rol personalizado *Operador de máquina virtual* no está disponible en la suscripción *Production4* debido a que la suscripción no se encuentra entre los valores de **AssignableScopes** del rol.</span><span class="sxs-lookup"><span data-stu-id="749bf-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Línea de comandos de Azure RBAC: lista de roles de Azure para roles personalizados (captura de pantalla)](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="749bf-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="749bf-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

