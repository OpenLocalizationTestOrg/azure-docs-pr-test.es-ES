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
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Tutorial: Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure
## <a name="introduction"></a>Introducción
Este tutorial trata cómo toomake el uso de cifrado de almacenamiento del lado cliente con el almacén de claves de Azure. Le explicamos cómo tooencrypt y descifrar un blob en una aplicación de consola con estas tecnologías.

**Estimado toocomplete de tiempo:** 20 minutos

Para información general sobre Azure Key Vault, consulte [¿Qué es Azure Key Vault?](../key-vault/key-vault-whatis.md).

Para obtener información general sobre el cifrado de cliente para Azure Storage, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](storage-client-side-encryption.md).

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, debe tener Hola siguientes:

* Una cuenta de almacenamiento de Azure.
* Visual Studio 2013 o posterior.
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Información general sobre el cifrado del lado cliente
Para obtener información general acerca del cifrado de cliente para Azure Storage, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](storage-client-side-encryption.md).

Esta es una breve descripción de cómo funciona el cifrado del lado cliente:

1. SDK de cliente de almacenamiento de Azure de Hola genera una clave de cifrado de contenido (CEK), que es una clave simétrica de un solo uso.
2. Los datos de usuario se cifran mediante esta CEK.
3. Hello CEK se incluye después (cifrada) con clave de cifrado de claves de Hola (de claves KEK). Hola KEK se identifica mediante un identificador de clave y puede ser un par de claves asimétricas o una clave simétrica y se puede administrar de forma local o almacenado en el almacén de claves de Azure. cliente de almacenamiento de Hello propio nunca tiene acceso toohello KEK. Solo se invoca algoritmo de encapsulado de clave de hello proporcionada por el almacén de claves. Los clientes pueden elegir toouse proveedores personalizados para la clave ajuste/desencapsulación si lo desean.
4. Hola datos cifrados están, a continuación, cargar el servicio de almacenamiento de Azure toohello.

## <a name="set-up-your-azure-key-vault"></a>Configuración de Almacén de claves de Azure
En orden tooproceed con este tutorial, necesita hello toodo siguiendo los pasos, que se describen en el tutorial de hello [empezar a trabajar con el almacén de claves de Azure](../key-vault/key-vault-get-started.md):

* Cree un almacén de claves.
* Agregar una clave o un almacén de claves de toohello secreto.
* Registre una aplicación con Azure Active Directory.
* Autorizar Hola aplicación toouse Hola clave o el secreto.

Asegúrese de nota de hello ClientID y ClientSecret que se generaron al registrar una aplicación con Azure Active Directory.

Crear las claves en el almacén de claves de Hola. Se supone para el resto de Hola de tutorial de Hola que ha usado Hola después de nombres: ContosoKeyVault y TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Creación de una aplicación de consola con paquetes y AppSettings
En Visual Studio, cree una nueva aplicación de consola.

Agregar paquetes de nuget es necesario en la consola de administrador de paquetes de saludo.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Agregar AppSettings toohello App.Config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Agregue los siguiente hello `using` instrucciones y asegúrese de que tooadd un proyecto de toohello tooSystem.Configuration de referencia.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Agregar una tooget una aplicación de consola tooyour símbolo (token) de método
Hello siguiente método se utiliza las clases de almacén de claves que necesita tooauthenticate para el almacén de claves de acceso tooyour.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Acceso a Almacenamiento y Almacén de claves en el programa
Hola función Main, agregue Hola siguiente código.

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
> Modelos de objetos de Almacén de claves
> 
> Es importante toobe consciente de los modelos de toounderstand que hay en realidad dos objetos de almacén de claves: uno se basa en hello API de REST (espacio de nombres de KeyVault) y Hola otro es una extensión para el cifrado de cliente.
> 
> Hola clave de almacén de cliente interactúa con la API de REST de Hola y entiende que JSON Web claves y secretos para dos tipos de operaciones que se encuentran en el almacén de claves de Hola.
> 
> las extensiones de almacén de clave de Hello son clases que parezcan creadas específicamente para el cifrado de cliente en el almacenamiento de Azure. Contienen una interfaz para las claves (IKey) y las clases basadas en concepto de Hola de un solucionador de clave. Hay dos implementaciones de IKey necesita tooknow: RSAKey y SymmetricKey. Ahora que se produzcan toocoincide cosas Hola que se encuentran en un almacén de claves, pero en este momento son clases independientes (por lo que no implementan IKey Hola clave y el secreto recuperado por hello clave de almacén de cliente).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Cifrado y carga de blob
Agregue código tooencrypt un blob siguiente de Hola y cargarlo tooyour cuenta de almacenamiento de Azure. Hola **ResolveKeyAsync** método que se usa devuelve un IKey.

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

A continuación se muestra una captura de pantalla de hello [Portal clásico de Azure](https://manage.windowsazure.com) para un blob que se ha cifrado mediante el uso de cifrado en el cliente con una clave almacenada en el almacén de claves. Hola **KeyId** propiedad es hello URI para la clave de hello en el almacén de claves que actúa como Hola KEK. Hola **EncryptedKey** propiedad contiene la versión cifrada de Hola de hello CEK.

![Captura de pantalla en la que se muestran los metadatos del blob que incluyen los metadatos de cifrado](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Si observa en el constructor de BlobEncryptionPolicy hello, verá que puede aceptar una clave o una resolución. Tenga en cuenta que ahora no puede utilizar una resolución para el cifrado porque en la actualidad no admite una clave predeterminada.
> 
> 

## <a name="decrypt-blob-and-download"></a>Descifrado y carga del blob
Descifrado es realmente cuando utilizando Hola resolución clases tienen sentido. Id. de Hola de clave de hello usado para el cifrado está asociado con el blob de hello en sus metadatos, así que no hay ninguna razón para la clave hello tooretrieve y recordar la asociación de hello entre la clave y el blob. Sólo tiene toomake seguro que esa clave Hola permanece en el almacén de claves.   

clave privada de Hola de un permanece clave RSA en el almacén de claves, por lo que para toooccur de descifrado, Hola clave cifrada de hello metadatos del blob que contiene Hola CEK se envía tooKey almacén para el descifrado.

Agregar Hola después de blob de hello toodecrypt que acaba de cargar.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Hay un par de otros tipos de administración de claves de resoluciones toomake más fácil, incluidos: AggregateKeyResolver y CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Uso de secretos de Almacén de claves
Hola forma toouse un secreto con cifrado en el cliente es a través de hello SymmetricKey clase porque un secreto es básicamente una clave simétrica. Sin embargo, tal y como se mencionó anteriormente, un secreto en el almacén de claves no asigna exactamente tooa SymmetricKey. Hay unos toounderstand cosas:

* clave de Hello en un SymmetricKey tiene toobe una longitud fija: 128, 192, 256, 384 y 512 bits.
* clave de Hello en un SymmetricKey debe estar codificado en Base64.
* Un secreto de almacén de claves que se usará como un SymmetricKey debe toohave un tipo de contenido de "application/octet-stream" en el almacén de claves.

Este es un ejemplo en PowerShell de creación de un secreto en Almacén de claves que se puede usar como una SymmetricKey.
Tenga en cuenta que el valor codificado de forma rígida de hello, $key, es solo con fines de demostración. En su propio código debe tener toogenerate esta clave.

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

En la aplicación de consola, puede usar Hola misma llamada, como antes tooretrieve este secreto como un SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
Eso es todo. ¡Disfrute!

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre el uso de Microsoft Azure Storage con C#, consulte [Biblioteca de cliente de Microsoft Azure Storage para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Para obtener más información acerca de la API de REST de Blob de hello, consulte [API de REST del servicio Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Para información más reciente de hello en el almacenamiento de Azure de Microsoft, visite toohello [Blog del equipo de almacenamiento de Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).
