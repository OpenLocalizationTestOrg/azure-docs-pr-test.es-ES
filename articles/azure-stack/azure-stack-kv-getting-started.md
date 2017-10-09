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
# <a name="getting-started-with-key-vault"></a>Introducción al almacén de claves
Esta sección describen Hola pasos toocreate un almacén, administrar claves y secretos como autorizar usuarios o aplicaciones de operaciones de tooinvoke en el almacén de hello en la pila de Azure. Hola siguiendo los pasos se supone existe una suscripción de inquilino y servicio de KeyVault está registrado en esa suscripción. Todos los comandos de ejemplo de Hola se basan en hello KeyVault cmdlets disponibles como parte del SDK de Azure PowerShell Hola.

## <a name="enabling-hello-tenant-subscription-for-vault-operations"></a>Habilitar la suscripción de inquilino de Hola para las operaciones del almacén
Para poder emitir las operaciones en cualquier almacén, necesita tooensure que su suscripción está habilitada para las operaciones del almacén. Puede confirmar mediante la emisión de hello siguiente comando de PowerShell:

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

salida de Hello de hello encima comando debería notificar "Registrado" para hello el estado de "Registro" de cada fila.

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 Si no es el caso de hello, debe invocar Hola después de comando tooregister hello KeyVault servicio dentro de su suscripción:

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

Y lo siguiente hello es resultado de hello de comando de hello:

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> Si recibe el error de hello: "*Hola suscripción no está registrada con el almacén de claves de Azure*" al invocar KeyVault cmdlets, confirme que ha habilitado el proveedor de recursos de KeyVault Hola por instrucciones mencionadas anteriormente.
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-toostore-and-manage-cryptographic-keys-and-secrets"></a>Crear un contenedor reforzado (un almacén) en Azure pila toostore y administrar las claves criptográficas y secretos
En orden toocreate un almacén, un inquilino en primer lugar debe crear un grupo de recursos. Hello siguientes comandos de PowerShell crean un grupo de recursos y, a continuación, en un almacén de ese grupo de recursos. ejemplo de Hola también incluye la salida típica Hola de ese cmdlet.

### <a name="creating-a-resource-group"></a>Crear un grupo de recursos:
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

Salida:

    VERBOSE: Performing hello operation "Replacing resource group ..." on target "".
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
    Permissions tooKeys : get, create, delete, list, update, import, backup, restore
    Permissions tooSecrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

salida de Hello de este cmdlet muestra propiedades del almacén de claves de Hola que acaba de crear. propiedades de Hello dos más importantes son:

* **El nombre del almacén**: en el ejemplo de Hola, esto es **vault010**. Utilizará este nombre para otros cmdlets del Almacén de claves.
* **URI de almacén**: en el ejemplo de Hola, es https://vault010.vault.local.azurestack.global. Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.

Su cuenta de Azure es ahora tooperform autorizado cualquier operación en esta clave de seguridad del almacén. Hasta el momento, nadie más lo está.

## <a name="operating-on-keys-and-secrets"></a>Funciona en las claves y secretos
Después de crear un almacén, Hola de seguimiento por debajo de los pasos toocreate administrar claves y secretos:

### <a name="creating-a-key"></a>Crear una clave
En el orden toocreate una clave, usar hello **Add-AzureKeyVaultKey** por el siguiente ejemplo de Hola. Después de la creación de clave correcta, Hola cmdlet darán como resultado Hola que acaba de crear detalles de la clave.

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

Hello aquí te mostramos la salida de hello de hello *Add-AzureKeyVaultKey* cmdlet:

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

Ahora puede hacer referencia a esta clave que se creó o cargó tooAzure el almacén de claves, utilizando su URI. Usar **https://vault010.vault.local.azurestack.global:443/claves/keyVaultKeyName001** tooalways obtener la versión actual de hello; y usar **https://vault010.vault.local.azurestack.global:443/claves / keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget esta versión específica.

### <a name="retrieving-a-key"></a>Recuperar una clave
Hola de uso **Get-AzureKeyVaultKey** tooretrieve una clave y sus detalles por Hola después ejemplo:

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

Hola aquí te mostramos la salida de hello de Get-AzureKeyVaultKey

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

Ahora, el almacén de claves y la clave o el secreto está lista para toouse de aplicaciones.
Debe autorizar aplicaciones toouse ellos.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autorizar Hola aplicación toouse Hola clave o el secreto
tooauthorize Hola aplicación tooaccess Hola clave o el secreto en el almacén de Hola Hola use Set -**AzureRmKeyVaultAccessPolicy** cmdlet.

Por ejemplo, si el nombre del almacén es *ContosoKeyVault* y aplicación hello desea tooauthorize tiene un *Id. de cliente* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*y desea tooauthorize Hola aplicación toodecrypt e inicie sesión con las claves en el almacén, ejecute hello siguiente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>Pasos siguientes
[Implementación de una máquina virtual con una contraseña de Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Implementación de una máquina virtual con un certificado de Key Vault](azure-stack-kv-push-secret-into-vm.md)

