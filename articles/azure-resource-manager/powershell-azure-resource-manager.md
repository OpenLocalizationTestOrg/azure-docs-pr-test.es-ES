---
title: aaaManage Azure soluciones con PowerShell | Documentos de Microsoft
description: Usar PowerShell de Azure y el Administrador de recursos toomanage los recursos.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="b5bb9-103">Administración de recursos con Azure PowerShell y Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b5bb9-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5bb9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b5bb9-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="b5bb9-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b5bb9-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="b5bb9-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5bb9-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="b5bb9-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="b5bb9-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="b5bb9-108">En este artículo, aprenderá cómo toomanage sus soluciones con PowerShell de Azure y Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="b5bb9-109">Si no está familiarizado con Resource Manager, consulte [Información general de Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="b5bb9-110">Este tema se centra en las tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="b5bb9-111">Podrá:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-111">You will:</span></span>

1. <span data-ttu-id="b5bb9-112">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-112">Create a resource group</span></span>
2. <span data-ttu-id="b5bb9-113">Agregar un grupo de recursos de toohello de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="b5bb9-114">Agregar un recurso de toohello de etiqueta</span><span class="sxs-lookup"><span data-stu-id="b5bb9-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="b5bb9-115">Consulta de recursos según nombres y valores de etiqueta</span><span class="sxs-lookup"><span data-stu-id="b5bb9-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="b5bb9-116">Aplicar y quitar un bloqueo de recurso de Hola</span><span class="sxs-lookup"><span data-stu-id="b5bb9-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="b5bb9-117">Eliminación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-117">Delete a resource group</span></span>

<span data-ttu-id="b5bb9-118">En este artículo no se muestra cómo toodeploy una suscripción de tooyour de plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="b5bb9-119">Esa información la puede encontrar en [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="b5bb9-120">Introducción a Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5bb9-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="b5bb9-121">Si no ha instalado Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="b5bb9-122">Si ha instalado Azure PowerShell Hola anteriores, pero no han actualizado recientemente, considere la posibilidad de instalar la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="b5bb9-123">Puede actualizar la versión de Hola a través de hello mismo método usado tooinstall lo.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="b5bb9-124">Por ejemplo, si ha usado Hola instalador de plataforma Web, inicie de nuevo y busque una actualización.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="b5bb9-125">usar de la versión del módulo de recursos de Azure, hello toocheck Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="b5bb9-126">Este tema se ha actualizado a la versión 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="b5bb9-127">Si tiene una versión anterior, la experiencia podría no coincidir con los pasos de hello descritos en este tema.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="b5bb9-128">Para obtener documentación sobre los cmdlets de hello en esta versión, consulte [AzureRM.Resources módulo](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="b5bb9-129">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="b5bb9-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="b5bb9-130">Antes de trabajar en la solución, debe iniciar sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="b5bb9-131">toolog en tooyour cuenta de Azure, use hello **AzureRmAccount de inicio de sesión** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b5bb9-132">Hola cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="b5bb9-133">Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="b5bb9-134">Hola cmdlet devuelve información sobre la toouse de suscripción hello y cuenta para tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="b5bb9-135">Si tiene más de una suscripción, puede cambiar tooa otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="b5bb9-136">En primer lugar, vamos a ver todas las suscripciones de Hola para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="b5bb9-137">Se devuelven las suscripciones habilitadas y deshabilitadas.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="b5bb9-138">tooswitch tooa otra suscripción, proporcione el nombre de la suscripción de hello con hello **AzureRmContext conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="b5bb9-139">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-139">Create a resource group</span></span>
<span data-ttu-id="b5bb9-140">Antes de implementar cualquier suscripción de recursos de tooyour, debe crear un grupo de recursos que va a contener recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="b5bb9-141">toocreate un grupo de recursos, utilice hello **AzureRmResourceGroup New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="b5bb9-142">comando de Hello usa hello **nombre** toospecify parámetro un nombre para el grupo de recursos de Hola y Hola **ubicación** parámetro toospecify su ubicación.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="b5bb9-143">salida de Hello es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="b5bb9-144">Si necesita tooretrieve grupo de recursos de hello más tarde, utilice Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="b5bb9-145">tooget todos los grupos de recursos en su suscripción de Hola, no se especifica un nombre:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="b5bb9-146">Agregar grupo de recursos de tooa de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-146">Add resources tooa resource group</span></span>
<span data-ttu-id="b5bb9-147">tooadd un grupo de recursos de toohello de recursos, puede usar hello **New-AzureRmResource** cmdlet o un cmdlet que es de tipo toohello específico del recurso que está creando (como **AzureRmStorageAccount New**).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="b5bb9-148">Le resultará más fácil toouse un cmdlet que es el tipo de recurso específico tooa porque incluye parámetros para las propiedades de Hola que son necesarios para el nuevo recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="b5bb9-149">toouse **New-AzureRmResource**, debe conocer todos los tooset de propiedades de hello sin que se le solicite para ellos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="b5bb9-150">Sin embargo, al agregar un recurso a través de los cmdlets podría producir confusión futuras porque el nuevo recurso de hello no existe en una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="b5bb9-151">Microsoft recomienda que se defina la infraestructura de hello para la solución de Azure en una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="b5bb9-152">Las plantillas permiten tooreliably e implementación varias veces la solución.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="b5bb9-153">En este tema, creará una cuenta de almacenamiento con un cmdlet de PowerShell, pero más tarde generará una plantilla a partir de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="b5bb9-154">Hola siguiente cmdlet crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="b5bb9-155">En lugar de usar el nombre de Hola que se muestra en el ejemplo de Hola, proporcione un nombre único para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="b5bb9-156">nombre de Hello debe tener entre 3 y 24 caracteres de longitud y usar solo números y letras en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="b5bb9-157">Si usas nombre Hola que se muestra en el ejemplo de Hola, recibirá un error porque ese nombre ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="b5bb9-158">Si debe tooretrieve este recurso más adelante, utilice Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="b5bb9-159">Agregar una etiqueta</span><span class="sxs-lookup"><span data-stu-id="b5bb9-159">Add a tag</span></span>

<span data-ttu-id="b5bb9-160">Las etiquetas permiten tooorganize los recursos según las propiedades de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="b5bb9-161">Por ejemplo, puede tener varios recursos en distintos grupos de recursos que pertenecen toohello mismo departamento.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="b5bb9-162">Puede aplicar un toomark departamento etiqueta y el valor toothose recursos usarlas como pertenecientes toohello misma categoría.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="b5bb9-163">O bien, puede marcar si un recurso se usa en un entorno de producción o de prueba.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="b5bb9-164">En este tema, aplicar etiquetas tooonly un recurso, pero en su entorno lo más probable es que tiene sentido tooapply etiquetas tooall sus recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="b5bb9-165">Hola siguiente cmdlet aplica la cuenta de almacenamiento de dos etiquetas tooyour:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="b5bb9-166">Las etiquetas se actualizan como un único objeto.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-166">Tags are updated as a single object.</span></span> <span data-ttu-id="b5bb9-167">en primer lugar, tooadd un recurso de tooa de etiqueta que ya incluye etiquetas, recuperar las etiquetas existentes Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="b5bb9-168">Agregar Hola etiqueta toohello objeto nuevo que contiene las etiquetas existentes hello y volver a aplicar todos los recursos de toohello de etiquetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="b5bb9-169">Búsqueda de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-169">Search for resources</span></span>

<span data-ttu-id="b5bb9-170">Hola de uso **AzureRmResource buscar** cmdlet tooretrieve recursos para las condiciones de búsqueda diferentes.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="b5bb9-171">tooget un recurso por su nombre, proporcionar hello **ResourceNameContains** parámetro:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="b5bb9-172">tooget todos los recursos de hello en un grupo de recursos, proporcionar hello **ResourceGroupNameContains** parámetro:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="b5bb9-173">tooget todos los recursos de hello con un nombre de etiqueta y el valor, proporcionar hello **TagName** y **TagValue** parámetros:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="b5bb9-174">recursos de hello tooall con un tipo de recurso determinado, proporcionar hello **ResourceType** parámetro:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="b5bb9-175">Bloqueo de un recurso</span><span class="sxs-lookup"><span data-stu-id="b5bb9-175">Lock a resource</span></span>

<span data-ttu-id="b5bb9-176">Cuando necesite toomake seguro de que un recurso crítico no se elimina accidentalmente o modificado, aplicar un recurso de toohello de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="b5bb9-177">Puede especificar **CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="b5bb9-178">bloqueos de administración toocreate o delete, debe tener acceso demasiado`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` acciones.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="b5bb9-179">De las funciones integradas de hello, solo el propietario y el Administrador de acceso de usuario se conceden dichas acciones.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="b5bb9-180">tooapply un bloqueo, utilice Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="b5bb9-181">Hello recurso bloqueado en el anterior ejemplo de Hola no se puede eliminar hasta que se quite el bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="b5bb9-182">tooremove un bloqueo, utilice:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="b5bb9-183">Para más información sobre el establecimiento de bloqueos, consulte [Bloqueo de recursos con Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="b5bb9-184">Eliminación de recursos o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="b5bb9-184">Remove resources or resource group</span></span>
<span data-ttu-id="b5bb9-185">Puede quitar un recurso o un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="b5bb9-186">Al quitar un grupo de recursos, también quita todos los recursos de hello en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="b5bb9-187">un recurso del grupo de recursos de hello, use hello toodelete **Remove-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="b5bb9-188">Este cmdlet elimina el recurso de hello, pero no elimina el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="b5bb9-189">toodelete un grupo de recursos y todos sus recursos, use hello **Remove-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="b5bb9-190">Para los cmdlets, deberá tooconfirm que desea tooremove recursos de Hola o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="b5bb9-191">Si operación Hola elimina correctamente el recurso de Hola o grupo de recursos, devuelve **True**.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="b5bb9-192">Ejecución de scripts de Resource Manager con Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b5bb9-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="b5bb9-193">Este tema muestra cómo tooperform operaciones básicas en los recursos con PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="b5bb9-194">Para escenarios de administración más avanzados, normalmente desea toocreate una secuencia de comandos y volver a utilizar ese script según sea necesario o según una programación.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="b5bb9-195">[Automatización de Azure](../automation/automation-intro.md) le proporciona una manera de secuencias de comandos de tooautomate de uso frecuente que administran sus soluciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="b5bb9-196">Hello en los temas siguientes muestran cómo toouse automatización de Azure, el Administrador de recursos y PowerShell tooeffectively realizan tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="b5bb9-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="b5bb9-197">Para más información sobre la creación de un Runbook, consulte [Mi primer runbook de PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="b5bb9-198">Para más información sobre cómo trabajar con galerías de scripts, consulte [Galerías de runbooks y módulos para Azure Automation](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="b5bb9-199">Para runbooks que iniciar y detener las máquinas virtuales, consulte [escenario de automatización de Azure: toocreate de etiquetas con formato JSON utilizando una programación para el inicio de la máquina virtual de Azure y cierre](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="b5bb9-200">Para más información sobre Runbooks que iniciar y detienen máquinas virtuales fuera de las horas de trabajo, consulte [Inicio o detención de máquinas virtuales fuera de las horas de trabajo en Automation](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5bb9-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5bb9-201">Next steps</span></span>
* <span data-ttu-id="b5bb9-202">toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [creación de plantillas de administrador de recursos de Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b5bb9-203">toolearn sobre la implementación de plantillas, consulte [implementar una aplicación con la plantilla de administrador de recursos de Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="b5bb9-204">Puede mover recursos tooa nuevo grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="b5bb9-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="b5bb9-205">Para obtener ejemplos, vea [tooNew recursos Mover grupo de recursos o suscripción](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="b5bb9-206">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b5bb9-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

