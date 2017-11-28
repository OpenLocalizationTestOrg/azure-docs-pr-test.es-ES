---
title: 'Tutorial: Uso de la biblioteca de cliente de Azure Batch para .NET | Microsoft Docs'
description: "Aprenda los conceptos básicos de Azure Batch y cree una solución sencilla mediante .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="24baa-103">Introducción a la creación de soluciones con la biblioteca de cliente de Batch para .NET</span><span class="sxs-lookup"><span data-stu-id="24baa-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="24baa-104">.NET</span><span class="sxs-lookup"><span data-stu-id="24baa-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="24baa-105">Python</span><span class="sxs-lookup"><span data-stu-id="24baa-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="24baa-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="24baa-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="24baa-107">En este artículo, se explican los aspectos básicos de [Azure Batch][azure_batch] y de la biblioteca [.NET de Batch][net_api] a medida que se analiza paso a paso un ejemplo de aplicación escrito en C#.</span><span class="sxs-lookup"><span data-stu-id="24baa-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="24baa-108">Examinaremos la forma en que esta aplicación de ejemplo aprovecha el servicio Batch para procesar una carga de trabajo paralela en la nube y cómo interactúa con [Azure Storage](../storage/common/storage-introduction.md) para almacenar provisionalmente archivos y recuperarlos.</span><span class="sxs-lookup"><span data-stu-id="24baa-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="24baa-109">Aprenderá un flujo de trabajo de la aplicación de Batch habitual y obtenga un conocimiento básico de los componentes principales de Batch, como trabajos, tareas, grupos y nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="24baa-110">![Flujo de trabajo de soluciones de Batch (básico)][11]</span><span class="sxs-lookup"><span data-stu-id="24baa-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="24baa-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="24baa-111">Prerequisites</span></span>
<span data-ttu-id="24baa-112">En este artículo se asume que tiene conocimientos prácticos de C# y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24baa-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="24baa-113">También se asume que puede cumplir los requisitos para la creación de cuentas que se especifican a continuación en Azure y los servicios Batch y Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="24baa-114">Cuentas</span><span class="sxs-lookup"><span data-stu-id="24baa-114">Accounts</span></span>
* <span data-ttu-id="24baa-115">**Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="24baa-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="24baa-116">**Cuenta de Batch**: una vez que tenga una suscripción a Azure, [cree una cuenta de Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="24baa-117">**Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24baa-118">Actualmente, Batch *solo* admite el tipo de cuenta de almacenamiento **de uso general**, tal y como se describe en el paso 5 de la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="24baa-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24baa-119">Visual Studio</span></span>
<span data-ttu-id="24baa-120">Debe tener **Visual Studio 2015 o superior** para compilar el proyecto de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="24baa-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="24baa-121">Puede encontrar versiones de prueba y de evaluación gratuita de Visual Studio en la [información general de los productos de Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="24baa-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="24baa-122">*DotNetTutorial* </span><span class="sxs-lookup"><span data-stu-id="24baa-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="24baa-123">El ejemplo [DotNetTutorial][github_dotnettutorial] es uno de los muchos ejemplos de código de Batch que se encuentran en el repositorio [azure-batch-samples][github_samples] de GitHub.</span><span class="sxs-lookup"><span data-stu-id="24baa-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="24baa-124">Para descargar todos los ejemplos, haga clic en **Clone or download > Download ZIP** (Clonar o descargar > Descargar ZIP) en la página principal del repositorio o haga clic en el vínculo de descarga directa [azure-batch-samples-master.zip][github_samples_zip].</span><span class="sxs-lookup"><span data-stu-id="24baa-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="24baa-125">Una vez extraído el contenido del archivo ZIP, puede encontrar la solución en la carpeta siguiente:</span><span class="sxs-lookup"><span data-stu-id="24baa-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="24baa-126">Explorador de Azure Batch (opcional)</span><span class="sxs-lookup"><span data-stu-id="24baa-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="24baa-127">El [Explorador de Azure Batch][github_batchexplorer] es una utilidad gratuita que se incluye en el repositorio [azure-batch-samples][github_samples] de GitHub.</span><span class="sxs-lookup"><span data-stu-id="24baa-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="24baa-128">Aunque esta utilidad no es necesaria para completar este tutorial, puede resultar útil para desarrollar y depurar las soluciones de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="24baa-129">Información general del proyecto de ejemplo DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="24baa-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="24baa-130">El código de ejemplo *DotNetTutorial* es una solución de Visual Studio que consta de dos proyectos: **DotNetTutorial** y **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="24baa-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="24baa-131">**DotNetTutorial** es la aplicación cliente que interactúa con los servicios Batch y Storage para ejecutar una carga de trabajo paralela en los nodos de proceso (máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="24baa-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="24baa-132">DotNetTutorial se ejecuta en la estación de trabajo local.</span><span class="sxs-lookup"><span data-stu-id="24baa-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="24baa-133">**TaskApplication** es el programa que se ejecuta en los nodos de proceso de Azure para realizar el trabajo real.</span><span class="sxs-lookup"><span data-stu-id="24baa-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="24baa-134">En el ejemplo, `TaskApplication.exe` analiza el texto de un archivo descargado de Azure Storage (el archivo de entrada).</span><span class="sxs-lookup"><span data-stu-id="24baa-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="24baa-135">Luego genera un archivo de texto (el archivo de salida) que contiene una lista de las tres palabras que más veces aparecen en el archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="24baa-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="24baa-136">Después de crear el archivo de salida, TaskApplication lo carga en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="24baa-137">Esto hace que esté disponible para la aplicación cliente para su descarga.</span><span class="sxs-lookup"><span data-stu-id="24baa-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="24baa-138">El proyecto TaskApplication se ejecuta en paralelo en varios nodos de ejecución en el servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="24baa-139">El siguiente diagrama ilustra las operaciones principales que realiza la aplicación cliente, *DotNetTutorial*, y la aplicación que ejecutan las tareas, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="24baa-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="24baa-140">Este flujo de trabajo básico es típico de muchas soluciones de proceso que se crean con Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="24baa-141">Aunque no muestra todas las características disponibles en el servicio Batch , casi todos los escenarios de Batch incluyen partes de este flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="24baa-142">![Flujo de trabajo de ejemplo de Batch][8]</span><span class="sxs-lookup"><span data-stu-id="24baa-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="24baa-143">**Paso 1.**</span><span class="sxs-lookup"><span data-stu-id="24baa-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="24baa-144">Crear **contenedores** en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="24baa-145">
[**Paso 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="24baa-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="24baa-146">Cargar los archivos de aplicación y los archivos de entrada de la tarea en los contenedores.</span><span class="sxs-lookup"><span data-stu-id="24baa-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="24baa-147">
[**Paso 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="24baa-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="24baa-148">Cree un **grupo** de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="24baa-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="24baa-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="24baa-150">El grupo **StartTask** descarga los archivos binarios de la tarea (TaskApplication) en los nodos cuando se unen al grupo.</span><span class="sxs-lookup"><span data-stu-id="24baa-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="24baa-151">
[**Paso 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="24baa-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="24baa-152">Cree un **trabajo** de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="24baa-153">
[**Paso 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="24baa-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="24baa-154">Agregue **tareas** al trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="24baa-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="24baa-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="24baa-156">Las tareas se programan para ejecutarse en los nodos.</span><span class="sxs-lookup"><span data-stu-id="24baa-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="24baa-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="24baa-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="24baa-158">Cada tarea descarga sus datos de entrada de Azure Storage y comienza la ejecución.</span><span class="sxs-lookup"><span data-stu-id="24baa-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="24baa-159">
[**Paso 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="24baa-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="24baa-160">Supervisar las tareas.</span><span class="sxs-lookup"><span data-stu-id="24baa-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="24baa-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="24baa-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="24baa-162">A medida que se completan las tareas, cargan sus datos de salida en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="24baa-163">
[**Paso 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="24baa-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="24baa-164">Descargar el resultado de la tarea de Storage</span><span class="sxs-lookup"><span data-stu-id="24baa-164">Download task output from Storage.</span></span>

<span data-ttu-id="24baa-165">Como se ha indicado, no todas las soluciones de Batch realizan estos mismos pasos y puede haber muchos otros; sin embargo, la aplicación de ejemplo *DotNetTutorial* muestra los procesos comunes que se encuentran en una solución de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="24baa-166">Creación del proyecto de ejemplo *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="24baa-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="24baa-167">Para poder ejecutar correctamente el ejemplo, debe especificar las credenciales de las cuentas tanto de Batch como de Storage en el archivo `Program.cs` del proyecto *DotNetTutorial*.</span><span class="sxs-lookup"><span data-stu-id="24baa-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="24baa-168">Si aún no lo ha hecho, abra la solución en Visual Studio, para lo que debe hacer doble clic en el archivo de solución `DotNetTutorial.sln` .</span><span class="sxs-lookup"><span data-stu-id="24baa-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="24baa-169">También puede abrirla desde el propio Visual Studio haciendo clic en **Archivo > Abrir > Proyecto o solución**.</span><span class="sxs-lookup"><span data-stu-id="24baa-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="24baa-170">Abra `Program.cs` en el proyecto *DotNetTutorial* .</span><span class="sxs-lookup"><span data-stu-id="24baa-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="24baa-171">Luego, agregue las credenciales en la parte superior del archivo como se ha especificado:</span><span class="sxs-lookup"><span data-stu-id="24baa-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="24baa-172">Como ya se ha mencionado, ahora debe especificar las credenciales de una cuenta de almacenamiento de **uso general** en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="24baa-173">Las aplicaciones de Batch usan almacenamiento de blobs en la cuenta de almacenamiento de **uso general**.</span><span class="sxs-lookup"><span data-stu-id="24baa-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="24baa-174">No especifique las credenciales de una cuenta de almacenamiento que se haya creado mediante la selección del tipo de cuenta *Blob storage*.</span><span class="sxs-lookup"><span data-stu-id="24baa-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="24baa-175">Puede buscar las credenciales de las cuentas de Batch y de Storage en la hoja de la cuenta de cada uno de estos servicios en [Azure Portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="24baa-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="24baa-176">![Credenciales de Batch en el portal][9]
![Credenciales de Storage en el portal][10]</span><span class="sxs-lookup"><span data-stu-id="24baa-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="24baa-177">Tras actualizar el proyecto con sus credenciales, haga clic con el botón derecho en la solución en el Explorador de soluciones y haga clic en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="24baa-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="24baa-178">Si se le solicita, confirme la restauración de los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="24baa-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="24baa-179">Si los paquetes NuGet no se restauran automáticamente o si aparecen errores relacionados con la restauración de los paquetes, asegúrese de que el [Administrador de paquetes NuGet][nuget_packagemgr] está instalado y</span><span class="sxs-lookup"><span data-stu-id="24baa-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="24baa-180">habilite la descarga de los paquetes que falten.</span><span class="sxs-lookup"><span data-stu-id="24baa-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="24baa-181">Para habilitar la descarga de paquetes, consulte el tema sobre la [habilitación de la restauración de paquetes durante la compilación][nuget_restore].</span><span class="sxs-lookup"><span data-stu-id="24baa-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="24baa-182">En las secciones siguientes, se desglosarán los pasos que lleva a cabo la aplicación de ejemplo para procesar una carga de trabajo en el servicio Batch y se explicarán dichos pasos con detalle.</span><span class="sxs-lookup"><span data-stu-id="24baa-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="24baa-183">Es aconsejable consultar la solución abierta en Visual Studio a medida que se avanza en este artículo, ya que no se tratan todas las líneas de código del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="24baa-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="24baa-184">Para comenzar con el paso 1, vaya a la parte superior del método `MainAsync` en el archivo `Program.cs` del proyecto *DotNetTutorial*.</span><span class="sxs-lookup"><span data-stu-id="24baa-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="24baa-185">Los pasos que se describen a continuación siguen aproximadamente la progresión de las llamadas al método en `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="24baa-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="24baa-186">Paso 1: Crear contenedores de Storage</span><span class="sxs-lookup"><span data-stu-id="24baa-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="24baa-187">![Crear contenedores en Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="24baa-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="24baa-188">Batch incluye compatibilidad integrada para interactuar con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="24baa-189">Los contenedores de la cuenta de Storage proporcionarán los archivos que necesitarán las tareas que se ejecutan en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="24baa-190">Los contenedores también proporcionan un lugar para almacenar los datos de salida que producen las tareas.</span><span class="sxs-lookup"><span data-stu-id="24baa-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="24baa-191">Lo primero que hace la aplicación cliente *DotNetTutorial* es crear tres contenedores en [Azure Blob Storage](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="24baa-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="24baa-192">**application**: este contenedor almacenará la aplicación ejecutada por las tareas, así como todas sus dependencias, como los archivos DLL.</span><span class="sxs-lookup"><span data-stu-id="24baa-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="24baa-193">**input**: las tareas descargarán los archivos de datos que se van a procesar desde el contenedor *input* .</span><span class="sxs-lookup"><span data-stu-id="24baa-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="24baa-194">**output**: cuando las tareas completen el procesamiento de los archivos de entrada, cargarán los resultados en el contenedor *output* .</span><span class="sxs-lookup"><span data-stu-id="24baa-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="24baa-195">Para interactuar con una cuenta de Storage y crear contenedores, usamos la [biblioteca de cliente de Azure Storage para .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="24baa-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="24baa-196">Creamos una referencia a la cuenta con [CloudStorageAccount][net_cloudstorageaccount] y, desde dicha referencia, creamos un objeto [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="24baa-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="24baa-197">Usamos la referencia `blobClient` en toda la aplicación y la pasamos como parámetro a varios métodos.</span><span class="sxs-lookup"><span data-stu-id="24baa-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="24baa-198">Podemos ver un ejemplo de esto en el bloque de código que aparece inmediatamente después de código anterior, donde llamamos a `CreateContainerIfNotExistAsync` para crear realmente los contenedores.</span><span class="sxs-lookup"><span data-stu-id="24baa-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="24baa-199">Una vez creados los contenedores, la aplicación ya puede cargar los archivos que utilizarán las tareas.</span><span class="sxs-lookup"><span data-stu-id="24baa-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="24baa-200">[Uso de Blob Storage desde .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ofrece una buena introducción sobre cómo trabajar con blobs y contenedores de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="24baa-201">Al empezar a trabajar con Batch, debe encontrarse cerca de la parte superior de la lista de lectura.</span><span class="sxs-lookup"><span data-stu-id="24baa-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="24baa-202">Paso 2: Cargar la aplicación de tarea y los archivos de datos</span><span class="sxs-lookup"><span data-stu-id="24baa-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="24baa-203">![Cargar una aplicación de tarea y archivos de entrada (datos) en los contenedores][2]
</span><span class="sxs-lookup"><span data-stu-id="24baa-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="24baa-204">En la operación de carga de archivos, *DotNetTutorial* define en primer lugar las colecciones de las rutas de acceso a los archivos de **application** e **input**, tal como existen en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="24baa-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="24baa-205">Después cargará estos archivos en los contenedores que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="24baa-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="24baa-206">En `Program.cs` , hay dos métodos que intervienen en el proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="24baa-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="24baa-207">`UploadFilesToContainerAsync`: este método devuelve una colección de objetos [ResourceFile][net_resourcefile] (que se explican a continuación) y llama internamente a `UploadFileToContainerAsync` para cargar todos los archivos que se pasan en el parámetro *filePaths*.</span><span class="sxs-lookup"><span data-stu-id="24baa-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="24baa-208">`UploadFileToContainerAsync`: es el método que realiza la carga de archivos y crea los objetos [ResourceFile][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="24baa-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="24baa-209">Después de cargar el archivo, obtiene una firma de acceso compartido (SAS) para el archivo y devuelve un objeto ResourceFile que lo representa.</span><span class="sxs-lookup"><span data-stu-id="24baa-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="24baa-210">A continuación también se tratan las firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="24baa-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="24baa-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="24baa-211">ResourceFiles</span></span>
<span data-ttu-id="24baa-212">Un objeto [ResourceFile][net_resourcefile] proporciona tareas de Batch con la dirección URL a un archivo de Azure Storage que se descarga en un nodo de proceso antes de que la tarea se ejecute.</span><span class="sxs-lookup"><span data-stu-id="24baa-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="24baa-213">La propiedad [ResourceFile.BlobSource][net_resourcefile_blobsource] especifica la dirección URL completa del archivo, tal como existe en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="24baa-214">La dirección URL también puede incluir una firma de acceso compartido (SAS) que proporcione acceso seguro al archivo.</span><span class="sxs-lookup"><span data-stu-id="24baa-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="24baa-215">La mayoría de los tipos de tareas de .NET de Batch contienen una propiedad *ResourceFiles*, que incluye:</span><span class="sxs-lookup"><span data-stu-id="24baa-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="24baa-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="24baa-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="24baa-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="24baa-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="24baa-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="24baa-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="24baa-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="24baa-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="24baa-220">La aplicación de ejemplo DotNetTutorial no usa los tipos de tarea JobPreparationTask o JobReleaseTask. Para más información acerca de estos tipos de tarea, consulte [Ejecución de tareas de preparación y finalización de trabajos en nodos de proceso de Azure Batch](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="24baa-221">Firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="24baa-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="24baa-222">Las firmas de acceso compartido son cadenas que, cuando se incluyen como parte de una dirección URL, proporcionan acceso seguro a los contenedores y blobs de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="24baa-223">La aplicación DotNetTutorial utiliza direcciones URL de firma de acceso compartido de blobs y contenedores, y muestra cómo obtener estas cadenas de firma de acceso compartido en el servicio Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="24baa-224">**Firmas de acceso compartido de blobs**: la clase StartTask del grupo en DotNetTutorial usa firmas de acceso compartido de blobs al descargar los archivos binarios de la aplicación y los archivos de datos de entrada de Storage (consulte el paso 3).</span><span class="sxs-lookup"><span data-stu-id="24baa-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="24baa-225">El método `UploadFileToContainerAsync` del archivo `Program.cs` de DotNetTutorial contiene el código que obtiene la firma de acceso compartido de cada blob.</span><span class="sxs-lookup"><span data-stu-id="24baa-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="24baa-226">Para ello, llama a [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="24baa-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="24baa-227">**Firmas de acceso compartido de contenedores**: cuando cada tarea finaliza su trabajo en el nodo de proceso, carga su archivo de salida en el contenedor *output* de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="24baa-228">Para ello, TaskApplication usa una firma de acceso compartido de contenedor que proporciona acceso de escritura al contenedor como parte de la ruta de acceso al cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="24baa-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="24baa-229">La obtención de la firma de acceso compartido del contenedor se realiza de manera similar que cuando se obtiene la firma de acceso compartido de un blob.</span><span class="sxs-lookup"><span data-stu-id="24baa-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="24baa-230">En DotNetTutorial, observará que el método auxiliar `GetContainerSasUrl` llama a [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="24baa-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="24baa-231">En "Paso 6: Supervisar tareas", obtendrá más información acerca de la forma en que TaskApplication usa la firma de acceso compartido de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="24baa-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="24baa-232">Para más información acerca de cómo proporcionar acceso seguro a los datos de una cuenta de Storage, consulte la serie de dos partes acerca de las firmas de acceso compartido, [Parte 1: Descripción del modelo SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) y [Parte 2: Creación y uso de una SAS con Blob Storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="24baa-233">Paso 3: Crear el grupo de Batch</span><span class="sxs-lookup"><span data-stu-id="24baa-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="24baa-234">![Crear un grupo de Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="24baa-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="24baa-235">Un **grupo** de Batch es una colección de nodos de proceso (máquinas virtuales) en los que Batch ejecuta tareas de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="24baa-236">Después de cargar la aplicación y los archivos de datos a la cuenta de Storage con las API de Azure Storage, *DotNetTutorial* comienza a realizar llamadas al servicio de Batch con las API proporcionadas por la biblioteca .NET de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="24baa-237">El código crea primero una clase [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="24baa-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="24baa-238">Después, en el ejemplo se crea un grupo de nodos de proceso en la cuenta de Batch con una llamada a `CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="24baa-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="24baa-239">`CreatePoolIfNotExistsAsync` usa el método [BatchClient.PoolOperations.CreatePool][net_pool_create] para crear un grupo en el servicio Batch:</span><span class="sxs-lookup"><span data-stu-id="24baa-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="24baa-240">Cuando se crea un grupo con [CreatePool][net_pool_create], se especifican varios parámetros, como el número de nodos de proceso, el [tamaño de los nodos](../cloud-services/cloud-services-sizes-specs.md) y el sistema operativo de los nodos.</span><span class="sxs-lookup"><span data-stu-id="24baa-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="24baa-241">En *DotNetTutorial*, usamos [CloudServiceConfiguration][net_cloudserviceconfiguration] para especificar Windows Server 2012 R2 en [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="24baa-242">También puede crear grupos de nodos de proceso que son instancias de Azure Virtual Machines (VM) especificando [VirtualMachineConfiguration][net_virtualmachineconfiguration] para el grupo.</span><span class="sxs-lookup"><span data-stu-id="24baa-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="24baa-243">Puede crear un grupo de nodos de proceso de máquinas virtuales a partir de imágenes de Windows o [Linux](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="24baa-244">El origen de las imágenes de las máquinas virtuales puede ser:</span><span class="sxs-lookup"><span data-stu-id="24baa-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="24baa-245">[Azure Virtual Machines Marketplace][vm_marketplace], que proporciona imágenes de Windows y Linux que están listas para su uso.</span><span class="sxs-lookup"><span data-stu-id="24baa-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="24baa-246">Una imagen personalizada preparada y proporcionada por el usuario.</span><span class="sxs-lookup"><span data-stu-id="24baa-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="24baa-247">Para más información acerca de las imágenes personalizadas, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="24baa-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24baa-248">Se cobrará por recursos de proceso en Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="24baa-249">Para minimizar los costos, puede reducir `targetDedicatedComputeNodes` a 1 antes de ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="24baa-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="24baa-250">Además de estas propiedades del nodo físico, también puede especificar una clase [StartTask][net_pool_starttask] para el grupo.</span><span class="sxs-lookup"><span data-stu-id="24baa-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="24baa-251">StartTask se ejecutará en cada nodo cuando este se una al grupo, así como cada vez que se reinicie.</span><span class="sxs-lookup"><span data-stu-id="24baa-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="24baa-252">Esta clase es especialmente útil para instalar aplicaciones en nodos de ejecución antes de la ejecución de tareas.</span><span class="sxs-lookup"><span data-stu-id="24baa-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="24baa-253">Por ejemplo, si las tareas procesan los datos mediante scripts de Python, puede usar una clase StartTask para instalar Python en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="24baa-254">En este ejemplo de aplicación, StartTask copia los archivos que descarga de Storage (que se especifican mediante la propiedad [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles]) desde el directorio de trabajo de StartTask hasta el directorio compartido al que pueden acceder *todas* las tareas que se ejecutan en el nodo.</span><span class="sxs-lookup"><span data-stu-id="24baa-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="24baa-255">Básicamente, esto copia `TaskApplication.exe` y sus dependencias en el directorio compartido de cada nodo cuando el nodo se une al grupo, con el fin de que las tareas que se ejecuten en el nodo puedan acceder a él.</span><span class="sxs-lookup"><span data-stu-id="24baa-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="24baa-256">La característica **paquetes de aplicación** de Azure Batch proporciona otra manera de implementar la aplicación en los nodos de proceso de un grupo.</span><span class="sxs-lookup"><span data-stu-id="24baa-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="24baa-257">Consulte [Implementación de aplicaciones en nodos de proceso con paquetes de aplicaciones de Batch](batch-application-packages.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="24baa-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="24baa-258">En el fragmento de código anterior, también cabe destacar el uso de dos variables de entorno en la propiedad *CommandLine* de StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` y `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="24baa-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="24baa-259">Cada nodo de proceso de un grupo de Batch se configura automáticamente con un número de variables de entorno específicas de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="24baa-260">Todos los procesos que ejecute una tarea tienen acceso a estas variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="24baa-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="24baa-261">Para más información acerca de las variables de entorno disponibles en los nodos de proceso de un grupo de Batch, así como acerca de los directorios de trabajo de las tareas, consulte las secciones [Configuración del entorno para las tareas](batch-api-basics.md#environment-settings-for-tasks) y [Archivos y directorios](batch-api-basics.md#files-and-directories) de [Introducción a las características de Azure Batch para desarrolladores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="24baa-262">Paso 4: Crear el trabajo de Batch</span><span class="sxs-lookup"><span data-stu-id="24baa-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="24baa-263">![Crear un trabajo de Batch][4]</span><span class="sxs-lookup"><span data-stu-id="24baa-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="24baa-264">Un **trabajo** de Batch es una colección de tareas y está asociado a un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="24baa-265">Las tareas de un trabajo se ejecutan en los nodos de proceso del grupo asociado.</span><span class="sxs-lookup"><span data-stu-id="24baa-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="24baa-266">Se puede usar un trabajo no solo para la organización y seguimiento de las tareas en las cargas de trabajo relacionadas, sino también para imponer ciertas restricciones, como el tiempo máximo de ejecución del trabajo (y, por extensión, sus tareas), así como la prioridad del trabajo, en relación con los restantes trabajos de la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="24baa-267">Sin embargo, en este ejemplo, el trabajo está asociado solo con el grupo que se creó en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="24baa-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="24baa-268">No hay propiedades adicionales configuradas.</span><span class="sxs-lookup"><span data-stu-id="24baa-268">No additional properties are configured.</span></span>

<span data-ttu-id="24baa-269">Todos los trabajos de Batch están asociados a un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="24baa-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="24baa-270">Esta asociación indica en qué nodos se ejecutarán las tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="24baa-271">Para especificarlo, use la propiedad [CloudJob.PoolInformation][net_job_poolinfo], como se muestra en el siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="24baa-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="24baa-272">Ahora que se ha creado un trabajo, se agregan las tareas para realizar dicho trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="24baa-273">Paso 5: Agregar tareas al trabajo</span><span class="sxs-lookup"><span data-stu-id="24baa-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="24baa-274">![Agregar tareas al trabajo][5]</span><span class="sxs-lookup"><span data-stu-id="24baa-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="24baa-275">
*(1) Las tareas se agregan al trabajo, (2) las tareas se programan para ejecutarse en los nodos y (3) las tareas descargan los archivos de datos que se van a procesar*</span><span class="sxs-lookup"><span data-stu-id="24baa-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="24baa-276">Las **tareas** de Batch son unidades de trabajo individuales que se ejecutan en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="24baa-277">Una tarea tiene una línea de comandos y ejecuta los scripts o archivos ejecutables que se especifican en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="24baa-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="24baa-278">Para realizar el trabajo, las tareas deben agregarse a un trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="24baa-279">Cada tarea [CloudTask][net_task] se configura mediante una propiedad de línea de comandos y [ResourceFiles][net_task_resourcefiles] (igual que la tarea StartTask del grupo) que la tarea descarga en el nodo antes de que su línea de comandos se ejecute automáticamente.</span><span class="sxs-lookup"><span data-stu-id="24baa-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="24baa-280">En el proyecto de ejemplo *DotNetTutorial* , cada tarea procesa un solo archivo.</span><span class="sxs-lookup"><span data-stu-id="24baa-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="24baa-281">Por lo tanto, su colección ResourceFiles contiene un único elemento.</span><span class="sxs-lookup"><span data-stu-id="24baa-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="24baa-282">Cuando acceden a variables de entorno como `%AZ_BATCH_NODE_SHARED_DIR%` o ejecutan una aplicación que no se encuentra en el objeto `PATH` del nodo, las líneas de comandos de la tarea deben tener el prefijo `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="24baa-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="24baa-283">Así se ejecutará explícitamente el intérprete de comandos y se dará la orden de finalización después de ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="24baa-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="24baa-284">Este requisito no es necesario si las tareas ejecutan una aplicación en el elemento `PATH` del nodo (como *robocopy.exe* o *powershell.exe*) y no se utilizan variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="24baa-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="24baa-285">En el bucle `foreach` del fragmento de código anterior, puede ver que la línea de comandos de la tarea se construye de forma que se pasan tres argumentos de línea de comandos a *TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="24baa-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="24baa-286">El **primer argumento** es la ruta de acceso del archivo que se va a procesar.</span><span class="sxs-lookup"><span data-stu-id="24baa-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="24baa-287">Se trata de la ruta de acceso local al archivo, tal como existe en el nodo.</span><span class="sxs-lookup"><span data-stu-id="24baa-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="24baa-288">Cuando se creó el objeto ResourceFile de `UploadFileToContainerAsync` , se usó el nombre de archivo para esta propiedad (como un parámetro del constructor ResourceFile).</span><span class="sxs-lookup"><span data-stu-id="24baa-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="24baa-289">Esto indica que el archivo puede encontrarse en el mismo directorio que *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="24baa-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="24baa-290">El **segundo argumento** especifica que las *N* palabras más usadas deben escribirse en el archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="24baa-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="24baa-291">En el ejemplo, esto se codifica de forma rígida, con el fin de que las tres palabras más usadas se escriban en el archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="24baa-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="24baa-292">El **tercer argumento** es la firma de acceso compartido (SAS) que proporciona acceso de escritura al contenedor **output** de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="24baa-293">*TaskApplication.exe* utiliza la dirección URL de esta firma de acceso compartido al cargar el archivo de salida en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="24baa-294">El código de este proceso se puede encontrar en el método `UploadFileToContainer` del archivo `Program.cs` del proyecto TaskApplication:</span><span class="sxs-lookup"><span data-stu-id="24baa-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="24baa-295">Paso 6: Supervisar tareas</span><span class="sxs-lookup"><span data-stu-id="24baa-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="24baa-296">![Supervisar tareas][6]</span><span class="sxs-lookup"><span data-stu-id="24baa-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="24baa-297">
*La aplicación cliente (1) supervisa las tareas para comprobar que han finalizado y que el estado es correcto y (2) las tareas cargan los datos resultantes en Azure Storage.*</span><span class="sxs-lookup"><span data-stu-id="24baa-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="24baa-298">Cuando las tareas se agregan a un trabajo, automáticamente se ponen en cola y se programan para su ejecución en los nodos de ejecución del grupo asociado al trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="24baa-299">Según la configuración que especifique, Batch controla la administración de las colas, programación y reintentos de todas las tareas, así como otros cometidos de administración de tareas por usted.</span><span class="sxs-lookup"><span data-stu-id="24baa-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="24baa-300">Existen varios enfoques para supervisar la ejecución de tareas.</span><span class="sxs-lookup"><span data-stu-id="24baa-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="24baa-301">DotNetTutorial muestra un ejemplo sencillo que informa únicamente sobre la finalización y los estados de error y de realización correcta de la tarea.</span><span class="sxs-lookup"><span data-stu-id="24baa-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="24baa-302">En el método `MonitorTasks` del archivo `Program.cs` de DotNetTutorial, hay tres conceptos de .NET de Batch que merecen una explicación.</span><span class="sxs-lookup"><span data-stu-id="24baa-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="24baa-303">Dichos conceptos se enumeran a continuación en su orden de aparición:</span><span class="sxs-lookup"><span data-stu-id="24baa-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="24baa-304">**ODATADetailLevel**: es esencial especificar [ODATADetailLevel][net_odatadetaillevel] en las operaciones de lista (por ejemplo, obtener una lista de las tareas de un trabajo) para garantizar el rendimiento de una aplicación de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="24baa-305">Agregue [Consulta eficaz del servicio Azure Batch](batch-efficient-list-queries.md) a su lista de lecturas si planea realizar cualquier tipo de supervisión del estado en las aplicaciones de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="24baa-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] proporciona a aplicaciones de .NET de Batch utilidades auxiliares para la supervisión de los estados de las tareas.</span><span class="sxs-lookup"><span data-stu-id="24baa-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="24baa-307">En `MonitorTasks`, *DotNetTutorial* espera hasta que todas las tareas alcancen el estado [TaskState.Completed][net_taskstate] dentro de un límite de tiempo.</span><span class="sxs-lookup"><span data-stu-id="24baa-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="24baa-308">Luego finaliza el trabajo.</span><span class="sxs-lookup"><span data-stu-id="24baa-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="24baa-309">**TerminateJobAsync**: la finalización de un trabajo con [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (o JobOperations.TerminateJob de bloqueo) marca el trabajo como completado.</span><span class="sxs-lookup"><span data-stu-id="24baa-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="24baa-310">Esta operación es esencial si la solución de Batch usa [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="24baa-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="24baa-311">Se trata de un tipo de tarea especial, que se describe en [areas de preparación y finalización de trabajos](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="24baa-312">A continuación, se muestra el método `MonitorTasks` del archivo `Program.cs` de *DotNetTutorial*:</span><span class="sxs-lookup"><span data-stu-id="24baa-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="24baa-313">Paso 7: Descargar el resultado de la tarea</span><span class="sxs-lookup"><span data-stu-id="24baa-313">Step 7: Download task output</span></span>
<span data-ttu-id="24baa-314">![Descargar el resultado de la tarea de Storage][7]</span><span class="sxs-lookup"><span data-stu-id="24baa-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="24baa-315">Ahora que se ha completado el trabajo, el resultado de las tareas se puede descargar desde Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24baa-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="24baa-316">Esto se realiza con una llamada a `DownloadBlobsFromContainerAsync` en el archivo `Program.cs` de *DotNetTutorial*:</span><span class="sxs-lookup"><span data-stu-id="24baa-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="24baa-317">La llamada a `DownloadBlobsFromContainerAsync` en la aplicación *DotNetTutorial* especifica que los archivos se deben descargar en la carpeta `%TEMP%`.</span><span class="sxs-lookup"><span data-stu-id="24baa-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="24baa-318">Puede modificar si lo desea esta ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="24baa-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="24baa-319">Paso 8: Eliminar contenedores</span><span class="sxs-lookup"><span data-stu-id="24baa-319">Step 8: Delete containers</span></span>
<span data-ttu-id="24baa-320">Como se le cobrará por los datos que residen en Azure Storage, siempre es una buena idea quitar los blobs que ya no sean necesarios para los trabajos de Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="24baa-321">En el archivo `Program.cs` de DotNetTutorial, esto se realiza con tres llamadas al método auxiliar `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="24baa-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="24baa-322">El propio método simplemente obtiene una referencia al contenedor y después llama a [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="24baa-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="24baa-323">Paso 9: Eliminar el trabajo y el grupo</span><span class="sxs-lookup"><span data-stu-id="24baa-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="24baa-324">En el último paso, se le pedirá que elimine el trabajo y el grupo que creó la aplicación DotNetTutorial.</span><span class="sxs-lookup"><span data-stu-id="24baa-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="24baa-325">Aunque no se cobran los trabajos y las tareas, *sí* se cobran los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="24baa-326">Por consiguiente, se recomienda asignar solo los nodos necesarios.</span><span class="sxs-lookup"><span data-stu-id="24baa-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="24baa-327">La eliminación de los grupos que no se usen puede formar parte del proceso de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="24baa-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="24baa-328">Las propiedades [JobOperations][net_joboperations] y [PoolOperations][net_pooloperations] de BatchClient tienen sus métodos de eliminación correspondientes, a los que se llama si el usuario confirma la eliminación:</span><span class="sxs-lookup"><span data-stu-id="24baa-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="24baa-329">Tenga en cuenta que los recursos de proceso se cobran; la eliminación de grupos sin usar reducirá el costo.</span><span class="sxs-lookup"><span data-stu-id="24baa-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="24baa-330">Tenga en cuenta que al eliminar un grupo se eliminan todos los nodos de proceso del grupo y que los datos de los nodos no se podrán recuperar cuando se elimine el grupo.</span><span class="sxs-lookup"><span data-stu-id="24baa-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="24baa-331">Ejecución del ejemplo de *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="24baa-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="24baa-332">Al ejecutar la aplicación de ejemplo, el resultado de la consola será similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="24baa-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="24baa-333">Durante la ejecución, experimentará una pausa en `Awaiting task completion, timeout in 00:30:00...` mientras se inician los nodos de proceso del grupo.</span><span class="sxs-lookup"><span data-stu-id="24baa-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="24baa-334">Use [Azure Portal][azure_portal] para supervisar el grupo, los nodos de proceso, el trabajo y las tareas durante la ejecución y después de ella.</span><span class="sxs-lookup"><span data-stu-id="24baa-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="24baa-335">Use [Azure Portal][azure_portal] o el [Explorador de Azure Storage][storage_explorers] para ver los recursos de Storage (contenedores y blobs) que crea la aplicación.</span><span class="sxs-lookup"><span data-stu-id="24baa-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="24baa-336">El tiempo de ejecución es de **aproximadamente de 5 minutos** cuando se ejecuta la aplicación con su configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="24baa-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="24baa-337">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24baa-337">Next steps</span></span>
<span data-ttu-id="24baa-338">Puede realizar todos los cambios que desee en *DotNetTutorial* y *TaskApplication* para experimentar con distintos escenarios de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="24baa-339">Por ejemplo, pruebe a agregar a *TaskApplication* un retraso en la ejecución (por ejemplo, con [Thread.Sleep][net_thread_sleep]) para simular tareas de ejecución prolongada y supervisarlas en el portal.</span><span class="sxs-lookup"><span data-stu-id="24baa-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="24baa-340">Pruebe a agregar más tareas o a ajustar el número de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="24baa-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="24baa-341">Agregue lógica para buscar un grupo existente y permitir su uso para reducir el tiempo de ejecución (*sugerencia*: extraiga `ArticleHelpers.cs` en el proyecto [Microsoft.Azure.Batch.Samples.Common][github_samples_common] de [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="24baa-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="24baa-342">Ahora que está familiarizado con el flujo de trabajo básico de una solución de Batch, ha llegado el momento de adentrarse en las características adicionales del servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="24baa-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="24baa-343">Consulte el artículo [Información general de las características de Azure Batch](batch-api-basics.md) , que es especialmente recomendable si no se conoce el servicio.</span><span class="sxs-lookup"><span data-stu-id="24baa-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="24baa-344">Comience por los restantes artículos de desarrollo de Batch, en la sección **Desarrollo en profundidad** de la [ruta de aprendizaje de Batch][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="24baa-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="24baa-345">Consulte otra implementación del procesamiento de la carga de trabajo de "las N palabras más usadas" con Batch en el ejemplo [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="24baa-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="24baa-346">Revise las [notas de la versión](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) de la biblioteca de Batch para .NET para ver los cambios más recientes en la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="24baa-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Crear contenedores en Azure Storage"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Cargar una aplicación de tarea y archivos de entrada (datos) en los contenedores"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Crear el grupo de Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Crear trabajo de Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Agregar tareas al trabajo"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Supervisar tareas"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Descargar el resultado de la tarea de Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Flujo de trabajo de soluciones de Batch (diagrama completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenciales de Batch en el portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenciales de Storage en el portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Flujo de trabajo de soluciones de Batch (diagrama mínimo)"
