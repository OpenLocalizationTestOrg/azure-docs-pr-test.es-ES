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
# <a name="getting-started-with-key-vault"></a>Introducción al almacén de claves
Esta sección describen los pasos para crear un almacén, administrar claves y secretos, así como para autorizar a los usuarios o aplicaciones para invocar operaciones en el almacén en la pila de Azure. Los siguientes pasos se supone existe una suscripción de inquilino y servicio de KeyVault está registrado en esa suscripción. Todos los comandos de ejemplo se basan en los cmdlets de KeyVault disponibles como parte del SDK de Azure PowerShell.

## <a name="enabling-the-tenant-subscription-for-vault-operations"></a>Habilitar la suscripción de inquilino para las operaciones del almacén
Para poder emitir las operaciones en cualquier almacén, debe asegurarse de que su suscripción está habilitada para las operaciones del almacén. Se puede confirmar que emita el siguiente comando de PowerShell:

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

El resultado del comando anterior debería notificar "Registrado" para el estado de "Registro" de cada fila.

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 Si no es el caso, debe invocar el comando siguiente para registrar el servicio de KeyVault dentro de su suscripción:

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

Y lo siguiente es el resultado del comando:

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> Si se produce un error: "*la suscripción no está registrada con el almacén de claves de Azure*" al invocar KeyVault cmdlets, confirme que ha habilitado el proveedor de recursos de KeyVault por las instrucciones anteriores.
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-to-store-and-manage-cryptographic-keys-and-secrets"></a>Crear un contenedor reforzado (un almacén) en la pila de Azure para almacenar y administrar las claves criptográficas y secretos
Para crear un almacén, un inquilino en primer lugar debe crear un grupo de recursos. Los siguientes comandos de PowerShell crean un grupo de recursos y, a continuación, en un almacén de ese grupo de recursos. El ejemplo también incluye el resultado típico de ese cmdlet.

### <a name="creating-a-resource-group"></a>Crear un grupo de recursos:
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

Salida:

    VERBOSE: Performing the operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a>Creación de un almacén:
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

Salida:

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

El resultado de este cmdlet muestra las propiedades del Almacén de claves que acaba de crear. Las dos propiedades más importantes son:

* **El nombre del almacén**: en el ejemplo, esto es **vault010**. Utilizará este nombre para otros cmdlets del Almacén de claves.
* **URI de almacén**: en el ejemplo, esto es https://vault010.vault.local.azurestack.global. Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.

Su cuenta de Azure ahora está autorizada para realizar operaciones en este Almacén de claves. Hasta el momento, nadie más lo está.

## <a name="operating-on-keys-and-secrets"></a>Funciona en las claves y secretos
Después de crear un almacén, siga los pasos siguientes para crear, administrar claves y secretos:

### <a name="creating-a-key"></a>Crear una clave
Para crear una clave, use la **Add-AzureKeyVaultKey** por el ejemplo siguiente. Después de la creación de clave correcta, el cmdlet mostrará los detalles de la clave recién creados.

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

El siguiente es el resultado de la *Add-AzureKeyVaultKey* cmdlet:

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

Ahora puede utilizar el URI para hacer referencia a esta clave que creó o cargó en el Almacén de claves de Azure. Usar **https://vault010.vault.local.azurestack.global:443/claves/keyVaultKeyName001** para obtener la versión actual, siempre y usar **https://vault010.vault.local.azurestack.global:443/claves / keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** para obtener esta versión específica.

### <a name="retrieving-a-key"></a>Recuperar una clave
Use la **Get-AzureKeyVaultKey** para recuperar una clave y sus detalles según el ejemplo siguiente:

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

El siguiente es el resultado de Get-AzureKeyVaultKey

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a>Establecer un secreto
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

Salida

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

### <a name="retrieving-a-secret"></a>Recuperar un secreto
    Get-AzureKeyVaultSecret -VaultName vault010

Salida

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

Ahora, el Almacén de claves y la clave o el secreto están listos para que los usen las aplicaciones.
Las aplicaciones deben contar con autorización para poder usarlos.

## <a name="authorize-the-application-to-use-the-key-or-secret"></a>Autorización de la aplicación para que use la clave o el secreto
Para autorizar la aplicación para tener acceso a la clave o el secreto en el almacén, use Set -**AzureRmKeyVaultAccessPolicy** cmdlet.

Por ejemplo, si el nombre del almacén es *ContosoKeyVault* y la aplicación que desea autorizar tiene un *Id. de cliente* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*y ¿desea autorizar a la aplicación para descifrar y firmar con claves en el almacén, ejecute lo siguiente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Si desea autorizar a esa misma aplicación para leer los secretos en el almacén, ejecute lo siguiente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>Pasos siguientes
[Implementación de una máquina virtual con una contraseña de Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Implementación de una máquina virtual con un certificado de Key Vault](azure-stack-kv-push-secret-into-vm.md)

