---
ms.assetid: 
title: "aaaAzure claves de cuenta de almacenamiento de almacén de claves"
description: "Claves de la cuenta de almacenamiento proporcionan una integración sin problemas entre el almacén de claves de Azure y la clave acceso basado en tooAzure cuenta de almacenamiento."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Claves de cuenta de almacenamiento de Azure Key Vault

Antes de claves de cuenta de almacenamiento de almacén de la clave de Azure, los programadores tenían toomanage sus propias claves de cuenta de almacenamiento de Azure (ASA) e intercambiarlos manualmente o a través de una automatización externa. Ahora las claves de cuenta de almacenamiento de Key Vault se implementan como [secretos de Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) para autenticar con una cuenta de Azure Storage. 

característica clave de Hello ASA administra giro secreto y elimina la necesidad de hello para el contacto directo con una clave ASA, ya que ofrece las firmas de acceso compartido (SAS) como un método. 

Para más información general sobre las cuentas de Azure Storage, vea [Acerca de las cuentas de Azure Storage](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Interfaces admitidas

Hello característica de claves de cuenta de almacenamiento de Azure inicialmente, está disponible a través de hello REST, .NET / interfaces de C# y PowerShell. Para obtener más información, vea [Documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Comportamiento de las claves de cuenta de almacenamiento

### <a name="what-key-vault-manages"></a>¿Qué administra Key Vault?

Cuando usa las claves de la cuenta de almacenamiento, Key Vault realiza varias funciones de administración interna en su nombre.

1. Azure Key Vault administra las claves de una cuenta de Azure Storage (ASA). 
    - Internamente, Azure Key Vault puede enumerar (sincronizar) las claves con una cuenta de Azure Storage.  
    - Almacén de claves de Azure vuelve a generar (rota) hello las claves periódicamente. 
    - Valores de clave nunca se devuelven en respuesta toocaller. 
    - Azure Key Vault administra las claves de las cuentas de almacenamiento y de las cuentas de almacenamiento clásicas. 
2. Almacén de claves de Azure permite, propietario del almacén/objeto hello, definiciones de toocreate SAS (cuenta o servicio SAS). 
    - Hola valor SAS, creado con la definición de SAS, se devuelve como un secreto a través de la ruta de acceso de URI de REST de Hola. Para más información, vea [Azure Key Vault storage account operations (Operaciones de cuenta de almacenamiento de Azure Key Vault)](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Instrucciones de nomenclatura

Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.  
 
Los nombres de las definiciones de SAS deben tener una longitud de entre 1 y 102 caracteres y contener solo los caracteres 0-9, a-z, A-z.

## <a name="developer-experience"></a>Experiencia para el desarrollador 

### <a name="before-azure-key-vault-storage-keys"></a>Antes de la existencia de las claves de cuenta de almacenamiento de Azure Key Vault 

Los desarrolladores usan tooneed toodo Hola siguiendo procedimientos con un almacenamiento de tooAzure de acceso de almacenamiento cuenta tooget clave. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>A partir de la existencia de las claves de cuenta de almacenamiento de Azure Key Vault 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>Procedimientos recomendados para desarrolladores 

- Permitir solo el almacén de claves toomanage las claves ASA. No intente toomanage a usted mismo, interferirá con los procesos del almacén de claves. 
- No se permiten ASA claves toobe administrado por más de un objeto de almacén de claves. 
- Si necesita toomanually regenerar las claves ASA, se recomienda regenerar ellos a través del almacén de claves. 

## <a name="getting-started"></a>Introducción

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Configuración de permisos de control de acceso basado en roles (RBAC)

El almacén de claves necesita permisos demasiado*lista* y *regenerar* claves para una cuenta de almacenamiento. Configurar estos permisos con hello pasos:

- Obtenga ObjectId de Key Vault: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Asignar el rol de operador de la clave de almacenamiento tooAzure clave de almacén de identidades: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Para un tipo de cuenta clásico, establecer el parámetro de función de hello demasiado*"Clásico almacenamiento cuenta clave de servicio de función operador"*.

### <a name="storage-account-onboarding"></a>Incorporación de cuentas de almacenamiento 

Ejemplo: Como propietario de un objeto de almacén de claves agregar almacenamiento cuenta objeto tooyour el almacén de claves de Azure tooonboard una cuenta de almacenamiento.

Durante la incorporación, el almacén de claves debe tooverify que identidad Hola de cuenta de incorporación de hello tiene permisos demasiado*lista* y demasiado*regenerar* claves de almacenamiento. En orden tooverify estos permisos, el almacén de claves Obtiene un OBO (en nombre de) (token) de servicio de autenticación de hello, audiencia establece tooAzure el Administrador de recursos y realiza una *lista* la clave de servicio de almacenamiento de Azure toohello de llamada. Si hello *lista* se produce un error de la llamada, Hola el almacén de claves se produce un error en la creación de objetos con un código de estado HTTP *prohibido*. claves de Hello enumeradas en este modo se almacenan en caché con el almacenamiento de la entidad de almacén de claves. 

El almacén de claves debe comprobar que tiene identidad hello *regenerar* permisos antes de que puede tomar posesión de volver a generar las claves. tooverify que Hola identidad, a través de token OBO, así como Hola identidad de almacén de claves primera parte consta de estos permisos:

- El almacén de claves se enumeran los permisos de RBAC en recursos de cuenta de almacenamiento de Hola.
- El almacén de claves valida la respuesta de Hola a través de coincidencia de expresión regular de las acciones y acciones no. 

En [Key Vault - Managed Storage Account Keys Samples ](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault: ejemplos de administración de claves de cuentas de Azure Storage) encontrará algunos ejemplos auxiliares.

Si no dispone de identidad de hello *regenerar* permisos o si no tiene la primera identidad de usuario del almacén de claves *lista* o *regenerar* permiso y, a continuación, incorporación de Hola devolver un código de error y mensajes de error de solicitud. 

símbolo (token) de Hello OBO sólo funcionará cuando se utilizan cookies, las aplicaciones cliente nativas de PowerShell o CLI.

## <a name="other-applications"></a>Otras aplicaciones

- Los tokens SAS, construidos utilizando claves de cuenta de almacenamiento de almacén de claves, proporcionan incluso más acceso controlado tooan cuenta de almacenamiento de Azure. Consulte [Uso de firmas de acceso compartido](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) para más información.

## <a name="see-also"></a>Otras referencias

- [Información acerca de claves, secretos y certificados](https://docs.microsoft.com/rest/api/keyvault/)
- [Blog del equipo de Key Vault](https://blogs.technet.microsoft.com/kv/)
