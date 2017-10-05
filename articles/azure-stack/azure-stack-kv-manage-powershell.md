---
title: Administrar Key Vault en Azure Stack mediante PowerShell | Microsoft Docs
description: "Aprenda cómo administrar Key Vault en Azure Stack mediante PowerShell."
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
ms.openlocfilehash: 71320f8c55d014db6843e6247c53cc07832efc32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a>Administrar Key Vault en Azure Stack mediante PowerShell

En este artículo, encontrará ayuda para empezar a crear y administrar Key Vault en Azure Stack mediante PowerShell. Los cmdlets de PowerShell de Key Vault que se describen en este artículo están disponibles como parte del SDK de Azure PowerShell. En las secciones siguientes se describen los cmdlets de PowerShell necesarios para crear un almacén; almacenar y administrar claves y secretos criptográficos, y autorizar a los usuarios o aplicaciones a invocar operaciones en el almacén. 

## <a name="prerequisites"></a>Requisitos previos
* [Instalación de PowerShell para Azure Stack.](azure-stack-powershell-install.md)  
* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves.  
* Los usuarios tienen que [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que incluya el servicio Key Vault. 
* [Configuración del entorno de PowerShell del usuario de Azure Stack](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a>Habilitación de la suscripción de inquilino para operaciones de almacén

Para poder emitir cualquier operación en un almacén de claves, debe asegurarse de que su suscripción de inquilino esté habilitada para operaciones de almacén. Para comprobarlo, ejecute el siguiente comando:

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
**Salida**

Si la suscripción está habilitada para operaciones de almacén, la salida muestra el valor "Registrado" para "RegistrationState" para todos los tipos de recursos de un almacén de claves.

![estado de registro](media/azure-stack-kv-manage-powershell/image1.png)

Si no es así, invoque el comando siguiente para registrar el servicio Key Vault en su suscripción:

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

**Salida**

Si el registro se realiza correctamente, se devuelve la siguiente salida:

![registro](media/azure-stack-kv-manage-powershell/image2.png)

En las secciones siguientes se da por sentado que el servicio Key Vault está registrado en la suscripción del usuario. Al invocar comandos del almacén de claves, si aparece el error "La suscripción no está registrada para usar el espacio de nombres 'Microsoft.KeyVault'", confirme que tiene [habilitado el proveedor de recursos de Key Vault](#enable-your-tenant-subscription-for-vault-operations) según las instrucciones indicadas anteriormente.

## <a name="create-a-key-vault"></a>Creación de un Almacén de claves 

Antes de crear un almacén de claves, cree un grupo de recursos para que todos los recursos relacionados con el almacén de claves se encuentren en un grupo de recursos. Utilice el comando siguiente para crear un nuevo grupo de recursos:

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

**Salida**

![nuevo grupo de recursos](media/azure-stack-kv-manage-powershell/image3.png)

Ahora, utilice el comando **New-AzureRMKeyVault** para crear un almacén de claves en el grupo de recursos que creó anteriormente. Este comando lee tres parámetros obligatorios: el nombre del grupo de recursos, el nombre del almacén de claves y la ubicación geográfica. 

Ejecute el siguiente comando para crear un almacén de claves:

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
**Salida**

![new kv](media/azure-stack-kv-manage-powershell/image4.png)

La salida de este comando muestra las propiedades del almacén de claves que ha creado. Cuando una aplicación accede a este almacén, utiliza la propiedad **Vault URI** (URI de almacén) que se muestra en la salida. Por ejemplo, aquí el URI de almacén es **https://vault01.vault.local.azurestack.external**. Las aplicaciones que interactúan con este almacén de claves a través de la API de REST deben usar este URI.

En implementaciones basadas en ADFS, al crear un almacén de claves mediante PowerShell, puede aparecer la advertencia "Access policy is not set. No user or application has access permission to use this vault" (La directiva de acceso no está definida. Ningún usuario ni ninguna aplicación tienen permiso de acceso para utilizar este almacén). Para resolver este problema, establezca una directiva de acceso para el almacén mediante el comando [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret):

```PowerShell
# Obtain the security identifier(SID) of the active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set the key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a>Administración de claves y secretos

Después de crear un almacén, siga estos pasos para crear y administrar claves y secretos en el almacén.

### <a name="create-a-key"></a>Crear una clave

Use el comando **Add-AzureKeyVaultKey** para crear o importar una clave protegida mediante software en un almacén de claves. 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
El parámetro **Destination** (Destino) se utiliza para especificar que la clave está protegida mediante software. Cuando la clave se crea correctamente, el comando da como salida los detalles de la clave creada.

**Salida**

![Nueva clave](media/azure-stack-kv-manage-powershell/image5.png)

Ahora puede hacer referencia a la clave creada utilizando su URI. Si crea o importa una clave con el mismo nombre que una clave existente, la clave original se actualiza con los valores que se especifican en la nueva clave.  Puede acceder a la versión anterior utilizando el URI específico de la versión de la clave. Por ejemplo, 

* Use **https://vault10.vault.local.azurestack.external:443/keys/key01** para obtener siempre la versión actual.  
* Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** para obtener esta versión concreta.

### <a name="get-a-key"></a>Obtener una clave

Use el comando **Get-AzureKeyVaultKey** para leer una clave y sus detalles.

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a>Crear un secreto

Use el comando **Set-AzureKeyVaultSecret** para crear o actualizar un secreto en un almacén. Si aún no existe un secreto, se creará uno y, si ya existe, se creará una nueva versión del secreto.

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

**Salida**

![crear secreto](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a>Obtener un secreto

Use el comando **Get-AzureKeyVaultSecret** para leer un secreto en un almacén de claves. Este comando puede devolver todas las versiones de un secreto o algunas versiones concretas. 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

Después de crear claves y secretos, puede autorizar aplicaciones externas para que los usen.

## <a name="authorize-an-application-to-use-a-key-or-secret"></a>Autorización de una aplicación para que use una clave o un secreto

Para autorizar a una aplicación a acceder a una clave o un secreto del almacén de claves, use el comando **Set-AzureRmKeyVaultAccessPolicy**.
Por ejemplo, si el nombre del almacén es ContosoKeyVault y la aplicación que desea autorizar tiene el identificador de cliente 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, Ejecute el comando siguiente para autorizar la aplicación. Si lo desea, puede especificar el parámetro **PermissionsToKeys** para establecer permisos para un usuario, aplicación o grupo de seguridad:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

Si desea autorizar a esa misma aplicación a leer los secretos del almacén, ejecute el siguiente cmdlet:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a>Pasos siguientes
* [Implementación de una máquina virtual con una contraseña almacenada en un almacén de claves](azure-stack-kv-deploy-vm-with-secret.md)  
* [Implementación de una máquina virtual con un certificado almacenado en un almacén de claves](azure-stack-kv-push-secret-into-vm.md) 