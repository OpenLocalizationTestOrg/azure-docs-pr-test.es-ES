---
title: "aaaManage el almacén de claves en la pila de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage el almacén de claves en la pila de Azure con PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a>Administrar Key Vault en Azure Stack mediante PowerShell

En este artículo le ayuda a obtener toocreate iniciada y administrar el almacén de claves en la pila de Azure mediante PowerShell. cmdlets de PowerShell de almacén de claves de Hello descritos en este artículo están disponibles como parte del SDK de Azure PowerShell Hola. Hello las secciones siguientes describen los cmdlets de PowerShell de Hola que son necesario toocreate un almacén, almacenar y administrar las claves criptográficas y secretos, así como para autorizar a los usuarios o aplicaciones operaciones tooinvoke en el almacén de Hola. 

## <a name="prerequisites"></a>Requisitos previos
* [Instale PowerShell para Azure Stack.](azure-stack-powershell-install.md)  
* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Hola.  
* Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola. 
* [Configurar el entorno de PowerShell del usuario de hello pila de Azure](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a>Habilitación de la suscripción de inquilino para operaciones de almacén

Para poder emitir cualquier operación en un almacén de claves, debe tooensure que su suscripción de inquilino está habilitada para las operaciones del almacén. tooverify, ejecute el siguiente comando de hello:

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
**Salida**

Si la suscripción está habilitada para las operaciones del almacén, la salida de hello muestra "RegistrationState" es igual a "Registrado" para todos los tipos de recursos de un almacén de claves.

![estado de registro](media/azure-stack-kv-manage-powershell/image1.png)

Si no es el caso de hello, invoque Hola después el servicio de almacén de claves de comando tooregister hello en su suscripción:

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

**Salida**

Si el registro de hello es correcta, hello siguiente resultado se devuelve:

![registro](media/azure-stack-kv-manage-powershell/image2.png)

Hello las secciones siguientes se supone se registraba el servicio de almacén de claves de suscripción de usuario de Hola. Al invocar comandos de almacén de claves, si se produce un error: "hello suscripción no tiene espacio de nombres registrado toouse ' Microsoft.KeyVault" a continuación, confirme que tiene [habilitado el proveedor de recursos de almacén de claves de hello](#enable-your-tenant-subscription-for-vault-operations) según las instrucciones se ha mencionado anteriormente.

## <a name="create-a-key-vault"></a>Creación de un Almacén de claves 

Antes de crear un almacén de claves, cree un grupo de recursos para que todos los recursos relacionados con el almacén de claves se encuentren en un grupo de recursos. Usar hello después comando toocreate un nuevo grupo de recursos:

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

**Salida**

![nuevo grupo de recursos](media/azure-stack-kv-manage-powershell/image3.png)

Ahora, utilice hello **AzureRMKeyVault New** comando toocreate un almacén de claves de grupo de recursos de Hola que creó anteriormente. Este comando lee tres parámetros obligatorios: el nombre del grupo de recursos, el nombre del almacén de claves y la ubicación geográfica. 

Ejecute hello después toocreate de comando en un almacén de claves:

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
**Salida**

![new kv](media/azure-stack-kv-manage-powershell/image4.png)

salida de Hello de este comando muestra las propiedades de Hola de almacén de claves de Hola que ha creado. Cuando una aplicación tiene acceso a este almacén, usa hello **almacén URI** propiedad que se muestra en la salida de hello. Por ejemplo, el almacén de hello URI aquí es **https://vault01.vault.local.azurestack.external**. Las aplicaciones que interactúan con este almacén de claves a través de la API de REST deben usar este URI.

En implementaciones basadas en ADFS, al crear un almacén de claves mediante PowerShell, puede aparecer la advertencia "Access policy is not set. Ningún usuario o una aplicación tiene toouse de permiso de acceso a este almacén". tooresolve este problema, establezca una directiva de acceso para el almacén de Hola por mediante hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) comando:

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a>Administración de claves y secretos

Después de crear un almacén, use Hola siguiendo los pasos toocreate y administración de claves y secretos en el almacén de Hola de.

### <a name="create-a-key"></a>Crear una clave

Hola de uso **Add-AzureKeyVaultKey** comando toocreate o importar una clave protegida de software en un almacén de claves. 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
Hola **destino** se usa el parámetro toospecify esa clave hello es un software protegido. Cuando se crea correctamente la clave de hello, Hola comando da como resultado detalles Hola Hola que se creó la clave.

**Salida**

![Nueva clave](media/azure-stack-kv-manage-powershell/image5.png)

Ahora puede hacer referencia a Hola se creó la clave mediante el uso de su URI. Si crea o importar una clave que tenga el mismo nombre que una clave existente, clave de hello original se actualiza con los valores de hello que se especifican en la nueva clave de Hola.  Se puede tener acceso versión anterior de hello mediante Hola específicos de la versión URI de clave de Hola. Por ejemplo, 

* Use **https://vault10.vault.local.azurestack.external:443/claves/key01** tooalways obtener la versión actual de Hola  
* Use **https://vault010.vault.local.azurestack.external:443/claves/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget esta versión específica

### <a name="get-a-key"></a>Obtener una clave

Hola de uso **Get-AzureKeyVaultKey** comandos tooread una clave y sus detalles.

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a>Crear un secreto

Hola de uso **AzureKeyVaultSecret conjunto** comando toocreate o actualizar un secreto en un almacén. Si aún no existe, y se crea una nueva versión del secreto de hello si ya existe, se crea un secreto.

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

**Salida**

![crear secreto](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a>Obtener un secreto

Hola de uso **Get AzureKeyVaultSecret** comando tooread un secreto en un almacén de claves. Este comando puede devolver todas las versiones de un secreto o algunas versiones concretas. 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

Después de crear claves y secretos, puede autorizar aplicaciones externas toouse ellos.

## <a name="authorize-an-application-toouse-a-key-or-secret"></a>Autorizar una toouse una clave o un secreto de aplicación

tooauthorize una tooaccess una clave de aplicación o al secreto en hello clave almacén, use hello **Set-AzureRmKeyVaultAccessPolicy** comando.
Por ejemplo, si el nombre del almacén es aplicación hello y ContosoKeyVault desea tooauthorize tiene un identificador de cliente de 8f8c4bbd 485b 45fd 98f7 ec6300b7b4ed. Ejecute hello tras la aplicación de comando tooauthorize Hola. Si lo desea, puede especificar hello **PermissionsToKeys** permisos tooset de parámetro para un usuario, aplicación o un grupo de seguridad:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente cmdlet:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a>Pasos siguientes
* [Implementación de una máquina virtual con una contraseña almacenada en un almacén de claves](azure-stack-kv-deploy-vm-with-secret.md)  
* [Implementación de una máquina virtual con un certificado almacenado en un almacén de claves](azure-stack-kv-push-secret-into-vm.md) 
