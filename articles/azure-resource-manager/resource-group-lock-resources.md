---
title: cambios de tooprevent de aaaLock recursos de Azure | Documentos de Microsoft
description: Impida que los usuarios actualicen o eliminen recursos de Azure esenciales aplicando un bloqueo para todos los usuarios y roles.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="1b6a5-103">Bloquear recursos tooprevent cambios inesperados</span><span class="sxs-lookup"><span data-stu-id="1b6a5-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="1b6a5-104">Como administrador, puede que necesite toolock una suscripción, grupo de recursos o recurso tooprevent otros usuarios de su organización accidentalmente eliminen o modifiquen los recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="1b6a5-105">Puede establecer nivel de bloqueo de hello demasiado**CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="1b6a5-106">**CanNotDelete** significa que los usuarios autorizados todavía pueden leer y modificar un recurso, pero no pueden eliminar el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="1b6a5-107">**ReadOnly** significa que los usuarios autorizados pueden leer un recurso, pero que no se pueden eliminar o actualizar el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="1b6a5-108">Este bloqueo de la aplicación es similar toorestricting todo autorizado los usuarios toohello permisos concedidos por hello **lector** rol.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="1b6a5-109">Cómo se aplican los bloqueos</span><span class="sxs-lookup"><span data-stu-id="1b6a5-109">How locks are applied</span></span>

<span data-ttu-id="1b6a5-110">Cuando se aplica un bloqueo en un ámbito primario, todos los recursos dentro de ese ámbito heredan Hola mismo bloqueo.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="1b6a5-111">Incluso los recursos que se agreguen posteriormente heredan bloqueo Hola de hello primario.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="1b6a5-112">bloqueo de más restrictivo de Hello en la herencia de hello tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="1b6a5-113">A diferencia de control de acceso basado en roles, se usa administración bloqueos tooapply una restricción a través de todos los usuarios y roles.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="1b6a5-114">toolearn acerca de cómo establecer permisos para usuarios y roles, consulte [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b6a5-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="1b6a5-115">Bloqueos del Administrador de recursos aplican solo toooperations que se producen en el plano de administración de hello, que consta de las operaciones enviadas demasiado`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="1b6a5-116">bloqueos de Hello no restringen cómo recursos realizan sus propias funciones.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="1b6a5-117">Los cambios de recursos están restringidos, pero no así las operaciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="1b6a5-118">Por ejemplo, un bloqueo de solo lectura en una base de datos de SQL no le permitirá eliminar o modificar la base de datos de hello, pero no impiden crear, actualizar o eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="1b6a5-119">Se permiten las transacciones de datos porque esas operaciones no se envían demasiado`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="1b6a5-120">Aplicar **ReadOnly** puede provocar resultados toounexpected porque algunas operaciones que parezcan como lectura operaciones realmente requieren acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="1b6a5-121">Por ejemplo, colocar una **ReadOnly** bloqueo en una cuenta de almacenamiento impide que todos los usuarios de la lista de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="1b6a5-122">lista de Hello operación de claves se controla a través de una solicitud POST porque Hola devuelve las claves están disponibles para las operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="1b6a5-123">Para obtener otro ejemplo, colocar una **ReadOnly** bloqueo en un recurso de servicio de aplicaciones evita que Explorador de servidores de Visual Studio muestre archivos de recursos de hello porque esa interacción requiere acceso de escritura.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="1b6a5-124">Quién puede crear o eliminar bloqueos en su organización</span><span class="sxs-lookup"><span data-stu-id="1b6a5-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="1b6a5-125">bloqueos de administración toocreate o delete, debe tener acceso demasiado`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` acciones.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="1b6a5-126">De hello funciones integradas solo **propietario** y **Administrador de acceso de usuario** se conceden a esas acciones.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="1b6a5-127">Portal</span><span class="sxs-lookup"><span data-stu-id="1b6a5-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="1b6a5-128">Plantilla</span><span class="sxs-lookup"><span data-stu-id="1b6a5-128">Template</span></span>
<span data-ttu-id="1b6a5-129">Hello en el ejemplo siguiente se muestra una plantilla que crea un bloqueo en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="1b6a5-130">cuenta de almacenamiento de Hello en qué tooapply bloqueo Hola se proporciona como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="1b6a5-131">nombre del bloqueo de Hola Hola se crea una concatenando el nombre de recurso de hello con **/Microsoft.Authorization/** y Hola nombre del bloqueo de hello, en este caso **myLock**.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="1b6a5-132">tipo de Hello proporcionado es tipo de recurso de toohello específico.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="1b6a5-133">Para el almacenamiento, establezca Hola tipo too"Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="1b6a5-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="1b6a5-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b6a5-134">PowerShell</span></span>
<span data-ttu-id="1b6a5-135">Bloquear implementa recursos con PowerShell de Azure mediante hello [AzureRmResourceLock New](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="1b6a5-136">toolock un recurso, proporcione el nombre de hello del recurso de hello, su tipo de recurso y su nombre de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1b6a5-137">toolock un grupo de recursos, proporcionar nombre Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1b6a5-138">tooget información acerca de un bloqueo, utilice [AzureRmResourceLock Get](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="1b6a5-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="1b6a5-139">tooget todos los bloqueos de hello en su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="1b6a5-140">tooget todos los bloqueos para un recurso, use:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1b6a5-141">tooget todos los bloqueos para un grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1b6a5-142">PowerShell de Azure proporciona otros comandos para bloqueos de trabajo, como [conjunto AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate un bloqueo, y [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="1b6a5-143">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1b6a5-143">Azure CLI</span></span>

<span data-ttu-id="1b6a5-144">Bloquear implementa recursos con CLI de Azure mediante hello [crear bloqueo az](/cli/azure/lock#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="1b6a5-145">toolock un recurso, proporcione el nombre de hello del recurso de hello, su tipo de recurso y su nombre de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="1b6a5-146">toolock un grupo de recursos, proporcionar nombre Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="1b6a5-147">tooget información acerca de un bloqueo, utilice [lista de bloqueo az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="1b6a5-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="1b6a5-148">tooget todos los bloqueos de hello en su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="1b6a5-149">tooget todos los bloqueos para un recurso, use:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="1b6a5-150">tooget todos los bloqueos para un grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="1b6a5-151">CLI de Azure proporciona otros comandos para bloqueos de trabajo, como [actualización de bloqueo de az](/cli/azure/lock#update) tooupdate un bloqueo, y [bloqueo az eliminar](/cli/azure/lock#delete) toodelete un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="1b6a5-152">API de REST</span><span class="sxs-lookup"><span data-stu-id="1b6a5-152">REST API</span></span>
<span data-ttu-id="1b6a5-153">Puede bloquear los recursos implementados con hello [API de REST para bloqueos de administración](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="1b6a5-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="1b6a5-154">Hola REST API permite toocreate y eliminar bloqueos y recuperar información sobre los bloqueos existentes.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="1b6a5-155">toocreate un bloqueo, ejecute:</span><span class="sxs-lookup"><span data-stu-id="1b6a5-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="1b6a5-156">ámbito de Hello podría ser una suscripción, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="1b6a5-157">Hola nombre del bloqueo es todo lo que desees bloqueo de hello toocall.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="1b6a5-158">Como versión de la API, use **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="1b6a5-159">En la solicitud de hello, incluir un objeto JSON que especifica las propiedades de Hola de bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="1b6a5-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b6a5-160">Next steps</span></span>
* <span data-ttu-id="1b6a5-161">Para obtener más información sobre cómo trabajar con bloqueos de recursos, consulte [Bloqueo de los recursos de Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="1b6a5-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="1b6a5-162">toolearn acerca de cómo organizar lógicamente los recursos, consulte [mediante etiquetas tooorganize los recursos](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="1b6a5-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="1b6a5-163">toochange un recurso reside a qué grupo de recursos, consulte [grupo de recursos de mover recursos toonew](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="1b6a5-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="1b6a5-164">Puede aplicar restricciones y convenciones a través de su suscripción con directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="1b6a5-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="1b6a5-165">Para obtener más información, consulte [recursos toomanage de directiva de uso y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1b6a5-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="1b6a5-166">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="1b6a5-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

