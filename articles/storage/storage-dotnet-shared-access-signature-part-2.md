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
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="cbcb0-103">Firmas de acceso compartido, Parte 2: Creación y uso de una SAS con Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="cbcb0-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="cbcb0-104">[Parte 1](storage-dotnet-shared-access-signature-part-1.md) de este tutorial se analizaron las firmas de acceso compartido (SAS) y se explicaron los procedimientos recomendados para su uso.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="cbcb0-105">Parte 2 muestra cómo acceso comparten toogenerate y después usar las firmas con un almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="cbcb0-106">ejemplos de Hello están escritos en C# y usar hello biblioteca de cliente de almacenamiento de Azure para. NET.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="cbcb0-107">ejemplos de Hello en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="cbcb0-108">Se generará una firma de acceso compartido en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="cbcb0-109">Se generará una firma de acceso compartido en un blob.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="cbcb0-110">Crear un acceso almacenada firmas de toomanage de directiva en los recursos de un contenedor</span><span class="sxs-lookup"><span data-stu-id="cbcb0-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="cbcb0-111">Comprobar las firmas de acceso compartido de hello en una aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="cbcb0-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="cbcb0-112">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="cbcb0-112">About this tutorial</span></span>
<span data-ttu-id="cbcb0-113">En este tutorial, crearemos dos aplicaciones de consola para demostrar la creación y el uso de firmas de acceso compartido para contenedores y blobs:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="cbcb0-114">**Aplicación 1**: Hola aplicación de administración.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="cbcb0-115">Genera una firma de acceso compartido para un contenedor y un blob.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="cbcb0-116">Incluye la clave de acceso de cuenta de almacenamiento de hello en el código fuente.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="cbcb0-117">**Aplicación 2**: Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="cbcb0-118">Recursos de contenedor y blob de accesos con firmas de acceso de hello compartido creadas con la primera aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="cbcb0-119">Usa solo Hola acceso compartido firmas tooaccess contenedor y los recursos de blob--hace *no* incluyen la clave de acceso de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="cbcb0-120">Parte 1: Crear un acceso de toogenerate compartida de aplicación de consola firmas</span><span class="sxs-lookup"><span data-stu-id="cbcb0-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="cbcb0-121">En primer lugar, asegúrese de que tiene Hola biblioteca de cliente de almacenamiento de Azure para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="cbcb0-122">Puede instalar hello [paquete NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "paquete NuGet") que contienen los ensamblados más actualizados de hello para la biblioteca de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="cbcb0-123">Se trata de hello recomendada método para garantizar que haya correcciones más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="cbcb0-124">También puede descargar la biblioteca de cliente de hello como parte de la versión más reciente del programa Hola Hola [Azure SDK para .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cbcb0-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="cbcb0-125">En Visual Studio, cree una aplicación de consola de Windows y denomínela **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="cbcb0-126">Agregar referencias demasiado[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) y [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) mediante uno de los siguientes enfoques de hello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="cbcb0-127">Hola de uso [Administrador de paquetes de NuGet](https://docs.nuget.org/consume/installing-nuget) en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="cbcb0-128">Seleccione **Proyecto** > **Administrar paquetes NuGet**, busque en línea cada paquete (Microsoft.WindowsAzure.ConfigurationManager y WindowsAzure.Storage) e instálelo.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="cbcb0-129">Como alternativa, buscar estos ensamblados en la instalación del programa Hola a Azure SDK y agregar referencias toothem:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="cbcb0-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="cbcb0-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="cbcb0-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="cbcb0-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="cbcb0-132">En hello parte superior del archivo Program.cs de hello, agregue el siguiente de hello **con** directivas:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="cbcb0-133">Edite el archivo app.config de hello para que contenga un valor de configuración con una cadena de conexión que señala tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="cbcb0-134">El archivo app.config debe ser similar toothis uno:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-134">Your app.config file should look similar toothis one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="cbcb0-135">Generación de un URI de firma de acceso compartido para un contenedor</span><span class="sxs-lookup"><span data-stu-id="cbcb0-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="cbcb0-136">toobegin con, agregamos un toogenerate método una firma de acceso compartido en un nuevo contenedor.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="cbcb0-137">En este caso, firma de hello no está asociado a una directiva de acceso almacenada, por lo que lleva a cabo en hello información Hola del identificador URI que indica los permisos de hello y tiempo de expiración concede.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="cbcb0-138">En primer lugar, agregue código toohello **Main()** método tooauthenticate tener acceso a la cuenta de almacenamiento de tooyour y crear un nuevo contenedor:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

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

<span data-ttu-id="cbcb0-139">A continuación, agregue un método que genera la firma de acceso compartido de hello para el contenedor de Hola y devuelve el URI de firma de hello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

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

<span data-ttu-id="cbcb0-140">Agregar Hola después líneas final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, toocall **GetContainerSasUri()** y escribir Hola ventana de consola de toohello URI de firma:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="cbcb0-141">Compile y ejecute la firma de acceso compartido hello toooutput URI para el nuevo contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="cbcb0-142">Hola URI será similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="cbcb0-143">Una vez que se ha ejecutado el código de hello, firma de acceso compartido de Hola que creó para el contenedor de hello será válida para hello próximas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="cbcb0-144">firma de Hello concede a un cliente de blobs de toolist de permiso en un contenedor hello y toowrite nuevo contenedor de toohello de blobs.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="cbcb0-145">Generación de un URI de firma de acceso compartido para un blob</span><span class="sxs-lookup"><span data-stu-id="cbcb0-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="cbcb0-146">A continuación, escribir toocreate de código similar en un nuevo blob en contenedor de Hola y generar una firma de acceso compartido para el mismo.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="cbcb0-147">Esta firma de acceso compartido no es asociada con una directiva de acceso almacenada, por lo que incluye información sobre los permisos, la hora de expiración y hora de inicio de Hola Hola URI.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="cbcb0-148">Agregue un nuevo método que crea un nuevo blob y escribe algunos tooit de texto, a continuación, genera una firma de acceso compartido y devuelve el URI de firma de hello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

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

<span data-ttu-id="cbcb0-149">Final Hola de hello **Main()** método, agregar Hola después líneas toocall **GetBlobSasUri()**, antes de hello llamar a demasiado**Console.ReadLine ()**y escribir Hola compartido ventana de consola de toohello URI de la firma de acceso:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="cbcb0-150">Compile y ejecute la firma de acceso compartido hello toooutput URI para el nuevo blob en Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="cbcb0-151">Hola URI será similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="cbcb0-152">Crear una directiva de acceso almacenada en el contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="cbcb0-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="cbcb0-153">Ahora vamos a crear una directiva de acceso almacenada en el contenedor de hello, que define las restricciones de Hola para las firmas de acceso compartido que están asociadas a ella.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="cbcb0-154">En los ejemplos anteriores de hello, se especifica la hora de inicio de Hola (implícita o explícitamente), la hora de expiración de Hola y los permisos de hello en hello comparten URI propio de la firma de acceso.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="cbcb0-155">En hello en los ejemplos siguientes, se especifican en directiva de acceso de hello almacenado, no en la firma de acceso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="cbcb0-156">Esto nos permite toochange comparten estas restricciones sin volver a emitir Hola acceso firma.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="cbcb0-157">Es posible toohave uno o más de las restricciones de hello en la firma de acceso compartido de Hola y el resto de hello en directiva de acceso de hello almacenado.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="cbcb0-158">Sin embargo, solo puede especificar la hora de inicio de hello, la hora de expiración y los permisos en un lugar o hello otro.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="cbcb0-159">Por ejemplo, no puede especificar los permisos en la firma de acceso compartido de Hola y especificarlas en la directiva de acceso de hello almacenado.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="cbcb0-160">Cuando se agrega un contenedor de tooa de directivas de acceso almacenada, debe obtener los permisos existentes del contenedor de hello, agregar nueva directiva de acceso de hello y, a continuación, establecer permisos del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="cbcb0-161">Agregue un nuevo método que crea una nueva directiva de acceso almacenada en un contenedor y devuelve el nombre de Hola de directiva de hello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

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

<span data-ttu-id="cbcb0-162">Final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, agregue Hola después líneas toofirst desactive las directivas de acceso existente y, a continuación, llamar a hello  **CreateSharedAccessPolicy()** método:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

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

<span data-ttu-id="cbcb0-163">Al desactivar las directivas de acceso de hello en un contenedor, primero debe obtener del contenedor de hello permisos existentes, a continuación, permisos de borrar Hola después establecer permisos de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="cbcb0-164">Generar un URI para el contenedor de Hola que usa una directiva de acceso de la firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="cbcb0-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="cbcb0-165">A continuación, se crea otra firma de acceso compartido para el contenedor de Hola que hemos creado con anterioridad, pero esta vez asociamos de firma de hello con directiva de acceso de hello almacenado que hemos creado en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="cbcb0-166">Agregue un nuevo toogenerate método otra firma de acceso compartido para el contenedor de hello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

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

<span data-ttu-id="cbcb0-167">Final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, agregar Hola después Hola de toocall líneas **GetContainerSasUriWithPolicy** (método) :</span><span class="sxs-lookup"><span data-stu-id="cbcb0-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="cbcb0-168">Generar un URI de firma de acceso compartido en hello Blob que utiliza una directiva de acceso</span><span class="sxs-lookup"><span data-stu-id="cbcb0-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="cbcb0-169">Por último, se agregue un toocreate método similar otro blob y generar una firma de acceso compartido que esté asociada con una directiva de acceso almacenada.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="cbcb0-170">Agregue un nuevo toocreate de método un blob y generar una firma de acceso compartido:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

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

<span data-ttu-id="cbcb0-171">Final Hola de hello **Main()** método, antes de hello llamar a demasiado**Console.ReadLine ()**, agregar Hola después hello toocall de líneas **GetBlobSasUriWithPolicy** método:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="cbcb0-172">Hola **Main()** método debe tener el siguiente aspecto en su totalidad.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="cbcb0-173">Ejecutarlo firma de acceso compartido de hello toowrite ventana de la consola de toohello de URI, a continuación, copiar y pegarlos en un archivo de texto para su uso en la segunda parte de este tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

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

<span data-ttu-id="cbcb0-174">Cuando se ejecuta la aplicación de consola GenerateSharedAccessSignatures hello, verá el siguiente toohello similar de salida.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="cbcb0-175">Se trata de usar en la parte 2 del tutorial de hello las firmas de acceso Hola compartido.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="cbcb0-176">Parte 2: Crear un acceso de consola aplicación tootest Hola compartido firmas</span><span class="sxs-lookup"><span data-stu-id="cbcb0-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="cbcb0-177">Hola tootest compartidos creadas en los ejemplos anteriores de hello las firmas de acceso, creamos una segunda aplicación de consola que utiliza las operaciones de tooperform de firmas de hello en el contenedor de Hola y en un blob.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcb0-178">Si han pasado más de 24 horas desde que se ha completado la primera parte del tutorial Hola de hello, firmas de hello generó ya no serán válidas.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="cbcb0-179">En este caso, debe ejecutar código de hello en toogenerate de aplicación de consola primera Hola firmas de acceso compartido nueva para su uso en la segunda parte del tutorial Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="cbcb0-180">En Visual Studio, cree una nueva aplicación de consola de Windows y denomínela **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="cbcb0-181">Agregar referencias demasiado[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) y [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), tal y como se hacía anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="cbcb0-182">En hello parte superior del archivo Program.cs de hello, agregue el siguiente de hello **con** directivas:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="cbcb0-183">En el cuerpo de Hola de hello **Main()** método, agregar Hola siguiendo las constantes de cadena, el cambio de sus firmas de acceso de toohello comparten valores generados en la parte 1 del tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="cbcb0-184">Agregar método tootry contenedor las operaciones mediante una firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="cbcb0-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="cbcb0-185">A continuación, se agrega un método que algunas operaciones de contenedor mediante una firma de acceso compartido para el contenedor de Hola de prueba.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="cbcb0-186">firma de acceso compartido de Hello es tooreturn usa un contenedor de toohello de referencia, autenticación de contenedor de toohello de acceso basado en la firma de hello independiente.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="cbcb0-187">Agregue Hola siguiendo el método tooProgram.cs:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-187">Add hello following method tooProgram.cs:</span></span>

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

<span data-ttu-id="cbcb0-188">Hola de actualización **Main()** método toocall **UseContainerSAS()** con ambos Hola compartido que creó en el contenedor de hello las firmas de acceso:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="cbcb0-189">Agregar método tootry blob las operaciones mediante una firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="cbcb0-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="cbcb0-190">Por último, se agrega un método que prueba algunas operaciones de blob con una firma de acceso compartido en el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="cbcb0-191">En este caso, usamos el constructor de hello **CloudBlockBlob(String)**, pasando de firma de acceso compartido de hello, tooreturn un blob de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="cbcb0-192">Ninguna otra autenticación es necesario; se basa en la firma de hello independiente.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="cbcb0-193">Agregue Hola siguiendo el método tooProgram.cs:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-193">Add hello following method tooProgram.cs:</span></span>

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

<span data-ttu-id="cbcb0-194">Hola de actualización **Main()** método toocall **UseBlobSAS()** con ambos Hola compartido firmas de acceso que ha creado en el blob de hello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

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

<span data-ttu-id="cbcb0-195">Ejecutar la aplicación de consola de hello y observe toosee de salida de hello qué operaciones se permiten que las firmas.</span><span class="sxs-lookup"><span data-stu-id="cbcb0-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="cbcb0-196">salida de Hello en la ventana de la consola de hello tendrá una apariencia similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="cbcb0-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="cbcb0-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbcb0-197">Next Steps</span></span>

* [<span data-ttu-id="cbcb0-198">Firmas de acceso compartido, parte 1: Hola de descripción modelo SAS</span><span class="sxs-lookup"><span data-stu-id="cbcb0-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="cbcb0-199">Administrar blobs y acceso de lectura anónimo toocontainers</span><span class="sxs-lookup"><span data-stu-id="cbcb0-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="cbcb0-200">Delegación de acceso con una firma de acceso compartido (API de REST)</span><span class="sxs-lookup"><span data-stu-id="cbcb0-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="cbcb0-201">Introducción a las firmas de acceso compartido de tabla y cola</span><span class="sxs-lookup"><span data-stu-id="cbcb0-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
