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
# <a name="develop-for-azure-file-storage-with-net"></a>Desarrollo para Azure File Storage con .NET 
> [!NOTE]
> Este artículo se muestra cómo toomanage almacenamiento de archivos de Azure con código. NET. toolearn más información acerca del almacenamiento de archivos de Azure, vea hello [Introducción tooAzure almacenamiento de archivos](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial demuestra conceptos básicos de hello del uso toodevelop aplicaciones o servicios .NET que utilizan datos de archivos de toostore de almacenamiento de archivos de Azure. En este tutorial, crearemos una aplicación de consola simple y mostrar cómo tooperform acciones básicas con el almacenamiento de .NET y archivos de Azure:

* Obtener el contenido de Hola de un archivo
* Establecer la cuota de hello (tamaño máximo) para el recurso compartido de archivos de Hola.
* Crear una firma de acceso compartido (clave SAS) para un archivo que usa una directiva de acceso compartido definida en el recurso compartido de Hola.
* Copiar un archivo de tooanother Hola misma cuenta de almacenamiento.
* Copiar un blob de tooa archivo Hola misma cuenta de almacenamiento.
* Uso de las métricas de Almacenamiento de Azure para solucionar problemas

> [!Note]  
> Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante clases System.IO estándar de Hola para E/S de archivos. En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de .NET de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Crear aplicación de consola de Hola y obtener el ensamblado hello
En Visual Studio, cree una nueva aplicación de consola de Windows. Hola siguientes pasos muestra cómo toocreate una aplicación de consola en Visual Studio 2017, sin embargo, los pasos de hello son similares en otras versiones de Visual Studio.

1. Seleccione **Archivo** > **Nuevo** > **Proyecto**
2. Seleccione **Instalado** > **Plantillas** > **Visual C#** > **Escritorio clásico de Windows**
3. Seleccione **Aplicación de consola (.NET Framework)**
4. Escriba un nombre para la aplicación Hola **nombre:** campo
5. Seleccione **Aceptar**.

Todos los ejemplos de código de este tutorial pueden agregarse toohello `Main()` método de la aplicación de consola `Program.cs` archivo.

Puede usar hello biblioteca de cliente de almacenamiento de Azure en cualquier tipo de aplicación. NET, incluida una aplicación web o servicio de nube de Azure y las aplicaciones de escritorio y móviles. En esta guía, usamos una aplicación de consola para hacerlo más sencillo.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Usar paquetes de NuGet tooinstall Hola necesario
Hay dos paquetes necesita tooreference en su proyecto toocomplete este tutorial:

* [Biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): este paquete proporciona acceso mediante programación toodata recursos en su cuenta de almacenamiento.
* [Biblioteca de Administrador de configuración de Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este paquete proporciona una clase para analizar una cadena de conexión en un archivo de configuración, independientemente del lugar en que se ejecute la aplicación.

Puede usar NuGet tooobtain ambos paquetes. Siga estos pasos:

1. Haga clic con el botón derecho en el proyecto, en el **Explorador de soluciones**, y elija **Administrar paquetes NuGet**.
2. Busque en línea "WindowsAzure.Storage" y haga clic en **instalar** tooinstall Hola biblioteca cliente de almacenamiento y sus dependencias.
3. Busque en línea "WindowsAzure.ConfigurationManager" y haga clic en **instalar** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Guarde el archivo app.config de almacenamiento cuenta credenciales toohello
A continuación, guardará las credenciales en el archivo app.config del proyecto. Editar el archivo app.config de hello para que parezca toohello similar ejemplo siguiente, reemplazando `myaccount` con su nombre de cuenta de almacenamiento, y `mykey` con su clave de cuenta de almacenamiento.

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
> versión más reciente de Hola Hola Azure del emulador de almacenamiento no admite el almacenamiento de archivos de Azure. La cadena de conexión debe tener como destino una cuenta de almacenamiento de Azure en hello en la nube toowork con almacenamiento de archivos de Azure.

## <a name="add-using-directives"></a>Adición de directivas using
Abra hello `Program.cs` archivo desde el Explorador de soluciones y agregue Hola siguiente con la parte superior de toohello de directivas de archivo hello.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Archivo de acceso hello compartir mediante programación
A continuación, agregue Hola después código toohello `Main()` cadena de conexión de hello tooretrieve de método (después del código de hello mostrado anteriormente). Este código obtiene un archivo de toohello de referencia que se creó anteriormente y muestra la ventana de la consola de toohello de contenido.

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

Ejecute la salida de hello consola aplicación toosee Hola.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Hola tamaño máximo para un recurso compartido de archivos
A partir de la versión 5.x de hello biblioteca de cliente de almacenamiento de Azure, puede establecer conjunto Hola cuota (o tamaño máximo) para un recurso compartido de archivos, en gigabytes. También puede comprobar toosee la cantidad de datos está almacenada en el recurso compartido de Hola.

Establecer la cuota de Hola para un recurso compartido, puede limitar tamaño total de Hola de archivos de hello almacenados en recursos compartidos de Hola. Si supera el tamaño total de Hola de archivos en el recurso compartido de hello establece cuota de hello en el recurso compartido de hello, clientes no se puede tooincrease Hola tamaño de los archivos existentes o crear nuevos archivos, a menos que esos archivos están vacíos.

ejemplo de Hola siguiente muestra cómo toocheck Hola uso actual de un recurso compartido y cómo tooset Hola cuota para el recurso compartido de Hola.

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Generar una firma de acceso compartido para un archivo o recurso compartido de archivos
A partir de la versión 5.x de Hola biblioteca de cliente de almacenamiento de Azure, puede generar una firma de acceso compartido (SAS) para un recurso compartido de archivos o un archivo individual. También puede crear una directiva de acceso compartido en un acceso toomanage compartido firmas. Se recomienda crear una directiva de acceso compartido, ya que proporciona un medio de revocar Hola SAS si debe estar en peligro.

Hola de ejemplo siguiente crea una directiva de acceso compartido en un recurso compartido y, a continuación, usa que comparten tooprovide hello las restricciones de directivas para una SAS en un archivo en Hola.

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

Para más información sobre la creación y el uso de firmas de acceso compartido, consulte [Uso de firmas de acceso compartido (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) y [Creación y uso de una SAS con Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Copiar archivos
A partir de la versión 5.x de Hola biblioteca de cliente de almacenamiento de Azure, puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob. En las secciones siguientes de hello, demostraremos cómo tooperform estas copian operaciones mediante programación.

También puede utilizar un archivo tooanother de AzCopy toocopy o toocopy un blob tooa archivo o viceversa. Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

> [!NOTE]
> Si va a copiar un archivo de tooa de blob o un blob de tooa de archivo, debe usar un objeto de origen de acceso compartido (SAS) de la firma tooauthenticate hello, incluso si va a copiar en hello misma cuenta de almacenamiento.
> 
> 

**Copiar un archivo de tooanother** hello en el ejemplo siguiente se copia un archivo tooanother archivo Hola mismo recurso compartido. Puesto que esta operación de copia copia entre archivos en Hola la misma cuenta de almacenamiento, puede usar copia de Hola de tooperform de autenticación de clave compartida.

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

**Copiar un blob de tooa archivo** crea un archivo hello en el ejemplo siguiente se y copia tooa blob dentro de hello misma cuenta de almacenamiento. ejemplo de Hola crea una SAS para el archivo de origen de hello, qué servicio hello usa el archivo de código fuente de tooauthenticate acceso toohello durante la operación de copia de Hola.

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

Puede copiar un archivo de blob tooa Hola igual. Si el objeto de origen de hello es un blob, a continuación, crear un blob de toothat SAS tooauthenticate acceso durante la operación de copia de Hola.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Solución de problemas de Azure File Storage mediante métricas
Azure Storage Analytics ahora admite métricas para Azure File Storage. Con los datos de las métricas, es posible seguir paso a paso las solicitudes y diagnosticar problemas.


Puede habilitar las métricas para almacenamiento de archivos de Azure de hello [Portal de Azure](https://portal.azure.com). También puede habilitar las métricas mediante programación por llamada Hola operación establecer propiedades del servicio de archivos a través de la API de REST de hello, o uno de sus análogos Hola biblioteca cliente de almacenamiento.


Hola, ejemplo de código siguiente muestra cómo toouse Hola biblioteca cliente de almacenamiento para las métricas de tooenable de .NET para almacenar archivos de Azure.

En primer lugar, agregue los siguientes de hello `using` tooyour directivas `Program.cs` , además de archivos toothose agregadas anteriormente:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Tenga en cuenta que al BLOB de Azure, tabla de Azure y colas de Azure usar hello compartido `ServiceProperties` tipo Hola `Microsoft.WindowsAzure.Storage.Shared.Protocol` espacio de nombres de almacenamiento de archivos de Azure, usa su propio tipo hello `FileServiceProperties` tipo Hola `Microsoft.WindowsAzure.Storage.File.Protocol` espacio de nombres. Ambos espacios de nombres deben hacer referencia desde el código, sin embargo, para hello después toocompile de código.

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

Asimismo, puede hacer referencia demasiado[artículo de solución de problemas de almacenamiento de archivos de Azure](storage-troubleshoot-windows-file-connection-problems.md) para obtener instrucciones para solucionar problemas de-to-end.

## <a name="next-steps"></a>Pasos siguientes
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

### <a name="conceptual-articles-and-videos"></a>Artículos y vídeos conceptuales
* [Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [¿Cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Compatibilidad de herramientas con el almacenamiento de archivos
* [Cómo toouse AzCopy con almacenamiento de Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Uso de hello CLI de Azure con el almacenamiento de Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Solución de problemas de Azure File Storage](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Referencia
* [Referencia de la biblioteca de clientes de almacenamiento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referencia de la API REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Publicaciones de blog
* [El almacenamiento de archivos de Azure ya está disponible de manera general](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [En el interior de Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Conservar conexiones tooMicrosoft almacenamiento de archivos de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
