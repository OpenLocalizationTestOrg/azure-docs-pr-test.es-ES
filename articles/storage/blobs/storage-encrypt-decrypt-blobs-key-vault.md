---
title: 'Tutorial: Cifrado y descifrado de blobs en Azure Storage con Azure Key Vault | Microsoft Docs'
description: "¿Cómo tooencrypt y descifrar un blob usando cifrado en el cliente para el almacenamiento de Azure de Microsoft al almacén de claves de Azure."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="33548-103">Tutorial: Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="33548-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="33548-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="33548-104">Introduction</span></span>
<span data-ttu-id="33548-105">Este tutorial trata cómo toomake el uso de cifrado de almacenamiento del lado cliente con el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="33548-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="33548-106">Le explicamos cómo tooencrypt y descifrar un blob en una aplicación de consola con estas tecnologías.</span><span class="sxs-lookup"><span data-stu-id="33548-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="33548-107">**Estimado toocomplete de tiempo:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="33548-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="33548-108">Para información general sobre Azure Key Vault, consulte [¿Qué es Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33548-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="33548-109">Para obtener información general sobre el cifrado de cliente para Azure Storage, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33548-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33548-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="33548-110">Prerequisites</span></span>
<span data-ttu-id="33548-111">toocomplete este tutorial, debe tener Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="33548-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="33548-112">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="33548-112">An Azure Storage account</span></span>
* <span data-ttu-id="33548-113">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="33548-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="33548-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="33548-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="33548-115">Información general sobre el cifrado del lado cliente</span><span class="sxs-lookup"><span data-stu-id="33548-115">Overview of client-side encryption</span></span>
<span data-ttu-id="33548-116">Para obtener información general acerca del cifrado de cliente para Azure Storage, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33548-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="33548-117">Esta es una breve descripción de cómo funciona el cifrado del lado cliente:</span><span class="sxs-lookup"><span data-stu-id="33548-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="33548-118">SDK de cliente de almacenamiento de Azure de Hola genera una clave de cifrado de contenido (CEK), que es una clave simétrica de un solo uso.</span><span class="sxs-lookup"><span data-stu-id="33548-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="33548-119">Los datos de usuario se cifran mediante esta CEK.</span><span class="sxs-lookup"><span data-stu-id="33548-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="33548-120">Hello CEK se incluye después (cifrada) con clave de cifrado de claves de Hola (de claves KEK).</span><span class="sxs-lookup"><span data-stu-id="33548-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="33548-121">Hola KEK se identifica mediante un identificador de clave y puede ser un par de claves asimétricas o una clave simétrica y se puede administrar de forma local o almacenado en el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="33548-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="33548-122">cliente de almacenamiento de Hello propio nunca tiene acceso toohello KEK.</span><span class="sxs-lookup"><span data-stu-id="33548-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="33548-123">Solo se invoca algoritmo de encapsulado de clave de hello proporcionada por el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="33548-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="33548-124">Los clientes pueden elegir toouse proveedores personalizados para la clave ajuste/desencapsulación si lo desean.</span><span class="sxs-lookup"><span data-stu-id="33548-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="33548-125">Hola datos cifrados están, a continuación, cargar el servicio de almacenamiento de Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="33548-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="33548-126">Configuración de Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="33548-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="33548-127">En orden tooproceed con este tutorial, necesita hello toodo siguiendo los pasos, que se describen en el tutorial de hello [empezar a trabajar con el almacén de claves de Azure](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="33548-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="33548-128">Cree un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="33548-128">Create a key vault.</span></span>
* <span data-ttu-id="33548-129">Agregar una clave o un almacén de claves de toohello secreto.</span><span class="sxs-lookup"><span data-stu-id="33548-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="33548-130">Registre una aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33548-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="33548-131">Autorizar Hola aplicación toouse Hola clave o el secreto.</span><span class="sxs-lookup"><span data-stu-id="33548-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="33548-132">Asegúrese de nota de hello ClientID y ClientSecret que se generaron al registrar una aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33548-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="33548-133">Crear las claves en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="33548-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="33548-134">Se supone para el resto de Hola de tutorial de Hola que ha usado Hola después de nombres: ContosoKeyVault y TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="33548-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="33548-135">Creación de una aplicación de consola con paquetes y AppSettings</span><span class="sxs-lookup"><span data-stu-id="33548-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="33548-136">En Visual Studio, cree una nueva aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="33548-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="33548-137">Agregar paquetes de nuget es necesario en la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="33548-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="33548-138">Agregar AppSettings toohello App.Config.</span><span class="sxs-lookup"><span data-stu-id="33548-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="33548-139">Agregue los siguiente hello `using` instrucciones y asegúrese de que tooadd un proyecto de toohello tooSystem.Configuration de referencia.</span><span class="sxs-lookup"><span data-stu-id="33548-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="33548-140">Agregar una tooget una aplicación de consola tooyour símbolo (token) de método</span><span class="sxs-lookup"><span data-stu-id="33548-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="33548-141">Hello siguiente método se utiliza las clases de almacén de claves que necesita tooauthenticate para el almacén de claves de acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="33548-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="33548-142">Acceso a Almacenamiento y Almacén de claves en el programa</span><span class="sxs-lookup"><span data-stu-id="33548-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="33548-143">Hola función Main, agregue Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="33548-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="33548-144">Modelos de objetos de Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="33548-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="33548-145">Es importante toobe consciente de los modelos de toounderstand que hay en realidad dos objetos de almacén de claves: uno se basa en hello API de REST (espacio de nombres de KeyVault) y Hola otro es una extensión para el cifrado de cliente.</span><span class="sxs-lookup"><span data-stu-id="33548-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="33548-146">Hola clave de almacén de cliente interactúa con la API de REST de Hola y entiende que JSON Web claves y secretos para dos tipos de operaciones que se encuentran en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="33548-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="33548-147">las extensiones de almacén de clave de Hello son clases que parezcan creadas específicamente para el cifrado de cliente en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="33548-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="33548-148">Contienen una interfaz para las claves (IKey) y las clases basadas en concepto de Hola de un solucionador de clave.</span><span class="sxs-lookup"><span data-stu-id="33548-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="33548-149">Hay dos implementaciones de IKey necesita tooknow: RSAKey y SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="33548-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="33548-150">Ahora que se produzcan toocoincide cosas Hola que se encuentran en un almacén de claves, pero en este momento son clases independientes (por lo que no implementan IKey Hola clave y el secreto recuperado por hello clave de almacén de cliente).</span><span class="sxs-lookup"><span data-stu-id="33548-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="33548-151">Cifrado y carga de blob</span><span class="sxs-lookup"><span data-stu-id="33548-151">Encrypt blob and upload</span></span>
<span data-ttu-id="33548-152">Agregue código tooencrypt un blob siguiente de Hola y cargarlo tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="33548-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="33548-153">Hola **ResolveKeyAsync** método que se usa devuelve un IKey.</span><span class="sxs-lookup"><span data-stu-id="33548-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="33548-154">A continuación se muestra una captura de pantalla de hello [Portal clásico de Azure](https://manage.windowsazure.com) para un blob que se ha cifrado mediante el uso de cifrado en el cliente con una clave almacenada en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="33548-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="33548-155">Hola **KeyId** propiedad es hello URI para la clave de hello en el almacén de claves que actúa como Hola KEK.</span><span class="sxs-lookup"><span data-stu-id="33548-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="33548-156">Hola **EncryptedKey** propiedad contiene la versión cifrada de Hola de hello CEK.</span><span class="sxs-lookup"><span data-stu-id="33548-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Captura de pantalla en la que se muestran los metadatos del blob que incluyen los metadatos de cifrado](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="33548-158">Si observa en el constructor de BlobEncryptionPolicy hello, verá que puede aceptar una clave o una resolución.</span><span class="sxs-lookup"><span data-stu-id="33548-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="33548-159">Tenga en cuenta que ahora no puede utilizar una resolución para el cifrado porque en la actualidad no admite una clave predeterminada.</span><span class="sxs-lookup"><span data-stu-id="33548-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="33548-160">Descifrado y carga del blob</span><span class="sxs-lookup"><span data-stu-id="33548-160">Decrypt blob and download</span></span>
<span data-ttu-id="33548-161">Descifrado es realmente cuando utilizando Hola resolución clases tienen sentido.</span><span class="sxs-lookup"><span data-stu-id="33548-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="33548-162">Id. de Hola de clave de hello usado para el cifrado está asociado con el blob de hello en sus metadatos, así que no hay ninguna razón para la clave hello tooretrieve y recordar la asociación de hello entre la clave y el blob.</span><span class="sxs-lookup"><span data-stu-id="33548-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="33548-163">Sólo tiene toomake seguro que esa clave Hola permanece en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="33548-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="33548-164">clave privada de Hola de un permanece clave RSA en el almacén de claves, por lo que para toooccur de descifrado, Hola clave cifrada de hello metadatos del blob que contiene Hola CEK se envía tooKey almacén para el descifrado.</span><span class="sxs-lookup"><span data-stu-id="33548-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="33548-165">Agregar Hola después de blob de hello toodecrypt que acaba de cargar.</span><span class="sxs-lookup"><span data-stu-id="33548-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="33548-166">Hay un par de otros tipos de administración de claves de resoluciones toomake más fácil, incluidos: AggregateKeyResolver y CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="33548-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="33548-167">Uso de secretos de Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="33548-167">Use Key Vault secrets</span></span>
<span data-ttu-id="33548-168">Hola forma toouse un secreto con cifrado en el cliente es a través de hello SymmetricKey clase porque un secreto es básicamente una clave simétrica.</span><span class="sxs-lookup"><span data-stu-id="33548-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="33548-169">Sin embargo, tal y como se mencionó anteriormente, un secreto en el almacén de claves no asigna exactamente tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="33548-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="33548-170">Hay unos toounderstand cosas:</span><span class="sxs-lookup"><span data-stu-id="33548-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="33548-171">clave de Hello en un SymmetricKey tiene toobe una longitud fija: 128, 192, 256, 384 y 512 bits.</span><span class="sxs-lookup"><span data-stu-id="33548-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="33548-172">clave de Hello en un SymmetricKey debe estar codificado en Base64.</span><span class="sxs-lookup"><span data-stu-id="33548-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="33548-173">Un secreto de almacén de claves que se usará como un SymmetricKey debe toohave un tipo de contenido de "application/octet-stream" en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="33548-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="33548-174">Este es un ejemplo en PowerShell de creación de un secreto en Almacén de claves que se puede usar como una SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="33548-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="33548-175">Tenga en cuenta que el valor codificado de forma rígida de hello, $key, es solo con fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="33548-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="33548-176">En su propio código debe tener toogenerate esta clave.</span><span class="sxs-lookup"><span data-stu-id="33548-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="33548-177">En la aplicación de consola, puede usar Hola misma llamada, como antes tooretrieve este secreto como un SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="33548-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="33548-178">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="33548-178">That's it.</span></span> <span data-ttu-id="33548-179">¡Disfrute!</span><span class="sxs-lookup"><span data-stu-id="33548-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="33548-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33548-180">Next steps</span></span>
<span data-ttu-id="33548-181">Para más información sobre el uso de Microsoft Azure Storage con C#, consulte [Biblioteca de cliente de Microsoft Azure Storage para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="33548-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="33548-182">Para obtener más información acerca de la API de REST de Blob de hello, consulte [API de REST del servicio Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="33548-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="33548-183">Para información más reciente de hello en el almacenamiento de Azure de Microsoft, visite toohello [Blog del equipo de almacenamiento de Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="33548-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
