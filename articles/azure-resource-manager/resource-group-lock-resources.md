---
title: Bloqueo de recursos de Azure para impedir cambios | Microsoft Docs
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
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="6d951-103">Bloqueo de recursos para impedir cambios inesperados</span><span class="sxs-lookup"><span data-stu-id="6d951-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="6d951-104">Como administrador, puede que tenga que bloquear una suscripción, un grupo de recursos o un recurso para impedir que otros usuarios de su organización eliminen o modifiquen accidentalmente recursos esenciales.</span><span class="sxs-lookup"><span data-stu-id="6d951-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="6d951-105">Puede establecer el bloqueo de nivel en **CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="6d951-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="6d951-106">**CanNotDelete** significa que los usuarios autorizados pueden leer y modificar recursos, pero no eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="6d951-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="6d951-107">**ReadOnly** significa que los usuarios autorizados solo pueden leer recursos, pero no actualizarlos ni eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="6d951-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="6d951-108">Aplicar este bloqueo es similar a restringir todos los usuarios autorizados a los permisos concedidos por el rol **Lector**.</span><span class="sxs-lookup"><span data-stu-id="6d951-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="6d951-109">Cómo se aplican los bloqueos</span><span class="sxs-lookup"><span data-stu-id="6d951-109">How locks are applied</span></span>

<span data-ttu-id="6d951-110">Cuando se aplica un bloqueo en un ámbito primario, todos los recursos heredan el mismo bloqueo.</span><span class="sxs-lookup"><span data-stu-id="6d951-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="6d951-111">Incluso los recursos que agregue posteriormente heredan el bloqueo del elemento primario.</span><span class="sxs-lookup"><span data-stu-id="6d951-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="6d951-112">El bloqueo más restrictivo de toda la herencia tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="6d951-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="6d951-113">Al diferencia del control de acceso basado en rol, los bloqueos de administración se usan para aplicar una restricción a todos los usuarios y roles.</span><span class="sxs-lookup"><span data-stu-id="6d951-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="6d951-114">Para obtener información sobre cómo establecer permisos para usuarios y roles, vea [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6d951-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="6d951-115">Los bloqueos de Resource Manager solo se aplican a las operaciones que se producen en el plano de la administración, que consta de las operaciones enviadas a `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="6d951-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="6d951-116">Los bloqueos no restringen cómo los recursos realizan sus propias funciones.</span><span class="sxs-lookup"><span data-stu-id="6d951-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="6d951-117">Los cambios de recursos están restringidos, pero no así las operaciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d951-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="6d951-118">Por ejemplo, un bloqueo de solo lectura de una base de datos SQL evita tener que eliminar o modificar dicha base de datos, pero no podrá crear, actualizar o eliminar los datos de ella.</span><span class="sxs-lookup"><span data-stu-id="6d951-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="6d951-119">Se permiten las transacciones de datos porque esas operaciones no se envían a `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="6d951-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="6d951-120">Si aplica **ReadOnly** , pueden producirse resultados inesperados, ya que algunas operaciones que parecen ser similares a operaciones de lectura realmente requieren acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="6d951-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="6d951-121">Por ejemplo, al colocar un bloqueo **ReadOnly** en una cuenta de almacenamiento, evita que se muestren las claves a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6d951-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="6d951-122">La operación de visualización claves se administra mediante solicitudes POST debido a que las claves devueltas están disponibles para las operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="6d951-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="6d951-123">Otro ejemplo: al colocar un bloqueo **ReadOnly** en un recurso de servicio del Servicio de aplicaciones, evita que el Explorador de servidores de Visual Studio muestre los archivos del recurso, ya que esa interacción requiere acceso de escritura.</span><span class="sxs-lookup"><span data-stu-id="6d951-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="6d951-124">Quién puede crear o eliminar bloqueos en su organización</span><span class="sxs-lookup"><span data-stu-id="6d951-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="6d951-125">Para crear o eliminar bloqueos de administración, debe tener acceso a las acciones `Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="6d951-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="6d951-126">Entre los roles integrados, solamente se conceden esas acciones al **propietario** y al **administrador de acceso de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6d951-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="6d951-127">Portal</span><span class="sxs-lookup"><span data-stu-id="6d951-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="6d951-128">Plantilla</span><span class="sxs-lookup"><span data-stu-id="6d951-128">Template</span></span>
<span data-ttu-id="6d951-129">El ejemplo siguiente muestra una plantilla que crea un bloqueo en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6d951-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="6d951-130">La cuenta de almacenamiento en la que se va a aplicar el bloqueo se proporciona como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="6d951-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="6d951-131">El nombre del bloqueo se crea mediante la concatenación del nombre del recurso con **/Microsoft.Authorization/** y el propio nombre del bloqueo (en este caso, **myLock**).</span><span class="sxs-lookup"><span data-stu-id="6d951-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="6d951-132">El tipo proporcionado es específico del tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="6d951-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="6d951-133">Para el almacenamiento, establezca este tipo en "Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="6d951-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="6d951-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d951-134">PowerShell</span></span>
<span data-ttu-id="6d951-135">Bloquee recursos implementados con Azure PowerShell mediante el comando [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="6d951-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="6d951-136">Para bloquear un recurso, proporcione el nombre del recurso, su tipo y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d951-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="6d951-137">Para bloquear un grupo de recursos, proporcione el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d951-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="6d951-138">Para obtener información sobre un bloqueo, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="6d951-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="6d951-139">Para obtener todos los bloqueos en su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="6d951-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="6d951-140">Para obtener todos los bloqueos para un recurso, use:</span><span class="sxs-lookup"><span data-stu-id="6d951-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="6d951-141">Para obtener todos los bloqueos para un grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="6d951-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="6d951-142">Azure PowerShell ofrece otros comandos para trabajar con bloqueos, como [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) para actualizar un bloqueo y [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) para eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="6d951-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="6d951-143">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6d951-143">Azure CLI</span></span>

<span data-ttu-id="6d951-144">Bloquee recursos implementados con la CLI de Azure mediante el comando [az lock create](/cli/azure/lock#create).</span><span class="sxs-lookup"><span data-stu-id="6d951-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="6d951-145">Para bloquear un recurso, proporcione el nombre del recurso, su tipo y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d951-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="6d951-146">Para bloquear un grupo de recursos, proporcione el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d951-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="6d951-147">Para obtener información sobre un bloqueo, use [az lock list](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="6d951-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="6d951-148">Para obtener todos los bloqueos en su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="6d951-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="6d951-149">Para obtener todos los bloqueos para un recurso, use:</span><span class="sxs-lookup"><span data-stu-id="6d951-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="6d951-150">Para obtener todos los bloqueos para un grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="6d951-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="6d951-151">La CLI de Azure proporciona otros comandos para trabajar con bloqueos, como [az lock update](/cli/azure/lock#update) para actualizar un bloqueo y [az lock delete](/cli/azure/lock#delete) para eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="6d951-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="6d951-152">API de REST</span><span class="sxs-lookup"><span data-stu-id="6d951-152">REST API</span></span>
<span data-ttu-id="6d951-153">Puede bloquear los recursos implementados con la [API de REST para bloqueos de administración](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="6d951-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="6d951-154">La API de REST le permite crear y eliminar bloqueos, y recuperar información acerca de los bloqueos existentes.</span><span class="sxs-lookup"><span data-stu-id="6d951-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="6d951-155">Para crear un bloqueo, ejecute:</span><span class="sxs-lookup"><span data-stu-id="6d951-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="6d951-156">El ámbito puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="6d951-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="6d951-157">El nombre del bloqueo es el nombre con el que desee llamar al bloqueo.</span><span class="sxs-lookup"><span data-stu-id="6d951-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="6d951-158">Como versión de la API, use **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="6d951-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="6d951-159">En la solicitud, incluya un objeto JSON que especifique las propiedades para el bloqueo.</span><span class="sxs-lookup"><span data-stu-id="6d951-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="6d951-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d951-160">Next steps</span></span>
* <span data-ttu-id="6d951-161">Para obtener más información sobre cómo trabajar con bloqueos de recursos, consulte [Bloqueo de los recursos de Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="6d951-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="6d951-162">Para aprender a organizar de manera lógica los recursos, vea [Uso de etiquetas para organizar sus recursos](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="6d951-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="6d951-163">Para cambiar el grupo de recursos en que reside un recurso, vea [Traslado de los recursos a un nuevo grupo de recursos](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="6d951-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="6d951-164">Puede aplicar restricciones y convenciones a través de su suscripción con directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="6d951-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="6d951-165">Para más información, vea [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6d951-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="6d951-166">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6d951-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

