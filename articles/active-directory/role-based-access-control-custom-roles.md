---
title: "Creación de roles personalizados para Azure RBAC | Microsoft Docs"
description: "Aprenda a definir roles personalizados con Control de acceso basado en roles de Azure para administrar las identidades de manera más precisa en la suscripción de Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8e72f2c8095d13c4b6df3c6576bd58806a3c0f2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="0eac0-103">Creación de roles personalizados para el control de acceso basado en roles de Azure</span><span class="sxs-lookup"><span data-stu-id="0eac0-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="0eac0-104">Cree un rol personalizado en Control de acceso basado en rol (RBAC) de Azure si ninguno de los roles integrados satisface sus necesidades de acceso específicas.</span><span class="sxs-lookup"><span data-stu-id="0eac0-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="0eac0-105">Se pueden crear roles personalizados con [Azure PowerShell](role-based-access-control-manage-access-powershell.md), la [interfaz de la línea de comandos (CLI) de Azure](role-based-access-control-manage-access-azure-cli.md) y la [API de REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="0eac0-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="0eac0-106">Igual que los roles integrados, puede asignar roles personalizados a usuarios, grupos y aplicaciones en los ámbitos de suscripción, grupo de recursos y recurso.</span><span class="sxs-lookup"><span data-stu-id="0eac0-106">Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="0eac0-107">Los roles personalizados se almacenan en un inquilino de Azure AD y se pueden compartir entre suscripciones.</span><span class="sxs-lookup"><span data-stu-id="0eac0-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="0eac0-108">Cada inquilino puede crear hasta 2000 roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="0eac0-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="0eac0-109">A continuación se muestra un ejemplo de rol personalizado para supervisar y reiniciar máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="0eac0-109">The following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="0eac0-110">Acciones</span><span class="sxs-lookup"><span data-stu-id="0eac0-110">Actions</span></span>
<span data-ttu-id="0eac0-111">La propiedad **Actions** de un rol personalizado especifica las operaciones de Azure a las que el rol concede acceso.</span><span class="sxs-lookup"><span data-stu-id="0eac0-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="0eac0-112">Se trata de una colección de cadenas de operación que identifican a las operaciones protegibles de proveedores de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eac0-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="0eac0-113">Las cadenas de operaciones usan el formato `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="0eac0-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="0eac0-114">Las cadenas de la operación que contienen caracteres comodín (\*) conceden acceso a todas las operaciones que coinciden con la cadena de la operación.</span><span class="sxs-lookup"><span data-stu-id="0eac0-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="0eac0-115">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0eac0-115">For instance:</span></span>

* <span data-ttu-id="0eac0-116">`*/read` concede acceso a las operaciones de lectura a todos los tipos de recursos de todos los proveedores de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eac0-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="0eac0-117">`Microsoft.Compute/*` concede acceso a todas las operaciones a todos los tipos de recursos del proveedor de recursos Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="0eac0-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="0eac0-118">`Microsoft.Network/*/read` concede acceso a las operaciones de lectura a todos los tipos de recursos del proveedor de recursos Microsoft.Network de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eac0-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="0eac0-119">`Microsoft.Compute/virtualMachines/*` concede acceso a todas las operaciones de las máquinas virtuales y a sus tipos de recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="0eac0-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="0eac0-120">`Microsoft.Web/sites/restart/Action` concede acceso para reiniciar sitios web.</span><span class="sxs-lookup"><span data-stu-id="0eac0-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="0eac0-121">Use `Get-AzureRmProviderOperation` (en PowerShell) o `azure provider operations show` (en la CLI de Azure) para mostrar las operaciones de proveedores de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eac0-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="0eac0-122">También puede usar estos comandos para comprobar que una cadena de operación es válida y para expandir las cadenas de operación con comodín.</span><span class="sxs-lookup"><span data-stu-id="0eac0-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Captura de pantalla de PowerShell: Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="0eac0-124">Captura de pantalla de la CLI de Azure: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="0eac0-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="0eac0-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="0eac0-125">NotActions</span></span>
<span data-ttu-id="0eac0-126">Use la propiedad **NotActions** si el conjunto de operaciones que quiere permitir se define más fácilmente mediante la exclusión de las operaciones restringidas.</span><span class="sxs-lookup"><span data-stu-id="0eac0-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="0eac0-127">El acceso concedido por un rol personalizado se calcula restando las operaciones **NotActions** de las operaciones **Actions**.</span><span class="sxs-lookup"><span data-stu-id="0eac0-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="0eac0-128">Si un usuario tiene asignado un rol que excluye una operación en **NotActions** y se le asigna un segundo rol que sí concede acceso a esa operación, el usuario puede realizarla.</span><span class="sxs-lookup"><span data-stu-id="0eac0-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user is allowed to perform that operation.</span></span> <span data-ttu-id="0eac0-129">**NotActions** no es una regla de denegación, es simplemente una manera cómoda de crear un conjunto de operaciones permitidas cuando es necesario excluir operaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="0eac0-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="0eac0-130">Ámbitos asignables</span><span class="sxs-lookup"><span data-stu-id="0eac0-130">AssignableScopes</span></span>
<span data-ttu-id="0eac0-131">La propiedad **AssignableScopes** del rol personalizado especifica los ámbitos (suscripciones, grupos de recursos o recursos) dentro de los que dicho rol personalizado está disponible para su asignación.</span><span class="sxs-lookup"><span data-stu-id="0eac0-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="0eac0-132">Puede permitir que el rol personalizado esté disponible para su asignación solamente en las suscripciones o los grupos de recursos que lo requieran, sin necesidad de abarrotar la experiencia de usuario con el resto de las suscripciones o grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0eac0-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="0eac0-133">Ejemplos de ámbitos asignables válidos son:</span><span class="sxs-lookup"><span data-stu-id="0eac0-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="0eac0-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624”: permite la disponibilidad del rol para su asignación en dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="0eac0-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="0eac0-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”: permite la disponibilidad del rol para su asignación en una sola suscripción.</span><span class="sxs-lookup"><span data-stu-id="0eac0-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="0eac0-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network”: permite la disponibilidad del rol para su asignación solamente en el grupo de recursos de red.</span><span class="sxs-lookup"><span data-stu-id="0eac0-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="0eac0-137">Tiene que utilizar al menos una suscripción, grupo de recursos o identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="0eac0-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="0eac0-138">Control de acceso de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="0eac0-138">Custom roles access control</span></span>
<span data-ttu-id="0eac0-139">La propiedad **AssignableScopes** del rol personalizado también controla quién puede ver, modificar y eliminar el rol.</span><span class="sxs-lookup"><span data-stu-id="0eac0-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="0eac0-140">¿Quién puede crear un rol personalizado?</span><span class="sxs-lookup"><span data-stu-id="0eac0-140">Who can create a custom role?</span></span>
    <span data-ttu-id="0eac0-141">Los propietarios (y administradores del acceso de los usuarios) de las suscripciones, los grupos de recursos y los recursos pueden crear roles personalizados para su uso en esos ámbitos.</span><span class="sxs-lookup"><span data-stu-id="0eac0-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="0eac0-142">El usuario que crea el rol debe ser capaz de realizar la operación `Microsoft.Authorization/roleDefinition/write` en todos los elementos **AssignableScopes** del rol.</span><span class="sxs-lookup"><span data-stu-id="0eac0-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="0eac0-143">¿Quién puede modificar un rol personalizado?</span><span class="sxs-lookup"><span data-stu-id="0eac0-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="0eac0-144">Los propietarios (y administradores del acceso de los usuarios) de las suscripciones, los grupos de recursos y los recursos pueden modificar roles personalizados en esos ámbitos.</span><span class="sxs-lookup"><span data-stu-id="0eac0-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="0eac0-145">Los usuarios deben poder realizar la operación `Microsoft.Authorization/roleDefinition/write` en todos los elementos **AssignableScopes** de un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="0eac0-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="0eac0-146">¿Quién puede ver los roles personalizados?</span><span class="sxs-lookup"><span data-stu-id="0eac0-146">Who can view custom roles?</span></span>
    <span data-ttu-id="0eac0-147">Todos los roles integrados de RBAC de Azure permiten ver los roles que están disponibles para la asignación.</span><span class="sxs-lookup"><span data-stu-id="0eac0-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="0eac0-148">Los usuarios que pueden realizar la operación `Microsoft.Authorization/roleDefinition/read` en un ámbito, pueden ver los roles RBAC que están disponibles para su asignación en ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="0eac0-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="0eac0-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="0eac0-149">See also</span></span>
* <span data-ttu-id="0eac0-150">[Control de acceso basado en roles de Azure](role-based-access-control-configure.md): introducción a RBAC en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eac0-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="0eac0-151">Aprenda a administrar el acceso con:</span><span class="sxs-lookup"><span data-stu-id="0eac0-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="0eac0-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0eac0-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="0eac0-153">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0eac0-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="0eac0-154">API DE REST</span><span class="sxs-lookup"><span data-stu-id="0eac0-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="0eac0-155">[Roles integrados](role-based-access-built-in-roles.md): obtenga información sobre los roles incluidos de forma predeterminada en RBAC.</span><span class="sxs-lookup"><span data-stu-id="0eac0-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
