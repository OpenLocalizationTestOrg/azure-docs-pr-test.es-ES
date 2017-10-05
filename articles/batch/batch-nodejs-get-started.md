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
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Introducción al SDK de Batch para Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Obtenga información acerca de los conceptos básicos de la creación de un cliente de Batch con Node.js en [Microsoft Azure SDK for Node.js - Batch Service](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) (SDK de Microsoft Azure SDK para Node.js: servicio Batch). Vamos a describir paso a paso un escenario de aplicación por lotes y, a continuación, su configuración mediante un cliente de Node.js.  

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por hecho que tiene conocimientos prácticos de Node.js y está familiarizado con Linux. También necesitará una cuenta de Azure configurada con derechos de acceso para crear servicios de Batch y Storage.

Es recomendable leer [Azure Batch Technical Overview](batch-technical-overview.md) (Información general técnica de Azure Batch) antes de seguir los pasos que se describen en este artículo.

## <a name="the-tutorial-scenario"></a>Escenario del tutorial
Se va a explicar el escenario de un flujo de trabajo de Batch. Tenemos un script sencillo escrito en Python que descarga todos los archivos CSV de un contenedor de Azure Blob Storage y los convierte en JSON. Para procesar en paralelo varios contenedores de la cuenta de almacenamiento, podemos implementar el script como un trabajo de Azure Batch.

## <a name="azure-batch-architecture"></a>Arquitectura de Azure Batch
El siguiente diagrama muestra cómo se puede escalar el script de Python con Azure Batch y un cliente de Node.js.

![Escenario de Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

El cliente de node.js implementa un trabajo por lotes con una tarea de preparación (más adelante se explica con detalle) y un conjunto de tareas en función del número de contenedores de la cuenta de almacenamiento. Puede descargar los scripts del repositorio de Github.

* [Cliente de Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Scripts de shell de la tarea de preparación](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Procesador Python de CSV a JSON](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> El cliente de Node.js del enlace especificado no contiene código específico para implementarse como una instancia de Azure Function App. Puede consultar los siguientes enlaces para obtener instrucciones de cómo crear una.
> - [Creación de una instancia de Function App](../azure-functions/functions-create-first-azure-function.md)
> - [Creación de una función de desencadenador de temporizador](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a>Compilar la aplicación

Ahora, sigamos el proceso paso a paso para crear el cliente de Node.js:

### <a name="step-1-install-azure-batch-sdk"></a>Paso 1: Instalación del SDK de Azure Batch

Puede instalar el SDK de Azure Batch para Node.js con el comando npm install.

`npm install azure-batch`

Este comando instala la versión más reciente del SDK de Azure Batch.

>[!Tip]
> En una instancia de Azure Function App, puede ir a la "Consola Kudu" en la pestaña de configuración de la función de Azure para ejecutar los comandos npm install. En este caso, para instalar el SDK de Azure Batch para Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Paso 2: Creación de una cuenta de Azure Batch

Puede crearla desde [Azure Portal](batch-account-create-portal.md) o desde la línea de comandos ([Powershell](batch-powershell-cmdlets-get-started.md) /[CLI de Azure](https://docs.microsoft.com/cli/azure/overview)).

A continuación se muestran los comandos para crear una mediante la CLI de Azure.

Cree un grupo de recursos; omita este paso si ya tiene uno en el que desea crear la cuenta de Batch:

`az group create -n "<resource-group-name>" -l "<location>"`

A continuación, cree una cuenta de Azure Batch.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Cada cuenta de Batch tiene sus claves de acceso correspondientes. Estas claves se necesitan para crear más recursos en la cuenta de Azure Batch. Una práctica recomendada para el entorno de producción es usar Azure Key Vault para almacenar estas claves. Después, puede crear una entidad de servicio para la aplicación. Mediante esta entidad de servicio, la aplicación puede crear un token de OAuth para tener acceso a las claves del almacén de claves.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Copie y guarde la clave que se usará en los pasos siguientes.

### <a name="step-3-create-an-azure-batch-service-client"></a>Paso 3: Creación de un cliente de servicio de Azure Batch
El siguiente fragmento de código importa en primer lugar el módulo de Node.js de Azure Batch y, a continuación, crea un cliente de servicio de Batch. Debe crear primero un objeto SharedKeyCredentials con la clave de la cuenta de Batch que copió en el paso anterior.

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

La dirección URI de Azure Batch se puede encontrar en la pestaña Información general de Azure Portal. Tiene el formato:

`https://accountname.location.batch.azure.com`

Consulte la captura de pantalla:

![URI de Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Paso 4: Creación de un grupo de Azure Batch
Un grupo de Azure Batch consta de varias máquinas virtuales (también conocidas como nodos de Batch). El servicio Azure Batch implementa las tareas en los nodos y las administra. Puede definir los siguientes parámetros de configuración para el grupo.

* Tipo de imagen de máquina virtual
* Tamaño de los nodos de máquina virtual
* Número de nodos de máquina virtual

> [!Tip]
> El tamaño y el número de los nodos de máquina virtual dependen en gran medida del número de tareas que desee ejecutar en paralelo y de la propia tarea. Se recomienda realizar pruebas para determinar el número y tamaño ideales.
>
>

El fragmento de código siguiente crea los objetos de parámetros de configuración.

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
> Para obtener la lista de imágenes de máquinas virtuales Linux disponibles para Azure Batch y sus identificadores SKU, consulte la [Lista de imágenes de máquina virtual](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Una vez definida la configuración del grupo, puede crear el grupo de Azure Batch. El comando batch pool crea nodos de máquina virtual de Azure y los prepara para recibir tareas para ejecutar. Cada grupo debe tener un identificador único para hacer referencia a él en los siguientes pasos.

El siguiente fragmento de código crea un grupo de Azure Batch.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Puede comprobar el estado del grupo creado y asegurarse de que el estado es "activo" antes de continuar con el envío de un trabajo a ese grupo.

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

A continuación se muestra un ejemplo de objeto devuelto por la función pool.get.

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


### <a name="step-4-submit-an-azure-batch-job"></a>Paso 4: Envío de un trabajo a Azure Batch
Un trabajo de Azure Batch es un grupo lógico de tareas similares. En nuestro escenario, es "Conversión de CSV a JSON". Cada tarea aquí podría estar procesando archivos CSV presentes en cada contenedor de Azure Storage.

Estas tareas se ejecutan en paralelo y se implementan a través de varios nodos, organizados por el servicio de Azure Batch.

> [!Tip]
> Puede usar la propiedad [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) para especificar el número máximo de tareas que pueden ejecutarse simultáneamente en un único nodo.
>
>

#### <a name="preparation-task"></a>Tarea de preparación

Los nodos de máquina virtual creados son nodos Ubuntu en blanco. A menudo, necesitará instalar un conjunto de programas como requisitos previos.
Por lo general, para los nodos de Linux puede tener un script de shell que instale los requisitos previos antes de la ejecución de las tareas reales. No obstante, puede ser cualquier programa ejecutable.
El [script de shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) de este ejemplo instala Python-pip y el SDK de Azure Storage para Python.

Puede cargar el script en una cuenta de Azure Storage y generar un URI de SAS para tener acceso al script. Este proceso también se puede automatizar utilizando el SDK de Azure Storage para Node.js.

> [!Tip]
> Una tarea de preparación de un trabajo se ejecuta solo en los nodos de máquina virtual en los que la tarea específica necesita ejecutarse. Si desea que los requisitos previos se instalen en todos los nodos con independencia de las tareas que se ejecutan en él, puede usar la propiedad [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) al agregar un grupo. Puede utilizar como referencia la definición de tarea de preparación siguiente.
>
>

La tarea de preparación se especifica durante el envío de un trabajo de Azure Batch. Estos son los parámetros de configuración de la tarea de preparación:

* **ID**: identificador único de la tarea de preparación
* **commandLine**: comando para ejecutar la tarea
* **resourceFiles**: matriz de objetos que proporciona detalles de los archivos que se deben descargar para que la tarea se ejecute.  Las opciones son
    - blobSource: el URI de SAS del archivo
    - filePath: ruta de acceso local para descargar y guardar el archivo
    - fileMode: fileMode solo es aplicable para nodos de Linux, está en formato octal con un valor predeterminado de 0770
* **waitForSuccess**: si se establece en true, la tarea no se ejecuta si existen errores en la tarea de preparación
* **runElevated**: establézcalo en true si se necesitan privilegios elevados para ejecutar la tarea.

El fragmento de código siguiente muestra el ejemplo de script de configuración de la tarea de preparación:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Si no hay requisitos previos de instalación para la ejecución de las tareas, puede omitir las tareas de preparación. El código siguiente crea un trabajo con el nombre para mostrar "process csv files" (procesar archivos CSV).

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Paso 5: Envío de tareas de Azure Batch para un trabajo

Una vez creado el trabajo para procesar archivos CSV, se crearán las tareas para dicho trabajo. Suponiendo que tenemos cuatro contenedores, tenemos que crear cuatro tareas, una para cada contenedor.

Si observamos el [script de Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), vemos que acepta dos parámetros:

* container name: (nombre del contenedor) el contenedor de almacenamiento desde el que se van a descargar los archivos
* pattern: (patrón) parámetro opcional de un patrón de nombre de archivo

Suponiendo que tenemos cuatro contenedores denominados "con1", "con2", "con3" y "con4", el siguiente código muestra el envío de tareas al trabajo de Azure Batch denominado "process csv" (procesar archivos CSV) que creamos anteriormente.

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

El código agrega varias tareas al grupo. Y cada una de las tareas se ejecuta en un nodo en el grupo de máquinas virtuales que se creó. Si el número de tareas supera el número de máquinas virtuales en un grupo o el valor de la propiedad maxTasksPerNode, las tareas esperan hasta que un nodo queda disponible. Azure Batch controla esta orquestación de un modo automático.

El portal tiene vistas detalladas del estado de las tareas y trabajos. También puede utilizar la lista y obtener funciones en el SDK de Azure Batch para Node.js. En la documentación del siguiente [enlace](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html) se proporcionan más detalles.

## <a name="next-steps"></a>Pasos siguientes

- Consulte el artículo [Información general de las características de Lote de Azure](batch-api-basics.md) , que es especialmente recomendable si no se conoce el servicio.
- Consulte la [referencia de Batch Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) para explorar la API de Batch.

