---
ms.assetid: 
title: "Azure Key Vault: Uso de la eliminación temporal con PowerShell"
description: "Ejemplos de casos de uso de eliminación temporal con fragmentos de código de PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="dcfef-103">Uso de la eliminación temporal de Key Vault con PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcfef-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="dcfef-104">La característica de eliminación temporal de Azure Key Vault permite recuperar almacenes y objetos de almacenes eliminados.</span><span class="sxs-lookup"><span data-stu-id="dcfef-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="dcfef-105">En concreto, la eliminación temporal trata los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="dcfef-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="dcfef-106">Compatibilidad con la eliminación recuperable de una instancia de Key Vault</span><span class="sxs-lookup"><span data-stu-id="dcfef-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="dcfef-107">Compatibilidad con la eliminación recuperable de objetos de Key Vault: claves, secretos y certificados</span><span class="sxs-lookup"><span data-stu-id="dcfef-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcfef-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dcfef-108">Prerequisites</span></span>

- <span data-ttu-id="dcfef-109">Azure PowerShell 4.0.0 o posterior: si aún no lo tiene instalado, instale Azure PowerShell y asócielo con la suscripción de Azure. Para ello, consulte [Instalación y configuración de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcfef-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="dcfef-110">Hay una versión no actualizada del archivo de formato de salida de PowerShell de Key Vault que se **podría** cargar en el entorno en lugar de la versión correcta.</span><span class="sxs-lookup"><span data-stu-id="dcfef-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="dcfef-111">Se espera una versión actualizada de PowerShell que contenga la corrección necesaria para el formato de salida y este tema se actualizará en ese momento.</span><span class="sxs-lookup"><span data-stu-id="dcfef-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="dcfef-112">La solución actual, si se encuentra con este problema de formato, es:</span><span class="sxs-lookup"><span data-stu-id="dcfef-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="dcfef-113">Use la siguiente consulta si no ve la propiedad Habilitar la eliminación temporal descrita en este tema: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="dcfef-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="dcfef-114">Para más información específica de referencia sobre Key Vault para PowerShell, consulte la [referencia de Azure Key Vault para PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="dcfef-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="dcfef-115">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="dcfef-115">Required permissions</span></span>

<span data-ttu-id="dcfef-116">Las operaciones de Key Vault se administran por separado mediante los permisos de control de acceso basado en roles (RBAC) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="dcfef-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="dcfef-117">Operación</span><span class="sxs-lookup"><span data-stu-id="dcfef-117">Operation</span></span> | <span data-ttu-id="dcfef-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="dcfef-118">Description</span></span> | <span data-ttu-id="dcfef-119">Permiso del usuario</span><span class="sxs-lookup"><span data-stu-id="dcfef-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="dcfef-120">Enumerar</span><span class="sxs-lookup"><span data-stu-id="dcfef-120">List</span></span>|<span data-ttu-id="dcfef-121">Enumera los almacenes de claves eliminados.</span><span class="sxs-lookup"><span data-stu-id="dcfef-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="dcfef-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="dcfef-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="dcfef-123">Recuperar</span><span class="sxs-lookup"><span data-stu-id="dcfef-123">Recover</span></span>|<span data-ttu-id="dcfef-124">Restaura un almacén de claves eliminado.</span><span class="sxs-lookup"><span data-stu-id="dcfef-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="dcfef-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="dcfef-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="dcfef-126">Purgar</span><span class="sxs-lookup"><span data-stu-id="dcfef-126">Purge</span></span>|<span data-ttu-id="dcfef-127">Elimina permanentemente un almacén de claves eliminado y todo su contenido.</span><span class="sxs-lookup"><span data-stu-id="dcfef-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="dcfef-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="dcfef-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="dcfef-129">Para más información sobre los permisos y el control de acceso, consulte [Protección de un almacén de claves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="dcfef-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="dcfef-130">Habilitar la eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="dcfef-130">Enabling soft-delete</span></span>

<span data-ttu-id="dcfef-131">Para poder recuperar un almacén de claves eliminado o los objetos almacenados en un almacén de claves, primero debe habilitar la eliminación temporal para ese almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dcfef-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="dcfef-132">Almacén de claves existente</span><span class="sxs-lookup"><span data-stu-id="dcfef-132">Existing key vault</span></span>

<span data-ttu-id="dcfef-133">Para un almacén de claves existente denominado ContosoVault, habilite la eliminación temporal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="dcfef-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="dcfef-134">Actualmente debe usar la manipulación de recursos de Azure Resource Manager para escribir directamente la propiedad *enableSoftDelete* en el recurso de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dcfef-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="dcfef-135">Almacén de claves nuevo</span><span class="sxs-lookup"><span data-stu-id="dcfef-135">New key vault</span></span>

<span data-ttu-id="dcfef-136">La habilitación de la eliminación temporal para un nuevo almacén de claves se realiza en el momento de la creación agregando el indicador de habilitación de eliminación temporal al comando create.</span><span class="sxs-lookup"><span data-stu-id="dcfef-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="dcfef-137">Comprobación de la habilitación de la eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="dcfef-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="dcfef-138">Para comprobar que un almacén de claves tiene habilitada la eliminación temporal, ejecute el comando *get* y busque el atributo "Soft Delete Enabled?"</span><span class="sxs-lookup"><span data-stu-id="dcfef-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="dcfef-139">y su valor, true o false.</span><span class="sxs-lookup"><span data-stu-id="dcfef-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="dcfef-140">Eliminación de un almacén de claves protegido por eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="dcfef-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="dcfef-141">El comando para eliminar (o quitar) un almacén de claves sigue siendo el mismo, pero su comportamiento cambia dependiendo de si ha habilitado la eliminación temporal o no.</span><span class="sxs-lookup"><span data-stu-id="dcfef-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="dcfef-142">Si ejecuta el comando anterior para un almacén de claves que no tiene habilitada la eliminación temporal, se eliminará permanentemente este almacén de claves y todo su contenido sin ninguna opción de recuperación.</span><span class="sxs-lookup"><span data-stu-id="dcfef-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="dcfef-143">Uso de la eliminación temporal para proteger los almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="dcfef-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="dcfef-144">Con la eliminación temporal habilitada:</span><span class="sxs-lookup"><span data-stu-id="dcfef-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="dcfef-145">Cuando se elimina un almacén de claves, se quita de su grupo de recursos y se coloca en un espacio de nombres reservado que solo está asociado a la ubicación donde se creó.</span><span class="sxs-lookup"><span data-stu-id="dcfef-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="dcfef-146">Los objetos de un almacén de claves eliminado como, por ejemplo, las claves, los secretos y los certificados, son inaccesibles y permanecen así mientras que el almacén de claves que los contiene está en el estado eliminado.</span><span class="sxs-lookup"><span data-stu-id="dcfef-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="dcfef-147">El nombre DNS de un almacén de claves en estado eliminado se reserva por lo que no se podrá crear ningún nuevo almacén de claves con ese mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="dcfef-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="dcfef-148">Puede ver los almacenes de claves en estado eliminado asociados a su suscripción con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="dcfef-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

<span data-ttu-id="dcfef-149">El *identificador de recurso* en la salida hace referencia al identificador de recurso original de este almacén.</span><span class="sxs-lookup"><span data-stu-id="dcfef-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="dcfef-150">Puesto que este almacén de claves está ahora en estado eliminado, no existe ningún recurso con ese identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="dcfef-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="dcfef-151">El campo *Identificador* se puede utilizar para identificar el recurso durante la recuperación o purga.</span><span class="sxs-lookup"><span data-stu-id="dcfef-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="dcfef-152">El campo *Scheduled Purge Date* (Fecha de purga programada) indica si el almacén se eliminará permanentemente (se purgará) si no se realiza ninguna acción en ese almacén eliminado.</span><span class="sxs-lookup"><span data-stu-id="dcfef-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="dcfef-153">El período de retención predeterminado que se utiliza para calcular la *fecha de purga programada* es de 90 días.</span><span class="sxs-lookup"><span data-stu-id="dcfef-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="dcfef-154">Recuperación de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="dcfef-154">Recovering a key vault</span></span>

<span data-ttu-id="dcfef-155">Para recuperar un almacén de claves, debe especificar el nombre del almacén de claves, el grupo de recursos y la ubicación.</span><span class="sxs-lookup"><span data-stu-id="dcfef-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="dcfef-156">Anote la ubicación y el grupo de recursos del almacén de claves eliminado ya que los necesitará para un proceso de recuperación del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dcfef-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="dcfef-157">Cuando se recupera un almacén de claves, el resultado es un nuevo recurso con el identificador de recurso original del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dcfef-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="dcfef-158">Si se ha quitado el grupo de recursos donde existía el almacén de claves, se deberá crear un nuevo grupo de recursos con el mismo nombre antes de poder recuperar el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dcfef-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="dcfef-159">Objetos de Key Vault y eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="dcfef-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="dcfef-160">Si tiene una clave, "ContosoFirstKey", en un almacén de claves denominado "ContosoVault" con eliminación temporal habilitada, este es el procedimiento para eliminarla.</span><span class="sxs-lookup"><span data-stu-id="dcfef-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="dcfef-161">Con el almacén de claves habilitado para la eliminación temporal, una clave eliminada seguirá apareciendo como eliminada excepto si enumera o recupera explícitamente las claves eliminadas.</span><span class="sxs-lookup"><span data-stu-id="dcfef-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="dcfef-162">La mayoría de las operaciones que se realicen en una clave en el estado eliminado producirán error, excepto las operaciones de enumeración, recuperación o purga.</span><span class="sxs-lookup"><span data-stu-id="dcfef-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="dcfef-163">Por ejemplo, para solicitar la enumeración de las claves eliminadas de un almacén de claves, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="dcfef-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="dcfef-164">Estado de transición</span><span class="sxs-lookup"><span data-stu-id="dcfef-164">Transition state</span></span> 

<span data-ttu-id="dcfef-165">Cuando se elimina una clave de un almacén de claves con eliminación temporal habilitada, puede tardar unos segundos en completarse la transición.</span><span class="sxs-lookup"><span data-stu-id="dcfef-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="dcfef-166">Durante este estado de transición, puede parecer que la clave no está ni en el estado activo ni en el estado eliminado.</span><span class="sxs-lookup"><span data-stu-id="dcfef-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="dcfef-167">Este comando permite enumerar todas las claves eliminadas en el almacén de claves denominado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="dcfef-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="dcfef-168">Uso de la eliminación temporal con objetos de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="dcfef-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="dcfef-169">Al igual que con los almacenes de claves, una clave, secreto o certificado eliminados permanecerán en este estado durante 90 días a menos que los recupere o los purgue.</span><span class="sxs-lookup"><span data-stu-id="dcfef-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="dcfef-170">simétricas</span><span class="sxs-lookup"><span data-stu-id="dcfef-170">Keys</span></span>

<span data-ttu-id="dcfef-171">Para recuperar una clave eliminada:</span><span class="sxs-lookup"><span data-stu-id="dcfef-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="dcfef-172">Para eliminar permanentemente una clave:</span><span class="sxs-lookup"><span data-stu-id="dcfef-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="dcfef-173">Si purga una clave se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="dcfef-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="dcfef-174">Las acciones de **recuperación** y **purga** tienen sus propios permisos asociados en una directiva de acceso del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dcfef-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="dcfef-175">Para que un usuario o una entidad de servicio puedan ejecutar una acción de **recuperación** o **purga** deben tener el permiso correspondiente para ese objeto (clave o secreto) en la directiva de acceso del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dcfef-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="dcfef-176">De forma predeterminada, el permiso de **purga** no se agrega a la directiva de acceso del almacén de claves cuando se usa el acceso directo "all" para conceder todos los permisos a un usuario.</span><span class="sxs-lookup"><span data-stu-id="dcfef-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="dcfef-177">Debe conceder el permiso de **purga** de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="dcfef-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="dcfef-178">Por ejemplo, el siguiente comando concede el permiso user@contoso.com para realizar varias operaciones en las claves de *ContosoVault* incluidas las operaciones de **purga**.</span><span class="sxs-lookup"><span data-stu-id="dcfef-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="dcfef-179">Establecimiento de una directiva de acceso del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="dcfef-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="dcfef-180">Si tiene un almacén de claves existente para el que se acaba de habilitar la eliminación temporal, puede que no tenga los permisos de **recuperación** y **purga**.</span><span class="sxs-lookup"><span data-stu-id="dcfef-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="dcfef-181">Secretos</span><span class="sxs-lookup"><span data-stu-id="dcfef-181">Secrets</span></span>

<span data-ttu-id="dcfef-182">Al igual que con las claves, se trabaja con los secretos de un almacén de claves con sus propios comandos.</span><span class="sxs-lookup"><span data-stu-id="dcfef-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="dcfef-183">A continuación, se muestran los comandos para eliminar, enumerar, recuperar y purgar secretos.</span><span class="sxs-lookup"><span data-stu-id="dcfef-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="dcfef-184">Elimine un secreto llamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="dcfef-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="dcfef-185">Enumere todos los secretos eliminados de un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="dcfef-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="dcfef-186">Recupere un secreto en el estado eliminado:</span><span class="sxs-lookup"><span data-stu-id="dcfef-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="dcfef-187">Purgue un secreto en el estado eliminado:</span><span class="sxs-lookup"><span data-stu-id="dcfef-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="dcfef-188">Si purga un secreto se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="dcfef-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="dcfef-189">Purga y almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="dcfef-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="dcfef-190">Objetos de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="dcfef-190">Key vault objects</span></span>

<span data-ttu-id="dcfef-191">Si purga una clave, un secreto o un certificado se eliminarán permanentemente, lo que significa que no se podrán recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="dcfef-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="dcfef-192">No obstante, el almacén de claves que contenía el objeto eliminado permanecerá intacto al igual que el resto de objetos del almacén.</span><span class="sxs-lookup"><span data-stu-id="dcfef-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="dcfef-193">Almacenes de claves como contenedores</span><span class="sxs-lookup"><span data-stu-id="dcfef-193">Key vaults as containers</span></span>
<span data-ttu-id="dcfef-194">Cuando se purga un almacén de claves, todo su contenido, incluidas las claves, los secretos y los certificados, se eliminan permanentemente.</span><span class="sxs-lookup"><span data-stu-id="dcfef-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="dcfef-195">Para purgar un almacén de claves, use el comando `Remove-AzureRmKeyVault` con la opción `-InRemovedState` especificando la ubicación del almacén de claves eliminado con el argumento `-Location location`.</span><span class="sxs-lookup"><span data-stu-id="dcfef-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="dcfef-196">Puede encontrar la ubicación de un almacén eliminado mediante el comando `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="dcfef-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="dcfef-197">Si purga un almacén de claves se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="dcfef-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="dcfef-198">Se requieren permisos de purga</span><span class="sxs-lookup"><span data-stu-id="dcfef-198">Purge permissions required</span></span>
- <span data-ttu-id="dcfef-199">Para purgar un almacén de claves eliminado, de forma que el almacén y todo su contenido se quite de forma permanente, el usuario necesita el permiso de RBAC para realizar una operación *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="dcfef-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="dcfef-200">Para que se muestre el almacén de claves eliminado, el usuario necesita el permiso de RBAC para realizar una operación *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="dcfef-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="dcfef-201">Solo un administrador de suscripción tiene estos permisos.</span><span class="sxs-lookup"><span data-stu-id="dcfef-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="dcfef-202">Purga programada</span><span class="sxs-lookup"><span data-stu-id="dcfef-202">Scheduled purge</span></span>

<span data-ttu-id="dcfef-203">La enumeración de los objetos de almacén de claves eliminados muestra cuándo se han programado para que Key Vault efectúe la purga.</span><span class="sxs-lookup"><span data-stu-id="dcfef-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="dcfef-204">El campo *Scheduled Purge Date* (Fecha de purga programada) indica cuándo se eliminará permanentemente un objeto de almacén de claves si no se realiza ninguna acción en ese almacén.</span><span class="sxs-lookup"><span data-stu-id="dcfef-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="dcfef-205">De forma predeterminada, el período de retención para un objeto de almacén de claves eliminado es de 90 días.</span><span class="sxs-lookup"><span data-stu-id="dcfef-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="dcfef-206">Un objeto de almacén purgado, desencadenado por el valor de su campo de *fecha de purga programada*, se eliminará permanentemente.</span><span class="sxs-lookup"><span data-stu-id="dcfef-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="dcfef-207">No se podrá volver a recuperar.</span><span class="sxs-lookup"><span data-stu-id="dcfef-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="dcfef-208">Otros recursos:</span><span class="sxs-lookup"><span data-stu-id="dcfef-208">Other resources</span></span>

- <span data-ttu-id="dcfef-209">Para obtener una información general sobre la nueva característica de eliminación temporal, consulte [la información general sobre la eliminación temporal de Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="dcfef-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="dcfef-210">Para obtener una descripción general del uso de Azure Key Vault, consulte [Introducción a Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcfef-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

