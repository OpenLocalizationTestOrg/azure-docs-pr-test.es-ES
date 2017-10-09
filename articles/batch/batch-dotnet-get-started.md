---
title: 'aaaTutorial: utilizar la biblioteca cliente en hello Azure Batch para .NET | Documentos de Microsoft'
description: "Obtenga información acerca de los conceptos básicos de Azure Batch hello y generar una solución simple con. NET."
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
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="8c2dd-103">Empezar a crear soluciones a la biblioteca de cliente de hello Batch para .NET</span><span class="sxs-lookup"><span data-stu-id="8c2dd-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c2dd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8c2dd-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="8c2dd-105">Python</span><span class="sxs-lookup"><span data-stu-id="8c2dd-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="8c2dd-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8c2dd-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="8c2dd-107">Obtenga información acerca de los conceptos básicos de Hola de [Azure Batch] [ azure_batch] hello y [.NET de lotes] [ net_api] biblioteca en este artículo tal y como se describe un paso de la aplicación de ejemplo en C# por paso.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="8c2dd-108">Veremos cómo aprovecha la aplicación de ejemplo de Hola Hola lote servicio tooprocess una carga de trabajo paralelo en la nube de Hola y cómo interactúa con [el almacenamiento de Azure](../storage/common/storage-introduction.md) para almacenamiento provisional de archivo y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="8c2dd-109">Podrá Obtenga información acerca de un flujo de trabajo de aplicación común de lote y obtener una descripción de base de componentes principales Hola de lote como trabajos, tareas, grupos y nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="8c2dd-110">![Flujo de trabajo de soluciones de Batch (básico)][11]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="8c2dd-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8c2dd-111">Prerequisites</span></span>
<span data-ttu-id="8c2dd-112">En este artículo se asume que tiene conocimientos prácticos de C# y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="8c2dd-113">También se da por supuesto que es capaz de toosatisfy Hola creación requisitos de las cuentas que se especifican a continuación para Azure y Hola por lotes y los servicios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="8c2dd-114">Cuentas</span><span class="sxs-lookup"><span data-stu-id="8c2dd-114">Accounts</span></span>
* <span data-ttu-id="8c2dd-115">**Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="8c2dd-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="8c2dd-116">**Cuenta de Batch**: una vez que tenga una suscripción a Azure, [cree una cuenta de Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="8c2dd-117">**Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c2dd-118">Procesar por lotes admite actualmente *sólo* hello **general** tipo de cuenta de almacenamiento, tal como se describe en el paso 5 de # [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [acerca de Azure las cuentas de almacenamiento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="8c2dd-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c2dd-119">Visual Studio</span></span>
<span data-ttu-id="8c2dd-120">Debe tener **Visual Studio 2015 o versiones más recientes** toobuild proyecto de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="8c2dd-121">Puede encontrar versiones gratuitas y de prueba de Visual Studio en hello [información general de productos de Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="8c2dd-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="8c2dd-122">*DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="8c2dd-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="8c2dd-123">Hola [DotNetTutorial] [ github_dotnettutorial] ejemplo es uno de los muchos ejemplos de código de proceso por lotes que se encuentran en Hola de hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="8c2dd-124">Puede descargar todos los ejemplos de hello haciendo clic en **clon o una descarga > Download ZIP** en página de inicio del repositorio de hello, o haciendo clic en hello [azure-lote-ejemplos-master.zip] [ github_samples_zip]vínculo de descarga directa.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="8c2dd-125">Una vez que haya extraído contenido Hola del archivo ZIP de hello, puede encontrar soluciones Hola Hola después de la carpeta:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="8c2dd-126">Explorador de Azure Batch (opcional)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="8c2dd-127">Hola [Explorador de lote de Azure] [ github_batchexplorer] es una utilidad gratuita que se incluye en hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="8c2dd-128">Mientras no se requiere toocomplete este tutorial, puede ser útil al desarrollar y depurar las soluciones de lote.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="8c2dd-129">Información general del proyecto de ejemplo DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="8c2dd-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="8c2dd-130">Hola *DotNetTutorial* ejemplo de código es una solución de Visual Studio que consta de dos proyectos: **DotNetTutorial** y **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="8c2dd-131">**DotNetTutorial** es aplicación de cliente de Hola que interactúa con tooexecute de servicios de almacenamiento y por lotes Hola una carga de trabajo paralelo en nodos de proceso (máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="8c2dd-132">DotNetTutorial se ejecuta en la estación de trabajo local.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="8c2dd-133">**TaskApplication** es programa Hola que se ejecuta en nodos de proceso de trabajo real de Azure tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="8c2dd-134">En el ejemplo de Hola, `TaskApplication.exe` analiza Hola texto en un archivo descargado desde el almacenamiento de Azure (archivo de entrada de hello).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="8c2dd-135">A continuación, genera un archivo de texto (archivo de salida de Hola) que contiene una lista de palabras de tres primeras Hola que aparecen en el archivo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="8c2dd-136">Después de crear el archivo de salida de hello, TaskApplication carga Hola archivo tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="8c2dd-137">Esto facilita la aplicación de cliente de toohello disponibles para su descarga.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="8c2dd-138">TaskApplication se ejecuta en paralelo en varios nodos de proceso de hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="8c2dd-139">Hello siguiente diagrama muestra operaciones principales de hello realizadas por la aplicación de cliente de hello, *DotNetTutorial*y la aplicación hello que ejecuta tareas de hello, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="8c2dd-140">Este flujo de trabajo básico es típico de muchas soluciones de proceso que se crean con Batch.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="8c2dd-141">Mientras no muestran todas las características disponibles en hello servicio por lotes, casi cada escenario de lote incluye algunas partes de este flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="8c2dd-142">![Flujo de trabajo de ejemplo de Batch][8]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="8c2dd-143">**Paso 1.**</span><span class="sxs-lookup"><span data-stu-id="8c2dd-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="8c2dd-144">Crear **contenedores** en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="8c2dd-145">
[**Paso 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="8c2dd-146">Archivos de aplicación de tarea de carga y toocontainers de archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="8c2dd-147">
[**Paso 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="8c2dd-148">Cree un **grupo** de Batch.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="8c2dd-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="8c2dd-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="8c2dd-150">Hola grupo **StartTask** descargas Hola toonodes de archivos binarios (TaskApplication) de tarea cuando se unen a grupo Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="8c2dd-151">
[**Paso 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="8c2dd-152">Cree un **trabajo** de Batch.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="8c2dd-153">
[**Paso 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="8c2dd-154">Agregar **tareas** toohello trabajo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="8c2dd-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="8c2dd-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="8c2dd-156">las tareas de Hello son tooexecute programada en nodos.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="8c2dd-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="8c2dd-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="8c2dd-158">Cada tarea descarga sus datos de entrada de Azure Storage y comienza la ejecución.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="8c2dd-159">
[**Paso 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="8c2dd-160">Supervisar las tareas.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="8c2dd-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="8c2dd-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="8c2dd-162">Tal y como se completan tareas, cargan su tooAzure de datos de salida almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="8c2dd-163">
[**Paso 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="8c2dd-164">Descargar el resultado de la tarea de Storage</span><span class="sxs-lookup"><span data-stu-id="8c2dd-164">Download task output from Storage.</span></span>

<span data-ttu-id="8c2dd-165">Tal y como se ha mencionado, no todas las soluciones lote realiza estos pasos exactos y pueden incluir muchos más, pero Hola *DotNetTutorial* aplicación de ejemplo muestra procesos comunes que se encuentra en una solución de lote.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="8c2dd-166">Compilar hello *DotNetTutorial* proyecto de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c2dd-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="8c2dd-167">Antes de poder ejecutar correctamente el ejemplo de Hola, debe especificar las credenciales de cuenta de lote y el almacenamiento en hello *DotNetTutorial* del proyecto `Program.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="8c2dd-168">Si aún no lo ha hecho, abra la solución de hello en Visual Studio haciendo doble clic en hello `DotNetTutorial.sln` archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="8c2dd-169">O ábralo desde dentro de Visual Studio mediante el uso de hello **archivo > Abrir > proyecto/solución** menú.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="8c2dd-170">Abra `Program.cs` en hello *DotNetTutorial* proyecto.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="8c2dd-171">A continuación, agregue las credenciales tal como se especifica en parte superior de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="8c2dd-172">Como se mencionó anteriormente, actualmente debe especificar credenciales de Hola para un **general** cuenta de almacenamiento en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="8c2dd-173">Las aplicaciones de lote usan almacenamiento blob de hello **general** cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="8c2dd-174">No se especifican credenciales de Hola para una cuenta de almacenamiento que se creó mediante la selección de hello *almacenamiento de blobs* tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="8c2dd-175">Puede encontrar sus credenciales de cuenta de lote y el almacenamiento en la hoja de la cuenta de hello de cada servicio en hello [portal de Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="8c2dd-176">![Procesar por lotes las credenciales en el portal de hello][9]
![credenciales de almacenamiento en el portal de Hola][10]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="8c2dd-177">Ahora que ha actualizado el proyecto de hello con sus credenciales, haga clic en solución de hello en el Explorador de soluciones y haga clic en **generar solución**.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="8c2dd-178">Confirmar restauración de Hola de los paquetes de NuGet, si se le pide.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="8c2dd-179">Si no se restauran automáticamente paquetes de NuGet hello, o si ve errores sobre un paquetes de saludo de toorestore de error, asegúrese de que tiene hello [Administrador de paquetes de NuGet] [ nuget_packagemgr] instalado.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="8c2dd-180">A continuación, habilitar la descarga de Hola de paquetes que faltan.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="8c2dd-181">Vea [habilitar paquete restaurar durante la compilación] [ nuget_restore] tooenable descarga del paquete.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="8c2dd-182">En las secciones siguientes de hello, se divide hacia abajo de la aplicación de ejemplo de Hola en pasos Hola que realiza tooprocess una carga de trabajo en hello servicio por lotes y se explican estos pasos detalladamente.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="8c2dd-183">Le recomendamos que toorefer toohello solución abierta en Visual Studio mientras trabaja su camino a través de rest de Hola de este artículo, ya que no todas las líneas de código de ejemplo de Hola se explica.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="8c2dd-184">Desplazarse arriba toohello de hello `MainAsync` método Hola *DotNetTutorial* del proyecto `Program.cs` archivo toostart con el paso 1.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="8c2dd-185">Cada paso a continuación, a continuación, aproximadamente sigue Hola progresión del método se llama `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="8c2dd-186">Paso 1: Crear contenedores de Storage</span><span class="sxs-lookup"><span data-stu-id="8c2dd-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="8c2dd-187">![Crear contenedores en Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="8c2dd-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="8c2dd-188">Batch incluye compatibilidad integrada para interactuar con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="8c2dd-189">Contenedores en su cuenta de almacenamiento proporcionará los archivos de hello necesarios para las tareas de Hola que se ejecutan en su cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="8c2dd-190">los contenedores de Hello también proporcionan un colocar toostore Hola salida los datos que producen las tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="8c2dd-191">lo primero que Hola Hola *DotNetTutorial* aplicación de cliente hace es crear tres contenedores en [almacenamiento de blobs de Azure](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="8c2dd-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="8c2dd-192">**aplicación**: este contenedor almacenará aplicación hello ejecutar tareas de hello, así como cualquiera de sus dependencias, como archivos DLL.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="8c2dd-193">**entrada**: tareas descargará tooprocess de archivos de datos de Hola de hello *entrada* contenedor.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="8c2dd-194">**salida**: cuando completen de tareas de procesamiento del archivo de entrada, cargará Hola resultados toohello *salida* contenedor.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="8c2dd-195">En orden toointeract con un almacenamiento de información de la cuenta y crear contenedores, usamos hello [biblioteca de cliente de almacenamiento de Azure para .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="8c2dd-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="8c2dd-196">Creamos una cuenta de toohello de referencia con [CloudStorageAccount][net_cloudstorageaccount]y desde el que crear un [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="8c2dd-197">Usamos hello `blobClient` hacen referencia a lo largo de la aplicación hello y pasarla como un parámetro tooseveral métodos.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="8c2dd-198">Un ejemplo de esto es en bloque de código de hello que sigue inmediatamente a Hola anterior, donde se llamó a `CreateContainerIfNotExistAsync` tooactually crear contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
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

<span data-ttu-id="8c2dd-199">Una vez que se han creado los contenedores de hello, aplicación hello ahora puede cargar archivos de Hola que se usará en las tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="8c2dd-200">[¿Cómo toouse almacenamiento de blobs en .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) proporciona una buena información general sobre cómo trabajar con contenedores de almacenamiento de Azure y los blobs.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="8c2dd-201">Debe ser cerca de la parte superior de saludo de la lista de lectura como comienza a trabajar con el lote.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="8c2dd-202">Paso 2: Cargar la aplicación de tarea y los archivos de datos</span><span class="sxs-lookup"><span data-stu-id="8c2dd-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="8c2dd-203">![Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)][2]
</span><span class="sxs-lookup"><span data-stu-id="8c2dd-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="8c2dd-204">En el archivo hello cargar el operación, *DotNetTutorial* define en primer lugar las colecciones de **aplicación** y **entrada** las rutas de acceso de archivo tal como aparecen en la máquina local Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="8c2dd-205">A continuación, se cargan estos contenedores de toohello de archivos que creó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="8c2dd-206">Hay dos métodos de `Program.cs` que intervienen en el proceso de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="8c2dd-207">`UploadFilesToContainerAsync`: Este método devuelve una colección de [ResourceFile] [ net_resourcefile] objetos (descritos a continuación) e internamente llama `UploadFileToContainerAsync` tooupload cada archivo que es pasa hello *filePaths* parámetro.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="8c2dd-208">`UploadFileToContainerAsync`: Se trata de método hello que realmente realiza la carga de archivos de Hola y crea hello [ResourceFile] [ net_resourcefile] objetos.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="8c2dd-209">Después de cargar el archivo hello, obtiene una firma de acceso compartido (SAS) para el archivo hello y devuelve un objeto ResourceFile que lo representa.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="8c2dd-210">A continuación también se tratan las firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="8c2dd-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="8c2dd-211">ResourceFiles</span></span>
<span data-ttu-id="8c2dd-212">A [ResourceFile] [ net_resourcefile] proporciona el nodo de ejecución de tareas en el lote con el archivo de tooa de dirección URL de hello en el almacenamiento de Azure que está tooa descargado antes de que se ejecuta dicha tarea.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="8c2dd-213">Hola [ResourceFile.BlobSource] [ net_resourcefile_blobsource] propiedad especifica Hola de dirección URL completa del archivo hello tal como existe en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="8c2dd-214">dirección URL de Hello también puede incluir una firma de acceso compartido (SAS) que proporciona un acceso seguro toohello archivo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="8c2dd-215">La mayoría de los tipos de tareas de .NET de Batch contienen una propiedad *ResourceFiles*, que incluye:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="8c2dd-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="8c2dd-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="8c2dd-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="8c2dd-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="8c2dd-220">Hola DotNetTutorial aplicación de ejemplo no utiliza Hola JobPreparationTask o tipos de tareas de JobReleaseTask, pero puede obtener más información acerca de esto en [nodos de ejecución de las tareas de preparación y finalización del trabajo de ejecución en Azure Batch](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="8c2dd-221">Firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="8c2dd-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="8c2dd-222">Acceso compartido firmas son cadenas que, cuando se incluye como parte de una dirección URL: proporcionar un acceso seguro toocontainers y blobs en almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="8c2dd-223">Hola DotNetTutorial aplicación usa ambos blob y contenedor comparten las URL de firma de acceso y muestra cómo tooobtain estos compartidos tener acceso a las cadenas de firmas de hello servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="8c2dd-224">**Firmas de acceso compartido de BLOB**: StartTask del grupo de hello en DotNetTutorial usa firmas de acceso compartido de blob cuando descarga los archivos binarios de aplicación de Hola y archivos de datos de entrada de almacenamiento (vea el paso 3 siguiente).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="8c2dd-225">Hola `UploadFileToContainerAsync` método del DotNetTutorial `Program.cs` contiene código de hello que obtiene la firma de acceso compartido de cada blob.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="8c2dd-226">Para ello, llama a [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="8c2dd-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="8c2dd-227">**Contenedor de firmas de acceso compartido**: a medida que cada tarea finaliza su trabajo en el nodo de proceso de hello, que se carga su toohello del archivo de salida *salida* contenedor en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="8c2dd-228">toodo por lo tanto, TaskApplication utiliza una firma de acceso compartido de contenedor que proporciona acceso de escritura toohello contenedor como parte de la ruta de acceso de hello cuando carga el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="8c2dd-229">Firma de acceso compartido de obtención Hola contenedor se realiza de forma similar, como cuando obtención blob Hola firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="8c2dd-230">En DotNetTutorial, encontrará que hello `GetContainerSasUrl` llamadas al método auxiliar [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo para.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="8c2dd-231">Podrá leer más acerca de cómo TaskApplication usa contenedor Hola compartido firma de acceso en "paso 6: las tareas de supervisión."</span><span class="sxs-lookup"><span data-stu-id="8c2dd-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="8c2dd-232">Desprotección serie de dos partes de hello en firmas de acceso compartido, [parte 1: Hola descripción compartido modelo de firma (SAS) de acceso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) y [parte 2: crear y utilizar una firma de acceso compartido (SAS) con el almacenamiento de blobs](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn más acerca de cómo proporcionar un acceso seguro toodata en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="8c2dd-233">Paso 3: Crear el grupo de Batch</span><span class="sxs-lookup"><span data-stu-id="8c2dd-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="8c2dd-234">![Crear un grupo de Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="8c2dd-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="8c2dd-235">Un **grupo** de Batch es una colección de nodos de proceso (máquinas virtuales) en los que Batch ejecuta tareas de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="8c2dd-236">Después de cargar la aplicación hello y toohello de archivos de datos cuenta de almacenamiento con la API de almacenamiento de Azure, *DotNetTutorial* comienza a realizar el servicio por lotes de llamadas a toohello con las API proporcionadas por la biblioteca de .NET de lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="8c2dd-237">Hello código crea primero un [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="8c2dd-238">A continuación, ejemplo de Hola a crea un grupo de nodos de proceso en la cuenta de lote de hello con una llamada demasiado`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="8c2dd-239">`CreatePoolIfNotExistsAsync`hello usa [BatchClient.PoolOperations.CreatePool] [ net_pool_create] método toocreate un nuevo grupo en hello servicio por lotes:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="8c2dd-240">Cuando se crea un grupo con [CreatePool][net_pool_create], especifique varios parámetros como el número de Hola de nodos de proceso, hello [tamaño de los nodos de hello](../cloud-services/cloud-services-sizes-specs.md), y Hola operativo nodos sistema.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="8c2dd-241">En *DotNetTutorial*, usamos [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 desde [servicios en la nube](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="8c2dd-242">También puede crear grupos de nodos de proceso que son máquinas virtuales (VM) de Azure mediante la especificación de hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] para el grupo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="8c2dd-243">Puede crear un grupo de nodos de proceso de máquinas virtuales a partir de imágenes de Windows o [Linux](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="8c2dd-244">origen de Hola para las imágenes de máquina virtual puede ser:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="8c2dd-245">Hola [máquinas virtuales de Azure Marketplace][vm_marketplace], lo que proporciona imágenes de Windows y Linux que están listos para usar.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="8c2dd-246">Una imagen personalizada preparada y proporcionada por el usuario.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="8c2dd-247">Para más información acerca de las imágenes personalizadas, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c2dd-248">Se cobrará por recursos de proceso en Batch.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="8c2dd-249">los costos de toominimize, puede reducir `targetDedicatedComputeNodes` too1 antes de ejecutar el ejemplo hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="8c2dd-250">Junto con estas propiedades de nodo físico, también puede especificar un [StartTask] [ net_pool_starttask] para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="8c2dd-251">Hola StartTask se ejecuta en cada nodo según ese nodo une a grupo de Hola y cada vez que se reinicie un nodo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="8c2dd-252">Hola StartTask resulta especialmente útil para instalar aplicaciones en ejecución de toohello anteriores de nodos de proceso de tareas.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="8c2dd-253">Por ejemplo, si las tareas para procesar datos mediante el uso de scripts de Python, podría utilizar un tooinstall StartTask Python en nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="8c2dd-254">En esta aplicación de ejemplo Hola StartTask copia los archivos de Hola que descarga desde el almacenamiento (que se especifican mediante hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] propiedad) del directorio compartido toohello del directorio de trabajo de hello StartTask que *todos los* pueden tener acceso tareas que se ejecutan en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="8c2dd-255">Básicamente, se copian `TaskApplication.exe` y su dependencias toohello directorio compartido en cada nodo como nodo de Hola une a grupo de hello, para que las tareas que se ejecutan en el nodo de hello pueden tener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="8c2dd-256">Hola **paquetes de aplicación** característica de lote de Azure proporciona tooget de otra manera su aplicación en los nodos de proceso de hello en un grupo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="8c2dd-257">Vea [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="8c2dd-258">También importantes en el fragmento de código de hello anterior es el uso de Hola de dos variables de entorno de hello *CommandLine* propiedad de hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` y `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="8c2dd-259">Cada nodo de ejecución dentro de un grupo de proceso por lotes se configura automáticamente con varias variables de entorno que están tooBatch específico.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="8c2dd-260">Cualquier proceso que se ejecuta una tarea tiene acceso a variables de entorno de toothese.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="8c2dd-261">toofind más información sobre las variables de entorno de Hola que están disponibles en los nodos de proceso en un grupo de lote e información de directorios de trabajo de tarea, vea hello [configuración del entorno para tareas](batch-api-basics.md#environment-settings-for-tasks) y [archivos y directorios ](batch-api-basics.md#files-and-directories) secciones de hello [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="8c2dd-262">Paso 4: Crear el trabajo de Batch</span><span class="sxs-lookup"><span data-stu-id="8c2dd-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="8c2dd-263">![Crear un trabajo de Batch][4]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="8c2dd-264">Un **trabajo** de Batch es una colección de tareas y está asociado a un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="8c2dd-265">las tareas de Hello en un trabajo que se ejecutan en nodos de proceso del grupo de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="8c2dd-266">Puede usar un trabajo no solo para organizar y seguimiento de las tareas en las cargas de trabajo relacionados, sino también para imponer ciertas restricciones, como el tiempo de ejecución máximo de hello para el trabajo de hello (y por extensión, sus tareas), así como la prioridad del trabajo en los trabajos de relación tooother Hola por lotes cuenta.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="8c2dd-267">Sin embargo, en este ejemplo, el trabajo de Hola se asocia únicamente a grupo Hola que creó en el paso 3 de #.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="8c2dd-268">No hay propiedades adicionales configuradas.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-268">No additional properties are configured.</span></span>

<span data-ttu-id="8c2dd-269">Todos los trabajos de Batch están asociados a un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="8c2dd-270">Esta asociación indica qué nodos se ejecutarán las tareas del trabajo de hello en.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="8c2dd-271">Especifique este mediante el uso de hello [CloudJob.PoolInformation] [ net_job_poolinfo] propiedad, como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="8c2dd-272">Ahora que se ha creado un trabajo, las tareas se agregan trabajo de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="8c2dd-273">Paso 5: Agregar toojob de tareas</span><span class="sxs-lookup"><span data-stu-id="8c2dd-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="8c2dd-274">![Agregar tareas toojob][5]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="8c2dd-275">
*(1) tareas se agregan toohello trabajo, tareas de hello (2) son toorun programada en nodos y tareas (3) Hola descargar tooprocess de archivos de datos de Hola*</span><span class="sxs-lookup"><span data-stu-id="8c2dd-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="8c2dd-276">Lote **tareas** son nodos de proceso de hello unidades de trabajo que se ejecutan en Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="8c2dd-277">Una tarea tiene una línea de comandos y ejecuta scripts de Hola o archivos ejecutables que especifique en esa línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="8c2dd-278">tooactually realizar el trabajo, se deben agregar tareas tooa trabajo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="8c2dd-279">Cada [CloudTask] [ net_task] se configura con una propiedad de línea de comandos y [ResourceFiles] [ net_task_resourcefiles] (al igual que con StartTask del grupo de Hola) que tarea Hello descarga toohello nodo antes de su línea de comandos se ejecuta automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="8c2dd-280">Hola *DotNetTutorial* proyecto de ejemplo, cada tarea procesa un solo archivo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="8c2dd-281">Por lo tanto, su colección ResourceFiles contiene un único elemento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
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

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="8c2dd-282">Cuando tengan acceso a las variables de entorno como `%AZ_BATCH_NODE_SHARED_DIR%` o ejecutar una aplicación no se encuentra en el nodo de hello `PATH`, líneas de comandos de tarea deben ir precedidas de `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="8c2dd-283">Esto explícitamente ejecutará el intérprete de comandos de Hola e indicar a tooterminate después de llevar a cabo el comando.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="8c2dd-284">Este requisito no es necesario si las tareas ejecutan una aplicación en el nodo de hello `PATH` (como *robocopy.exe* o *powershell.exe*) y no se usa ninguna variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="8c2dd-285">Dentro de hello `foreach` bucle en el fragmento de código de hello anterior, puede ver que se construye la línea de comandos de hello para la tarea hello, que se pasan tres argumentos de línea de comandos demasiado*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="8c2dd-286">Hola **primer argumento** es ruta Hola Hola archivo tooprocess.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="8c2dd-287">Este es el archivo de toohello de ruta de acceso local de hello tal como existe en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="8c2dd-288">Hola al objeto ResourceFile en `UploadFileToContainerAsync` creó por primera vez los casos anteriores, el nombre del archivo de Hola se usó para esta propiedad (como un constructor al parámetro toohello ResourceFile).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="8c2dd-289">Esto indica que ese archivo hello puede encontrarse en hello mismo directorio como *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="8c2dd-290">Hola **el segundo argumento** especifica ese Hola hacia arriba *N* palabras deberían escribir el archivo de salida de toohello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="8c2dd-291">En el ejemplo de Hola, esto está codificado de forma rígida para que superior tres palabras de Hola se escriben toohello archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="8c2dd-292">Hola **tercer argumento** es la firma de acceso compartido (SAS) de Hola que proporciona acceso de escritura toohello **salida** contenedor en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="8c2dd-293">*TaskApplication.exe* utiliza este recurso compartido acceso URL de firma cuando se carga de tooAzure de archivo de salida de hello almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="8c2dd-294">Puede encontrar código de hello para esto en hello `UploadFileToContainer` método en hello TaskApplication proyecto `Program.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
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

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="8c2dd-295">Paso 6: Supervisar tareas</span><span class="sxs-lookup"><span data-stu-id="8c2dd-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="8c2dd-296">![Supervisar tareas][6]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="8c2dd-297">
*monitores (1) aplicación de cliente de Hola Hola tareas de finalización y el estado de correcto y (2) Hola tooAzure de datos de resultado de carga de tareas almacenamiento*</span><span class="sxs-lookup"><span data-stu-id="8c2dd-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="8c2dd-298">Cuando las tareas se agregan trabajo tooa, están en cola y programadas para ejecutarse en nodos de ejecución dentro del bloque de hello asociado al trabajo de Hola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="8c2dd-299">En función de la configuración de Hola que especifique, por lotes controla Queue de todas las tareas, programación, Reintentar y otras tareas de administración de la tarea de.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="8c2dd-300">Existen muchos enfoques de ejecución de la tarea de toomonitoring.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="8c2dd-301">DotNetTutorial muestra un ejemplo sencillo que informa únicamente sobre la finalización y los estados de error y de realización correcta de la tarea.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="8c2dd-302">Dentro de hello `MonitorTasks` método del DotNetTutorial `Program.cs`, hay tres conceptos de .NET de lotes que justifican una explicación.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="8c2dd-303">Dichos conceptos se enumeran a continuación en su orden de aparición:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="8c2dd-304">**ODATADetailLevel**: es esencial especificar [ODATADetailLevel][net_odatadetaillevel] en las operaciones de lista (por ejemplo, obtener una lista de las tareas de un trabajo) para garantizar el rendimiento de una aplicación de Batch.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="8c2dd-305">Agregar [consultar el servicio de Azure Batch Hola eficazmente](batch-efficient-list-queries.md) tooyour leer lista si planea realizar algún tipo de supervisión de estado en las aplicaciones de lote.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="8c2dd-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] proporciona a aplicaciones de .NET de Batch utilidades auxiliares para la supervisión de los estados de las tareas.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="8c2dd-307">En `MonitorTasks`, *DotNetTutorial* espera a que todos los tooreach de tareas [TaskState.Completed] [ net_taskstate] dentro de un límite de tiempo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="8c2dd-308">A continuación, finaliza el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="8c2dd-309">**TerminateJobAsync**: finalizar un trabajo con [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (u Hola bloqueando JobOperations.TerminateJob) marca ese trabajo como completado.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="8c2dd-310">Resulta esencial toodo por lo que si la solución de lote usa un [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="8c2dd-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="8c2dd-311">Se trata de un tipo de tarea especial, que se describe en [areas de preparación y finalización de trabajos](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="8c2dd-312">Hola `MonitorTasks` método de *DotNetTutorial*del `Program.cs` aparece a continuación:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
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

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="8c2dd-313">Paso 7: Descargar el resultado de la tarea</span><span class="sxs-lookup"><span data-stu-id="8c2dd-313">Step 7: Download task output</span></span>
<span data-ttu-id="8c2dd-314">![Descargar el resultado de la tarea de Storage][7]</span><span class="sxs-lookup"><span data-stu-id="8c2dd-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="8c2dd-315">Ahora que hello trabajo se completa, resultado de hello de las tareas de hello puede descargarse desde el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="8c2dd-316">Esto se realiza con una llamada demasiado`DownloadBlobsFromContainerAsync` en *DotNetTutorial*del `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="8c2dd-317">Hola llamada demasiado`DownloadBlobsFromContainerAsync` en hello *DotNetTutorial* aplicación especifica que los archivos de hello deben ser descargado tooyour `%TEMP%` carpeta.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="8c2dd-318">Cree toomodify libre esta ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="8c2dd-319">Paso 8: Eliminar contenedores</span><span class="sxs-lookup"><span data-stu-id="8c2dd-319">Step 8: Delete containers</span></span>
<span data-ttu-id="8c2dd-320">Dado que se le cobrará por datos que residen en el almacenamiento de Azure, siempre es una buena idea tooremove los blobs que ya no son necesarios para los trabajos por lotes.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="8c2dd-321">Del DotNetTutorial `Program.cs`, esto se realiza con el método de aplicación auxiliar de tres llamadas toohello `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="8c2dd-322">el propio método Hello simplemente obtiene un contenedor de toohello de referencia y, a continuación, se llama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="8c2dd-323">Paso 9: Eliminar trabajo hello y grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="8c2dd-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="8c2dd-324">En el paso final de hello, le toodelete solicitadas Hola hello y trabajo de grupo creados por la aplicación de hello DotNetTutorial.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="8c2dd-325">Aunque no se cobran los trabajos y las tareas, *sí* se cobran los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="8c2dd-326">Por consiguiente, se recomienda asignar solo los nodos necesarios.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="8c2dd-327">La eliminación de los grupos que no se usen puede formar parte del proceso de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="8c2dd-328">Hola BatchClient [JobOperations] [ net_joboperations] y [PoolOperations] [ net_pooloperations] tienen métodos de eliminación correspondientes, que se denominan si usuario de Hello confirma la eliminación:</span><span class="sxs-lookup"><span data-stu-id="8c2dd-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
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
> <span data-ttu-id="8c2dd-329">Tenga en cuenta que los recursos de proceso se cobran; la eliminación de grupos sin usar reducirá el costo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="8c2dd-330">Además, tenga en cuenta que al eliminar un grupo eliminan todos los nodos de proceso dentro de ese grupo y que todos los datos de los nodos de hello serán irrecuperables después de elimina el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="8c2dd-331">Ejecute hello *DotNetTutorial* ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c2dd-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="8c2dd-332">Cuando se ejecuta la aplicación de ejemplo de Hola, resultado de la consola de hello será similar siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="8c2dd-333">Durante la ejecución, experimentarán una pausa en `Awaiting task completion, timeout in 00:30:00...` mientras se inician los nodos de proceso del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="8c2dd-334">Hola de uso [portal de Azure] [ azure_portal] toomonitor su grupo, nodos de proceso, trabajo y las tareas durante y después de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="8c2dd-335">Hola de uso [portal de Azure] [ azure_portal] o hello [Azure Storage Explorer] [ storage_explorers] tooview Hola recursos de almacenamiento (contenedores y blobs) que están Creando aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="8c2dd-336">Tiempo de ejecución típica es **aproximadamente 5 minutos** al ejecutar la aplicación hello en su configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="8c2dd-337">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c2dd-337">Next steps</span></span>
<span data-ttu-id="8c2dd-338">Cree cambios toomake libre demasiado*DotNetTutorial* y *TaskApplication* tooexperiment con diferentes escenarios de proceso.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="8c2dd-339">Por ejemplo, intente agregar un retraso de ejecución demasiado*TaskApplication*, por ejemplo, al igual que con [Thread.Sleep][net_thread_sleep], toosimulate larga ejecución tareas y supervisarlos en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="8c2dd-340">Intente agregar más tareas o ajustar Hola número de nodos de cálculo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="8c2dd-341">Agregar lógica toocheck para y permitir el uso de Hola de tiempo de ejecución existente grupo toospeed (*sugerencia*: extraer del repositorio `ArticleHelpers.cs` en hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] proyecto [ejemplos de lote de azure][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="8c2dd-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="8c2dd-342">Ahora que está familiarizado con un flujo de trabajo básico de Hola de una solución de lote, es hora toodig en toohello características adicionales de hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="8c2dd-343">Hola de revisión [características de información general de Azure Batch](batch-api-basics.md) artículo, que se recomienda si dispone de un nuevo servicio de toohello.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="8c2dd-344">Inicio de Hola otros artículos de desarrollo de lote en **desarrollo detallada** en hello [ruta de acceso de aprendizaje por lotes][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="8c2dd-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="8c2dd-345">Extraer del repositorio una implementación diferente de procesamiento de cargas de trabajo de Hola "top N palabras" mediante el proceso por lotes en hello [TopNWords] [ github_topnwords] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="8c2dd-346">Hola revisión .NET de lotes [notas de la versión](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) de cambios más recientes de hello en la biblioteca de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c2dd-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Crear el grupo de Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Crear trabajo de Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Agregar tareas toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Supervisar tareas"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Descargar el resultado de la tarea de Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Flujo de trabajo de soluciones de Batch (diagrama completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenciales de Batch en el portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenciales de Storage en el portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Flujo de trabajo de soluciones de Batch (diagrama mínimo)"
