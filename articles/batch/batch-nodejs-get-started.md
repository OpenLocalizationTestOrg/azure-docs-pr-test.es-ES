---
title: 'Tutorial: Uso de la biblioteca de clientes de Azure Batch para Node.js | Microsoft Docs'
description: "Aprenda los conceptos básicos de Azure Batch y cree una solución sencilla mediante Node.js."
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
ms.openlocfilehash: c48171d8634a651718a0775183414f463c6a468c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="b82f4-103">Introducción al SDK de Batch para Node.js</span><span class="sxs-lookup"><span data-stu-id="b82f4-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b82f4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b82f4-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="b82f4-105">Python</span><span class="sxs-lookup"><span data-stu-id="b82f4-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="b82f4-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="b82f4-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="b82f4-107">Obtenga información acerca de los conceptos básicos de la creación de un cliente de Batch con Node.js en [Microsoft Azure SDK for Node.js - Batch Service](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) (SDK de Microsoft Azure SDK para Node.js: servicio Batch).</span><span class="sxs-lookup"><span data-stu-id="b82f4-107">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="b82f4-108">Vamos a describir paso a paso un escenario de aplicación por lotes y, a continuación, su configuración mediante un cliente de Node.js.</span><span class="sxs-lookup"><span data-stu-id="b82f4-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b82f4-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b82f4-109">Prerequisites</span></span>
<span data-ttu-id="b82f4-110">En este artículo se da por hecho que tiene conocimientos prácticos de Node.js y está familiarizado con Linux.</span><span class="sxs-lookup"><span data-stu-id="b82f4-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="b82f4-111">También necesitará una cuenta de Azure configurada con derechos de acceso para crear servicios de Batch y Storage.</span><span class="sxs-lookup"><span data-stu-id="b82f4-111">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="b82f4-112">Es recomendable leer [Azure Batch Technical Overview](batch-technical-overview.md) (Información general técnica de Azure Batch) antes de seguir los pasos que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="b82f4-113">Escenario del tutorial</span><span class="sxs-lookup"><span data-stu-id="b82f4-113">The tutorial scenario</span></span>
<span data-ttu-id="b82f4-114">Se va a explicar el escenario de un flujo de trabajo de Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-114">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="b82f4-115">Tenemos un script sencillo escrito en Python que descarga todos los archivos CSV de un contenedor de Azure Blob Storage y los convierte en JSON.</span><span class="sxs-lookup"><span data-stu-id="b82f4-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="b82f4-116">Para procesar en paralelo varios contenedores de la cuenta de almacenamiento, podemos implementar el script como un trabajo de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-116">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="b82f4-117">Arquitectura de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b82f4-117">Azure Batch Architecture</span></span>
<span data-ttu-id="b82f4-118">El siguiente diagrama muestra cómo se puede escalar el script de Python con Azure Batch y un cliente de Node.js.</span><span class="sxs-lookup"><span data-stu-id="b82f4-118">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Escenario de Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="b82f4-120">El cliente de node.js implementa un trabajo por lotes con una tarea de preparación (más adelante se explica con detalle) y un conjunto de tareas en función del número de contenedores de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b82f4-120">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="b82f4-121">Puede descargar los scripts del repositorio de Github.</span><span class="sxs-lookup"><span data-stu-id="b82f4-121">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="b82f4-122">Cliente de Node.js</span><span class="sxs-lookup"><span data-stu-id="b82f4-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="b82f4-123">Scripts de shell de la tarea de preparación</span><span class="sxs-lookup"><span data-stu-id="b82f4-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="b82f4-124">Procesador Python de CSV a JSON</span><span class="sxs-lookup"><span data-stu-id="b82f4-124">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="b82f4-125">El cliente de Node.js del enlace especificado no contiene código específico para implementarse como una instancia de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="b82f4-125">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="b82f4-126">Puede consultar los siguientes enlaces para obtener instrucciones de cómo crear una.</span><span class="sxs-lookup"><span data-stu-id="b82f4-126">You can refer to the following links for instructions to create one.</span></span>
> - [<span data-ttu-id="b82f4-127">Creación de una instancia de Function App</span><span class="sxs-lookup"><span data-stu-id="b82f4-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="b82f4-128">Creación de una función de desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="b82f4-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a><span data-ttu-id="b82f4-129">Compilar la aplicación</span><span class="sxs-lookup"><span data-stu-id="b82f4-129">Build the application</span></span>

<span data-ttu-id="b82f4-130">Ahora, sigamos el proceso paso a paso para crear el cliente de Node.js:</span><span class="sxs-lookup"><span data-stu-id="b82f4-130">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="b82f4-131">Paso 1: Instalación del SDK de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b82f4-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="b82f4-132">Puede instalar el SDK de Azure Batch para Node.js con el comando npm install.</span><span class="sxs-lookup"><span data-stu-id="b82f4-132">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="b82f4-133">Este comando instala la versión más reciente del SDK de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-133">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="b82f4-134">En una instancia de Azure Function App, puede ir a la "Consola Kudu" en la pestaña de configuración de la función de Azure para ejecutar los comandos npm install.</span><span class="sxs-lookup"><span data-stu-id="b82f4-134">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="b82f4-135">En este caso, para instalar el SDK de Azure Batch para Node.js.</span><span class="sxs-lookup"><span data-stu-id="b82f4-135">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="b82f4-136">Paso 2: Creación de una cuenta de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b82f4-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="b82f4-137">Puede crearla desde [Azure Portal](batch-account-create-portal.md) o desde la línea de comandos ([Powershell](batch-powershell-cmdlets-get-started.md) /[CLI de Azure](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="b82f4-137">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="b82f4-138">A continuación se muestran los comandos para crear una mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b82f4-138">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="b82f4-139">Cree un grupo de recursos; omita este paso si ya tiene uno en el que desea crear la cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="b82f4-139">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="b82f4-140">A continuación, cree una cuenta de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="b82f4-141">Cada cuenta de Batch tiene sus claves de acceso correspondientes.</span><span class="sxs-lookup"><span data-stu-id="b82f4-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="b82f4-142">Estas claves se necesitan para crear más recursos en la cuenta de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-142">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="b82f4-143">Una práctica recomendada para el entorno de producción es usar Azure Key Vault para almacenar estas claves.</span><span class="sxs-lookup"><span data-stu-id="b82f4-143">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="b82f4-144">Después, puede crear una entidad de servicio para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b82f4-144">You can then create a Service principal for the application.</span></span> <span data-ttu-id="b82f4-145">Mediante esta entidad de servicio, la aplicación puede crear un token de OAuth para tener acceso a las claves del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b82f4-145">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="b82f4-146">Copie y guarde la clave que se usará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="b82f4-146">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="b82f4-147">Paso 3: Creación de un cliente de servicio de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b82f4-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="b82f4-148">El siguiente fragmento de código importa en primer lugar el módulo de Node.js de Azure Batch y, a continuación, crea un cliente de servicio de Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-148">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="b82f4-149">Debe crear primero un objeto SharedKeyCredentials con la clave de la cuenta de Batch que copió en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="b82f4-149">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

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

<span data-ttu-id="b82f4-150">La dirección URI de Azure Batch se puede encontrar en la pestaña Información general de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b82f4-150">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="b82f4-151">Tiene el formato:</span><span class="sxs-lookup"><span data-stu-id="b82f4-151">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="b82f4-152">Consulte la captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="b82f4-152">Refer to the screenshot:</span></span>

![URI de Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="b82f4-154">Paso 4: Creación de un grupo de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b82f4-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="b82f4-155">Un grupo de Azure Batch consta de varias máquinas virtuales (también conocidas como nodos de Batch).</span><span class="sxs-lookup"><span data-stu-id="b82f4-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="b82f4-156">El servicio Azure Batch implementa las tareas en los nodos y las administra.</span><span class="sxs-lookup"><span data-stu-id="b82f4-156">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="b82f4-157">Puede definir los siguientes parámetros de configuración para el grupo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-157">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="b82f4-158">Tipo de imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b82f4-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="b82f4-159">Tamaño de los nodos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b82f4-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="b82f4-160">Número de nodos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b82f4-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="b82f4-161">El tamaño y el número de los nodos de máquina virtual dependen en gran medida del número de tareas que desee ejecutar en paralelo y de la propia tarea.</span><span class="sxs-lookup"><span data-stu-id="b82f4-161">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="b82f4-162">Se recomienda realizar pruebas para determinar el número y tamaño ideales.</span><span class="sxs-lookup"><span data-stu-id="b82f4-162">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="b82f4-163">El fragmento de código siguiente crea los objetos de parámetros de configuración.</span><span class="sxs-lookup"><span data-stu-id="b82f4-163">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="b82f4-164">Para obtener la lista de imágenes de máquinas virtuales Linux disponibles para Azure Batch y sus identificadores SKU, consulte la [Lista de imágenes de máquina virtual](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="b82f4-164">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="b82f4-165">Una vez definida la configuración del grupo, puede crear el grupo de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-165">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="b82f4-166">El comando batch pool crea nodos de máquina virtual de Azure y los prepara para recibir tareas para ejecutar.</span><span class="sxs-lookup"><span data-stu-id="b82f4-166">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="b82f4-167">Cada grupo debe tener un identificador único para hacer referencia a él en los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="b82f4-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="b82f4-168">El siguiente fragmento de código crea un grupo de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-168">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="b82f4-169">Puede comprobar el estado del grupo creado y asegurarse de que el estado es "activo" antes de continuar con el envío de un trabajo a ese grupo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-169">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

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

<span data-ttu-id="b82f4-170">A continuación se muestra un ejemplo de objeto devuelto por la función pool.get.</span><span class="sxs-lookup"><span data-stu-id="b82f4-170">Following is a sample result object returned by the pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="b82f4-171">Paso 4: Envío de un trabajo a Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b82f4-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="b82f4-172">Un trabajo de Azure Batch es un grupo lógico de tareas similares.</span><span class="sxs-lookup"><span data-stu-id="b82f4-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="b82f4-173">En nuestro escenario, es "Conversión de CSV a JSON".</span><span class="sxs-lookup"><span data-stu-id="b82f4-173">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="b82f4-174">Cada tarea aquí podría estar procesando archivos CSV presentes en cada contenedor de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b82f4-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="b82f4-175">Estas tareas se ejecutan en paralelo y se implementan a través de varios nodos, organizados por el servicio de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="b82f4-176">Puede usar la propiedad [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) para especificar el número máximo de tareas que pueden ejecutarse simultáneamente en un único nodo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-176">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="b82f4-177">Tarea de preparación</span><span class="sxs-lookup"><span data-stu-id="b82f4-177">Preparation task</span></span>

<span data-ttu-id="b82f4-178">Los nodos de máquina virtual creados son nodos Ubuntu en blanco.</span><span class="sxs-lookup"><span data-stu-id="b82f4-178">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="b82f4-179">A menudo, necesitará instalar un conjunto de programas como requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="b82f4-179">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="b82f4-180">Por lo general, para los nodos de Linux puede tener un script de shell que instale los requisitos previos antes de la ejecución de las tareas reales.</span><span class="sxs-lookup"><span data-stu-id="b82f4-180">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="b82f4-181">No obstante, puede ser cualquier programa ejecutable.</span><span class="sxs-lookup"><span data-stu-id="b82f4-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="b82f4-182">El [script de shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) de este ejemplo instala Python-pip y el SDK de Azure Storage para Python.</span><span class="sxs-lookup"><span data-stu-id="b82f4-182">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="b82f4-183">Puede cargar el script en una cuenta de Azure Storage y generar un URI de SAS para tener acceso al script.</span><span class="sxs-lookup"><span data-stu-id="b82f4-183">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="b82f4-184">Este proceso también se puede automatizar utilizando el SDK de Azure Storage para Node.js.</span><span class="sxs-lookup"><span data-stu-id="b82f4-184">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="b82f4-185">Una tarea de preparación de un trabajo se ejecuta solo en los nodos de máquina virtual en los que la tarea específica necesita ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="b82f4-185">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="b82f4-186">Si desea que los requisitos previos se instalen en todos los nodos con independencia de las tareas que se ejecutan en él, puede usar la propiedad [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) al agregar un grupo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-186">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="b82f4-187">Puede utilizar como referencia la definición de tarea de preparación siguiente.</span><span class="sxs-lookup"><span data-stu-id="b82f4-187">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="b82f4-188">La tarea de preparación se especifica durante el envío de un trabajo de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-188">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="b82f4-189">Estos son los parámetros de configuración de la tarea de preparación:</span><span class="sxs-lookup"><span data-stu-id="b82f4-189">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="b82f4-190">**ID**: identificador único de la tarea de preparación</span><span class="sxs-lookup"><span data-stu-id="b82f4-190">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="b82f4-191">**commandLine**: comando para ejecutar la tarea</span><span class="sxs-lookup"><span data-stu-id="b82f4-191">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="b82f4-192">**resourceFiles**: matriz de objetos que proporciona detalles de los archivos que se deben descargar para que la tarea se ejecute.</span><span class="sxs-lookup"><span data-stu-id="b82f4-192">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="b82f4-193">Las opciones son</span><span class="sxs-lookup"><span data-stu-id="b82f4-193">Following are its options</span></span>
    - <span data-ttu-id="b82f4-194">blobSource: el URI de SAS del archivo</span><span class="sxs-lookup"><span data-stu-id="b82f4-194">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="b82f4-195">filePath: ruta de acceso local para descargar y guardar el archivo</span><span class="sxs-lookup"><span data-stu-id="b82f4-195">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="b82f4-196">fileMode: fileMode solo es aplicable para nodos de Linux, está en formato octal con un valor predeterminado de 0770</span><span class="sxs-lookup"><span data-stu-id="b82f4-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="b82f4-197">**waitForSuccess**: si se establece en true, la tarea no se ejecuta si existen errores en la tarea de preparación</span><span class="sxs-lookup"><span data-stu-id="b82f4-197">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="b82f4-198">**runElevated**: establézcalo en true si se necesitan privilegios elevados para ejecutar la tarea.</span><span class="sxs-lookup"><span data-stu-id="b82f4-198">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="b82f4-199">El fragmento de código siguiente muestra el ejemplo de script de configuración de la tarea de preparación:</span><span class="sxs-lookup"><span data-stu-id="b82f4-199">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="b82f4-200">Si no hay requisitos previos de instalación para la ejecución de las tareas, puede omitir las tareas de preparación.</span><span class="sxs-lookup"><span data-stu-id="b82f4-200">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="b82f4-201">El código siguiente crea un trabajo con el nombre para mostrar "process csv files" (procesar archivos CSV).</span><span class="sxs-lookup"><span data-stu-id="b82f4-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="b82f4-202">Paso 5: Envío de tareas de Azure Batch para un trabajo</span><span class="sxs-lookup"><span data-stu-id="b82f4-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="b82f4-203">Una vez creado el trabajo para procesar archivos CSV, se crearán las tareas para dicho trabajo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="b82f4-204">Suponiendo que tenemos cuatro contenedores, tenemos que crear cuatro tareas, una para cada contenedor.</span><span class="sxs-lookup"><span data-stu-id="b82f4-204">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="b82f4-205">Si observamos el [script de Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), vemos que acepta dos parámetros:</span><span class="sxs-lookup"><span data-stu-id="b82f4-205">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="b82f4-206">container name: (nombre del contenedor) el contenedor de almacenamiento desde el que se van a descargar los archivos</span><span class="sxs-lookup"><span data-stu-id="b82f4-206">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="b82f4-207">pattern: (patrón) parámetro opcional de un patrón de nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="b82f4-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="b82f4-208">Suponiendo que tenemos cuatro contenedores denominados "con1", "con2", "con3" y "con4", el siguiente código muestra el envío de tareas al trabajo de Azure Batch denominado "process csv" (procesar archivos CSV) que creamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b82f4-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="b82f4-209">El código agrega varias tareas al grupo.</span><span class="sxs-lookup"><span data-stu-id="b82f4-209">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="b82f4-210">Y cada una de las tareas se ejecuta en un nodo en el grupo de máquinas virtuales que se creó.</span><span class="sxs-lookup"><span data-stu-id="b82f4-210">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="b82f4-211">Si el número de tareas supera el número de máquinas virtuales en un grupo o el valor de la propiedad maxTasksPerNode, las tareas esperan hasta que un nodo queda disponible.</span><span class="sxs-lookup"><span data-stu-id="b82f4-211">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="b82f4-212">Azure Batch controla esta orquestación de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="b82f4-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="b82f4-213">El portal tiene vistas detalladas del estado de las tareas y trabajos.</span><span class="sxs-lookup"><span data-stu-id="b82f4-213">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="b82f4-214">También puede utilizar la lista y obtener funciones en el SDK de Azure Batch para Node.js.</span><span class="sxs-lookup"><span data-stu-id="b82f4-214">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="b82f4-215">En la documentación del siguiente [enlace](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html) se proporcionan más detalles.</span><span class="sxs-lookup"><span data-stu-id="b82f4-215">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b82f4-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b82f4-216">Next steps</span></span>

- <span data-ttu-id="b82f4-217">Consulte el artículo [Información general de las características de Lote de Azure](batch-api-basics.md) , que es especialmente recomendable si no se conoce el servicio.</span><span class="sxs-lookup"><span data-stu-id="b82f4-217">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="b82f4-218">Consulte la [referencia de Batch Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) para explorar la API de Batch.</span><span class="sxs-lookup"><span data-stu-id="b82f4-218">See the [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) to explore the Batch API.</span></span>

