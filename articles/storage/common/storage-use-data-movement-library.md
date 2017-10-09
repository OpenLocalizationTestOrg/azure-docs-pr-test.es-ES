---
title: aaaTransfer datos con hello biblioteca de movimiento de datos de almacenamiento de Microsoft Azure | Documentos de Microsoft
description: "Utilice la biblioteca de movimiento de datos de Hola a toomove o copia de la tooor de datos con el del contenido de blob y archivo. Copiar datos tooAzure almacenamiento de archivos locales, o copiar datos dentro de o entre cuentas de almacenamiento. Migrar fácilmente el almacenamiento de datos tooAzure."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Transferencia de datos con hello biblioteca de movimiento de datos de almacenamiento de Microsoft Azure

## <a name="overview"></a>Información general
Hola biblioteca de movimiento de datos de almacenamiento de Microsoft Azure es una biblioteca multiplataforma de código abierto que se ha diseñado para cargar, descargar y cómo copiar Blobs de almacenamiento de Azure y archivos de alto rendimiento. Esta biblioteca es el marco de movimiento de datos de núcleo de Hola que alimenta [AzCopy](../storage-use-azcopy.md). Hola biblioteca de movimiento de datos proporciona métodos útiles que no están disponibles en nuestro tradicional [biblioteca de cliente de almacenamiento de Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md). Esto incluye Hola capacidad tooset Hola número de operaciones en paralelo, seguir el progreso de transferencia, reanudar con facilidad una transferencia cancelada y mucho más.  

Esta biblioteca también utiliza .NET Core, lo que significa que puede usarla para crear aplicaciones .NET para Windows, Linux y MacOS. toolearn más información acerca de .NET Core, consulte toohello [documentación básica de .NET](https://dotnet.github.io/). Esta biblioteca también funciona para las aplicaciones de .NET Framework tradicionales para Windows. 

Este documento muestra cómo toocreate un núcleo de .NET que se ejecuta en Windows, Linux y Mac OS y realiza Hola los escenarios siguientes de la aplicación de consola:

- Cargar archivos y directorios tooBlob almacenamiento.
- Definir el número de Hola de operaciones en paralelo al transferir datos.
- Seguir el progreso de la transferencia de datos.
- Reanudar la transferencia de datos cancelada. 
- Copie el archivo de dirección URL tooBlob almacenamiento. 
- Copiar desde el almacenamiento de blobs tooBlob almacenamiento.

**Lo que necesita:**

* [código de Visual Studio](https://code.visualstudio.com/)
* Una [cuenta de almacenamiento de Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Esta guía asume que ya está familiarizado con el [Almacenamiento de Azure](https://azure.microsoft.com/services/storage/). Si no es así, leyendo hello [Introducción tooAzure almacenamiento](storage-introduction.md) documentación es útil. Lo más importante, necesita demasiado[crear una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account) utilizando toostart Hola biblioteca de movimiento de datos.
> 
> 

## <a name="setup"></a>Configuración  

1. Visite hello [Guía de instalación de .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Al seleccionar el entorno, elija la opción de línea de comandos de Hola. 
2. Desde la línea de comandos de hello, cree un directorio para el proyecto. Navegue en este directorio, a continuación, escriba `dotnet new` proyecto de consola toocreate C#.
3. Abra este directorio en Visual Studio Code. Este paso puede realizarse rápidamente a través de la línea de comandos de hello escribiendo `code .`.  
4. Instalar hello [C# extensión](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) de hello Marketplace de código de Visual Studio. Reinicie Visual Studio Code. 
5. Llegados a este punto, debe ver dos mensajes. Uno es para agregar "toobuild activos necesarios y depuración". Haga clic "sí". El otro mensaje es para restaurar dependencias no resueltas. Haga clic en "restaurar".
6. La aplicación debe contener ahora un `launch.json` archivo bajo hello `.vscode` directory. En este archivo, cambie hello `externalConsole` valor demasiado`true`.
7. Código de Visual Studio le permite toodebug aplicaciones de .NET Core. Aciertos `F5` toorun la aplicación y comprobar que funciona el programa de instalación. Debe ver "Hello World!" consola de toohello impresos. 

## <a name="add-data-movement-library-tooyour-project"></a>Agregar proyecto de biblioteca de movimiento de datos de tooyour

1. Agregar la versión más reciente de Hola de hello biblioteca de movimiento de datos toohello `dependencies` sección de su `project.json` archivo. En tiempo de Hola de escritura, sería esta versión`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Agregar `"portable-net45+win8"` toohello `imports` sección. 
3. Un símbolo del sistema debe mostrar toorestore el proyecto. Haga clic en el botón de "restaurar" Hola. También puede restaurar el proyecto desde la línea de comandos de hello escribiendo el comando hello `dotnet restore` en la raíz de Hola de su directorio de proyecto.

Modifique `project.json`:

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Configurar el esqueleto de saludo de la aplicación
Hello primero que hacemos es configurar Hola "esqueleto" código de nuestra aplicación. Este código nos pide una clave de cuenta y el nombre de la cuenta de almacenamiento y usa esas credenciales toocreate un `CloudStorageAccount` objeto. Este objeto es toointeract utilizado con la cuenta de almacenamiento en todos los escenarios de transferencia. código de Hello solicita nos toochoose tipo de Hola de operación de transferencia nos gustaría tooexecute. 

Modifique `Program.cs`:

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Transferencia de archivos local tooAzure Blob
Agregue los métodos de hello `GetSourcePath` y `GetBlob` demasiado`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Modificar hello `TransferLocalFileToAzureBlob` método:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Este código nos pide archivo local de tooa de ruta de acceso de hello, el nombre de Hola de un contenedor nuevo o existente y el nombre de Hola de un nuevo blob. Hola `TransferManager.UploadAsync` método realiza la carga de hello con esta información. 

Aciertos `F5` toorun la aplicación. Puede comprobar esa carga de hello producido mediante la visualización de la cuenta de almacenamiento con hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Establecimiento del número de operaciones paralelas
Una característica excelente que ofrece Hola que biblioteca de movimiento de datos es el número de Hola de tooset de capacidad de Hola de rendimiento de transferencia de datos de operaciones en paralelo tooincrease Hola. De forma predeterminada, Hola biblioteca de movimiento de datos establece número Hola de operaciones en paralelo too8 * Hola número de núcleos en su equipo. 

Tenga en cuenta que muchas operaciones en paralelo en un entorno de poco ancho de banda pueden saturar la conexión de red de Hola y realmente evitar operaciones complete totalmente. Necesitará tooexperiment con esta configuración toodetermine ¿qué funciona mejor basándose en el ancho de banda de red disponible. 

Vamos a agregar código que permite que nos tooset Hola número de operaciones en paralelo. Vamos a agregar código que el tiempo de espera cuánto tiempo tarda hello toocomplete de transferencia.

Agregar un `SetNumberOfParallelOperations` método demasiado`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Modificar hello `ExecuteChoice` toouse método `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Modificar hello `TransferLocalFileToAzureBlob` método toouse un temporizador:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Seguimiento del progreso de transferencia
Saber cuánto tiempo se tardó para nuestro tootransfer de datos es grande. Sin embargo, que se va toosee capaz de progreso de Hola de nuestro transferencia *durante* operación de transferencia de hello sería aún mejor. tooachieve este escenario, necesitamos toocreate un `TransferContext` objeto. Hola `TransferContext` objeto viene en dos formas: `SingleTransferContext` y `DirectoryTransferContext`. Hola anterior es para la transferencia de un solo archivo (que es lo que hacemos ahora) y Hola este último para transferir un directorio de archivos (lo que vamos a agregar más adelante).

Agregue los métodos de hello `GetSingleTransferContext` y `GetDirectoryTransferContext` demasiado`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Modificar hello `TransferLocalFileToAzureBlob` toouse método `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>Reanudación de una transferencia cancelada
Otra característica muy útil que ofrece Hola biblioteca de movimiento de datos es Hola capacidad tooresume una transferencia cancelada. Vamos a agregar código que nos permite tootemporarily Cancelar Hola transferencia escribiendo `c`y, a continuación, reanudar la transferencia de hello 3 segundos más tarde.

Modifique `TransferLocalFileToAzureBlob`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Hasta ahora, nuestro `checkpoint` valor siempre se establece demasiado`null`. Ahora, si se cancela la transferencia de hello, se recuperar el último punto de comprobación hello de la transferencia, utilice este nuevo punto de control en el contexto de la transferencia. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Transferencia de directorio de Blob de tooAzure de directorio local
Sería decepcionantes si Hola biblioteca de movimiento de datos solo puede transferir un archivo a la vez. Por suerte, esto no es el caso de hello. Hola biblioteca de movimiento de datos proporciona Hola capacidad tootransfer un directorio de archivos y de todos sus subdirectorios. Vamos a agregar código que nos permite toodo exactamente eso.

En primer lugar, agregue el método hello `GetBlobDirectory` demasiado`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

A continuación, modifique `TransferLocalDirectoryToAzureBlobDirectory`:

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Hay algunas diferencias entre este método y el método de hello para cargar un único archivo. Ahora que estamos usando `TransferManager.UploadDirectoryAsync` hello y `getDirectoryTransferContext` método hemos creado con anterioridad. Además, ahora se dan una `options` valor de la operación de carga de tooour, que nos permite tooindicate que deseamos tooinclude subdirectorios en las opciones de envío. 

## <a name="copy-file-from-url-tooazure-blob"></a>Copie el archivo de la dirección URL tooAzure Blob
Ahora, vamos a agregar código que nos permite toocopy un archivo de un Blob de Azure tooan de dirección URL. 

Modifique `TransferUrlToAzureBlob`:

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Un caso de uso importante de esta característica es cuando necesite toomove datos desde otro tooAzure de servicio (p. ej., AWS) en la nube. Siempre que tengan una dirección URL que proporciona acceso toohello recursos, se puede mover fácilmente ese recurso en Blobs de Azure mediante el uso de hello `TransferManager.CopyAsync` método. Este método también introduce un nuevo parámetro booleano. Establecer este parámetro demasiado`true` indica que deseamos copia toodo un servidor asincrónico. Establecer este parámetro demasiado`false` indica una copia sincrónica - lo que significa recursos hello es equipo local tooour descargado en primer lugar, a continuación, carga tooAzure Blob. Sin embargo, actualmente solo está disponible para la copia de un tooanother de recursos de almacenamiento de Azure copia sincrónica. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Transferencia de Blob de Azure tooAzure Blob
Otra característica de forma exclusiva proporcionada por hello biblioteca de movimiento de datos es Hola capacidad toocopy desde una tooanother de recursos de almacenamiento de Azure. 

Modifique `TransferAzureBlobToAzureBlob`:

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

En este ejemplo, establecemos parámetro booleano hello `TransferManager.CopyAsync` demasiado`false` tooindicate que deseamos toodo una copia sincrónica. Esto significa que los recursos de hello es equipo local tooour descargado por primera vez y después cargan tooAzure Blob. opción de copia sincrónica de Hello es un tooensure excelente manera que la operación de copia tiene una velocidad constante. En cambio, velocidad Hola de una copia asincrónica de servidor es dependiente de ancho de banda de red disponible de Hola en servidor de hello, que puede fluctuar. Sin embargo, copia sincrónica puede generar salida adicional en comparación con el costo tooasynchronous copia. Hola recomendado consiste toouse copia sincrónica en una máquina virtual de Azure que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.

## <a name="conclusion"></a>Conclusión
Nuestra aplicación de movimiento de datos ahora está completa. [ejemplo de código completo de Hello está disponible en GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Pasos siguientes
En esta introducción, hemos creado una aplicación que interactúa con Azure Storage y se ejecuta en Windows, Linux y MacOS. Esta introducción estaba dedicada a Blob Storage. Sin embargo, este mismo conocimiento puede ser aplicada tooFile almacenamiento. más información, consulte toolearn [documentación de referencia de biblioteca de movimiento de datos de almacenamiento de Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




