---
title: 'aaaTutorial: utilizar la biblioteca cliente en hello lote de Azure para Node.js | Documentos de Microsoft'
description: "Obtenga información acerca de los conceptos básicos de Azure Batch hello y generar una solución simple con Node.js."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="0e8df-103">Introducción al SDK de Batch para Node.js</span><span class="sxs-lookup"><span data-stu-id="0e8df-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e8df-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0e8df-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="0e8df-105">Python</span><span class="sxs-lookup"><span data-stu-id="0e8df-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="0e8df-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="0e8df-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="0e8df-107">Obtenga información acerca de los conceptos básicos de hello de la creación de un cliente de lote de uso de Node.js [Node.js de lote de Azure SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="0e8df-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="0e8df-108">Vamos a describir paso a paso un escenario de aplicación por lotes y, a continuación, su configuración mediante un cliente de Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e8df-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="0e8df-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e8df-109">Prerequisites</span></span>
<span data-ttu-id="0e8df-110">En este artículo se da por hecho que tiene conocimientos prácticos de Node.js y está familiarizado con Linux.</span><span class="sxs-lookup"><span data-stu-id="0e8df-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="0e8df-111">También se da por supuesto que tiene una configuración de Azure cuenta con acceso derechos toocreate por lotes y almacenamiento de los servicios.</span><span class="sxs-lookup"><span data-stu-id="0e8df-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="0e8df-112">Es recomendable leer [Introducción técnica a Azure Batch](batch-technical-overview.md) antes de ir a través de pasos de hello, que describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0e8df-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="0e8df-113">escenario del tutorial Hola</span><span class="sxs-lookup"><span data-stu-id="0e8df-113">hello tutorial scenario</span></span>
<span data-ttu-id="0e8df-114">Vamos a explicar escenario de flujo de trabajo por lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="0e8df-115">Tenemos un script simple escrito en Python que descarga csv todos los archivos de un contenedor de almacenamiento de blobs de Azure y los convierte tooJSON.</span><span class="sxs-lookup"><span data-stu-id="0e8df-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="0e8df-116">tooprocess cuenta de almacenamiento varios contenedores en paralelo, podemos implementar secuencias de comandos de Hola como un trabajo por lotes de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="0e8df-117">Arquitectura de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0e8df-117">Azure Batch Architecture</span></span>
<span data-ttu-id="0e8df-118">Hello siguiente diagrama muestra cómo se puede escalar script de Python de hello con Azure Batch y un cliente de Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e8df-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Escenario de Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="0e8df-120">cliente de node.js Hola implementa un proceso por lotes con una tarea de preparación (más adelante se explica con detalle) y un conjunto de tareas en función del número de Hola de contenedores en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="0e8df-121">Puede descargar scripts de Hola de repositorio de github de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="0e8df-122">Cliente de Node.js</span><span class="sxs-lookup"><span data-stu-id="0e8df-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="0e8df-123">Scripts de shell de la tarea de preparación</span><span class="sxs-lookup"><span data-stu-id="0e8df-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="0e8df-124">Procesador de tooJSON de csv de Python</span><span class="sxs-lookup"><span data-stu-id="0e8df-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="0e8df-125">cliente de Node.js de Hello en el vínculo de hello especificado no contiene toobe de código concretos implementado como una aplicación de Azure de función.</span><span class="sxs-lookup"><span data-stu-id="0e8df-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="0e8df-126">Puede hacer referencia a toohello siguientes vínculos para obtener instrucciones toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="0e8df-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="0e8df-127">Creación de una instancia de Function App</span><span class="sxs-lookup"><span data-stu-id="0e8df-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="0e8df-128">Creación de una función de desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="0e8df-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="0e8df-129">Compilar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="0e8df-129">Build hello application</span></span>

<span data-ttu-id="0e8df-130">Ahora, nos gustaría seguir el proceso de hello paso a paso en la compilación de cliente de Node.js de Hola:</span><span class="sxs-lookup"><span data-stu-id="0e8df-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="0e8df-131">Paso 1: Instalación del SDK de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0e8df-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="0e8df-132">Puede instalar el SDK de lote de Azure para Node.js con el comando de instalación de npm Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="0e8df-133">Este comando instala la versión más reciente de hello del nodo de lote de azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0e8df-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="0e8df-134">En una aplicación de la función de Azure, puede ir demasiado comandos de instalación de configuración de la "Kudu consola" Hola función Azure pestaña toorun Hola npm.</span><span class="sxs-lookup"><span data-stu-id="0e8df-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="0e8df-135">En este caso tooinstall SDK de lote de Azure para Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e8df-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="0e8df-136">Paso 2: Creación de una cuenta de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0e8df-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="0e8df-137">Se puede crear desde hello [portal de Azure](batch-account-create-portal.md) o desde la línea de comandos ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli de Azure](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="0e8df-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="0e8df-138">Estos son Hola comandos toocreate uno mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="0e8df-139">Crear un grupo de recursos, omita este paso si ya tiene una en la que desea toocreate Hola cuenta de lote:</span><span class="sxs-lookup"><span data-stu-id="0e8df-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="0e8df-140">A continuación, cree una cuenta de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0e8df-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="0e8df-141">Cada cuenta de Batch tiene sus claves de acceso correspondientes.</span><span class="sxs-lookup"><span data-stu-id="0e8df-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="0e8df-142">Estas claves son toocreate necesarios más recursos en la cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="0e8df-143">Una práctica recomendada para el entorno de producción es toouse el almacén de claves de Azure toostore estas claves.</span><span class="sxs-lookup"><span data-stu-id="0e8df-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="0e8df-144">A continuación, puede crear un servicio principal para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0e8df-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="0e8df-145">Con esta aplicación Hola principal de servicio, puede crear un claves de tooaccess token de OAuth de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="0e8df-146">Copie y almacene hello toobe clave usado en pasos posteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="0e8df-147">Paso 3: Creación de un cliente de servicio de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0e8df-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="0e8df-148">Fragmento de código siguiente primero importa módulo Node.js de hello lote de azure y, a continuación, crea a un cliente de servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="0e8df-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="0e8df-149">Necesita toofirst crear un objeto SharedKeyCredentials con clave de cuenta de lote Hola copiado desde el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="0e8df-150">Hola URI de lote de Azure puede encontrarse en la ficha de información general de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="0e8df-151">Es de formato de hello:</span><span class="sxs-lookup"><span data-stu-id="0e8df-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="0e8df-152">Consulte la captura de pantalla de toohello:</span><span class="sxs-lookup"><span data-stu-id="0e8df-152">Refer toohello screenshot:</span></span>

![URI de Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="0e8df-154">Paso 4: Creación de un grupo de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0e8df-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="0e8df-155">Un grupo de Azure Batch consta de varias máquinas virtuales (también conocidas como nodos de Batch).</span><span class="sxs-lookup"><span data-stu-id="0e8df-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="0e8df-156">Servicio de lote de Azure implementa tareas hello en esos nodos y administrarlos.</span><span class="sxs-lookup"><span data-stu-id="0e8df-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="0e8df-157">Puede definir Hola siguientes parámetros de configuración para el grupo.</span><span class="sxs-lookup"><span data-stu-id="0e8df-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="0e8df-158">Tipo de imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0e8df-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="0e8df-159">Tamaño de los nodos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0e8df-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="0e8df-160">Número de nodos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0e8df-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="0e8df-161">tamaño de Hola y el número de nodos de la máquina Virtual dependen en gran medida Hola número de tareas que desea toorun en paralelo y también propia tarea hello.</span><span class="sxs-lookup"><span data-stu-id="0e8df-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="0e8df-162">Se recomienda probar el tamaño y número ideal de toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="0e8df-163">Hello fragmento de código siguiente crea Hola objetos de parámetro de configuración.</span><span class="sxs-lookup"><span data-stu-id="0e8df-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="0e8df-164">Consulte Hola lista de imágenes de VM de Linux disponibles para el lote de Azure y sus identificadores de SKU, [lista de imágenes de máquina virtual](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="0e8df-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="0e8df-165">Una vez que se define la configuración del grupo de hello, puede crear el grupo de lote de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="0e8df-166">Hola comando de grupo por lotes crea nodos de máquina Virtual de Azure y prepararlos toobe tooreceive listo tareas tooexecute.</span><span class="sxs-lookup"><span data-stu-id="0e8df-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="0e8df-167">Cada grupo debe tener un identificador único para hacer referencia a él en los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="0e8df-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="0e8df-168">Hola siguiente fragmento de código crea un grupo de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="0e8df-169">Puede comprobar el estado de Hola Hola del grupo de creado y asegúrese de que es el estado de hello en "activo" antes de seguir adelante con el envío de un grupo de trabajo toothat.</span><span class="sxs-lookup"><span data-stu-id="0e8df-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="0e8df-170">Aquí te mostramos un objeto de resultado de ejemplo devuelto por la función de pool.get Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-170">Following is a sample result object returned by hello pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="0e8df-171">Paso 4: Envío de un trabajo a Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0e8df-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="0e8df-172">Un trabajo de Azure Batch es un grupo lógico de tareas similares.</span><span class="sxs-lookup"><span data-stu-id="0e8df-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="0e8df-173">En nuestro escenario, es "Proceso csv tooJSON."</span><span class="sxs-lookup"><span data-stu-id="0e8df-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="0e8df-174">Cada tarea aquí podría estar procesando archivos CSV presentes en cada contenedor de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0e8df-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="0e8df-175">Estas tareas se ejecutan en paralelo e implementan a través de varios nodos, organizados por el servicio de Azure Batch Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="0e8df-176">Puede usar hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) número máximo de propiedad toospecify de tareas que pueden ejecutarse simultáneamente en un único nodo.</span><span class="sxs-lookup"><span data-stu-id="0e8df-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="0e8df-177">Tarea de preparación</span><span class="sxs-lookup"><span data-stu-id="0e8df-177">Preparation task</span></span>

<span data-ttu-id="0e8df-178">nodos VM de Hello creados son en blanco Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0e8df-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="0e8df-179">A menudo, deberá tooinstall un conjunto de programas como requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="0e8df-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="0e8df-180">Por lo general, para los nodos de Linux puede tener una secuencia de comandos de shell que instala los requisitos previos de hello antes de tareas reales Hola ejecutar.</span><span class="sxs-lookup"><span data-stu-id="0e8df-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="0e8df-181">No obstante, puede ser cualquier programa ejecutable.</span><span class="sxs-lookup"><span data-stu-id="0e8df-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="0e8df-182">Hola [secuencia de comandos de shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) en este ejemplo instala pip de Python y Hola SDK de almacenamiento de Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="0e8df-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="0e8df-183">Puede cargar el script de Hola en una cuenta de almacenamiento de Azure y generar un script de Hola tooaccess de URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="0e8df-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="0e8df-184">También se puede automatizar este proceso con hello SDK de Node.js de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="0e8df-185">Una tarea de preparación de un trabajo se ejecuta solo en nodos VM de Hola donde hello necesidades específicas toorun.</span><span class="sxs-lookup"><span data-stu-id="0e8df-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="0e8df-186">Si desea toobe de requisitos previos instalado en todos los nodos con independencia de las tareas de Hola que se ejecutan en él, puede usar hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propiedad al agregar un grupo.</span><span class="sxs-lookup"><span data-stu-id="0e8df-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="0e8df-187">Puede usar Hola después de la definición de la tarea de preparación para la referencia.</span><span class="sxs-lookup"><span data-stu-id="0e8df-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="0e8df-188">Una tarea de preparación se especifica durante el envío de Hola de proceso por lotes de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="0e8df-189">A continuación se Hola parámetros de configuración de preparación de la tarea:</span><span class="sxs-lookup"><span data-stu-id="0e8df-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="0e8df-190">**Id. de**: un identificador único para la tarea de preparación de hello</span><span class="sxs-lookup"><span data-stu-id="0e8df-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="0e8df-191">**la línea de comandos**: tarea de hello tooexecute de línea de comandos ejecutable</span><span class="sxs-lookup"><span data-stu-id="0e8df-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="0e8df-192">**resourceFiles**: matriz de objetos que proporcionan los detalles de los archivos necesarios toobe descargado para este toorun de tarea.</span><span class="sxs-lookup"><span data-stu-id="0e8df-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="0e8df-193">Las opciones son</span><span class="sxs-lookup"><span data-stu-id="0e8df-193">Following are its options</span></span>
    - <span data-ttu-id="0e8df-194">blobSource: Hola URI de archivo hello SAS</span><span class="sxs-lookup"><span data-stu-id="0e8df-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="0e8df-195">filePath: toodownload de ruta de acceso Local y guarde el archivo hello</span><span class="sxs-lookup"><span data-stu-id="0e8df-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="0e8df-196">fileMode: fileMode solo es aplicable para nodos de Linux, está en formato octal con un valor predeterminado de 0770</span><span class="sxs-lookup"><span data-stu-id="0e8df-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="0e8df-197">**waitForSuccess**: si no se ejecuta set tootrue, tarea hello en errores de tareas de preparación</span><span class="sxs-lookup"><span data-stu-id="0e8df-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="0e8df-198">**runElevated**: establecer tootrue si privilegios elevados tarea de hello toorun necesarios.</span><span class="sxs-lookup"><span data-stu-id="0e8df-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="0e8df-199">Fragmento de código siguiente muestra el ejemplo de configuración de script de Hola preparación de la tarea:</span><span class="sxs-lookup"><span data-stu-id="0e8df-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="0e8df-200">Si no hay ningún toobe de requisitos previos instalado para su toorun de tareas, puede omitir las tareas de preparación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8df-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="0e8df-201">El código siguiente crea un trabajo con el nombre para mostrar "process csv files" (procesar archivos CSV).</span><span class="sxs-lookup"><span data-stu-id="0e8df-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="0e8df-202">Paso 5: Envío de tareas de Azure Batch para un trabajo</span><span class="sxs-lookup"><span data-stu-id="0e8df-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="0e8df-203">Una vez creado el trabajo para procesar archivos CSV, se crearán las tareas para dicho trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e8df-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="0e8df-204">Suponiendo que tenemos cuatro contenedores, tenemos toocreate cuatro tareas, uno para cada contenedor.</span><span class="sxs-lookup"><span data-stu-id="0e8df-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="0e8df-205">Si miramos hello [script de Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), acepta dos parámetros:</span><span class="sxs-lookup"><span data-stu-id="0e8df-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="0e8df-206">nombre del contenedor: Hola archivos de toodownload de contenedor de almacenamiento de</span><span class="sxs-lookup"><span data-stu-id="0e8df-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="0e8df-207">pattern: (patrón) parámetro opcional de un patrón de nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="0e8df-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="0e8df-208">Suponiendo que tenemos cuatro contenedores "con1", "con2", "con3", "con4" siguiente código muestra enviar para tareas toohello Azure batch trabajo "proceso csv" hemos creado con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="0e8df-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="0e8df-209">código de Hello agrega grupo de toohello de varias tareas.</span><span class="sxs-lookup"><span data-stu-id="0e8df-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="0e8df-210">Y cada una de las tareas de Hola se ejecuta en un nodo de grupo de Hola de máquinas virtuales que se creó.</span><span class="sxs-lookup"><span data-stu-id="0e8df-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="0e8df-211">Si número Hola de tareas supera el número de Hola de máquinas virtuales en una propiedad de grupo o hello maxTasksPerNode, tareas de hello esperan hasta que un nodo se pone a disposición.</span><span class="sxs-lookup"><span data-stu-id="0e8df-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="0e8df-212">Azure Batch controla esta orquestación de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="0e8df-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="0e8df-213">portal de Hello, detallaron vistas sobre las tareas de Hola y Estados de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e8df-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="0e8df-214">También puede usar la lista de Hola y obtener funciones en hello SDK de nodo de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8df-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="0e8df-215">Se proporcionan detalles en la documentación de hello [vínculo](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="0e8df-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e8df-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e8df-216">Next steps</span></span>

- <span data-ttu-id="0e8df-217">Hola de revisión [características de información general de Azure Batch](batch-api-basics.md) artículo, que se recomienda si dispone de un nuevo servicio de toohello.</span><span class="sxs-lookup"><span data-stu-id="0e8df-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="0e8df-218">Vea hello [Node.js de lote referencia](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore Hola API de lote.</span><span class="sxs-lookup"><span data-stu-id="0e8df-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

