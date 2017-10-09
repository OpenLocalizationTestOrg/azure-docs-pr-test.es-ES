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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="439ae-105">Transferencia de datos con hello biblioteca de movimiento de datos de almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="439ae-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="439ae-106">Información general</span><span class="sxs-lookup"><span data-stu-id="439ae-106">Overview</span></span>
<span data-ttu-id="439ae-107">Hola biblioteca de movimiento de datos de almacenamiento de Microsoft Azure es una biblioteca multiplataforma de código abierto que se ha diseñado para cargar, descargar y cómo copiar Blobs de almacenamiento de Azure y archivos de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="439ae-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="439ae-108">Esta biblioteca es el marco de movimiento de datos de núcleo de Hola que alimenta [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="439ae-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="439ae-109">Hola biblioteca de movimiento de datos proporciona métodos útiles que no están disponibles en nuestro tradicional [biblioteca de cliente de almacenamiento de Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="439ae-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="439ae-110">Esto incluye Hola capacidad tooset Hola número de operaciones en paralelo, seguir el progreso de transferencia, reanudar con facilidad una transferencia cancelada y mucho más.</span><span class="sxs-lookup"><span data-stu-id="439ae-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="439ae-111">Esta biblioteca también utiliza .NET Core, lo que significa que puede usarla para crear aplicaciones .NET para Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="439ae-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="439ae-112">toolearn más información acerca de .NET Core, consulte toohello [documentación básica de .NET](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="439ae-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="439ae-113">Esta biblioteca también funciona para las aplicaciones de .NET Framework tradicionales para Windows.</span><span class="sxs-lookup"><span data-stu-id="439ae-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="439ae-114">Este documento muestra cómo toocreate un núcleo de .NET que se ejecuta en Windows, Linux y Mac OS y realiza Hola los escenarios siguientes de la aplicación de consola:</span><span class="sxs-lookup"><span data-stu-id="439ae-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="439ae-115">Cargar archivos y directorios tooBlob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="439ae-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="439ae-116">Definir el número de Hola de operaciones en paralelo al transferir datos.</span><span class="sxs-lookup"><span data-stu-id="439ae-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="439ae-117">Seguir el progreso de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="439ae-117">Track data transfer progress.</span></span>
- <span data-ttu-id="439ae-118">Reanudar la transferencia de datos cancelada.</span><span class="sxs-lookup"><span data-stu-id="439ae-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="439ae-119">Copie el archivo de dirección URL tooBlob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="439ae-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="439ae-120">Copiar desde el almacenamiento de blobs tooBlob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="439ae-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="439ae-121">**Lo que necesita:**</span><span class="sxs-lookup"><span data-stu-id="439ae-121">**What you need:**</span></span>

* [<span data-ttu-id="439ae-122">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="439ae-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="439ae-123">Una [cuenta de almacenamiento de Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="439ae-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="439ae-124">Esta guía asume que ya está familiarizado con el [Almacenamiento de Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="439ae-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="439ae-125">Si no es así, leyendo hello [Introducción tooAzure almacenamiento](storage-introduction.md) documentación es útil.</span><span class="sxs-lookup"><span data-stu-id="439ae-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="439ae-126">Lo más importante, necesita demasiado[crear una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account) utilizando toostart Hola biblioteca de movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="439ae-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="439ae-127">Configuración</span><span class="sxs-lookup"><span data-stu-id="439ae-127">Setup</span></span>  

1. <span data-ttu-id="439ae-128">Visite hello [Guía de instalación de .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="439ae-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="439ae-129">Al seleccionar el entorno, elija la opción de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="439ae-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="439ae-130">Desde la línea de comandos de hello, cree un directorio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="439ae-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="439ae-131">Navegue en este directorio, a continuación, escriba `dotnet new` proyecto de consola toocreate C#.</span><span class="sxs-lookup"><span data-stu-id="439ae-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="439ae-132">Abra este directorio en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="439ae-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="439ae-133">Este paso puede realizarse rápidamente a través de la línea de comandos de hello escribiendo `code .`.</span><span class="sxs-lookup"><span data-stu-id="439ae-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="439ae-134">Instalar hello [C# extensión](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) de hello Marketplace de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="439ae-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="439ae-135">Reinicie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="439ae-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="439ae-136">Llegados a este punto, debe ver dos mensajes.</span><span class="sxs-lookup"><span data-stu-id="439ae-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="439ae-137">Uno es para agregar "toobuild activos necesarios y depuración".</span><span class="sxs-lookup"><span data-stu-id="439ae-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="439ae-138">Haga clic "sí".</span><span class="sxs-lookup"><span data-stu-id="439ae-138">Click "yes."</span></span> <span data-ttu-id="439ae-139">El otro mensaje es para restaurar dependencias no resueltas.</span><span class="sxs-lookup"><span data-stu-id="439ae-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="439ae-140">Haga clic en "restaurar".</span><span class="sxs-lookup"><span data-stu-id="439ae-140">Click "restore."</span></span>
6. <span data-ttu-id="439ae-141">La aplicación debe contener ahora un `launch.json` archivo bajo hello `.vscode` directory.</span><span class="sxs-lookup"><span data-stu-id="439ae-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="439ae-142">En este archivo, cambie hello `externalConsole` valor demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="439ae-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="439ae-143">Código de Visual Studio le permite toodebug aplicaciones de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="439ae-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="439ae-144">Aciertos `F5` toorun la aplicación y comprobar que funciona el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="439ae-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="439ae-145">Debe ver "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="439ae-145">You should see "Hello World!"</span></span> <span data-ttu-id="439ae-146">consola de toohello impresos.</span><span class="sxs-lookup"><span data-stu-id="439ae-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="439ae-147">Agregar proyecto de biblioteca de movimiento de datos de tooyour</span><span class="sxs-lookup"><span data-stu-id="439ae-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="439ae-148">Agregar la versión más reciente de Hola de hello biblioteca de movimiento de datos toohello `dependencies` sección de su `project.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="439ae-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="439ae-149">En tiempo de Hola de escritura, sería esta versión`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="439ae-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="439ae-150">Agregar `"portable-net45+win8"` toohello `imports` sección.</span><span class="sxs-lookup"><span data-stu-id="439ae-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="439ae-151">Un símbolo del sistema debe mostrar toorestore el proyecto.</span><span class="sxs-lookup"><span data-stu-id="439ae-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="439ae-152">Haga clic en el botón de "restaurar" Hola.</span><span class="sxs-lookup"><span data-stu-id="439ae-152">Click hello "restore" button.</span></span> <span data-ttu-id="439ae-153">También puede restaurar el proyecto desde la línea de comandos de hello escribiendo el comando hello `dotnet restore` en la raíz de Hola de su directorio de proyecto.</span><span class="sxs-lookup"><span data-stu-id="439ae-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="439ae-154">Modifique `project.json`:</span><span class="sxs-lookup"><span data-stu-id="439ae-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="439ae-155">Configurar el esqueleto de saludo de la aplicación</span><span class="sxs-lookup"><span data-stu-id="439ae-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="439ae-156">Hello primero que hacemos es configurar Hola "esqueleto" código de nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="439ae-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="439ae-157">Este código nos pide una clave de cuenta y el nombre de la cuenta de almacenamiento y usa esas credenciales toocreate un `CloudStorageAccount` objeto.</span><span class="sxs-lookup"><span data-stu-id="439ae-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="439ae-158">Este objeto es toointeract utilizado con la cuenta de almacenamiento en todos los escenarios de transferencia.</span><span class="sxs-lookup"><span data-stu-id="439ae-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="439ae-159">código de Hello solicita nos toochoose tipo de Hola de operación de transferencia nos gustaría tooexecute.</span><span class="sxs-lookup"><span data-stu-id="439ae-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="439ae-160">Modifique `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="439ae-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="439ae-161">Transferencia de archivos local tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="439ae-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="439ae-162">Agregue los métodos de hello `GetSourcePath` y `GetBlob` demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="439ae-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="439ae-163">Modificar hello `TransferLocalFileToAzureBlob` método:</span><span class="sxs-lookup"><span data-stu-id="439ae-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="439ae-164">Este código nos pide archivo local de tooa de ruta de acceso de hello, el nombre de Hola de un contenedor nuevo o existente y el nombre de Hola de un nuevo blob.</span><span class="sxs-lookup"><span data-stu-id="439ae-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="439ae-165">Hola `TransferManager.UploadAsync` método realiza la carga de hello con esta información.</span><span class="sxs-lookup"><span data-stu-id="439ae-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="439ae-166">Aciertos `F5` toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="439ae-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="439ae-167">Puede comprobar esa carga de hello producido mediante la visualización de la cuenta de almacenamiento con hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="439ae-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="439ae-168">Establecimiento del número de operaciones paralelas</span><span class="sxs-lookup"><span data-stu-id="439ae-168">Set number of parallel operations</span></span>
<span data-ttu-id="439ae-169">Una característica excelente que ofrece Hola que biblioteca de movimiento de datos es el número de Hola de tooset de capacidad de Hola de rendimiento de transferencia de datos de operaciones en paralelo tooincrease Hola.</span><span class="sxs-lookup"><span data-stu-id="439ae-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="439ae-170">De forma predeterminada, Hola biblioteca de movimiento de datos establece número Hola de operaciones en paralelo too8 * Hola número de núcleos en su equipo.</span><span class="sxs-lookup"><span data-stu-id="439ae-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="439ae-171">Tenga en cuenta que muchas operaciones en paralelo en un entorno de poco ancho de banda pueden saturar la conexión de red de Hola y realmente evitar operaciones complete totalmente.</span><span class="sxs-lookup"><span data-stu-id="439ae-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="439ae-172">Necesitará tooexperiment con esta configuración toodetermine ¿qué funciona mejor basándose en el ancho de banda de red disponible.</span><span class="sxs-lookup"><span data-stu-id="439ae-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="439ae-173">Vamos a agregar código que permite que nos tooset Hola número de operaciones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="439ae-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="439ae-174">Vamos a agregar código que el tiempo de espera cuánto tiempo tarda hello toocomplete de transferencia.</span><span class="sxs-lookup"><span data-stu-id="439ae-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="439ae-175">Agregar un `SetNumberOfParallelOperations` método demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="439ae-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="439ae-176">Modificar hello `ExecuteChoice` toouse método `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="439ae-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="439ae-177">Modificar hello `TransferLocalFileToAzureBlob` método toouse un temporizador:</span><span class="sxs-lookup"><span data-stu-id="439ae-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="439ae-178">Seguimiento del progreso de transferencia</span><span class="sxs-lookup"><span data-stu-id="439ae-178">Track transfer progress</span></span>
<span data-ttu-id="439ae-179">Saber cuánto tiempo se tardó para nuestro tootransfer de datos es grande.</span><span class="sxs-lookup"><span data-stu-id="439ae-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="439ae-180">Sin embargo, que se va toosee capaz de progreso de Hola de nuestro transferencia *durante* operación de transferencia de hello sería aún mejor.</span><span class="sxs-lookup"><span data-stu-id="439ae-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="439ae-181">tooachieve este escenario, necesitamos toocreate un `TransferContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="439ae-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="439ae-182">Hola `TransferContext` objeto viene en dos formas: `SingleTransferContext` y `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="439ae-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="439ae-183">Hola anterior es para la transferencia de un solo archivo (que es lo que hacemos ahora) y Hola este último para transferir un directorio de archivos (lo que vamos a agregar más adelante).</span><span class="sxs-lookup"><span data-stu-id="439ae-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="439ae-184">Agregue los métodos de hello `GetSingleTransferContext` y `GetDirectoryTransferContext` demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="439ae-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="439ae-185">Modificar hello `TransferLocalFileToAzureBlob` toouse método `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="439ae-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="439ae-186">Reanudación de una transferencia cancelada</span><span class="sxs-lookup"><span data-stu-id="439ae-186">Resume a canceled transfer</span></span>
<span data-ttu-id="439ae-187">Otra característica muy útil que ofrece Hola biblioteca de movimiento de datos es Hola capacidad tooresume una transferencia cancelada.</span><span class="sxs-lookup"><span data-stu-id="439ae-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="439ae-188">Vamos a agregar código que nos permite tootemporarily Cancelar Hola transferencia escribiendo `c`y, a continuación, reanudar la transferencia de hello 3 segundos más tarde.</span><span class="sxs-lookup"><span data-stu-id="439ae-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="439ae-189">Modifique `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="439ae-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="439ae-190">Hasta ahora, nuestro `checkpoint` valor siempre se establece demasiado`null`.</span><span class="sxs-lookup"><span data-stu-id="439ae-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="439ae-191">Ahora, si se cancela la transferencia de hello, se recuperar el último punto de comprobación hello de la transferencia, utilice este nuevo punto de control en el contexto de la transferencia.</span><span class="sxs-lookup"><span data-stu-id="439ae-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="439ae-192">Transferencia de directorio de Blob de tooAzure de directorio local</span><span class="sxs-lookup"><span data-stu-id="439ae-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="439ae-193">Sería decepcionantes si Hola biblioteca de movimiento de datos solo puede transferir un archivo a la vez.</span><span class="sxs-lookup"><span data-stu-id="439ae-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="439ae-194">Por suerte, esto no es el caso de hello.</span><span class="sxs-lookup"><span data-stu-id="439ae-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="439ae-195">Hola biblioteca de movimiento de datos proporciona Hola capacidad tootransfer un directorio de archivos y de todos sus subdirectorios.</span><span class="sxs-lookup"><span data-stu-id="439ae-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="439ae-196">Vamos a agregar código que nos permite toodo exactamente eso.</span><span class="sxs-lookup"><span data-stu-id="439ae-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="439ae-197">En primer lugar, agregue el método hello `GetBlobDirectory` demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="439ae-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="439ae-198">A continuación, modifique `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="439ae-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="439ae-199">Hay algunas diferencias entre este método y el método de hello para cargar un único archivo.</span><span class="sxs-lookup"><span data-stu-id="439ae-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="439ae-200">Ahora que estamos usando `TransferManager.UploadDirectoryAsync` hello y `getDirectoryTransferContext` método hemos creado con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="439ae-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="439ae-201">Además, ahora se dan una `options` valor de la operación de carga de tooour, que nos permite tooindicate que deseamos tooinclude subdirectorios en las opciones de envío.</span><span class="sxs-lookup"><span data-stu-id="439ae-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="439ae-202">Copie el archivo de la dirección URL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="439ae-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="439ae-203">Ahora, vamos a agregar código que nos permite toocopy un archivo de un Blob de Azure tooan de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="439ae-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="439ae-204">Modifique `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="439ae-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="439ae-205">Un caso de uso importante de esta característica es cuando necesite toomove datos desde otro tooAzure de servicio (p. ej., AWS) en la nube.</span><span class="sxs-lookup"><span data-stu-id="439ae-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="439ae-206">Siempre que tengan una dirección URL que proporciona acceso toohello recursos, se puede mover fácilmente ese recurso en Blobs de Azure mediante el uso de hello `TransferManager.CopyAsync` método.</span><span class="sxs-lookup"><span data-stu-id="439ae-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="439ae-207">Este método también introduce un nuevo parámetro booleano.</span><span class="sxs-lookup"><span data-stu-id="439ae-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="439ae-208">Establecer este parámetro demasiado`true` indica que deseamos copia toodo un servidor asincrónico.</span><span class="sxs-lookup"><span data-stu-id="439ae-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="439ae-209">Establecer este parámetro demasiado`false` indica una copia sincrónica - lo que significa recursos hello es equipo local tooour descargado en primer lugar, a continuación, carga tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="439ae-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="439ae-210">Sin embargo, actualmente solo está disponible para la copia de un tooanother de recursos de almacenamiento de Azure copia sincrónica.</span><span class="sxs-lookup"><span data-stu-id="439ae-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="439ae-211">Transferencia de Blob de Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="439ae-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="439ae-212">Otra característica de forma exclusiva proporcionada por hello biblioteca de movimiento de datos es Hola capacidad toocopy desde una tooanother de recursos de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="439ae-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="439ae-213">Modifique `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="439ae-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="439ae-214">En este ejemplo, establecemos parámetro booleano hello `TransferManager.CopyAsync` demasiado`false` tooindicate que deseamos toodo una copia sincrónica.</span><span class="sxs-lookup"><span data-stu-id="439ae-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="439ae-215">Esto significa que los recursos de hello es equipo local tooour descargado por primera vez y después cargan tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="439ae-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="439ae-216">opción de copia sincrónica de Hello es un tooensure excelente manera que la operación de copia tiene una velocidad constante.</span><span class="sxs-lookup"><span data-stu-id="439ae-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="439ae-217">En cambio, velocidad Hola de una copia asincrónica de servidor es dependiente de ancho de banda de red disponible de Hola en servidor de hello, que puede fluctuar.</span><span class="sxs-lookup"><span data-stu-id="439ae-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="439ae-218">Sin embargo, copia sincrónica puede generar salida adicional en comparación con el costo tooasynchronous copia.</span><span class="sxs-lookup"><span data-stu-id="439ae-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="439ae-219">Hola recomendado consiste toouse copia sincrónica en una máquina virtual de Azure que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="439ae-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="439ae-220">Conclusión</span><span class="sxs-lookup"><span data-stu-id="439ae-220">Conclusion</span></span>
<span data-ttu-id="439ae-221">Nuestra aplicación de movimiento de datos ahora está completa.</span><span class="sxs-lookup"><span data-stu-id="439ae-221">Our data movement application is now complete.</span></span> <span data-ttu-id="439ae-222">[ejemplo de código completo de Hello está disponible en GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="439ae-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="439ae-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="439ae-223">Next steps</span></span>
<span data-ttu-id="439ae-224">En esta introducción, hemos creado una aplicación que interactúa con Azure Storage y se ejecuta en Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="439ae-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="439ae-225">Esta introducción estaba dedicada a Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="439ae-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="439ae-226">Sin embargo, este mismo conocimiento puede ser aplicada tooFile almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="439ae-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="439ae-227">más información, consulte toolearn [documentación de referencia de biblioteca de movimiento de datos de almacenamiento de Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="439ae-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




