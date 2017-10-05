---
title: "Introducción al almacén de claves en la pila de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 32fad3ce17c877db661573e67c9cb5948b3c78fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-key-vault"></a><span data-ttu-id="4329b-103">Introducción al almacén de claves</span><span class="sxs-lookup"><span data-stu-id="4329b-103">Getting started with Key Vault</span></span>
<span data-ttu-id="4329b-104">Esta sección describen los pasos para crear un almacén, administrar claves y secretos, así como para autorizar a los usuarios o aplicaciones para invocar operaciones en el almacén en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="4329b-104">This section describes the steps to create a vault, manage keys and secrets as well as authorize users or applications to invoke operations in the vault in Azure Stack.</span></span> <span data-ttu-id="4329b-105">Los siguientes pasos se supone existe una suscripción de inquilino y servicio de KeyVault está registrado en esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="4329b-105">The following steps assume a tenant subscription exists and KeyVault service is registered within that subscription.</span></span> <span data-ttu-id="4329b-106">Todos los comandos de ejemplo se basan en los cmdlets de KeyVault disponibles como parte del SDK de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4329b-106">All the example commands are based on the KeyVault cmdlets available as part of the Azure PowerShell SDK.</span></span>

## <a name="enabling-the-tenant-subscription-for-vault-operations"></a><span data-ttu-id="4329b-107">Habilitar la suscripción de inquilino para las operaciones del almacén</span><span class="sxs-lookup"><span data-stu-id="4329b-107">Enabling the tenant subscription for Vault operations</span></span>
<span data-ttu-id="4329b-108">Para poder emitir las operaciones en cualquier almacén, debe asegurarse de que su suscripción está habilitada para las operaciones del almacén.</span><span class="sxs-lookup"><span data-stu-id="4329b-108">Before you can issue operations against any vault, you need to ensure that your subscription is enabled for vault operations.</span></span> <span data-ttu-id="4329b-109">Se puede confirmar que emita el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4329b-109">You can confirm that by issuing the following PowerShell command:</span></span>

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

<span data-ttu-id="4329b-110">El resultado del comando anterior debería notificar "Registrado" para el estado de "Registro" de cada fila.</span><span class="sxs-lookup"><span data-stu-id="4329b-110">The output of the above command should report “Registered” for the “Registration” state of every row.</span></span>

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 <span data-ttu-id="4329b-111">Si no es el caso, debe invocar el comando siguiente para registrar el servicio de KeyVault dentro de su suscripción:</span><span class="sxs-lookup"><span data-stu-id="4329b-111">If that’s not the case, you should invoke the following command to register the KeyVault service within your subscription:</span></span>

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

<span data-ttu-id="4329b-112">Y lo siguiente es el resultado del comando:</span><span class="sxs-lookup"><span data-stu-id="4329b-112">And the folowing is the output of the command:</span></span>

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> <span data-ttu-id="4329b-113">Si se produce un error: "*la suscripción no está registrada con el almacén de claves de Azure*" al invocar KeyVault cmdlets, confirme que ha habilitado el proveedor de recursos de KeyVault por las instrucciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="4329b-113">If you get the error: "*The subscription is not registered with Azure Key Vault*" when invoking KeyVault cmdlets, please confirm you have enabled the KeyVault resource provider per instructions above.</span></span>
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-to-store-and-manage-cryptographic-keys-and-secrets"></a><span data-ttu-id="4329b-114">Crear un contenedor reforzado (un almacén) en la pila de Azure para almacenar y administrar las claves criptográficas y secretos</span><span class="sxs-lookup"><span data-stu-id="4329b-114">Creating a hardened container (a vault) in Azure Stack to store and manage cryptographic keys and secrets</span></span>
<span data-ttu-id="4329b-115">Para crear un almacén, un inquilino en primer lugar debe crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4329b-115">In order to create a Vault, a tenant should first create a resource group.</span></span> <span data-ttu-id="4329b-116">Los siguientes comandos de PowerShell crean un grupo de recursos y, a continuación, en un almacén de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4329b-116">The following PowerShell commands create a resource group and then a Vault in that Resource Group.</span></span> <span data-ttu-id="4329b-117">El ejemplo también incluye el resultado típico de ese cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4329b-117">The example also includes the typical output from that cmdlet.</span></span>

### <a name="creating-a-resource-group"></a><span data-ttu-id="4329b-118">Crear un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="4329b-118">Creating a resource group:</span></span>
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

<span data-ttu-id="4329b-119">Salida:</span><span class="sxs-lookup"><span data-stu-id="4329b-119">Output:</span></span>

    VERBOSE: Performing the operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a><span data-ttu-id="4329b-120">Creación de un almacén:</span><span class="sxs-lookup"><span data-stu-id="4329b-120">Creating a vault:</span></span>
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

<span data-ttu-id="4329b-121">Salida:</span><span class="sxs-lookup"><span data-stu-id="4329b-121">Output:</span></span>

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
    Permissions to Keys : get, create, delete, list, update, import, backup, restore
    Permissions to Secrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

<span data-ttu-id="4329b-122">El resultado de este cmdlet muestra las propiedades del Almacén de claves que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="4329b-122">The output of this cmdlet shows properties of the key vault that you’ve just created.</span></span> <span data-ttu-id="4329b-123">Las dos propiedades más importantes son:</span><span class="sxs-lookup"><span data-stu-id="4329b-123">The two most important properties are:</span></span>

* <span data-ttu-id="4329b-124">**El nombre del almacén**: en el ejemplo, esto es **vault010**.</span><span class="sxs-lookup"><span data-stu-id="4329b-124">**Vault Name**: In the example, this is **vault010**.</span></span> <span data-ttu-id="4329b-125">Utilizará este nombre para otros cmdlets del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="4329b-125">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="4329b-126">**URI de almacén**: en el ejemplo, esto es https://vault010.vault.local.azurestack.global.</span><span class="sxs-lookup"><span data-stu-id="4329b-126">**Vault URI**: In the example, this is https://vault010.vault.local.azurestack.global.</span></span> <span data-ttu-id="4329b-127">Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.</span><span class="sxs-lookup"><span data-stu-id="4329b-127">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="4329b-128">Su cuenta de Azure ahora está autorizada para realizar operaciones en este Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="4329b-128">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="4329b-129">Hasta el momento, nadie más lo está.</span><span class="sxs-lookup"><span data-stu-id="4329b-129">As yet, nobody else is.</span></span>

## <a name="operating-on-keys-and-secrets"></a><span data-ttu-id="4329b-130">Funciona en las claves y secretos</span><span class="sxs-lookup"><span data-stu-id="4329b-130">Operating on Keys and Secrets</span></span>
<span data-ttu-id="4329b-131">Después de crear un almacén, siga los pasos siguientes para crear, administrar claves y secretos:</span><span class="sxs-lookup"><span data-stu-id="4329b-131">After creating a vault, follow the below steps to create manage keys and secrets:</span></span>

### <a name="creating-a-key"></a><span data-ttu-id="4329b-132">Crear una clave</span><span class="sxs-lookup"><span data-stu-id="4329b-132">Creating a key</span></span>
<span data-ttu-id="4329b-133">Para crear una clave, use la **Add-AzureKeyVaultKey** por el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="4329b-133">In order to create a key, use the **Add-AzureKeyVaultKey** per the example below.</span></span> <span data-ttu-id="4329b-134">Después de la creación de clave correcta, el cmdlet mostrará los detalles de la clave recién creados.</span><span class="sxs-lookup"><span data-stu-id="4329b-134">After successful key creation, the cmdlet will output the newly created key details.</span></span>

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

<span data-ttu-id="4329b-135">El siguiente es el resultado de la *Add-AzureKeyVaultKey* cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4329b-135">The following is the output of the *Add-AzureKeyVaultKey* cmdlet:</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

<span data-ttu-id="4329b-136">Ahora puede utilizar el URI para hacer referencia a esta clave que creó o cargó en el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="4329b-136">You can now reference this key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="4329b-137">Usar **https://vault010.vault.local.azurestack.global:443/claves/keyVaultKeyName001** para obtener la versión actual, siempre y usar **https://vault010.vault.local.azurestack.global:443/claves / keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** para obtener esta versión específica.</span><span class="sxs-lookup"><span data-stu-id="4329b-137">Use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001** to always get the current version; and use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** to get this specific version.</span></span>

### <a name="retrieving-a-key"></a><span data-ttu-id="4329b-138">Recuperar una clave</span><span class="sxs-lookup"><span data-stu-id="4329b-138">Retrieving a key</span></span>
<span data-ttu-id="4329b-139">Use la **Get-AzureKeyVaultKey** para recuperar una clave y sus detalles según el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4329b-139">Use the **Get-AzureKeyVaultKey** to retrieve a key and its details per the following example:</span></span>

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

<span data-ttu-id="4329b-140">El siguiente es el resultado de Get-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="4329b-140">The following is the output of Get-AzureKeyVaultKey</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a><span data-ttu-id="4329b-141">Establecer un secreto</span><span class="sxs-lookup"><span data-stu-id="4329b-141">Setting a secret</span></span>
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

<span data-ttu-id="4329b-142">Salida</span><span class="sxs-lookup"><span data-stu-id="4329b-142">Output</span></span>

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

### <a name="retrieving-a-secret"></a><span data-ttu-id="4329b-143">Recuperar un secreto</span><span class="sxs-lookup"><span data-stu-id="4329b-143">Retrieving a secret</span></span>
    Get-AzureKeyVaultSecret -VaultName vault010

<span data-ttu-id="4329b-144">Salida</span><span class="sxs-lookup"><span data-stu-id="4329b-144">Output</span></span>

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

<span data-ttu-id="4329b-145">Ahora, el Almacén de claves y la clave o el secreto están listos para que los usen las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4329b-145">Now, your key vault and key or secret is ready for applications to use.</span></span>
<span data-ttu-id="4329b-146">Las aplicaciones deben contar con autorización para poder usarlos.</span><span class="sxs-lookup"><span data-stu-id="4329b-146">You must authorize applications to use them.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="4329b-147">Autorización de la aplicación para que use la clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="4329b-147">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="4329b-148">Para autorizar la aplicación para tener acceso a la clave o el secreto en el almacén, use Set -**AzureRmKeyVaultAccessPolicy** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4329b-148">To authorize the application to access the key or secret in the vault, use the Set-**AzureRmKeyVaultAccessPolicy** cmdlet.</span></span>

<span data-ttu-id="4329b-149">Por ejemplo, si el nombre del almacén es *ContosoKeyVault* y la aplicación que desea autorizar tiene un *Id. de cliente* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*y ¿desea autorizar a la aplicación para descifrar y firmar con claves en el almacén, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4329b-149">For example, if your vault name is *ContosoKeyVault* and the application you want to authorize has a *Client ID* of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="4329b-150">Si desea autorizar a esa misma aplicación para leer los secretos en el almacén, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4329b-150">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a><span data-ttu-id="4329b-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4329b-151">Next steps</span></span>
[<span data-ttu-id="4329b-152">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="4329b-152">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="4329b-153">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="4329b-153">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

