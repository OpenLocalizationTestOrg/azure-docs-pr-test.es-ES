---
ms.assetid: 
title: Claves de cuenta de almacenamiento de Azure Key Vault
description: "Las claves de cuenta de almacenamiento proporcionan una integración sin problemas entre Azure Key Vault y el acceso basado en claves a la cuenta de Azure Storage."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="f64e5-103">Claves de cuenta de almacenamiento de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f64e5-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="f64e5-104">Antes de que existieran las claves de cuenta de almacenamiento de Azure Key Vault, los desarrolladores tenían que administrar sus propias claves de cuenta de Azure Storage (ASA) y rotarlas manualmente o mediante la automatización externa.</span><span class="sxs-lookup"><span data-stu-id="f64e5-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="f64e5-105">Ahora las claves de cuenta de almacenamiento de Key Vault se implementan como [secretos de Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) para autenticar con una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f64e5-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="f64e5-106">La característica de clave de ASA administra la rotación de secretos automáticamente y elimina la necesidad de tener contacto directo con una clave de ASA, ya que ofrece como método las firmas de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="f64e5-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="f64e5-107">Para más información general sobre las cuentas de Azure Storage, vea [Acerca de las cuentas de Azure Storage](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f64e5-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="f64e5-108">Interfaces admitidas</span><span class="sxs-lookup"><span data-stu-id="f64e5-108">Supporting interfaces</span></span>

<span data-ttu-id="f64e5-109">La característica de claves de la cuenta de Azure Storage está disponible inicialmente a través de las interfaces de REST, .NET/C# y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f64e5-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="f64e5-110">Para obtener más información, vea [Documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="f64e5-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="f64e5-111">Comportamiento de las claves de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f64e5-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="f64e5-112">¿Qué administra Key Vault?</span><span class="sxs-lookup"><span data-stu-id="f64e5-112">What Key Vault manages</span></span>

<span data-ttu-id="f64e5-113">Cuando usa las claves de la cuenta de almacenamiento, Key Vault realiza varias funciones de administración interna en su nombre.</span><span class="sxs-lookup"><span data-stu-id="f64e5-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="f64e5-114">Azure Key Vault administra las claves de una cuenta de Azure Storage (ASA).</span><span class="sxs-lookup"><span data-stu-id="f64e5-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="f64e5-115">Internamente, Azure Key Vault puede enumerar (sincronizar) las claves con una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f64e5-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="f64e5-116">Azure Key Vault vuelve a generar (rotar) las claves periódicamente.</span><span class="sxs-lookup"><span data-stu-id="f64e5-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="f64e5-117">Los valores de clave nunca se devuelven como respuesta al autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="f64e5-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="f64e5-118">Azure Key Vault administra las claves de las cuentas de almacenamiento y de las cuentas de almacenamiento clásicas.</span><span class="sxs-lookup"><span data-stu-id="f64e5-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="f64e5-119">Azure Key Vault le permite a usted, como propietario del almacén/objeto, crear definiciones de SAS (SAS de cuenta o de servicio).</span><span class="sxs-lookup"><span data-stu-id="f64e5-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="f64e5-120">El valor de SAS, creado mediante la definición de SAS, se devuelve como un secreto a través de la ruta de acceso de URI de REST.</span><span class="sxs-lookup"><span data-stu-id="f64e5-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="f64e5-121">Para más información, vea [Azure Key Vault storage account operations (Operaciones de cuenta de almacenamiento de Azure Key Vault)](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="f64e5-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="f64e5-122">Instrucciones de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="f64e5-122">Naming guidance</span></span>

<span data-ttu-id="f64e5-123">Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f64e5-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="f64e5-124">Los nombres de las definiciones de SAS deben tener una longitud de entre 1 y 102 caracteres y contener solo los caracteres 0-9, a-z, A-z.</span><span class="sxs-lookup"><span data-stu-id="f64e5-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="f64e5-125">Experiencia para el desarrollador</span><span class="sxs-lookup"><span data-stu-id="f64e5-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="f64e5-126">Antes de la existencia de las claves de cuenta de almacenamiento de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f64e5-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="f64e5-127">Anteriormente, para obtener acceso a Azure Storage, los desarrolladores debían realizar los procedimientos siguientes con una clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f64e5-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="f64e5-128">A partir de la existencia de las claves de cuenta de almacenamiento de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f64e5-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="f64e5-129">Procedimientos recomendados para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="f64e5-129">Developer best practices</span></span> 

- <span data-ttu-id="f64e5-130">Permita que solo Key Vault administre las claves de ASA.</span><span class="sxs-lookup"><span data-stu-id="f64e5-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="f64e5-131">No intente administrarlas usted mismo, ya que interferiría con los procesos de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f64e5-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="f64e5-132">No permita que más de un objeto de Key Vault administre las claves de ASA.</span><span class="sxs-lookup"><span data-stu-id="f64e5-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="f64e5-133">Si tiene que volver a generar manualmente las claves de ASA, se recomienda hacerlo a través de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f64e5-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="f64e5-134">Introducción</span><span class="sxs-lookup"><span data-stu-id="f64e5-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="f64e5-135">Configuración de permisos de control de acceso basado en roles (RBAC)</span><span class="sxs-lookup"><span data-stu-id="f64e5-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="f64e5-136">Key Vault necesita permisos para *mostrar* y *volver a generar* las claves de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f64e5-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="f64e5-137">Configure estos permisos mediante los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f64e5-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="f64e5-138">Obtenga ObjectId de Key Vault:</span><span class="sxs-lookup"><span data-stu-id="f64e5-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="f64e5-139">Asigne el rol Operador de claves de almacenamiento a la identidad de Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="f64e5-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="f64e5-140">Para un tipo de cuenta clásica, establezca el parámetro del rol en *"Rol de servicio de operador de claves de cuentas de almacenamiento clásicas"*.</span><span class="sxs-lookup"><span data-stu-id="f64e5-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="f64e5-141">Incorporación de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f64e5-141">Storage account onboarding</span></span> 

<span data-ttu-id="f64e5-142">Ejemplo: como propietario de un objeto de Key Vault, agregue un objeto de cuenta de almacenamiento a Azure Key Vault para incorporar una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f64e5-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="f64e5-143">Durante la incorporación, Key Vault debe comprobar que la identidad de la cuenta que se está incorporando tiene permisos para *mostrar* y *volver a generar* las claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f64e5-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="f64e5-144">Para comprobar estos permisos, Key Vault obtiene un token OBO (del inglés On Behalf Of [en nombre de]) desde el servicio de autenticación, estable la audiencia en Azure Resource Manager y realiza una llamada de clave de *lista* al servicio Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f64e5-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="f64e5-145">Si hay un error en la llamada de *lista*, se produce un error en la creación del objeto de Key Vault con un código de estado HTTP de *Prohibido*.</span><span class="sxs-lookup"><span data-stu-id="f64e5-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="f64e5-146">Las claves que se muestran de esta manera se almacenan en caché con el almacenamiento de la entidad de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f64e5-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="f64e5-147">Key Vault debe comprobar que la identidad tiene permisos para *volver a generar* antes de encargarse de volver a generar las claves.</span><span class="sxs-lookup"><span data-stu-id="f64e5-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="f64e5-148">Para comprobar que la identidad (a través del token OBO) y la identidad propia de Key Vault tienen estos permisos:</span><span class="sxs-lookup"><span data-stu-id="f64e5-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="f64e5-149">Key Vault enumera los permisos RBAC en el recurso de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f64e5-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="f64e5-150">Key Vault valida la respuesta a través de la coincidencia de expresión regular de acciones y no acciones.</span><span class="sxs-lookup"><span data-stu-id="f64e5-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="f64e5-151">En [Key Vault - Managed Storage Account Keys Samples ](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault: ejemplos de administración de claves de cuentas de Azure Storage) encontrará algunos ejemplos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="f64e5-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="f64e5-152">Si la identidad no dispone de permisos para *volver a generar* o si la identidad propia de Key Vault no tiene permiso para *mostrar* o *volver a generar*, se produce un error en la solicitud de incorporación, que devuelve el código de error y el mensaje correspondientes.</span><span class="sxs-lookup"><span data-stu-id="f64e5-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="f64e5-153">El token OBO solo funcionará cuando se usen aplicaciones cliente nativas propias de PowerShell o la CLI.</span><span class="sxs-lookup"><span data-stu-id="f64e5-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="f64e5-154">Otras aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f64e5-154">Other applications</span></span>

- <span data-ttu-id="f64e5-155">Los tokens de SAS, construidos mediante claves de cuenta de almacenamiento de Key Vault, proporcionan acceso todavía más controlado a una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f64e5-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="f64e5-156">Para obtener más información, vea [Uso de firmas de acceso compartido](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="f64e5-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="f64e5-157">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f64e5-157">See also</span></span>

- [<span data-ttu-id="f64e5-158">Información acerca de claves, secretos y certificados</span><span class="sxs-lookup"><span data-stu-id="f64e5-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="f64e5-159">Blog del equipo de Key Vault</span><span class="sxs-lookup"><span data-stu-id="f64e5-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
