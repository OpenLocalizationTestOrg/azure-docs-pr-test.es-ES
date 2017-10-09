---
ms.assetid: 
title: "aaaAzure del almacén de claves: cómo eliminar toouse automático con CLI"
description: "Ejemplos de casos de uso de eliminación temporal con fragmentos de código de la CLI"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="2392c-103">Cómo toouse el almacén de claves soft-delete con CLI</span><span class="sxs-lookup"><span data-stu-id="2392c-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="2392c-104">La característica de eliminación temporal de Azure Key Vault permite recuperar almacenes y objetos de almacenes eliminados.</span><span class="sxs-lookup"><span data-stu-id="2392c-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="2392c-105">En concreto, soft-delete Hola direcciones los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="2392c-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="2392c-106">Compatibilidad con la eliminación recuperable de una instancia de Key Vault</span><span class="sxs-lookup"><span data-stu-id="2392c-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="2392c-107">Compatibilidad con la eliminación recuperable de objetos de Key Vault: claves, secretos y certificados</span><span class="sxs-lookup"><span data-stu-id="2392c-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2392c-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2392c-108">Prerequisites</span></span>

- <span data-ttu-id="2392c-109">CLI de Azure 2.0: si no tiene esta configuración para su entorno, consulte [Administración de Key Vault mediante CLI 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="2392c-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="2392c-110">Para obtener información de referencia específica sobre Key Vault para la CLI, consulte la [referencia de Key Vault para la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="2392c-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="2392c-111">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="2392c-111">Required permissions</span></span>

<span data-ttu-id="2392c-112">Las operaciones de Key Vault se administran por separado mediante los permisos de control de acceso basado en roles (RBAC) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2392c-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="2392c-113">Operación</span><span class="sxs-lookup"><span data-stu-id="2392c-113">Operation</span></span> | <span data-ttu-id="2392c-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="2392c-114">Description</span></span> | <span data-ttu-id="2392c-115">Permiso del usuario</span><span class="sxs-lookup"><span data-stu-id="2392c-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="2392c-116">Enumerar</span><span class="sxs-lookup"><span data-stu-id="2392c-116">List</span></span>|<span data-ttu-id="2392c-117">Enumera los almacenes de claves eliminados.</span><span class="sxs-lookup"><span data-stu-id="2392c-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="2392c-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="2392c-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="2392c-119">Recuperar</span><span class="sxs-lookup"><span data-stu-id="2392c-119">Recover</span></span>|<span data-ttu-id="2392c-120">Restaura un almacén de claves eliminado.</span><span class="sxs-lookup"><span data-stu-id="2392c-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="2392c-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="2392c-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="2392c-122">Purgar</span><span class="sxs-lookup"><span data-stu-id="2392c-122">Purge</span></span>|<span data-ttu-id="2392c-123">Elimina permanentemente un almacén de claves eliminado y todo su contenido.</span><span class="sxs-lookup"><span data-stu-id="2392c-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="2392c-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="2392c-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="2392c-125">Para más información sobre los permisos y el control de acceso, consulte [Protección de un almacén de claves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="2392c-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="2392c-126">Habilitar la eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="2392c-126">Enabling soft-delete</span></span>

<span data-ttu-id="2392c-127">toobe puede toorecover del almacén de objetos almacenados en una clave o un almacén de claves se eliminó, primero debe habilitar la eliminación de software para ese almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="2392c-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="2392c-128">Almacén de claves existente</span><span class="sxs-lookup"><span data-stu-id="2392c-128">Existing key vault</span></span>

<span data-ttu-id="2392c-129">Para un almacén de claves existente denominado ContosoVault, habilite la eliminación temporal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="2392c-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="2392c-130">Actualmente necesita Hola de escritura de toouse Azure Resource Manager recursos manipulación toodirectly *enableSoftDelete* toohello recursos de almacén de claves de propiedad.</span><span class="sxs-lookup"><span data-stu-id="2392c-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="2392c-131">Almacén de claves nuevo</span><span class="sxs-lookup"><span data-stu-id="2392c-131">New key vault</span></span>

<span data-ttu-id="2392c-132">Habilitar la eliminación de software para un nuevo almacén de claves se realiza en el momento de creación mediante la adición de marca de soft-delete enable hello tooyour crear comando.</span><span class="sxs-lookup"><span data-stu-id="2392c-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="2392c-133">Comprobación de la habilitación de la eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="2392c-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="2392c-134">tooverify que un almacén de claves tiene habilitado, soft-delete Hola ejecución *mostrar* de comandos y busque hello 'Suave eliminar Enabled?'</span><span class="sxs-lookup"><span data-stu-id="2392c-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="2392c-135">y su valor, true o false.</span><span class="sxs-lookup"><span data-stu-id="2392c-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="2392c-136">Eliminación de un almacén de claves protegido por eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="2392c-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="2392c-137">Hola comando toodelete (o quitar) un almacén de claves permanece Hola mismo, pero sus cambios de comportamiento dependen de si ha habilitado soft-delete o no.</span><span class="sxs-lookup"><span data-stu-id="2392c-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="2392c-138">Si ejecuta el comando anterior de Hola para un almacén de claves que no tiene habilitada la eliminación temporal, se eliminará permanentemente este almacén de claves y todo su contenido sin ninguna opción para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="2392c-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="2392c-139">Uso de la eliminación temporal para proteger los almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="2392c-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="2392c-140">Con la eliminación temporal habilitada:</span><span class="sxs-lookup"><span data-stu-id="2392c-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="2392c-141">Cuando se elimina un almacén de claves, se quita de su grupo de recursos y se coloca en un espacio de nombres reservado que solo está asociado a la ubicación de Hola donde se creó.</span><span class="sxs-lookup"><span data-stu-id="2392c-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="2392c-142">Objetos de una clave eliminada del almacén, como las claves, secretos y certificados, son inaccesibles y mantenerse así mientras su almacén de claves que lo contiene está en estado de hello eliminado.</span><span class="sxs-lookup"><span data-stu-id="2392c-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="2392c-143">nombre DNS de Hola para un almacén de claves en un estado de eliminación se sigue reservando por lo tanto, no se puede crear un nuevo almacén de claves con el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="2392c-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="2392c-144">Puede ver almacenes de clave de estado eliminado, asociados a su suscripción, con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2392c-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="2392c-145">Hola *Id. de recurso* Hola salida hace referencia toohello de identificador de recurso original de este almacén.</span><span class="sxs-lookup"><span data-stu-id="2392c-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="2392c-146">Puesto que este almacén de claves está ahora en estado eliminado, no existe ningún recurso con ese identificador de recurso.</span><span class="sxs-lookup"><span data-stu-id="2392c-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="2392c-147">Hola *identificador* campo puede ser recurso de Hola de tooidentify usado durante la recuperación o purgar.</span><span class="sxs-lookup"><span data-stu-id="2392c-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="2392c-148">Hola *programada fecha purgar* campo indica al almacén de Hola se eliminarán permanentemente (purga) si no se realiza ninguna acción para este almacén eliminado.</span><span class="sxs-lookup"><span data-stu-id="2392c-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="2392c-149">Hola toocalculate período, que se usa de Hello predeterminado retención *programada fecha purgar*, es de 90 días.</span><span class="sxs-lookup"><span data-stu-id="2392c-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="2392c-150">Recuperación de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="2392c-150">Recovering a key vault</span></span>

<span data-ttu-id="2392c-151">toorecover un almacén de claves, necesita nombre de almacén de claves de hello toospecify, grupo de recursos y ubicación.</span><span class="sxs-lookup"><span data-stu-id="2392c-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="2392c-152">Nota Hola hello y ubicación del grupo de recursos del programa Hola a elimina el almacén de claves según sea necesario para un proceso de recuperación del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="2392c-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="2392c-153">Cuando se recupera un almacén de claves, el resultado de hello es un nuevo recurso con el identificador de recurso original. del almacén de hello claves</span><span class="sxs-lookup"><span data-stu-id="2392c-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="2392c-154">Si se ha quitado el grupo de recursos de Hola donde existía el almacén de claves de hello, debe crearse un nuevo grupo de recursos con el mismo nombre antes de que se puede recuperar el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="2392c-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="2392c-155">Objetos de Key Vault y eliminación temporal</span><span class="sxs-lookup"><span data-stu-id="2392c-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="2392c-156">Si tiene una clave, "ContosoFirstKey", en un almacén de claves denominado "ContosoVault" con eliminación temporal habilitada, este es el procedimiento para eliminarla.</span><span class="sxs-lookup"><span data-stu-id="2392c-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="2392c-157">Con el almacén de claves habilitado para la eliminación temporal, una clave eliminada seguirá apareciendo como eliminada excepto si enumera o recupera explícitamente las claves eliminadas.</span><span class="sxs-lookup"><span data-stu-id="2392c-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="2392c-158">Se producirá un error de mayoría de las operaciones en una clave de estado de hello eliminado excepto para enumerar una clave eliminada, recuperarlo o purgar.</span><span class="sxs-lookup"><span data-stu-id="2392c-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="2392c-159">Por ejemplo, las claves de toolist eliminar toorequest en un almacén de claves, utilizar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2392c-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="2392c-160">Estado de transición</span><span class="sxs-lookup"><span data-stu-id="2392c-160">Transition state</span></span> 

<span data-ttu-id="2392c-161">Cuando se elimina una clave en un almacén de claves con la eliminación de software habilitada, puede tardar unos segundos hello toocomplete de transición.</span><span class="sxs-lookup"><span data-stu-id="2392c-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="2392c-162">Durante este estado de transición, puede aparecer que esa clave hello no está en estado activo de Hola u Hola eliminado.</span><span class="sxs-lookup"><span data-stu-id="2392c-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="2392c-163">Este comando permite enumerar todas las claves eliminadas en el almacén de claves denominado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="2392c-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="2392c-164">Uso de la eliminación temporal con objetos de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="2392c-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="2392c-165">Igual que los almacenes de claves, una clave eliminada, secreto o certificado permanecerá en estado de eliminación para los días de too90 a menos que recuperarlo o lo purga.</span><span class="sxs-lookup"><span data-stu-id="2392c-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="2392c-166">simétricas</span><span class="sxs-lookup"><span data-stu-id="2392c-166">Keys</span></span>

<span data-ttu-id="2392c-167">toorecover una clave eliminada:</span><span class="sxs-lookup"><span data-stu-id="2392c-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="2392c-168">toopermanently eliminar una clave:</span><span class="sxs-lookup"><span data-stu-id="2392c-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="2392c-169">Si purga una clave se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2392c-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="2392c-170">Hola **recuperar** y **purgar** las acciones tienen sus propios permisos asociados en una directiva de acceso del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="2392c-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="2392c-171">Para una tooexecute de capaz de toobe principal de usuario o servicio un **recuperar** o **purgar** acción que deben tener permiso respectivos Hola para ese objeto (clave o el secreto) en directiva de acceso del almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="2392c-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="2392c-172">De forma predeterminada, Hola **purgar** permiso no se agrega la directiva de acceso del almacén de tooa claves cuando contextual 'all' hello es toogrant usado todos los datos de usuario de tooa de permisos.</span><span class="sxs-lookup"><span data-stu-id="2392c-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="2392c-173">Debe conceder el permiso de **purga** de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="2392c-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="2392c-174">Por ejemplo, Hola después concede comando user@contoso.com tooperform permiso varias operaciones de claves de *ContosoVault* incluidos **purgar**.</span><span class="sxs-lookup"><span data-stu-id="2392c-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="2392c-175">Establecimiento de una directiva de acceso del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="2392c-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="2392c-176">Si tiene un almacén de claves existente para el que se acaba de habilitar la eliminación temporal, puede que no tenga los permisos de **recuperación** y **purga**.</span><span class="sxs-lookup"><span data-stu-id="2392c-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="2392c-177">Secretos</span><span class="sxs-lookup"><span data-stu-id="2392c-177">Secrets</span></span>

<span data-ttu-id="2392c-178">Al igual que con las claves, se trabaja con los secretos de un almacén de claves con sus propios comandos.</span><span class="sxs-lookup"><span data-stu-id="2392c-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="2392c-179">Después, son comandos de Hola para eliminar, enumerar, recuperación y purga de secretos.</span><span class="sxs-lookup"><span data-stu-id="2392c-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="2392c-180">Elimine un secreto llamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="2392c-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="2392c-181">Enumere todos los secretos eliminados de un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="2392c-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="2392c-182">Recuperar un secreto en estado de hello eliminado:</span><span class="sxs-lookup"><span data-stu-id="2392c-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="2392c-183">Purgue un secreto en el estado eliminado:</span><span class="sxs-lookup"><span data-stu-id="2392c-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="2392c-184">Si purga un secreto se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2392c-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="2392c-185">Purga y almacenes de claves</span><span class="sxs-lookup"><span data-stu-id="2392c-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="2392c-186">Objetos de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="2392c-186">Key vault objects</span></span>

<span data-ttu-id="2392c-187">Si purga una clave, un secreto o un certificado se eliminarán permanentemente, lo que significa que no se podrán recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2392c-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="2392c-188">almacén de claves de Hola que contenía Hola Eliminar objeto sin embargo permanecerán intacto así como todos los demás objetos de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="2392c-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="2392c-189">Almacenes de claves como contenedores</span><span class="sxs-lookup"><span data-stu-id="2392c-189">Key vaults as containers</span></span>
<span data-ttu-id="2392c-190">Cuando se purga un almacén de claves, todo su contenido, incluidas las claves, los secretos y los certificados, se eliminan permanentemente.</span><span class="sxs-lookup"><span data-stu-id="2392c-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="2392c-191">toopurge un almacén de claves, use hello `az keyvault purge` comando.</span><span class="sxs-lookup"><span data-stu-id="2392c-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="2392c-192">Puede encontrar ubicación Hola almacenes de clave eliminada la suscripción con el comando de hello `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="2392c-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="2392c-193">Si purga un almacén de claves se eliminará permanentemente, lo que significa que no se podrá recuperar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2392c-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="2392c-194">Se requieren permisos de purga</span><span class="sxs-lookup"><span data-stu-id="2392c-194">Purge permissions required</span></span>
- <span data-ttu-id="2392c-195">toopurge un almacén de claves eliminado, tal que el almacén de Hola y todo su contenido se quita de forma permanente, Hola usuario necesita RBAC permiso tooperform una *Microsoft.KeyVault/locations/deletedVaults/purge/action* operación.</span><span class="sxs-lookup"><span data-stu-id="2392c-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="2392c-196">clave de hello eliminado de toolist, almacén Hola un usuario tiene RBAC permiso tooperform *Microsoft.KeyVault/deletedVaults/read* permiso.</span><span class="sxs-lookup"><span data-stu-id="2392c-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="2392c-197">Solo un administrador de suscripción tiene estos permisos.</span><span class="sxs-lookup"><span data-stu-id="2392c-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="2392c-198">Purga programada</span><span class="sxs-lookup"><span data-stu-id="2392c-198">Scheduled purge</span></span>

<span data-ttu-id="2392c-199">Enumerar los objetos de almacén de claves eliminadas muestra cuándo son toobe schedled purgado por el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="2392c-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="2392c-200">Hola *programada fecha purgar* campo indica cuando un objeto de almacén de claves se eliminará permanentemente, si se realiza ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="2392c-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="2392c-201">De forma predeterminada, el período de retención de Hola para un objeto de almacén de claves eliminadas es 90 días.</span><span class="sxs-lookup"><span data-stu-id="2392c-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="2392c-202">Un objeto de almacén purgado, desencadenado por el valor de su campo de *fecha de purga programada*, se eliminará permanentemente.</span><span class="sxs-lookup"><span data-stu-id="2392c-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="2392c-203">No se podrá volver a recuperar.</span><span class="sxs-lookup"><span data-stu-id="2392c-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="2392c-204">Otros recursos:</span><span class="sxs-lookup"><span data-stu-id="2392c-204">Other resources</span></span>

- <span data-ttu-id="2392c-205">Para obtener una información general sobre la nueva característica de eliminación temporal, consulte [la información general sobre la eliminación temporal de Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="2392c-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="2392c-206">Para obtener una descripción general del uso de Azure Key Vault, consulte [Introducción a Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2392c-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

