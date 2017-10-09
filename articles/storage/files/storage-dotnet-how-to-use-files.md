---
title: aaaDevelop para el almacenamiento de archivos de Azure con .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de .NET toodevelop y servicios que usen toostore de almacenamiento de archivos de Azure datos de archivos."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="f3cde-103">Desarrollo para Azure File Storage con .NET</span><span class="sxs-lookup"><span data-stu-id="f3cde-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="f3cde-104">Este artículo se muestra cómo toomanage almacenamiento de archivos de Azure con código. NET.</span><span class="sxs-lookup"><span data-stu-id="f3cde-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="f3cde-105">toolearn más información acerca del almacenamiento de archivos de Azure, vea hello [Introducción tooAzure almacenamiento de archivos](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f3cde-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="f3cde-106">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="f3cde-106">About this tutorial</span></span>
<span data-ttu-id="f3cde-107">Este tutorial demuestra conceptos básicos de hello del uso toodevelop aplicaciones o servicios .NET que utilizan datos de archivos de toostore de almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3cde-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="f3cde-108">En este tutorial, crearemos una aplicación de consola simple y mostrar cómo tooperform acciones básicas con el almacenamiento de .NET y archivos de Azure:</span><span class="sxs-lookup"><span data-stu-id="f3cde-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="f3cde-109">Obtener el contenido de Hola de un archivo</span><span class="sxs-lookup"><span data-stu-id="f3cde-109">Get hello contents of a file</span></span>
* <span data-ttu-id="f3cde-110">Establecer la cuota de hello (tamaño máximo) para el recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="f3cde-111">Crear una firma de acceso compartido (clave SAS) para un archivo que usa una directiva de acceso compartido definida en el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="f3cde-112">Copiar un archivo de tooanother Hola misma cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="f3cde-113">Copiar un blob de tooa archivo Hola misma cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="f3cde-114">Uso de las métricas de Almacenamiento de Azure para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="f3cde-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="f3cde-115">Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante clases System.IO estándar de Hola para E/S de archivos.</span><span class="sxs-lookup"><span data-stu-id="f3cde-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="f3cde-116">En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de .NET de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="f3cde-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="f3cde-117">Crear aplicación de consola de Hola y obtener el ensamblado hello</span><span class="sxs-lookup"><span data-stu-id="f3cde-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="f3cde-118">En Visual Studio, cree una nueva aplicación de consola de Windows.</span><span class="sxs-lookup"><span data-stu-id="f3cde-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="f3cde-119">Hola siguientes pasos muestra cómo toocreate una aplicación de consola en Visual Studio 2017, sin embargo, los pasos de hello son similares en otras versiones de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3cde-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="f3cde-120">Seleccione **Archivo** > **Nuevo** > **Proyecto**</span><span class="sxs-lookup"><span data-stu-id="f3cde-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="f3cde-121">Seleccione **Instalado** > **Plantillas** > **Visual C#** > **Escritorio clásico de Windows**</span><span class="sxs-lookup"><span data-stu-id="f3cde-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="f3cde-122">Seleccione **Aplicación de consola (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="f3cde-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="f3cde-123">Escriba un nombre para la aplicación Hola **nombre:** campo</span><span class="sxs-lookup"><span data-stu-id="f3cde-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="f3cde-124">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3cde-124">Select **OK**</span></span>

<span data-ttu-id="f3cde-125">Todos los ejemplos de código de este tutorial pueden agregarse toohello `Main()` método de la aplicación de consola `Program.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="f3cde-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="f3cde-126">Puede usar hello biblioteca de cliente de almacenamiento de Azure en cualquier tipo de aplicación. NET, incluida una aplicación web o servicio de nube de Azure y las aplicaciones de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="f3cde-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="f3cde-127">En esta guía, usamos una aplicación de consola para hacerlo más sencillo.</span><span class="sxs-lookup"><span data-stu-id="f3cde-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="f3cde-128">Usar paquetes de NuGet tooinstall Hola necesario</span><span class="sxs-lookup"><span data-stu-id="f3cde-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="f3cde-129">Hay dos paquetes necesita tooreference en su proyecto toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="f3cde-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="f3cde-130">[Biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): este paquete proporciona acceso mediante programación toodata recursos en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="f3cde-131">[Biblioteca de Administrador de configuración de Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este paquete proporciona una clase para analizar una cadena de conexión en un archivo de configuración, independientemente del lugar en que se ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f3cde-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="f3cde-132">Puede usar NuGet tooobtain ambos paquetes.</span><span class="sxs-lookup"><span data-stu-id="f3cde-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="f3cde-133">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f3cde-133">Follow these steps:</span></span>

1. <span data-ttu-id="f3cde-134">Haga clic con el botón derecho en el proyecto, en el **Explorador de soluciones**, y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f3cde-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="f3cde-135">Busque en línea "WindowsAzure.Storage" y haga clic en **instalar** tooinstall Hola biblioteca cliente de almacenamiento y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f3cde-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="f3cde-136">Busque en línea "WindowsAzure.ConfigurationManager" y haga clic en **instalar** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="f3cde-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="f3cde-137">Guarde el archivo app.config de almacenamiento cuenta credenciales toohello</span><span class="sxs-lookup"><span data-stu-id="f3cde-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="f3cde-138">A continuación, guardará las credenciales en el archivo app.config del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f3cde-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="f3cde-139">Editar el archivo app.config de hello para que parezca toohello similar ejemplo siguiente, reemplazando `myaccount` con su nombre de cuenta de almacenamiento, y `mykey` con su clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> versión más reciente de Hola Hola Azure del emulador de almacenamiento no admite el almacenamiento de archivos de Azure. <span data-ttu-id="f3cde-141">La cadena de conexión debe tener como destino una cuenta de almacenamiento de Azure en hello en la nube toowork con almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3cde-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="f3cde-142">Adición de directivas using</span><span class="sxs-lookup"><span data-stu-id="f3cde-142">Add using directives</span></span>
<span data-ttu-id="f3cde-143">Abra hello `Program.cs` archivo desde el Explorador de soluciones y agregue Hola siguiente con la parte superior de toohello de directivas de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="f3cde-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="f3cde-144">Archivo de acceso hello compartir mediante programación</span><span class="sxs-lookup"><span data-stu-id="f3cde-144">Access hello file share programmatically</span></span>
<span data-ttu-id="f3cde-145">A continuación, agregue Hola después código toohello `Main()` cadena de conexión de hello tooretrieve de método (después del código de hello mostrado anteriormente).</span><span class="sxs-lookup"><span data-stu-id="f3cde-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="f3cde-146">Este código obtiene un archivo de toohello de referencia que se creó anteriormente y muestra la ventana de la consola de toohello de contenido.</span><span class="sxs-lookup"><span data-stu-id="f3cde-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="f3cde-147">Ejecute la salida de hello consola aplicación toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="f3cde-148">Hola tamaño máximo para un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="f3cde-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="f3cde-149">A partir de la versión 5.x de hello biblioteca de cliente de almacenamiento de Azure, puede establecer conjunto Hola cuota (o tamaño máximo) para un recurso compartido de archivos, en gigabytes.</span><span class="sxs-lookup"><span data-stu-id="f3cde-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="f3cde-150">También puede comprobar toosee la cantidad de datos está almacenada en el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="f3cde-151">Establecer la cuota de Hola para un recurso compartido, puede limitar tamaño total de Hola de archivos de hello almacenados en recursos compartidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="f3cde-152">Si supera el tamaño total de Hola de archivos en el recurso compartido de hello establece cuota de hello en el recurso compartido de hello, clientes no se puede tooincrease Hola tamaño de los archivos existentes o crear nuevos archivos, a menos que esos archivos están vacíos.</span><span class="sxs-lookup"><span data-stu-id="f3cde-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="f3cde-153">ejemplo de Hola siguiente muestra cómo toocheck Hola uso actual de un recurso compartido y cómo tooset Hola cuota para el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="f3cde-154">Generar una firma de acceso compartido para un archivo o recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="f3cde-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="f3cde-155">A partir de la versión 5.x de Hola biblioteca de cliente de almacenamiento de Azure, puede generar una firma de acceso compartido (SAS) para un recurso compartido de archivos o un archivo individual.</span><span class="sxs-lookup"><span data-stu-id="f3cde-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="f3cde-156">También puede crear una directiva de acceso compartido en un acceso toomanage compartido firmas.</span><span class="sxs-lookup"><span data-stu-id="f3cde-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="f3cde-157">Se recomienda crear una directiva de acceso compartido, ya que proporciona un medio de revocar Hola SAS si debe estar en peligro.</span><span class="sxs-lookup"><span data-stu-id="f3cde-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="f3cde-158">Hola de ejemplo siguiente crea una directiva de acceso compartido en un recurso compartido y, a continuación, usa que comparten tooprovide hello las restricciones de directivas para una SAS en un archivo en Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="f3cde-159">Para más información sobre la creación y el uso de firmas de acceso compartido, consulte [Uso de firmas de acceso compartido (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) y [Creación y uso de una SAS con Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="f3cde-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="f3cde-160">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="f3cde-160">Copy files</span></span>
<span data-ttu-id="f3cde-161">A partir de la versión 5.x de Hola biblioteca de cliente de almacenamiento de Azure, puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="f3cde-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="f3cde-162">En las secciones siguientes de hello, demostraremos cómo tooperform estas copian operaciones mediante programación.</span><span class="sxs-lookup"><span data-stu-id="f3cde-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="f3cde-163">También puede utilizar un archivo tooanother de AzCopy toocopy o toocopy un blob tooa archivo o viceversa.</span><span class="sxs-lookup"><span data-stu-id="f3cde-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="f3cde-164">Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3cde-164">See [Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="f3cde-165">Si va a copiar un archivo de tooa de blob o un blob de tooa de archivo, debe usar un objeto de origen de acceso compartido (SAS) de la firma tooauthenticate hello, incluso si va a copiar en hello misma cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="f3cde-166">**Copiar un archivo de tooanother** hello en el ejemplo siguiente se copia un archivo tooanother archivo Hola mismo recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="f3cde-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="f3cde-167">Puesto que esta operación de copia copia entre archivos en Hola la misma cuenta de almacenamiento, puede usar copia de Hola de tooperform de autenticación de clave compartida.</span><span class="sxs-lookup"><span data-stu-id="f3cde-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="f3cde-168">**Copiar un blob de tooa archivo** crea un archivo hello en el ejemplo siguiente se y copia tooa blob dentro de hello misma cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="f3cde-169">ejemplo de Hola crea una SAS para el archivo de origen de hello, qué servicio hello usa el archivo de código fuente de tooauthenticate acceso toohello durante la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="f3cde-170">Puede copiar un archivo de blob tooa Hola igual.</span><span class="sxs-lookup"><span data-stu-id="f3cde-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="f3cde-171">Si el objeto de origen de hello es un blob, a continuación, crear un blob de toothat SAS tooauthenticate acceso durante la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3cde-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="f3cde-172">Solución de problemas de Azure File Storage mediante métricas</span><span class="sxs-lookup"><span data-stu-id="f3cde-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="f3cde-173">Azure Storage Analytics ahora admite métricas para Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="f3cde-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="f3cde-174">Con los datos de las métricas, es posible seguir paso a paso las solicitudes y diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="f3cde-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="f3cde-175">Puede habilitar las métricas para almacenamiento de archivos de Azure de hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3cde-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="f3cde-176">También puede habilitar las métricas mediante programación por llamada Hola operación establecer propiedades del servicio de archivos a través de la API de REST de hello, o uno de sus análogos Hola biblioteca cliente de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3cde-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="f3cde-177">Hola, ejemplo de código siguiente muestra cómo toouse Hola biblioteca cliente de almacenamiento para las métricas de tooenable de .NET para almacenar archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3cde-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="f3cde-178">En primer lugar, agregue los siguientes de hello `using` tooyour directivas `Program.cs` , además de archivos toothose agregadas anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f3cde-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="f3cde-179">Tenga en cuenta que al BLOB de Azure, tabla de Azure y colas de Azure usar hello compartido `ServiceProperties` tipo Hola `Microsoft.WindowsAzure.Storage.Shared.Protocol` espacio de nombres de almacenamiento de archivos de Azure, usa su propio tipo hello `FileServiceProperties` tipo Hola `Microsoft.WindowsAzure.Storage.File.Protocol` espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="f3cde-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="f3cde-180">Ambos espacios de nombres deben hacer referencia desde el código, sin embargo, para hello después toocompile de código.</span><span class="sxs-lookup"><span data-stu-id="f3cde-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="f3cde-181">Asimismo, puede hacer referencia demasiado[artículo de solución de problemas de almacenamiento de archivos de Azure](storage-troubleshoot-windows-file-connection-problems.md) para obtener instrucciones para solucionar problemas de-to-end.</span><span class="sxs-lookup"><span data-stu-id="f3cde-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3cde-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3cde-182">Next steps</span></span>
<span data-ttu-id="f3cde-183">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3cde-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="f3cde-184">Artículos y vídeos conceptuales</span><span class="sxs-lookup"><span data-stu-id="f3cde-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="f3cde-185">Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux</span><span class="sxs-lookup"><span data-stu-id="f3cde-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="f3cde-186">¿Cómo toouse almacenamiento de archivos de Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="f3cde-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="f3cde-187">Compatibilidad de herramientas con el almacenamiento de archivos</span><span class="sxs-lookup"><span data-stu-id="f3cde-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="f3cde-188">Cómo toouse AzCopy con almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f3cde-188">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="f3cde-189">Uso de hello CLI de Azure con el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f3cde-189">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="f3cde-190">Solución de problemas de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="f3cde-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="f3cde-191">Referencia</span><span class="sxs-lookup"><span data-stu-id="f3cde-191">Reference</span></span>
* [<span data-ttu-id="f3cde-192">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="f3cde-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="f3cde-193">Referencia de la API REST del servicio de archivos</span><span class="sxs-lookup"><span data-stu-id="f3cde-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="f3cde-194">Publicaciones de blog</span><span class="sxs-lookup"><span data-stu-id="f3cde-194">Blog posts</span></span>
* [<span data-ttu-id="f3cde-195">El almacenamiento de archivos de Azure ya está disponible de manera general</span><span class="sxs-lookup"><span data-stu-id="f3cde-195">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="f3cde-196">En el interior de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="f3cde-196">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="f3cde-197">Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="f3cde-197">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="f3cde-198">Conservar conexiones tooMicrosoft almacenamiento de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="f3cde-198">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
