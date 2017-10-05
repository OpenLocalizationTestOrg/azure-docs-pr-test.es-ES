---
title: Transferencia de datos con la Biblioteca de movimiento de datos de Microsoft Azure Storage | Microsoft Docs
description: "Use la Biblioteca de movimiento de datos para realizar operaciones de movimiento o copia de datos con blobs y contenido de archivos. Copie datos a Almacenamiento de Azure desde archivos locales o copie datos en o entre cuentas de almacenamiento. Migre fácilmente sus datos a Almacenamiento de Azure."
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
ms.openlocfilehash: 7db1761a9a3b8a74a39b2d441849fb89d44cd42b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="9c765-105">Transferencia de datos con la Biblioteca de movimiento de datos de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c765-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="9c765-106">Información general</span><span class="sxs-lookup"><span data-stu-id="9c765-106">Overview</span></span>
<span data-ttu-id="9c765-107">La Biblioteca de movimiento de datos de Microsoft Azure Storage es una biblioteca multiplataforma de código abierto que se ha diseñado para carga, descarga y copia de alto rendimiento de blobs y archivos de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9c765-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="9c765-108">Esta biblioteca es el marco de movimiento de datos principal que alimenta a [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="9c765-108">This library is the core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="9c765-109">La Biblioteca de movimiento de datos proporciona métodos útiles que no están disponibles en nuestra [biblioteca de cliente de Azure Storage .NET](../blobs/storage-dotnet-how-to-use-blobs.md) tradicional.</span><span class="sxs-lookup"><span data-stu-id="9c765-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="9c765-110">Esto incluye la capacidad de establecer el número de operaciones paralelas, seguir el progreso de transferencia, reanudar con facilidad una transferencia cancelada y mucho más.</span><span class="sxs-lookup"><span data-stu-id="9c765-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="9c765-111">Esta biblioteca también utiliza .NET Core, lo que significa que puede usarla para crear aplicaciones .NET para Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="9c765-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="9c765-112">Para más información sobre .NET Core, consulte la [documentación de .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="9c765-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="9c765-113">Esta biblioteca también funciona para las aplicaciones de .NET Framework tradicionales para Windows.</span><span class="sxs-lookup"><span data-stu-id="9c765-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="9c765-114">En este documento se muestra cómo crear una aplicación de consola de .NET Core que se ejecuta en Windows, Linux y MacOS y lleva a cabo los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="9c765-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="9c765-115">Cargar archivos y directorios en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9c765-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="9c765-116">Definir el número de operaciones paralelas al transferir datos.</span><span class="sxs-lookup"><span data-stu-id="9c765-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="9c765-117">Seguir el progreso de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="9c765-117">Track data transfer progress.</span></span>
- <span data-ttu-id="9c765-118">Reanudar la transferencia de datos cancelada.</span><span class="sxs-lookup"><span data-stu-id="9c765-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="9c765-119">Copiar el archivo desde la dirección URL en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9c765-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="9c765-120">Copiar de Blob Storage a Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9c765-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="9c765-121">**Lo que necesita:**</span><span class="sxs-lookup"><span data-stu-id="9c765-121">**What you need:**</span></span>

* [<span data-ttu-id="9c765-122">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c765-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="9c765-123">Una [cuenta de almacenamiento de Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="9c765-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="9c765-124">Esta guía asume que ya está familiarizado con el [Almacenamiento de Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="9c765-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="9c765-125">Si no es así, la lectura de la documentación de [Introducción a Microsoft Azure Storage](storage-introduction.md) le resultará útil.</span><span class="sxs-lookup"><span data-stu-id="9c765-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="9c765-126">Y lo que es más importante, necesita [crear una cuenta de Storage](storage-create-storage-account.md#create-a-storage-account) para empezar a usar la Biblioteca de movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="9c765-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="9c765-127">Configuración</span><span class="sxs-lookup"><span data-stu-id="9c765-127">Setup</span></span>  

1. <span data-ttu-id="9c765-128">Visite la [guía de instalación de .NET Core](https://www.microsoft.com/net/core) para instalar .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9c765-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="9c765-129">Cuando seleccione el entorno, elija la opción de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="9c765-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="9c765-130">Desde la línea de comandos, cree un directorio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9c765-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="9c765-131">Vaya a este directorio y escriba `dotnet new` para crear un proyecto de consola en C#.</span><span class="sxs-lookup"><span data-stu-id="9c765-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="9c765-132">Abra este directorio en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9c765-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="9c765-133">Este paso puede realizarse rápidamente a través de la línea de comandos escribiendo `code .`.</span><span class="sxs-lookup"><span data-stu-id="9c765-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="9c765-134">Instale la [extensión de C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) desde Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9c765-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="9c765-135">Reinicie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9c765-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="9c765-136">Llegados a este punto, debe ver dos mensajes.</span><span class="sxs-lookup"><span data-stu-id="9c765-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="9c765-137">Uno es para agregar "recursos necesarios para compilar y depurar".</span><span class="sxs-lookup"><span data-stu-id="9c765-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="9c765-138">Haga clic "sí".</span><span class="sxs-lookup"><span data-stu-id="9c765-138">Click "yes."</span></span> <span data-ttu-id="9c765-139">El otro mensaje es para restaurar dependencias no resueltas.</span><span class="sxs-lookup"><span data-stu-id="9c765-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="9c765-140">Haga clic en "restaurar".</span><span class="sxs-lookup"><span data-stu-id="9c765-140">Click "restore."</span></span>
6. <span data-ttu-id="9c765-141">La aplicación ahora debe contener un archivo `launch.json` en el directorio `.vscode`.</span><span class="sxs-lookup"><span data-stu-id="9c765-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="9c765-142">En este archivo, cambie el valor de `externalConsole` a `true`.</span><span class="sxs-lookup"><span data-stu-id="9c765-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="9c765-143">Visual Studio Code permite depurar aplicaciones de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9c765-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="9c765-144">Presione `F5` para ejecutar la aplicación y compruebe que la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="9c765-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="9c765-145">Debe ver "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="9c765-145">You should see "Hello World!"</span></span> <span data-ttu-id="9c765-146">impreso en la consola.</span><span class="sxs-lookup"><span data-stu-id="9c765-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="9c765-147">Incorporación de la Biblioteca de movimiento de datos al proyecto</span><span class="sxs-lookup"><span data-stu-id="9c765-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="9c765-148">Agregue la versión más reciente de la Biblioteca de movimiento de datos a la sección `dependencies` de su archivo `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9c765-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="9c765-149">En el momento de la escritura, esta versión sería `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`.</span><span class="sxs-lookup"><span data-stu-id="9c765-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="9c765-150">Agregue `"portable-net45+win8"` a la sección `imports`.</span><span class="sxs-lookup"><span data-stu-id="9c765-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="9c765-151">Debe aparecer un mensaje para restaurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9c765-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="9c765-152">Haga clic en el botón "restaurar".</span><span class="sxs-lookup"><span data-stu-id="9c765-152">Click the "restore" button.</span></span> <span data-ttu-id="9c765-153">También puede restaurar el proyecto desde la línea de comandos escribiendo el comando `dotnet restore` en la raíz del directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9c765-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="9c765-154">Modifique `project.json`:</span><span class="sxs-lookup"><span data-stu-id="9c765-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="9c765-155">Configuración del esqueleto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9c765-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="9c765-156">Lo primero que hacemos es configurar el código de "esqueleto" de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9c765-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="9c765-157">Este código nos pide una clave de cuenta y un nombre de cuenta de Storage y usa esas credenciales para crear un objeto `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="9c765-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="9c765-158">Este objeto se usa para interactuar con nuestra cuenta de Storage en todos los escenarios de transferencia.</span><span class="sxs-lookup"><span data-stu-id="9c765-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="9c765-159">El código también nos pedirá que elijamos el tipo de operación de transferencia que se desea ejecutar.</span><span class="sxs-lookup"><span data-stu-id="9c765-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="9c765-160">Modifique `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="9c765-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="9c765-161">Transferencia del archivo local al blob de Azure</span><span class="sxs-lookup"><span data-stu-id="9c765-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="9c765-162">Agregue los métodos `GetSourcePath` y `GetBlob` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="9c765-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="9c765-163">Modifique el método `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="9c765-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="9c765-164">Este código nos pide la ruta de acceso a un archivo local, el nombre de un contenedor nuevo o existente y el nombre de un nuevo blob.</span><span class="sxs-lookup"><span data-stu-id="9c765-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="9c765-165">El método `TransferManager.UploadAsync` realiza la carga con esta información.</span><span class="sxs-lookup"><span data-stu-id="9c765-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="9c765-166">Presione `F5` para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9c765-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="9c765-167">Puede comprobar que se ha producido la carga mediante la visualización de la cuenta de Storage con el [Explorador de Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9c765-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="9c765-168">Establecimiento del número de operaciones paralelas</span><span class="sxs-lookup"><span data-stu-id="9c765-168">Set number of parallel operations</span></span>
<span data-ttu-id="9c765-169">Una característica excelente que ofrece la Biblioteca de movimiento de datos es la capacidad para establecer el número de operaciones paralelas para aumentar el rendimiento de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="9c765-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="9c765-170">De forma predeterminada, la Biblioteca de movimiento de datos establece el número de operaciones paralelas en 8 multiplicado por el número de núcleos de la máquina.</span><span class="sxs-lookup"><span data-stu-id="9c765-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="9c765-171">Tenga en cuenta que muchas operaciones paralelas en un entorno con poco ancho de banda puede saturar la conexión de red e impedir que las operaciones se completen.</span><span class="sxs-lookup"><span data-stu-id="9c765-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="9c765-172">Debe experimentar con esta configuración para determinar qué funciona mejor basándose en el ancho de banda de red disponible.</span><span class="sxs-lookup"><span data-stu-id="9c765-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="9c765-173">Vamos a agregar código que nos permita establecer el número de operaciones paralelas.</span><span class="sxs-lookup"><span data-stu-id="9c765-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="9c765-174">Vamos a agregar también código que cronometra el tiempo que tarda la transferencia en completarse.</span><span class="sxs-lookup"><span data-stu-id="9c765-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="9c765-175">Agregar un método `SetNumberOfParallelOperations` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="9c765-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="9c765-176">Modifique el método `ExecuteChoice` para usar `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="9c765-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="9c765-177">Modifique el método `TransferLocalFileToAzureBlob` para usar un temporizador:</span><span class="sxs-lookup"><span data-stu-id="9c765-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="9c765-178">Seguimiento del progreso de transferencia</span><span class="sxs-lookup"><span data-stu-id="9c765-178">Track transfer progress</span></span>
<span data-ttu-id="9c765-179">Saber cuánto tiempo tardaron los datos en transferirse es magnífico.</span><span class="sxs-lookup"><span data-stu-id="9c765-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="9c765-180">Sin embargo, tener la posibilidad de ver el progreso de la transferencia *durante* la operación de transferencia sería incluso mejor.</span><span class="sxs-lookup"><span data-stu-id="9c765-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="9c765-181">Para lograr este escenario, es necesario crear un objeto `TransferContext`.</span><span class="sxs-lookup"><span data-stu-id="9c765-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="9c765-182">El objeto `TransferContext` se proporciona en dos formas: `SingleTransferContext` y `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="9c765-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="9c765-183">La primera de ellas es para transferir un archivo único (que es lo que estamos haciendo ahora) y la segunda es para transferir un directorio de archivos (que agregaremos más adelante).</span><span class="sxs-lookup"><span data-stu-id="9c765-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="9c765-184">Agregue los métodos `GetSingleTransferContext` y `GetDirectoryTransferContext` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="9c765-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="9c765-185">Modifique el método `TransferLocalFileToAzureBlob` para usar `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="9c765-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="9c765-186">Reanudación de una transferencia cancelada</span><span class="sxs-lookup"><span data-stu-id="9c765-186">Resume a canceled transfer</span></span>
<span data-ttu-id="9c765-187">Otra característica muy útil que ofrece la Biblioteca de movimiento de datos es la capacidad de reanudar una transferencia cancelada.</span><span class="sxs-lookup"><span data-stu-id="9c765-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="9c765-188">Vamos a agregar código que nos permite cancelar la transferencia temporalmente escribiendo `c` y luego reanudar dicha transferencia 3 segundos más tarde.</span><span class="sxs-lookup"><span data-stu-id="9c765-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="9c765-189">Modifique `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="9c765-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="9c765-190">Hasta ahora, nuestro valor de `checkpoint` siempre se ha establecido en `null`.</span><span class="sxs-lookup"><span data-stu-id="9c765-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="9c765-191">Ahora, si se cancela la transferencia, recuperaremos el último punto de comprobación de dicha transferencia y luego utilizaremos este nuevo punto de comprobación en nuestro contexto de la transferencia.</span><span class="sxs-lookup"><span data-stu-id="9c765-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="9c765-192">Transferencia de directorio local al directorio de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="9c765-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="9c765-193">Sería decepcionante que la Biblioteca de movimiento de datos solo pudiera transferir un archivo a la vez.</span><span class="sxs-lookup"><span data-stu-id="9c765-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="9c765-194">Afortunadamente, no es el caso.</span><span class="sxs-lookup"><span data-stu-id="9c765-194">Luckily, this is not the case.</span></span> <span data-ttu-id="9c765-195">La Biblioteca de movimiento de datos proporciona la capacidad de transferir un directorio de archivos y todos sus subdirectorios.</span><span class="sxs-lookup"><span data-stu-id="9c765-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="9c765-196">Vamos a agregar código que nos permita hacer exactamente eso.</span><span class="sxs-lookup"><span data-stu-id="9c765-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="9c765-197">En primer lugar, agregue el método `GetBlobDirectory` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="9c765-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="9c765-198">A continuación, modifique `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="9c765-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="9c765-199">Hay algunas diferencias entre este método y el método para cargar un único archivo.</span><span class="sxs-lookup"><span data-stu-id="9c765-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="9c765-200">Ahora estamos usando `TransferManager.UploadDirectoryAsync` y el método `getDirectoryTransferContext` que hemos creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9c765-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="9c765-201">Además, ahora proporcionamos un valor de `options` a nuestra operación de carga, lo que nos permite indicar que deseamos incluir los subdirectorios en nuestra carga.</span><span class="sxs-lookup"><span data-stu-id="9c765-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="9c765-202">Copia del archivo desde la dirección URL a blob de Azure</span><span class="sxs-lookup"><span data-stu-id="9c765-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="9c765-203">Ahora, vamos a agregar código que nos permite copiar un archivo desde una dirección URL a un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="9c765-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="9c765-204">Modifique `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="9c765-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="9c765-205">Un caso de uso importante de esta característica es cuando necesita mover datos de otro servicio en la nube (p. ej., AWS) a Azure.</span><span class="sxs-lookup"><span data-stu-id="9c765-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="9c765-206">Siempre que tengan una dirección URL que le proporcione acceso al recurso, podrá mover fácilmente ese recurso a blobs de Azure mediante el uso del método `TransferManager.CopyAsync`.</span><span class="sxs-lookup"><span data-stu-id="9c765-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="9c765-207">Este método también introduce un nuevo parámetro booleano.</span><span class="sxs-lookup"><span data-stu-id="9c765-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="9c765-208">El establecimiento de este parámetro en `true` indica que se desea hacer una copia asincrónica del lado servidor.</span><span class="sxs-lookup"><span data-stu-id="9c765-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="9c765-209">El establecimiento de este parámetro en `false` indica una copia sincrónica, lo que significa que el recurso se descarga primero en el equipo local y después se carga en el blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="9c765-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="9c765-210">Sin embargo, la copia asincrónica solo está disponible actualmente para copiar desde un recurso de Azure Storage a otro.</span><span class="sxs-lookup"><span data-stu-id="9c765-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="9c765-211">Transferencia entre blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="9c765-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="9c765-212">Otra característica que proporciona de forma única la Biblioteca de movimiento de datos es la capacidad de copiar desde un recurso de Azure Storage a otro.</span><span class="sxs-lookup"><span data-stu-id="9c765-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="9c765-213">Modifique `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="9c765-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="9c765-214">En este ejemplo, se establece el parámetro booleano de `TransferManager.CopyAsync` en `false` para indicar que desea hacer una copia sincrónica.</span><span class="sxs-lookup"><span data-stu-id="9c765-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="9c765-215">Esto significa que el recurso se descarga primero en la máquina local y después se carga en el blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="9c765-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="9c765-216">La opción de copia sincrónica es una excelente manera de asegurarse de que la operación de copia tiene una velocidad constante.</span><span class="sxs-lookup"><span data-stu-id="9c765-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="9c765-217">En cambio, la velocidad de una copia asincrónica del lado servidor depende del ancho de banda de red disponible en el servidor, el cual puede fluctuar.</span><span class="sxs-lookup"><span data-stu-id="9c765-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="9c765-218">Sin embargo, la copia sincrónica puede generar un costo de salida adicional en comparación con la copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="9c765-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="9c765-219">El enfoque recomendado es usar una copia asincrónica en una VM de Azure que se encuentre en la misma región que la cuenta de almacenamiento de origen, para evitar el costo de salida.</span><span class="sxs-lookup"><span data-stu-id="9c765-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9c765-220">Conclusión</span><span class="sxs-lookup"><span data-stu-id="9c765-220">Conclusion</span></span>
<span data-ttu-id="9c765-221">Nuestra aplicación de movimiento de datos ahora está completa.</span><span class="sxs-lookup"><span data-stu-id="9c765-221">Our data movement application is now complete.</span></span> <span data-ttu-id="9c765-222">[El ejemplo de código completo está disponible en GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="9c765-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c765-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c765-223">Next steps</span></span>
<span data-ttu-id="9c765-224">En esta introducción, hemos creado una aplicación que interactúa con Azure Storage y se ejecuta en Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="9c765-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="9c765-225">Esta introducción estaba dedicada a Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9c765-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="9c765-226">Sin embargo, estos mismos conocimientos pueden aplicarse a File Storage.</span><span class="sxs-lookup"><span data-stu-id="9c765-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="9c765-227">Para más información, visite la [documentación de referencia de la de datos de Azure Storage](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="9c765-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




