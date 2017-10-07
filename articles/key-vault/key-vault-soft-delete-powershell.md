---
ms.assetid: 
title: "Almacén de claves de aaaAzure: cómo toouse soft-delete con PowerShell"
description: "Ejemplos de casos de uso de eliminación temporal con fragmentos de código de PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="e3649-103">Cómo toouse el almacén de claves soft-delete con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3649-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="e3649-104">La característica de eliminación temporal de Azure Key Vault permite recuperar almacenes y objetos de almacenes eliminados.</span><span class="sxs-lookup"><span data-stu-id="e3649-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="e3649-105">En concreto, soft-delete Hola direcciones los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="e3649-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="e3649-106">Compatibilidad con la eliminación recuperable de una instancia de Key Vault</span><span class="sxs-lookup"><span data-stu-id="e3649-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="e3649-107">Compatibilidad con la eliminación recuperable de objetos de Key Vault: claves, secretos y certificados</span><span class="sxs-lookup"><span data-stu-id="e3649-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3649-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e3649-108">Prerequisites</span></span>

- <span data-ttu-id="e3649-109">Azure PowerShell 4.0.0 o una versión posterior: si no tiene este ya el programa de instalación, instale Azure PowerShell y asociarla a su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e3649-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="e3649-110">Hay una versión no actualizada de nuestro formato de salida de PowerShell de almacén de claves de archivo que **puede** se va a cargar en el entorno en lugar de la versión correcta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3649-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="e3649-111">Se espera que una versión actualizada del programa Hola a toocontain PowerShell necesarios corrección para el formato de salida de hello y se actualizará en este tema en ese momento.</span><span class="sxs-lookup"><span data-stu-id="e3649-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="e3649-112">Hola actual solucionar este problema, debe se produce este problema de formato, es:</span><span class="sxs-lookup"><span data-stu-id="e3649-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="e3649-113">Hola de uso después de consulta si observa que no puede ver Hola soft-delete habilitada la propiedad descrita en este tema: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="e3649-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="e3649-114">Para más información específica de referencia sobre Key Vault para PowerShell, consulte la [referencia de Azure Key Vault para PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="e3649-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="e3649-115">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="e3649-115">Required permissions</span></span>

<span data-ttu-id="e3649-116">Las operaciones de Key Vault se administran por separado mediante los permisos de control de acceso basado en roles (RBAC) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="e3649-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="e3649-117">Operación</span><span class="sxs-lookup"><span data-stu-id="e3649-117">Operation</span></span> | <span data-ttu-id="e3649-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="e3649-118">Description</span></span> | <span data-ttu-id="e3649-119">Permiso del usuario</span><span class="sxs-lookup"><span data-stu-id="e3649-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="e3649-120">Enumerar</span><span class="sxs-lookup"><span data-stu-id="e3649-120">List</span></span>|<span data-ttu-id="e3649-121">Enumera los almacenes de claves eliminados.</span><span class="sxs-lookup"><span data-stu-id="e3649-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="e3649-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="e3649-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="e3649-123">Recuperar</span><span class="sxs-lookup"><span data-stu-id="e3649-123">Recover</span></span>|<span data-ttu-id="e3649-124">Restaura un almacén de claves eliminado.</span><span class="sxs-lookup"><span data-stu-id="e3649-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="e3649-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="e3649-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="e3649-126">Purgar</span><span class="sxs-lookup"><span data-stu-id="e3649-126">Purge</span></span>|<span data-ttu-id="e3649-127">Elimina permanentemente un almacén de claves eliminado y todo su contenido.</span><span class="sxs-lookup"><span data-stu-id="e3649-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="e3649-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="e3649-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="e3649-129">Para más información sobre los permisos y el control de acceso, consulte [Protección de un almacén de claves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e3649-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="e3649-130">Habilitar la eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="e3649-130">Enabling soft-delete</span></span>

<span data-ttu-id="e3649-131">toobe puede toorecover del almacén de objetos almacenados en una clave o un almacén de claves se eliminó, primero debe habilitar la eliminación de software para ese almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e3649-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="e3649-132">Almacén de claves existente</span><span class="sxs-lookup"><span data-stu-id="e3649-132">Existing key vault</span></span>

<span data-ttu-id="e3649-133">Para un almacén de claves existente denominado ContosoVault, habilite la eliminación temporal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="e3649-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="e3649-134">Actualmente necesita Hola de escritura de toouse Azure Resource Manager recursos manipulación toodirectly *enableSoftDelete* toohello recursos de almacén de claves de propiedad.</span><span class="sxs-lookup"><span data-stu-id="e3649-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="e3649-135">Almacén de claves nuevo</span><span class="sxs-lookup"><span data-stu-id="e3649-135">New key vault</span></span>

<span data-ttu-id="e3649-136">Habilitar la eliminación de software para un nuevo almacén de claves se realiza en el momento de creación mediante la adición de marca de soft-delete enable hello tooyour crear comando.</span><span class="sxs-lookup"><span data-stu-id="e3649-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="e3649-137">Comprobación de la habilitación de la eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="e3649-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="e3649-138">tooverify que un almacén de claves tiene habilitado, soft-delete Hola ejecución *obtener* comando y busque hello 'Suave eliminar Enabled?'</span><span class="sxs-lookup"><span data-stu-id="e3649-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="e3649-139">y su valor, true o false.</span><span class="sxs-lookup"><span data-stu-id="e3649-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="e3649-140">Eliminación de un almacén de claves protegido por eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="e3649-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="e3649-141">Hola comando toodelete (o quitar) un almacén de claves permanece Hola mismo, pero sus cambios de comportamiento dependen de si ha habilitado soft-delete o no.</span><span class="sxs-lookup"><span data-stu-id="e3649-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="e3649-142">Si ejecuta el comando anterior de Hola para un almacén de claves que no tiene habilitada la eliminación temporal, se eliminará permanentemente este almacén de claves y todo su contenido sin ninguna opción para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="e3649-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="e3649-143">Uso de la eliminación temporal para proteger los almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="e3649-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="e3649-144">Con la eliminación temporal habilitada:</span><span class="sxs-lookup"><span data-stu-id="e3649-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="e3649-145">Cuando se elimina un almacén de claves, se quita de su grupo de recursos y se coloca en un espacio de nombres reservado que solo está asociado a la ubicación de Hola donde se creó.</span><span class="sxs-lookup"><span data-stu-id="e3649-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="e3649-146">Objetos de una clave eliminada del almacén, como las claves, secretos y certificados, son inaccesibles y mantenerse así mientras su almacén de claves que lo contiene está en estado de hello eliminado.</span><span class="sxs-lookup"><span data-stu-id="e3649-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="e3649-147">nombre DNS de Hola para un almacén de claves en un estado de eliminación se sigue reservando por lo tanto, no se puede crear un nuevo almacén de claves con el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="e3649-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="e3649-148">Puede ver almacenes de clave de estado eliminado, asociados a su suscripción, con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e3649-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="e3649-149">Hola *Id. de recurso* Hola salida hace referencia toohello de identificador de recurso original de este almacén.</span><span class="sxs-lookup"><span data-stu-id="e3649-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="e3649-150">Puesto que este almacén de claves está ahora en estado eliminado, no existe ningún recurso con ese identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="e3649-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="e3649-151">Hola *identificador* campo puede ser recurso de Hola de tooidentify usado durante la recuperación o purgar.</span><span class="sxs-lookup"><span data-stu-id="e3649-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="e3649-152">Hola *programada fecha purgar* campo indica al almacén de Hola se eliminarán permanentemente (purga) si no se realiza ninguna acción para este almacén eliminado.</span><span class="sxs-lookup"><span data-stu-id="e3649-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="e3649-153">Hola toocalculate período, que se usa de Hello predeterminado retención *programada fecha purgar*, es de 90 días.</span><span class="sxs-lookup"><span data-stu-id="e3649-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="e3649-154">Recuperación de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e3649-154">Recovering a key vault</span></span>

<span data-ttu-id="e3649-155">toorecover un almacén de claves, necesita nombre de almacén de claves de hello toospecify, grupo de recursos y ubicación.</span><span class="sxs-lookup"><span data-stu-id="e3649-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="e3649-156">Nota Hola hello y ubicación del grupo de recursos del programa Hola a elimina el almacén de claves según sea necesario para un proceso de recuperación del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e3649-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="e3649-157">Cuando se recupera un almacén de claves, el resultado de hello es un nuevo recurso con el identificador de recurso original. del almacén de hello claves</span><span class="sxs-lookup"><span data-stu-id="e3649-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="e3649-158">Si se ha quitado el grupo de recursos de Hola donde existía el almacén de claves de hello, debe crearse un nuevo grupo de recursos con el mismo nombre antes de que se puede recuperar el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3649-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="e3649-159">Objetos de Key Vault y eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="e3649-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="e3649-160">Si tiene una clave, "ContosoFirstKey", en un almacén de claves denominado "ContosoVault" con eliminación temporal habilitada, este es el procedimiento para eliminarla.</span><span class="sxs-lookup"><span data-stu-id="e3649-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e3649-161">Con el almacén de claves habilitado para la eliminación temporal, una clave eliminada seguirá apareciendo como eliminada excepto si enumera o recupera explícitamente las claves eliminadas.</span><span class="sxs-lookup"><span data-stu-id="e3649-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="e3649-162">Se producirá un error de mayoría de las operaciones en una clave de estado de hello eliminado excepto para enumerar una clave eliminada, recuperarlo o purgar.</span><span class="sxs-lookup"><span data-stu-id="e3649-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="e3649-163">Por ejemplo, las claves de toolist eliminar toorequest en un almacén de claves, utilizar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e3649-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="e3649-164">Estado de transición</span><span class="sxs-lookup"><span data-stu-id="e3649-164">Transition state</span></span> 

<span data-ttu-id="e3649-165">Cuando se elimina una clave en un almacén de claves con la eliminación de software habilitada, puede tardar unos segundos hello toocomplete de transición.</span><span class="sxs-lookup"><span data-stu-id="e3649-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="e3649-166">Durante este estado de transición, puede aparecer que esa clave hello no está en estado activo de Hola u Hola eliminado.</span><span class="sxs-lookup"><span data-stu-id="e3649-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="e3649-167">Este comando permite enumerar todas las claves eliminadas en el almacén de claves denominado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="e3649-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="e3649-168">Uso de la eliminación temporal con objetos de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e3649-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="e3649-169">Igual que los almacenes de claves, una clave eliminada, secreto o certificado permanecerá en estado de eliminación para los días de too90 a menos que recuperarlo o lo purga.</span><span class="sxs-lookup"><span data-stu-id="e3649-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="e3649-170">simétricas</span><span class="sxs-lookup"><span data-stu-id="e3649-170">Keys</span></span>

<span data-ttu-id="e3649-171">toorecover una clave eliminada:</span><span class="sxs-lookup"><span data-stu-id="e3649-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e3649-172">toopermanently eliminar una clave:</span><span class="sxs-lookup"><span data-stu-id="e3649-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="e3649-173">Si purga una clave se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e3649-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="e3649-174">Hola **recuperar** y **purgar** las acciones tienen sus propios permisos asociados en una directiva de acceso del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e3649-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="e3649-175">Para una tooexecute de capaz de toobe principal de usuario o servicio un **recuperar** o **purgar** acción que deben tener permiso respectivos Hola para ese objeto (clave o el secreto) en directiva de acceso del almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3649-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="e3649-176">De forma predeterminada, Hola **purgar** permiso no se agrega la directiva de acceso del almacén de tooa claves cuando contextual 'all' hello es toogrant usado todos los datos de usuario de tooa de permisos.</span><span class="sxs-lookup"><span data-stu-id="e3649-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="e3649-177">Debe conceder el permiso de **purga** de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="e3649-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="e3649-178">Por ejemplo, Hola después concede comando user@contoso.com tooperform permiso varias operaciones de claves de *ContosoVault* incluidos **purgar**.</span><span class="sxs-lookup"><span data-stu-id="e3649-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="e3649-179">Establecimiento de una directiva de acceso del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e3649-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="e3649-180">Si tiene un almacén de claves existente para el que se acaba de habilitar la eliminación temporal, puede que no tenga los permisos de **recuperación** y **purga**.</span><span class="sxs-lookup"><span data-stu-id="e3649-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="e3649-181">Secretos</span><span class="sxs-lookup"><span data-stu-id="e3649-181">Secrets</span></span>

<span data-ttu-id="e3649-182">Al igual que con las claves, se trabaja con los secretos de un almacén de claves con sus propios comandos.</span><span class="sxs-lookup"><span data-stu-id="e3649-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="e3649-183">Después, son comandos de Hola para eliminar, enumerar, recuperación y purga de secretos.</span><span class="sxs-lookup"><span data-stu-id="e3649-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="e3649-184">Elimine un secreto llamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="e3649-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="e3649-185">Enumere todos los secretos eliminados de un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e3649-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="e3649-186">Recuperar un secreto en estado de hello eliminado:</span><span class="sxs-lookup"><span data-stu-id="e3649-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="e3649-187">Purgue un secreto en el estado eliminado:</span><span class="sxs-lookup"><span data-stu-id="e3649-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="e3649-188">Si purga un secreto se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e3649-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="e3649-189">Purga y almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="e3649-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="e3649-190">Objetos de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e3649-190">Key vault objects</span></span>

<span data-ttu-id="e3649-191">Si purga una clave, un secreto o un certificado se eliminarán permanentemente, lo que significa que no se podrán recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e3649-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="e3649-192">almacén de claves de Hola que contenía Hola Eliminar objeto sin embargo permanecerán intacto así como todos los demás objetos de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3649-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="e3649-193">Almacenes de claves como contenedores</span><span class="sxs-lookup"><span data-stu-id="e3649-193">Key vaults as containers</span></span>
<span data-ttu-id="e3649-194">Cuando se purga un almacén de claves, todo su contenido, incluidas las claves, los secretos y los certificados, se eliminan permanentemente.</span><span class="sxs-lookup"><span data-stu-id="e3649-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="e3649-195">toopurge un almacén de claves, use hello `Remove-AzureRmKeyVault` comando con la opción de hello `-InRemovedState` y especificando la ubicación de Hola de almacén de claves de hello eliminado con hello `-Location location` argumento.</span><span class="sxs-lookup"><span data-stu-id="e3649-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="e3649-196">Puede encontrar la ubicación Hola de un almacén eliminado mediante el comando hello `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="e3649-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="e3649-197">Si purga un almacén de claves se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e3649-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="e3649-198">Se requieren permisos de purga</span><span class="sxs-lookup"><span data-stu-id="e3649-198">Purge permissions required</span></span>
- <span data-ttu-id="e3649-199">toopurge un almacén de claves eliminado, tal que el almacén de Hola y todo su contenido se quita de forma permanente, Hola usuario necesita RBAC permiso tooperform una *Microsoft.KeyVault/locations/deletedVaults/purge/action* operación.</span><span class="sxs-lookup"><span data-stu-id="e3649-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="e3649-200">clave de hello eliminado de toolist, almacén Hola un usuario tiene RBAC permiso tooperform *Microsoft.KeyVault/deletedVaults/read* permiso.</span><span class="sxs-lookup"><span data-stu-id="e3649-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="e3649-201">Solo un administrador de suscripción tiene estos permisos.</span><span class="sxs-lookup"><span data-stu-id="e3649-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="e3649-202">Purga programada</span><span class="sxs-lookup"><span data-stu-id="e3649-202">Scheduled purge</span></span>

<span data-ttu-id="e3649-203">Enumerar los objetos de almacén de claves eliminadas muestra cuándo son toobe schedled purgado por el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e3649-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="e3649-204">Hola *programada fecha purgar* campo indica cuando un objeto de almacén de claves se eliminará permanentemente, si se realiza ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="e3649-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="e3649-205">De forma predeterminada, el período de retención de Hola para un objeto de almacén de claves eliminadas es 90 días.</span><span class="sxs-lookup"><span data-stu-id="e3649-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="e3649-206">Un objeto de almacén purgado, desencadenado por el valor de su campo de *fecha de purga programada*, se eliminará permanentemente.</span><span class="sxs-lookup"><span data-stu-id="e3649-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="e3649-207">No se podrá volver a recuperar.</span><span class="sxs-lookup"><span data-stu-id="e3649-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="e3649-208">Otros recursos:</span><span class="sxs-lookup"><span data-stu-id="e3649-208">Other resources</span></span>

- <span data-ttu-id="e3649-209">Para obtener una información general sobre la nueva característica de eliminación temporal, consulte [la información general sobre la eliminación temporal de Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="e3649-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="e3649-210">Para obtener una descripción general del uso de Azure Key Vault, consulte [Introducción a Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e3649-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

