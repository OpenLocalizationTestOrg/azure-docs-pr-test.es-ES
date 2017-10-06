---
title: aaaCreate roles personalizados para RBAC de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodefine de roles personalizados con Control de acceso de Azure Role-Based para una administración más pormenorizada de identidad en la suscripción de Azure."
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
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="1e03b-103">Creación de roles personalizados para el control de acceso basado en roles de Azure</span><span class="sxs-lookup"><span data-stu-id="1e03b-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="1e03b-104">Crear un rol personalizado en el Control de acceso de Azure Role-Based (RBAC) si ninguna de las funciones integradas de hello satisface sus necesidades de acceso específico.</span><span class="sxs-lookup"><span data-stu-id="1e03b-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="1e03b-105">Roles personalizados pueden crearse con [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfaz de línea de comandos de Azure](role-based-access-control-manage-access-azure-cli.md) (CLI), hello y [API de REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="1e03b-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="1e03b-106">Al igual que las funciones integradas, puede asignar roles personalizados toousers, grupos y aplicaciones en la suscripción, grupo de recursos y ámbitos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e03b-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="1e03b-107">Los roles personalizados se almacenan en un inquilino de Azure AD y se pueden compartir entre suscripciones.</span><span class="sxs-lookup"><span data-stu-id="1e03b-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="1e03b-108">Cada inquilino puede crear los roles personalizados too2000.</span><span class="sxs-lookup"><span data-stu-id="1e03b-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="1e03b-109">Hello en el ejemplo siguiente se muestra una función personalizada para la supervisión y reiniciar máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="1e03b-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="1e03b-110">Acciones</span><span class="sxs-lookup"><span data-stu-id="1e03b-110">Actions</span></span>
<span data-ttu-id="1e03b-111">Hola **acciones** propiedad de un rol personalizado especifica hello Azure operaciones toowhich Hola función concede acceso.</span><span class="sxs-lookup"><span data-stu-id="1e03b-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="1e03b-112">Se trata de una colección de cadenas de operación que identifican a las operaciones protegibles de proveedores de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e03b-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="1e03b-113">Las cadenas de operación seguir el formato de Hola de `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="1e03b-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="1e03b-114">Las cadenas de operación que contienen caracteres comodín (\*) conceder acceso tooall operaciones que coinciden con la cadena de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e03b-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="1e03b-115">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e03b-115">For instance:</span></span>

* <span data-ttu-id="1e03b-116">`*/read`concede acceso a las operaciones de tooread para todos los tipos de recursos de todos los proveedores de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e03b-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="1e03b-117">`Microsoft.Compute/*`concede acceso a las operaciones de tooall para todos los tipos de recursos de proveedor de recursos de Microsoft.Compute Hola.</span><span class="sxs-lookup"><span data-stu-id="1e03b-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="1e03b-118">`Microsoft.Network/*/read`concede acceso a las operaciones de tooread para todos los tipos de recursos de proveedor de recursos de Microsoft.Network Hola de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e03b-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="1e03b-119">`Microsoft.Compute/virtualMachines/*`concede acceso a las operaciones de tooall de máquinas virtuales y sus tipos de recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="1e03b-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="1e03b-120">`Microsoft.Web/sites/restart/Action`concede acceso a sitios Web de toorestart.</span><span class="sxs-lookup"><span data-stu-id="1e03b-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="1e03b-121">Use `Get-AzureRmProviderOperation` (en PowerShell) o `azure provider operations show` (en CLI de Azure) operaciones toolist de proveedores de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e03b-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="1e03b-122">También puede usar estas cadenas de operación de comodín tooexpand y tooverify de comandos que una cadena de la operación es válida.</span><span class="sxs-lookup"><span data-stu-id="1e03b-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Captura de pantalla de PowerShell: Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="1e03b-124">Captura de pantalla de la CLI de Azure: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="1e03b-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="1e03b-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="1e03b-125">NotActions</span></span>
<span data-ttu-id="1e03b-126">Hola de uso **NotActions** propiedad si conjunto Hola de operaciones que desea tooallow se define más fácilmente mediante la exclusión de operaciones restringidas.</span><span class="sxs-lookup"><span data-stu-id="1e03b-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="1e03b-127">Hello acceso concedido por un rol personalizado se calcula restando hello **NotActions** las operaciones de hello **acciones** operaciones.</span><span class="sxs-lookup"><span data-stu-id="1e03b-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="1e03b-128">Si un usuario está asignado un rol que excluye una operación en **NotActions**y se le asigna un segundo rol que concede acceso toohello es la misma operación, el usuario de hello permite tooperform esa operación.</span><span class="sxs-lookup"><span data-stu-id="1e03b-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="1e03b-129">**NotActions** no es una instrucción deny de regla: es simplemente una toocreate de forma adecuada un conjunto de operaciones permitidas cuando las operaciones concretas necesitan toobe excluido.</span><span class="sxs-lookup"><span data-stu-id="1e03b-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="1e03b-130">Ámbitos asignables</span><span class="sxs-lookup"><span data-stu-id="1e03b-130">AssignableScopes</span></span>
<span data-ttu-id="1e03b-131">Hola **AssignableScopes** propiedad del rol personalizado Hola especifica los ámbitos de hello (suscripciones, grupos de recursos o recursos) dentro de qué Hola está disponible para la asignación de roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="1e03b-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="1e03b-132">Puede realizar disponibles para la asignación de roles personalizados de hello en suscripciones de hello solo o la experiencia de los grupos de recursos que requieren la base de datos y no el usuario de acumulación de elementos de rest de Hola de suscripciones de Hola o grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e03b-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="1e03b-133">Ejemplos de ámbitos asignables válidos son:</span><span class="sxs-lookup"><span data-stu-id="1e03b-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="1e03b-134">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - pone a disposición para la asignación de rol de hello en dos suscripciones.</span><span class="sxs-lookup"><span data-stu-id="1e03b-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="1e03b-135">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - pone a disposición para la asignación de rol de hello en una sola suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e03b-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="1e03b-136">"/ suscripciones/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/red" - hace Hola roles disponibles para la asignación solo en el grupo de recursos de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e03b-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="1e03b-137">Tiene que utilizar al menos una suscripción, grupo de recursos o identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="1e03b-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="1e03b-138">Control de acceso de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="1e03b-138">Custom roles access control</span></span>
<span data-ttu-id="1e03b-139">Hola **AssignableScopes** propiedad de roles personalizados de hello también controla quién puede ver, modificar y eliminar el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e03b-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="1e03b-140">¿Quién puede crear un rol personalizado?</span><span class="sxs-lookup"><span data-stu-id="1e03b-140">Who can create a custom role?</span></span>
    <span data-ttu-id="1e03b-141">Los propietarios (y administradores del acceso de los usuarios) de las suscripciones, los grupos de recursos y los recursos pueden crear roles personalizados para su uso en esos ámbitos.</span><span class="sxs-lookup"><span data-stu-id="1e03b-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="1e03b-142">usuario que crea el rol de Hola Hola necesita toobe capaz de tooperform `Microsoft.Authorization/roleDefinition/write` operación en todos los hello **AssignableScopes** del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e03b-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="1e03b-143">¿Quién puede modificar un rol personalizado?</span><span class="sxs-lookup"><span data-stu-id="1e03b-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="1e03b-144">Los propietarios (y administradores del acceso de los usuarios) de las suscripciones, los grupos de recursos y los recursos pueden modificar roles personalizados en esos ámbitos.</span><span class="sxs-lookup"><span data-stu-id="1e03b-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="1e03b-145">Los usuarios necesitan toobe tooperform capaz de hello `Microsoft.Authorization/roleDefinition/write` operación en todos los hello **AssignableScopes** de un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="1e03b-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="1e03b-146">¿Quién puede ver los roles personalizados?</span><span class="sxs-lookup"><span data-stu-id="1e03b-146">Who can view custom roles?</span></span>
    <span data-ttu-id="1e03b-147">Todos los roles integrados de RBAC de Azure permiten ver los roles que están disponibles para la asignación.</span><span class="sxs-lookup"><span data-stu-id="1e03b-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="1e03b-148">Los usuarios que pueden realizar hello `Microsoft.Authorization/roleDefinition/read` operación en un ámbito puede ver los roles RBAC Hola que están disponibles para la asignación en ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="1e03b-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="1e03b-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1e03b-149">See also</span></span>
* <span data-ttu-id="1e03b-150">[Control de acceso basado en roles](role-based-access-control-configure.md): comience a usar RBAC en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e03b-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="1e03b-151">Obtenga información acerca de cómo tener acceso toomanage con:</span><span class="sxs-lookup"><span data-stu-id="1e03b-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="1e03b-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e03b-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="1e03b-153">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1e03b-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="1e03b-154">API DE REST</span><span class="sxs-lookup"><span data-stu-id="1e03b-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="1e03b-155">[Funciones integradas](role-based-access-built-in-roles.md): obtener detalles acerca de los roles de Hola que vienen en RBAC.</span><span class="sxs-lookup"><span data-stu-id="1e03b-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
