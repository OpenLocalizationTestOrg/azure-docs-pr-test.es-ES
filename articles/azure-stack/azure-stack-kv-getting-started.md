---
title: "aaaGetting a trabajar con el almacén de claves en la pila de Azure | Documentos de Microsoft"
description: "Introducción al uso de almacén de claves de pila de Azure"
services: azure-stack
documentationcenter: 
author: rlfmendes
manager: natmack
editor: 
ms.assetid: b973be33-2fc1-4ee6-976a-84ed270e7254
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: ricardom
ms.openlocfilehash: 66ae55291951ee0c673ba2b50ea4aecb3df19a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-key-vault"></a><span data-ttu-id="aff3a-103">Introducción al almacén de claves</span><span class="sxs-lookup"><span data-stu-id="aff3a-103">Getting started with Key Vault</span></span>
<span data-ttu-id="aff3a-104">Esta sección describen Hola pasos toocreate un almacén, administrar claves y secretos como autorizar usuarios o aplicaciones de operaciones de tooinvoke en el almacén de hello en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="aff3a-104">This section describes hello steps toocreate a vault, manage keys and secrets as well as authorize users or applications tooinvoke operations in hello vault in Azure Stack.</span></span> <span data-ttu-id="aff3a-105">Hola siguiendo los pasos se supone existe una suscripción de inquilino y servicio de KeyVault está registrado en esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="aff3a-105">hello following steps assume a tenant subscription exists and KeyVault service is registered within that subscription.</span></span> <span data-ttu-id="aff3a-106">Todos los comandos de ejemplo de Hola se basan en hello KeyVault cmdlets disponibles como parte del SDK de Azure PowerShell Hola.</span><span class="sxs-lookup"><span data-stu-id="aff3a-106">All hello example commands are based on hello KeyVault cmdlets available as part of hello Azure PowerShell SDK.</span></span>

## <a name="enabling-hello-tenant-subscription-for-vault-operations"></a><span data-ttu-id="aff3a-107">Habilitar la suscripción de inquilino de Hola para las operaciones del almacén</span><span class="sxs-lookup"><span data-stu-id="aff3a-107">Enabling hello tenant subscription for Vault operations</span></span>
<span data-ttu-id="aff3a-108">Para poder emitir las operaciones en cualquier almacén, necesita tooensure que su suscripción está habilitada para las operaciones del almacén.</span><span class="sxs-lookup"><span data-stu-id="aff3a-108">Before you can issue operations against any vault, you need tooensure that your subscription is enabled for vault operations.</span></span> <span data-ttu-id="aff3a-109">Puede confirmar mediante la emisión de hello siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aff3a-109">You can confirm that by issuing hello following PowerShell command:</span></span>

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

<span data-ttu-id="aff3a-110">salida de Hello de hello encima comando debería notificar "Registrado" para hello el estado de "Registro" de cada fila.</span><span class="sxs-lookup"><span data-stu-id="aff3a-110">hello output of hello above command should report “Registered” for hello “Registration” state of every row.</span></span>

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 <span data-ttu-id="aff3a-111">Si no es el caso de hello, debe invocar Hola después de comando tooregister hello KeyVault servicio dentro de su suscripción:</span><span class="sxs-lookup"><span data-stu-id="aff3a-111">If that’s not hello case, you should invoke hello following command tooregister hello KeyVault service within your subscription:</span></span>

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

<span data-ttu-id="aff3a-112">Y lo siguiente hello es resultado de hello de comando de hello:</span><span class="sxs-lookup"><span data-stu-id="aff3a-112">And hello folowing is hello output of hello command:</span></span>

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> <span data-ttu-id="aff3a-113">Si recibe el error de hello: "*Hola suscripción no está registrada con el almacén de claves de Azure*" al invocar KeyVault cmdlets, confirme que ha habilitado el proveedor de recursos de KeyVault Hola por instrucciones mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aff3a-113">If you get hello error: "*hello subscription is not registered with Azure Key Vault*" when invoking KeyVault cmdlets, please confirm you have enabled hello KeyVault resource provider per instructions above.</span></span>
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-toostore-and-manage-cryptographic-keys-and-secrets"></a><span data-ttu-id="aff3a-114">Crear un contenedor reforzado (un almacén) en Azure pila toostore y administrar las claves criptográficas y secretos</span><span class="sxs-lookup"><span data-stu-id="aff3a-114">Creating a hardened container (a vault) in Azure Stack toostore and manage cryptographic keys and secrets</span></span>
<span data-ttu-id="aff3a-115">En orden toocreate un almacén, un inquilino en primer lugar debe crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aff3a-115">In order toocreate a Vault, a tenant should first create a resource group.</span></span> <span data-ttu-id="aff3a-116">Hello siguientes comandos de PowerShell crean un grupo de recursos y, a continuación, en un almacén de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aff3a-116">hello following PowerShell commands create a resource group and then a Vault in that Resource Group.</span></span> <span data-ttu-id="aff3a-117">ejemplo de Hola también incluye la salida típica Hola de ese cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aff3a-117">hello example also includes hello typical output from that cmdlet.</span></span>

### <a name="creating-a-resource-group"></a><span data-ttu-id="aff3a-118">Crear un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="aff3a-118">Creating a resource group:</span></span>
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

<span data-ttu-id="aff3a-119">Salida:</span><span class="sxs-lookup"><span data-stu-id="aff3a-119">Output:</span></span>

    VERBOSE: Performing hello operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a><span data-ttu-id="aff3a-120">Creación de un almacén:</span><span class="sxs-lookup"><span data-stu-id="aff3a-120">Creating a vault:</span></span>
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

<span data-ttu-id="aff3a-121">Salida:</span><span class="sxs-lookup"><span data-stu-id="aff3a-121">Output:</span></span>

    VaultUri : https://vault010.vault.local.azurestack.global
    TenantId : 5454420b-2e38-4b9e-8b56-1712d321cf33
    TenantName : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Sku : Standard
    EnabledForDeployment : False
    EnabledForTemplateDeployment : False
    EnabledForDiskEncryption : False
    AccessPolicies : {5454420b-2e38-4b9e-8b56-1712d321cf33}
    AccessPoliciesText :
    Tenant ID : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Object ID : ca342e90-f6aa-435b-a11c-dfe5ef0bfeeb
    Application ID :
    Display Name : Tenant Admin (tenantadmin1@msazurestack.onmicrosoft.com)
    Permissions tooKeys : get, create, delete, list, update, import, backup, restore
    Permissions tooSecrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

<span data-ttu-id="aff3a-122">salida de Hello de este cmdlet muestra propiedades del almacén de claves de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="aff3a-122">hello output of this cmdlet shows properties of hello key vault that you’ve just created.</span></span> <span data-ttu-id="aff3a-123">propiedades de Hello dos más importantes son:</span><span class="sxs-lookup"><span data-stu-id="aff3a-123">hello two most important properties are:</span></span>

* <span data-ttu-id="aff3a-124">**El nombre del almacén**: en el ejemplo de Hola, esto es **vault010**.</span><span class="sxs-lookup"><span data-stu-id="aff3a-124">**Vault Name**: In hello example, this is **vault010**.</span></span> <span data-ttu-id="aff3a-125">Utilizará este nombre para otros cmdlets del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="aff3a-125">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="aff3a-126">**URI de almacén**: en el ejemplo de Hola, es https://vault010.vault.local.azurestack.global.</span><span class="sxs-lookup"><span data-stu-id="aff3a-126">**Vault URI**: In hello example, this is https://vault010.vault.local.azurestack.global.</span></span> <span data-ttu-id="aff3a-127">Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.</span><span class="sxs-lookup"><span data-stu-id="aff3a-127">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="aff3a-128">Su cuenta de Azure es ahora tooperform autorizado cualquier operación en esta clave de seguridad del almacén.</span><span class="sxs-lookup"><span data-stu-id="aff3a-128">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="aff3a-129">Hasta el momento, nadie más lo está.</span><span class="sxs-lookup"><span data-stu-id="aff3a-129">As yet, nobody else is.</span></span>

## <a name="operating-on-keys-and-secrets"></a><span data-ttu-id="aff3a-130">Funciona en las claves y secretos</span><span class="sxs-lookup"><span data-stu-id="aff3a-130">Operating on Keys and Secrets</span></span>
<span data-ttu-id="aff3a-131">Después de crear un almacén, Hola de seguimiento por debajo de los pasos toocreate administrar claves y secretos:</span><span class="sxs-lookup"><span data-stu-id="aff3a-131">After creating a vault, follow hello below steps toocreate manage keys and secrets:</span></span>

### <a name="creating-a-key"></a><span data-ttu-id="aff3a-132">Crear una clave</span><span class="sxs-lookup"><span data-stu-id="aff3a-132">Creating a key</span></span>
<span data-ttu-id="aff3a-133">En el orden toocreate una clave, usar hello **Add-AzureKeyVaultKey** por el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aff3a-133">In order toocreate a key, use hello **Add-AzureKeyVaultKey** per hello example below.</span></span> <span data-ttu-id="aff3a-134">Después de la creación de clave correcta, Hola cmdlet darán como resultado Hola que acaba de crear detalles de la clave.</span><span class="sxs-lookup"><span data-stu-id="aff3a-134">After successful key creation, hello cmdlet will output hello newly created key details.</span></span>

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

<span data-ttu-id="aff3a-135">Hello aquí te mostramos la salida de hello de hello *Add-AzureKeyVaultKey* cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aff3a-135">hello following is hello output of hello *Add-AzureKeyVaultKey* cmdlet:</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

<span data-ttu-id="aff3a-136">Ahora puede hacer referencia a esta clave que se creó o cargó tooAzure el almacén de claves, utilizando su URI.</span><span class="sxs-lookup"><span data-stu-id="aff3a-136">You can now reference this key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="aff3a-137">Usar **https://vault010.vault.local.azurestack.global:443/claves/keyVaultKeyName001** tooalways obtener la versión actual de hello; y usar **https://vault010.vault.local.azurestack.global:443/claves / keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget esta versión específica.</span><span class="sxs-lookup"><span data-stu-id="aff3a-137">Use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001** tooalways get hello current version; and use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget this specific version.</span></span>

### <a name="retrieving-a-key"></a><span data-ttu-id="aff3a-138">Recuperar una clave</span><span class="sxs-lookup"><span data-stu-id="aff3a-138">Retrieving a key</span></span>
<span data-ttu-id="aff3a-139">Hola de uso **Get-AzureKeyVaultKey** tooretrieve una clave y sus detalles por Hola después ejemplo:</span><span class="sxs-lookup"><span data-stu-id="aff3a-139">Use hello **Get-AzureKeyVaultKey** tooretrieve a key and its details per hello following example:</span></span>

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

<span data-ttu-id="aff3a-140">Hola aquí te mostramos la salida de hello de Get-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="aff3a-140">hello following is hello output of Get-AzureKeyVaultKey</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a><span data-ttu-id="aff3a-141">Establecer un secreto</span><span class="sxs-lookup"><span data-stu-id="aff3a-141">Setting a secret</span></span>
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

<span data-ttu-id="aff3a-142">Salida</span><span class="sxs-lookup"><span data-stu-id="aff3a-142">Output</span></span>

    Vault Name : vault010
    Name : MySecret
    Version : 65a387f2ed4a416180e852b970846f5b
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret/65a387f2ed4a416180e852b970846f5b
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags : 

### <a name="retrieving-a-secret"></a><span data-ttu-id="aff3a-143">Recuperar un secreto</span><span class="sxs-lookup"><span data-stu-id="aff3a-143">Retrieving a secret</span></span>
    Get-AzureKeyVaultSecret -VaultName vault010

<span data-ttu-id="aff3a-144">Salida</span><span class="sxs-lookup"><span data-stu-id="aff3a-144">Output</span></span>

    Vault Name : vault010
    Name : MySecret
    Version :
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags :

<span data-ttu-id="aff3a-145">Ahora, el almacén de claves y la clave o el secreto está lista para toouse de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aff3a-145">Now, your key vault and key or secret is ready for applications toouse.</span></span>
<span data-ttu-id="aff3a-146">Debe autorizar aplicaciones toouse ellos.</span><span class="sxs-lookup"><span data-stu-id="aff3a-146">You must authorize applications toouse them.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="aff3a-147">Autorizar Hola aplicación toouse Hola clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="aff3a-147">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="aff3a-148">tooauthorize Hola aplicación tooaccess Hola clave o el secreto en el almacén de Hola Hola use Set -**AzureRmKeyVaultAccessPolicy** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aff3a-148">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello Set-**AzureRmKeyVaultAccessPolicy** cmdlet.</span></span>

<span data-ttu-id="aff3a-149">Por ejemplo, si el nombre del almacén es *ContosoKeyVault* y aplicación hello desea tooauthorize tiene un *Id. de cliente* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*y desea tooauthorize Hola aplicación toodecrypt e inicie sesión con las claves en el almacén, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="aff3a-149">For example, if your vault name is *ContosoKeyVault* and hello application you want tooauthorize has a *Client ID* of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="aff3a-150">Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="aff3a-150">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a><span data-ttu-id="aff3a-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aff3a-151">Next steps</span></span>
[<span data-ttu-id="aff3a-152">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="aff3a-152">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="aff3a-153">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="aff3a-153">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

