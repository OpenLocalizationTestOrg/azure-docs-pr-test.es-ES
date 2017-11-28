---
title: 'Tutorial: Cifrado y descifrado de blobs en Azure Storage con Azure Key Vault | Microsoft Docs'
description: "Cómo cifrar y descifrar un blob mediante el cifrado del lado cliente de Microsoft Azure Storage con Azure Key Vault."
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
ms.openlocfilehash: a2a3a4773d33fe6b8589ad8d9d219acda4d1015e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="68932-103">Tutorial: Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="68932-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="68932-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="68932-104">Introduction</span></span>
<span data-ttu-id="68932-105">Este tutorial explica cómo hacer uso del cifrado de almacenamiento del lado cliente con Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="68932-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="68932-106">Se explica cómo cifrar y descifrar un blob en una aplicación de consola con estas tecnologías.</span><span class="sxs-lookup"><span data-stu-id="68932-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="68932-107">**Tiempo estimado para completar el tutorial:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="68932-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="68932-108">Para información general sobre Azure Key Vault, consulte [¿Qué es Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68932-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="68932-109">Para obtener información general sobre el cifrado de cliente para Azure Storage, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68932-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68932-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="68932-110">Prerequisites</span></span>
<span data-ttu-id="68932-111">Para realizar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="68932-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="68932-112">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="68932-112">An Azure Storage account</span></span>
* <span data-ttu-id="68932-113">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="68932-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="68932-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="68932-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="68932-115">Información general sobre el cifrado del lado cliente</span><span class="sxs-lookup"><span data-stu-id="68932-115">Overview of client-side encryption</span></span>
<span data-ttu-id="68932-116">Para obtener información general acerca del cifrado de cliente para Azure Storage, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68932-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="68932-117">Esta es una breve descripción de cómo funciona el cifrado del lado cliente:</span><span class="sxs-lookup"><span data-stu-id="68932-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="68932-118">El SDK de cliente de Almacenamiento de Azure genera una clave de cifrado de contenido (CEK), que es una clave simétrica de un solo uso.</span><span class="sxs-lookup"><span data-stu-id="68932-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="68932-119">Los datos de usuario se cifran mediante esta CEK.</span><span class="sxs-lookup"><span data-stu-id="68932-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="68932-120">Se encapsula la CEK (cifrada) con la clave de cifrado de clave (KEK).</span><span class="sxs-lookup"><span data-stu-id="68932-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="68932-121">La KEK se identifica mediante un identificador de clave y puede ser un par de clave asimétrico o una clave simétrica que puede administrarse de forma local o guardarse en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="68932-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="68932-122">El propio cliente de almacenamiento no tiene acceso a KEK.</span><span class="sxs-lookup"><span data-stu-id="68932-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="68932-123">Simplemente invoca el algoritmo de ajuste de clave proporcionado por Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="68932-124">Los clientes pueden elegir usar proveedores personalizados para el ajuste y desajuste de la clave si así lo desean.</span><span class="sxs-lookup"><span data-stu-id="68932-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="68932-125">A continuación, se cargan los datos cifrados en el servicio Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="68932-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="68932-126">Configuración de Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="68932-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="68932-127">Para continuar con este tutorial, debe seguir los siguientes pasos que se describe en el tutorial: [Introducción a Azure Key Vault](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="68932-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="68932-128">Cree un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-128">Create a key vault.</span></span>
* <span data-ttu-id="68932-129">Agregue una clave o un secreto al almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="68932-130">Registre una aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68932-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="68932-131">Autorice la aplicación para usar la clave o el secreto.</span><span class="sxs-lookup"><span data-stu-id="68932-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="68932-132">Anote el ClientID y ClientSecret que se generaron al registrar una aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68932-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="68932-133">Cree ambas claves en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-133">Create both keys in the key vault.</span></span> <span data-ttu-id="68932-134">A partir de aquí asumiremos para el resto del tutorial que ha usado los nombres siguientes: ContosoKeyVault y TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="68932-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="68932-135">Creación de una aplicación de consola con paquetes y AppSettings</span><span class="sxs-lookup"><span data-stu-id="68932-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="68932-136">En Visual Studio, cree una nueva aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="68932-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="68932-137">Agregue los paquetes de NuGet necesarios en la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="68932-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="68932-138">Agregar AppSettings al archivo App.Config.</span><span class="sxs-lookup"><span data-stu-id="68932-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="68932-139">Agregue las siguientes instrucciones `using` y asegúrese de agregar una referencia el proyecto System.Configuration.</span><span class="sxs-lookup"><span data-stu-id="68932-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

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

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="68932-140">Agregar un método para obtener un token para la aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="68932-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="68932-141">El siguiente método lo usan las clases de Almacén de claves que tienen que autenticarse para poder acceder a su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="68932-142">Acceso a Almacenamiento y Almacén de claves en el programa</span><span class="sxs-lookup"><span data-stu-id="68932-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="68932-143">En la función Main, agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="68932-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="68932-144">Modelos de objetos de Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="68932-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="68932-145">Es importante entender que hay en realidad dos modelos de objeto de Almacén de claves a tener en cuenta: uno se basa en la API de REST (espacio de nombres KeyVault) y el otro es una extensión para el cifrado de cliente.</span><span class="sxs-lookup"><span data-stu-id="68932-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="68932-146">El cliente de Almacén de claves interactúa con la API de REST y entiende las claves web JSON y los secretos de los dos tipos de elementos que están contenidos en Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="68932-147">Las extensiones de Almacén de claves son clases que parecen creadas específicamente para el cifrado de cliente en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="68932-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="68932-148">Contienen una interfaz para claves (IKey) y clases basadas en el concepto de un solucionador de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="68932-149">Hay dos implementaciones de IKey que necesita conocer: RSAKey y SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="68932-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="68932-150">Ahora coinciden con las cosas que están contenidas en un almacén de datos, pero en este momento son clases independientes (la clave y el secreto recuperado por el cliente de almacén de claves no implementan IKey).</span><span class="sxs-lookup"><span data-stu-id="68932-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="68932-151">Cifrado y carga de blob</span><span class="sxs-lookup"><span data-stu-id="68932-151">Encrypt blob and upload</span></span>
<span data-ttu-id="68932-152">Agregue el código siguiente para cifrar un blob y cargarlo en la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="68932-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="68932-153">El método **ResolveKeyAsync** que se usa devuelve una IKey.</span><span class="sxs-lookup"><span data-stu-id="68932-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="68932-154">La siguiente es una captura de pantalla del [Portal de Azure clásico](https://manage.windowsazure.com) para un blob que se ha cifrado mediante el cifrado del lado cliente con una clave almacenada en Key Vault.</span><span class="sxs-lookup"><span data-stu-id="68932-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="68932-155">La propiedad **KeyId** es el URI de la clave en Key Vault que actúa como la clave de cifrado de claves (KEK).</span><span class="sxs-lookup"><span data-stu-id="68932-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="68932-156">La propiedad **EncryptedKey** contiene la versión cifrada de la CEK.</span><span class="sxs-lookup"><span data-stu-id="68932-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Captura de pantalla en la que se muestran los metadatos del blob que incluyen los metadatos de cifrado](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="68932-158">Si observa el constructor BlobEncryptionPolicy, verá que puede aceptar una clave o una resolución.</span><span class="sxs-lookup"><span data-stu-id="68932-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="68932-159">Tenga en cuenta que ahora no puede utilizar una resolución para el cifrado porque en la actualidad no admite una clave predeterminada.</span><span class="sxs-lookup"><span data-stu-id="68932-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="68932-160">Descifrado y carga del blob</span><span class="sxs-lookup"><span data-stu-id="68932-160">Decrypt blob and download</span></span>
<span data-ttu-id="68932-161">Es en el descifrado realmente cuando las clases de solucionador tienen sentido.</span><span class="sxs-lookup"><span data-stu-id="68932-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="68932-162">El identificador de la clave usada para el cifrado se asocia con el blob en sus metadatos, así que no hace falta que recupere la clave ni que recuerde la asociación entre la clave y el blob.</span><span class="sxs-lookup"><span data-stu-id="68932-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="68932-163">Solo tiene que asegurarse de que la clave se mantiene en Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="68932-164">La clave privada de una clave RSA permanece en Almacén de claves, por lo que para que se produzca el descifrado, la clave cifrada de los metadatos del blob que contiene la CEC (clave de cifrado de contenido) se envía a Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="68932-165">Agregue lo siguiente para descifrar el blob que acaba de cargar.</span><span class="sxs-lookup"><span data-stu-id="68932-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="68932-166">Existen un par de otros tipos de solucionadores que facilitan la administración de claves, incluidos AggregateKeyResolver y CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="68932-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="68932-167">Uso de secretos de Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="68932-167">Use Key Vault secrets</span></span>
<span data-ttu-id="68932-168">La manera de usar un secreto con cifrado del lado cliente es mediante la clase SymmetricKey, porque un secreto es esencialmente una clave simétrica.</span><span class="sxs-lookup"><span data-stu-id="68932-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="68932-169">Sin embargo, como se mencionó anteriormente, un secreto en Almacén de claves no se asigna exactamente a una SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="68932-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="68932-170">Existen algunos aspectos que debe comprender:</span><span class="sxs-lookup"><span data-stu-id="68932-170">There are a few things to understand:</span></span>

* <span data-ttu-id="68932-171">La clave en una SymmetricKey tiene que tener una longitud fija: 128, 192, 256, 384 o 512 bits</span><span class="sxs-lookup"><span data-stu-id="68932-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="68932-172">La clave en una SymmetricKey debe estar codificada en Base64.</span><span class="sxs-lookup"><span data-stu-id="68932-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="68932-173">Un secreto de Almacén de clave que se use como una SymmetricKey tiene que tener un tipo de contenido de "application/octet-stream" en Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="68932-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="68932-174">Este es un ejemplo en PowerShell de creación de un secreto en Almacén de claves que se puede usar como una SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="68932-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="68932-175">Tenga en cuenta que el valor codificado, $key, es solo para fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="68932-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="68932-176">En su código, es recomendable generar esta clave.</span><span class="sxs-lookup"><span data-stu-id="68932-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="68932-177">En la aplicación de consola, puede usar la misma llamada que antes para recuperar este secreto como una SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="68932-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="68932-178">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="68932-178">That's it.</span></span> <span data-ttu-id="68932-179">¡Disfrute!</span><span class="sxs-lookup"><span data-stu-id="68932-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="68932-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68932-180">Next steps</span></span>
<span data-ttu-id="68932-181">Para más información sobre el uso de Microsoft Azure Storage con C#, consulte [Biblioteca de cliente de Microsoft Azure Storage para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="68932-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="68932-182">Para más información sobre la API de REST de blobs, consulte [API de REST de Blob service](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="68932-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="68932-183">Para obtener la información más reciente sobre Microsoft Azure Storage, vaya al [blog del equipo de Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="68932-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
