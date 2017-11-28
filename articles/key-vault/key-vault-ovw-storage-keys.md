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
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="97e11-103">Claves de cuenta de almacenamiento de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="97e11-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="97e11-104">Antes de claves de cuenta de almacenamiento de almacén de la clave de Azure, los programadores tenían toomanage sus propias claves de cuenta de almacenamiento de Azure (ASA) e intercambiarlos manualmente o a través de una automatización externa.</span><span class="sxs-lookup"><span data-stu-id="97e11-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="97e11-105">Ahora las claves de cuenta de almacenamiento de Key Vault se implementan como [secretos de Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) para autenticar con una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="97e11-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="97e11-106">característica clave de Hello ASA administra giro secreto y elimina la necesidad de hello para el contacto directo con una clave ASA, ya que ofrece las firmas de acceso compartido (SAS) como un método.</span><span class="sxs-lookup"><span data-stu-id="97e11-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="97e11-107">Para más información general sobre las cuentas de Azure Storage, vea [Acerca de las cuentas de Azure Storage](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="97e11-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="97e11-108">Interfaces admitidas</span><span class="sxs-lookup"><span data-stu-id="97e11-108">Supporting interfaces</span></span>

<span data-ttu-id="97e11-109">Hello característica de claves de cuenta de almacenamiento de Azure inicialmente, está disponible a través de hello REST, .NET / interfaces de C# y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97e11-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="97e11-110">Para obtener más información, vea [Documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="97e11-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="97e11-111">Comportamiento de las claves de cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="97e11-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="97e11-112">¿Qué administra Key Vault?</span><span class="sxs-lookup"><span data-stu-id="97e11-112">What Key Vault manages</span></span>

<span data-ttu-id="97e11-113">Cuando usa las claves de la cuenta de almacenamiento, Key Vault realiza varias funciones de administración interna en su nombre.</span><span class="sxs-lookup"><span data-stu-id="97e11-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="97e11-114">Azure Key Vault administra las claves de una cuenta de Azure Storage (ASA).</span><span class="sxs-lookup"><span data-stu-id="97e11-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="97e11-115">Internamente, Azure Key Vault puede enumerar (sincronizar) las claves con una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="97e11-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="97e11-116">Almacén de claves de Azure vuelve a generar (rota) hello las claves periódicamente.</span><span class="sxs-lookup"><span data-stu-id="97e11-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="97e11-117">Valores de clave nunca se devuelven en respuesta toocaller.</span><span class="sxs-lookup"><span data-stu-id="97e11-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="97e11-118">Azure Key Vault administra las claves de las cuentas de almacenamiento y de las cuentas de almacenamiento clásicas.</span><span class="sxs-lookup"><span data-stu-id="97e11-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="97e11-119">Almacén de claves de Azure permite, propietario del almacén/objeto hello, definiciones de toocreate SAS (cuenta o servicio SAS).</span><span class="sxs-lookup"><span data-stu-id="97e11-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="97e11-120">Hola valor SAS, creado con la definición de SAS, se devuelve como un secreto a través de la ruta de acceso de URI de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e11-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="97e11-121">Para más información, vea [Azure Key Vault storage account operations (Operaciones de cuenta de almacenamiento de Azure Key Vault)](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="97e11-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="97e11-122">Instrucciones de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="97e11-122">Naming guidance</span></span>

<span data-ttu-id="97e11-123">Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="97e11-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="97e11-124">Los nombres de las definiciones de SAS deben tener una longitud de entre 1 y 102 caracteres y contener solo los caracteres 0-9, a-z, A-z.</span><span class="sxs-lookup"><span data-stu-id="97e11-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="97e11-125">Experiencia para el desarrollador</span><span class="sxs-lookup"><span data-stu-id="97e11-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="97e11-126">Antes de la existencia de las claves de cuenta de almacenamiento de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="97e11-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="97e11-127">Los desarrolladores usan tooneed toodo Hola siguiendo procedimientos con un almacenamiento de tooAzure de acceso de almacenamiento cuenta tooget clave.</span><span class="sxs-lookup"><span data-stu-id="97e11-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="97e11-128">A partir de la existencia de las claves de cuenta de almacenamiento de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="97e11-128">After Azure Key Vault Storage Keys</span></span> 

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
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="97e11-129">Procedimientos recomendados para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="97e11-129">Developer best practices</span></span> 

- <span data-ttu-id="97e11-130">Permitir solo el almacén de claves toomanage las claves ASA.</span><span class="sxs-lookup"><span data-stu-id="97e11-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="97e11-131">No intente toomanage a usted mismo, interferirá con los procesos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97e11-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="97e11-132">No se permiten ASA claves toobe administrado por más de un objeto de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97e11-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="97e11-133">Si necesita toomanually regenerar las claves ASA, se recomienda regenerar ellos a través del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97e11-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="97e11-134">Introducción</span><span class="sxs-lookup"><span data-stu-id="97e11-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="97e11-135">Configuración de permisos de control de acceso basado en roles (RBAC)</span><span class="sxs-lookup"><span data-stu-id="97e11-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="97e11-136">El almacén de claves necesita permisos demasiado*lista* y *regenerar* claves para una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97e11-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="97e11-137">Configurar estos permisos con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="97e11-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="97e11-138">Obtenga ObjectId de Key Vault:</span><span class="sxs-lookup"><span data-stu-id="97e11-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="97e11-139">Asignar el rol de operador de la clave de almacenamiento tooAzure clave de almacén de identidades:</span><span class="sxs-lookup"><span data-stu-id="97e11-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="97e11-140">Para un tipo de cuenta clásico, establecer el parámetro de función de hello demasiado*"Clásico almacenamiento cuenta clave de servicio de función operador"*.</span><span class="sxs-lookup"><span data-stu-id="97e11-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="97e11-141">Incorporación de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="97e11-141">Storage account onboarding</span></span> 

<span data-ttu-id="97e11-142">Ejemplo: Como propietario de un objeto de almacén de claves agregar almacenamiento cuenta objeto tooyour el almacén de claves de Azure tooonboard una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97e11-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="97e11-143">Durante la incorporación, el almacén de claves debe tooverify que identidad Hola de cuenta de incorporación de hello tiene permisos demasiado*lista* y demasiado*regenerar* claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97e11-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="97e11-144">En orden tooverify estos permisos, el almacén de claves Obtiene un OBO (en nombre de) (token) de servicio de autenticación de hello, audiencia establece tooAzure el Administrador de recursos y realiza una *lista* la clave de servicio de almacenamiento de Azure toohello de llamada.</span><span class="sxs-lookup"><span data-stu-id="97e11-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="97e11-145">Si hello *lista* se produce un error de la llamada, Hola el almacén de claves se produce un error en la creación de objetos con un código de estado HTTP *prohibido*.</span><span class="sxs-lookup"><span data-stu-id="97e11-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="97e11-146">claves de Hello enumeradas en este modo se almacenan en caché con el almacenamiento de la entidad de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97e11-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="97e11-147">El almacén de claves debe comprobar que tiene identidad hello *regenerar* permisos antes de que puede tomar posesión de volver a generar las claves.</span><span class="sxs-lookup"><span data-stu-id="97e11-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="97e11-148">tooverify que Hola identidad, a través de token OBO, así como Hola identidad de almacén de claves primera parte consta de estos permisos:</span><span class="sxs-lookup"><span data-stu-id="97e11-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="97e11-149">El almacén de claves se enumeran los permisos de RBAC en recursos de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e11-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="97e11-150">El almacén de claves valida la respuesta de Hola a través de coincidencia de expresión regular de las acciones y acciones no.</span><span class="sxs-lookup"><span data-stu-id="97e11-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="97e11-151">En [Key Vault - Managed Storage Account Keys Samples ](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault: ejemplos de administración de claves de cuentas de Azure Storage) encontrará algunos ejemplos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="97e11-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="97e11-152">Si no dispone de identidad de hello *regenerar* permisos o si no tiene la primera identidad de usuario del almacén de claves *lista* o *regenerar* permiso y, a continuación, incorporación de Hola devolver un código de error y mensajes de error de solicitud.</span><span class="sxs-lookup"><span data-stu-id="97e11-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="97e11-153">símbolo (token) de Hello OBO sólo funcionará cuando se utilizan cookies, las aplicaciones cliente nativas de PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="97e11-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="97e11-154">Otras aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97e11-154">Other applications</span></span>

- <span data-ttu-id="97e11-155">Los tokens SAS, construidos utilizando claves de cuenta de almacenamiento de almacén de claves, proporcionan incluso más acceso controlado tooan cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="97e11-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="97e11-156">Consulte [Uso de firmas de acceso compartido](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) para más información.</span><span class="sxs-lookup"><span data-stu-id="97e11-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="97e11-157">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="97e11-157">See also</span></span>

- [<span data-ttu-id="97e11-158">Información acerca de claves, secretos y certificados</span><span class="sxs-lookup"><span data-stu-id="97e11-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="97e11-159">Blog del equipo de Key Vault</span><span class="sxs-lookup"><span data-stu-id="97e11-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
