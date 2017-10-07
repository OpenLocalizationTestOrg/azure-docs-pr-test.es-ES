---
title: aaaCreate y usar una firma de acceso compartido (SAS) con el almacenamiento de blobs de Azure | Documentos de Microsoft
description: "Este tutorial muestra cómo toocreate comparten las firmas de acceso para su uso con el almacenamiento de blobs y cómo tooconsume ellas en las aplicaciones cliente."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Firmas de acceso compartido, Parte 2: Creación y uso de una SAS con Almacenamiento de blobs

[Parte 1](storage-dotnet-shared-access-signature-part-1.md) de este tutorial se analizaron las firmas de acceso compartido (SAS) y se explicaron los procedimientos recomendados para su uso. Parte 2 muestra cómo acceso comparten toogenerate y después usar las firmas con un almacenamiento de blobs. ejemplos de Hello están escritos en C# y usar hello biblioteca de cliente de almacenamiento de Azure para. NET. ejemplos de Hello en este tutorial:

* Se generará una firma de acceso compartido en un contenedor.
* Se generará una firma de acceso compartido en un blob.
* Crear un acceso almacenada firmas de toomanage de directiva en los recursos de un contenedor
* Comprobar las firmas de acceso compartido de hello en una aplicación cliente

## <a name="about-this-tutorial"></a>Acerca de este tutorial
En este tutorial, crearemos dos aplicaciones de consola para demostrar la creación y el uso de firmas de acceso compartido para contenedores y blobs:

**Aplicación 1**: Hola aplicación de administración. Genera una firma de acceso compartido para un contenedor y un blob. Incluye la clave de acceso de cuenta de almacenamiento de hello en el código fuente.

**Aplicación 2**: Hola aplicación cliente. Recursos de contenedor y blob de accesos con firmas de acceso de hello compartido creadas con la primera aplicación de Hola. Usa solo Hola acceso compartido firmas tooaccess contenedor y los recursos de blob--hace *no* incluyen la clave de acceso de cuenta de almacenamiento de Hola.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Parte 1: Crear un acceso de toogenerate compartida de aplicación de consola firmas
En primer lugar, asegúrese de que tiene Hola biblioteca de cliente de almacenamiento de Azure para .NET instalado. Puede instalar hello [paquete NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "paquete NuGet") que contienen los ensamblados más actualizados de hello para la biblioteca de cliente de Hola. Se trata de hello recomendada método para garantizar que haya correcciones más recientes de Hola. También puede descargar la biblioteca de cliente de hello como parte de la versión más reciente del programa Hola Hola [Azure SDK para .NET](https://azure.microsoft.com/downloads/).

En Visual Studio, cree una aplicación de consola de Windows y denomínela **GenerateSharedAccessSignatures**. Agregar referencias demasiado[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) y [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) mediante uno de los siguientes enfoques de hello:

* Hola de uso [Administrador de paquetes de NuGet](https://docs.nuget.org/consume/installing-nuget) en Visual Studio. Seleccione **Proyecto** > **Administrar paquetes NuGet**, busque en línea cada paquete (Microsoft.WindowsAzure.ConfigurationManager y WindowsAzure.Storage) e instálelo.
* Como alternativa, buscar estos ensamblados en la instalación del programa Hola a Azure SDK y agregar referencias toothem:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

En hello parte superior del archivo Program.cs de hello, agregue el siguiente de hello **con** directivas:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Edite el archivo app.config de hello para que contenga un valor de configuración con una cadena de conexión que señala tooyour cuenta de almacenamiento. El archivo app.config debe ser similar toothis uno:

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Generación de un URI de firma de acceso compartido para un contenedor
toobegin con, agregamos un toogenerate método una firma de acceso compartido en un nuevo contenedor. En este caso, firma de hello no está asociado a una directiva de acceso almacenada, por lo que lleva a cabo en hello información Hola del identificador URI que indica los permisos de hello y tiempo de expiración concede.

En primer lugar, agregue código toohello **Main()** método tooauthenticate tener acceso a la cuenta de almacenamiento de tooyour y crear un nuevo contenedor:

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

A continuación, agregue un método que genera la firma de acceso compartido de hello para el contenedor de Hola y devuelve el URI de firma de hello:

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Agregar Hola después líneas final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, toocall **GetContainerSasUri()** y escribir Hola ventana de consola de toohello URI de firma:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Compile y ejecute la firma de acceso compartido hello toooutput URI para el nuevo contenedor de Hola. Hola URI será similar siguiente toohello:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Una vez que se ha ejecutado el código de hello, firma de acceso compartido de Hola que creó para el contenedor de hello será válida para hello próximas 24 horas. firma de Hello concede a un cliente de blobs de toolist de permiso en un contenedor hello y toowrite nuevo contenedor de toohello de blobs.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Generación de un URI de firma de acceso compartido para un blob
A continuación, escribir toocreate de código similar en un nuevo blob en contenedor de Hola y generar una firma de acceso compartido para el mismo. Esta firma de acceso compartido no es asociada con una directiva de acceso almacenada, por lo que incluye información sobre los permisos, la hora de expiración y hora de inicio de Hola Hola URI.

Agregue un nuevo método que crea un nuevo blob y escribe algunos tooit de texto, a continuación, genera una firma de acceso compartido y devuelve el URI de firma de hello:

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Final Hola de hello **Main()** método, agregar Hola después líneas toocall **GetBlobSasUri()**, antes de hello llamar a demasiado**Console.ReadLine ()**y escribir Hola compartido ventana de consola de toohello URI de la firma de acceso:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Compile y ejecute la firma de acceso compartido hello toooutput URI para el nuevo blob en Hola. Hola URI será similar siguiente toohello:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Crear una directiva de acceso almacenada en el contenedor de Hola
Ahora vamos a crear una directiva de acceso almacenada en el contenedor de hello, que define las restricciones de Hola para las firmas de acceso compartido que están asociadas a ella.

En los ejemplos anteriores de hello, se especifica la hora de inicio de Hola (implícita o explícitamente), la hora de expiración de Hola y los permisos de hello en hello comparten URI propio de la firma de acceso. En hello en los ejemplos siguientes, se especifican en directiva de acceso de hello almacenado, no en la firma de acceso compartido de Hola. Esto nos permite toochange comparten estas restricciones sin volver a emitir Hola acceso firma.

Es posible toohave uno o más de las restricciones de hello en la firma de acceso compartido de Hola y el resto de hello en directiva de acceso de hello almacenado. Sin embargo, solo puede especificar la hora de inicio de hello, la hora de expiración y los permisos en un lugar o hello otro. Por ejemplo, no puede especificar los permisos en la firma de acceso compartido de Hola y especificarlas en la directiva de acceso de hello almacenado.

Cuando se agrega un contenedor de tooa de directivas de acceso almacenada, debe obtener los permisos existentes del contenedor de hello, agregar nueva directiva de acceso de hello y, a continuación, establecer permisos del contenedor de Hola.

Agregue un nuevo método que crea una nueva directiva de acceso almacenada en un contenedor y devuelve el nombre de Hola de directiva de hello:

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

Final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, agregue Hola después líneas toofirst desactive las directivas de acceso existente y, a continuación, llamar a hello  **CreateSharedAccessPolicy()** método:

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

Al desactivar las directivas de acceso de hello en un contenedor, primero debe obtener del contenedor de hello permisos existentes, a continuación, permisos de borrar Hola después establecer permisos de Hola de nuevo.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Generar un URI para el contenedor de Hola que usa una directiva de acceso de la firma de acceso compartido
A continuación, se crea otra firma de acceso compartido para el contenedor de Hola que hemos creado con anterioridad, pero esta vez asociamos de firma de hello con directiva de acceso de hello almacenado que hemos creado en el ejemplo anterior de Hola.

Agregue un nuevo toogenerate método otra firma de acceso compartido para el contenedor de hello:

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, agregar Hola después Hola de toocall líneas **GetContainerSasUriWithPolicy** (método) :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Generar un URI de firma de acceso compartido en hello Blob que utiliza una directiva de acceso
Por último, se agregue un toocreate método similar otro blob y generar una firma de acceso compartido que esté asociada con una directiva de acceso almacenada.

Agregue un nuevo toocreate de método un blob y generar una firma de acceso compartido:

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, agregar Hola después hello toocall de líneas **GetBlobSasUriWithPolicy** método:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Hola **Main()** método debe tener el siguiente aspecto en su totalidad. Ejecutarlo firma de acceso compartido de hello toowrite ventana de la consola de toohello de URI, a continuación, copiar y pegarlos en un archivo de texto para su uso en la segunda parte de este tutorial de Hola.

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

Cuando se ejecuta la aplicación de consola GenerateSharedAccessSignatures hello, verá el siguiente toohello similar de salida. Se trata de usar en la parte 2 del tutorial de hello las firmas de acceso Hola compartido.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Parte 2: Crear un acceso de consola aplicación tootest Hola compartido firmas
Hola tootest compartidos creadas en los ejemplos anteriores de hello las firmas de acceso, creamos una segunda aplicación de consola que utiliza las operaciones de tooperform de firmas de hello en el contenedor de Hola y en un blob.

> [!NOTE]
> Si han pasado más de 24 horas desde que se ha completado la primera parte del tutorial Hola de hello, firmas de hello generó ya no serán válidas. En este caso, debe ejecutar código de hello en toogenerate de aplicación de consola primera Hola firmas de acceso compartido nueva para su uso en la segunda parte del tutorial Hola de Hola.
>

En Visual Studio, cree una nueva aplicación de consola de Windows y denomínela **ConsumeSharedAccessSignatures**. Agregar referencias demasiado[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) y [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), tal y como se hacía anteriormente.

En hello parte superior del archivo Program.cs de hello, agregue el siguiente de hello **con** directivas:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

En el cuerpo de Hola de hello **Main()** método, agregar Hola siguiendo las constantes de cadena, el cambio de sus firmas de acceso de toohello comparten valores generados en la parte 1 del tutorial de Hola.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Agregar método tootry contenedor las operaciones mediante una firma de acceso compartido
A continuación, se agrega un método que algunas operaciones de contenedor mediante una firma de acceso compartido para el contenedor de Hola de prueba. firma de acceso compartido de Hello es tooreturn usa un contenedor de toohello de referencia, autenticación de contenedor de toohello de acceso basado en la firma de hello independiente.

Agregue Hola siguiendo el método tooProgram.cs:

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Hola de actualización **Main()** método toocall **UseContainerSAS()** con ambos Hola compartido que creó en el contenedor de hello las firmas de acceso:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Agregar método tootry blob las operaciones mediante una firma de acceso compartido
Por último, se agrega un método que prueba algunas operaciones de blob con una firma de acceso compartido en el blob de Hola. En este caso, usamos el constructor de hello **CloudBlockBlob(String)**, pasando de firma de acceso compartido de hello, tooreturn un blob de toohello de referencia. Ninguna otra autenticación es necesario; se basa en la firma de hello independiente.

Agregue Hola siguiendo el método tooProgram.cs:

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Hola de actualización **Main()** método toocall **UseBlobSAS()** con ambos Hola compartido firmas de acceso que ha creado en el blob de hello:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

Ejecutar la aplicación de consola de hello y observe toosee de salida de hello qué operaciones se permiten que las firmas. salida de Hello en la ventana de la consola de hello tendrá una apariencia similar siguiente toohello:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Pasos siguientes

* [Firmas de acceso compartido, parte 1: Hola de descripción modelo SAS](storage-dotnet-shared-access-signature-part-1.md)
* [Administrar blobs y acceso de lectura anónimo toocontainers](storage-manage-access-to-resources.md)
* [Delegación de acceso con una firma de acceso compartido (API de REST)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introducción a las firmas de acceso compartido de tabla y cola](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
