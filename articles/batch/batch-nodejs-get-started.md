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
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Introducción al SDK de Batch para Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Obtenga información acerca de los conceptos básicos de hello de la creación de un cliente de lote de uso de Node.js [Node.js de lote de Azure SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Vamos a describir paso a paso un escenario de aplicación por lotes y, a continuación, su configuración mediante un cliente de Node.js.  

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por hecho que tiene conocimientos prácticos de Node.js y está familiarizado con Linux. También se da por supuesto que tiene una configuración de Azure cuenta con acceso derechos toocreate por lotes y almacenamiento de los servicios.

Es recomendable leer [Introducción técnica a Azure Batch](batch-technical-overview.md) antes de ir a través de pasos de hello, que describen en este artículo.

## <a name="hello-tutorial-scenario"></a>escenario del tutorial Hola
Vamos a explicar escenario de flujo de trabajo por lotes de Hola. Tenemos un script simple escrito en Python que descarga csv todos los archivos de un contenedor de almacenamiento de blobs de Azure y los convierte tooJSON. tooprocess cuenta de almacenamiento varios contenedores en paralelo, podemos implementar secuencias de comandos de Hola como un trabajo por lotes de Azure.

## <a name="azure-batch-architecture"></a>Arquitectura de Azure Batch
Hello siguiente diagrama muestra cómo se puede escalar script de Python de hello con Azure Batch y un cliente de Node.js.

![Escenario de Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

cliente de node.js Hola implementa un proceso por lotes con una tarea de preparación (más adelante se explica con detalle) y un conjunto de tareas en función del número de Hola de contenedores en la cuenta de almacenamiento de Hola. Puede descargar scripts de Hola de repositorio de github de Hola.

* [Cliente de Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Scripts de shell de la tarea de preparación](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Procesador de tooJSON de csv de Python](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> cliente de Node.js de Hello en el vínculo de hello especificado no contiene toobe de código concretos implementado como una aplicación de Azure de función. Puede hacer referencia a toohello siguientes vínculos para obtener instrucciones toocreate uno.
> - [Creación de una instancia de Function App](../azure-functions/functions-create-first-azure-function.md)
> - [Creación de una función de desencadenador de temporizador](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Compilar la aplicación hello

Ahora, nos gustaría seguir el proceso de hello paso a paso en la compilación de cliente de Node.js de Hola:

### <a name="step-1-install-azure-batch-sdk"></a>Paso 1: Instalación del SDK de Azure Batch

Puede instalar el SDK de lote de Azure para Node.js con el comando de instalación de npm Hola.

`npm install azure-batch`

Este comando instala la versión más reciente de hello del nodo de lote de azure SDK.

>[!Tip]
> En una aplicación de la función de Azure, puede ir demasiado comandos de instalación de configuración de la "Kudu consola" Hola función Azure pestaña toorun Hola npm. En este caso tooinstall SDK de lote de Azure para Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Paso 2: Creación de una cuenta de Azure Batch

Se puede crear desde hello [portal de Azure](batch-account-create-portal.md) o desde la línea de comandos ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli de Azure](https://docs.microsoft.com/cli/azure/overview)).

Estos son Hola comandos toocreate uno mediante la CLI de Azure.

Crear un grupo de recursos, omita este paso si ya tiene una en la que desea toocreate Hola cuenta de lote:

`az group create -n "<resource-group-name>" -l "<location>"`

A continuación, cree una cuenta de Azure Batch.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Cada cuenta de Batch tiene sus claves de acceso correspondientes. Estas claves son toocreate necesarios más recursos en la cuenta de lote de Azure. Una práctica recomendada para el entorno de producción es toouse el almacén de claves de Azure toostore estas claves. A continuación, puede crear un servicio principal para la aplicación hello. Con esta aplicación Hola principal de servicio, puede crear un claves de tooaccess token de OAuth de almacén de claves de Hola.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Copie y almacene hello toobe clave usado en pasos posteriores de Hola.

### <a name="step-3-create-an-azure-batch-service-client"></a>Paso 3: Creación de un cliente de servicio de Azure Batch
Fragmento de código siguiente primero importa módulo Node.js de hello lote de azure y, a continuación, crea a un cliente de servicio por lotes. Necesita toofirst crear un objeto SharedKeyCredentials con clave de cuenta de lote Hola copiado desde el paso anterior de Hola.

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

Hola URI de lote de Azure puede encontrarse en la ficha de información general de Hola de hello portal de Azure. Es de formato de hello:

`https://accountname.location.batch.azure.com`

Consulte la captura de pantalla de toohello:

![URI de Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Paso 4: Creación de un grupo de Azure Batch
Un grupo de Azure Batch consta de varias máquinas virtuales (también conocidas como nodos de Batch). Servicio de lote de Azure implementa tareas hello en esos nodos y administrarlos. Puede definir Hola siguientes parámetros de configuración para el grupo.

* Tipo de imagen de máquina virtual
* Tamaño de los nodos de máquina virtual
* Número de nodos de máquina virtual

> [!Tip]
> tamaño de Hola y el número de nodos de la máquina Virtual dependen en gran medida Hola número de tareas que desea toorun en paralelo y también propia tarea hello. Se recomienda probar el tamaño y número ideal de toodetermine Hola.
>
>

Hello fragmento de código siguiente crea Hola objetos de parámetro de configuración.

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
> Consulte Hola lista de imágenes de VM de Linux disponibles para el lote de Azure y sus identificadores de SKU, [lista de imágenes de máquina virtual](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Una vez que se define la configuración del grupo de hello, puede crear el grupo de lote de Azure de Hola. Hola comando de grupo por lotes crea nodos de máquina Virtual de Azure y prepararlos toobe tooreceive listo tareas tooexecute. Cada grupo debe tener un identificador único para hacer referencia a él en los siguientes pasos.

Hola siguiente fragmento de código crea un grupo de lote de Azure.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Puede comprobar el estado de Hola Hola del grupo de creado y asegúrese de que es el estado de hello en "activo" antes de seguir adelante con el envío de un grupo de trabajo toothat.

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

Aquí te mostramos un objeto de resultado de ejemplo devuelto por la función de pool.get Hola.

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
Un trabajo de Azure Batch es un grupo lógico de tareas similares. En nuestro escenario, es "Proceso csv tooJSON." Cada tarea aquí podría estar procesando archivos CSV presentes en cada contenedor de Azure Storage.

Estas tareas se ejecutan en paralelo e implementan a través de varios nodos, organizados por el servicio de Azure Batch Hola.

> [!Tip]
> Puede usar hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) número máximo de propiedad toospecify de tareas que pueden ejecutarse simultáneamente en un único nodo.
>
>

#### <a name="preparation-task"></a>Tarea de preparación

nodos VM de Hello creados son en blanco Ubuntu. A menudo, deberá tooinstall un conjunto de programas como requisitos previos.
Por lo general, para los nodos de Linux puede tener una secuencia de comandos de shell que instala los requisitos previos de hello antes de tareas reales Hola ejecutar. No obstante, puede ser cualquier programa ejecutable.
Hola [secuencia de comandos de shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) en este ejemplo instala pip de Python y Hola SDK de almacenamiento de Azure para Python.

Puede cargar el script de Hola en una cuenta de almacenamiento de Azure y generar un script de Hola tooaccess de URI de SAS. También se puede automatizar este proceso con hello SDK de Node.js de almacenamiento de Azure.

> [!Tip]
> Una tarea de preparación de un trabajo se ejecuta solo en nodos VM de Hola donde hello necesidades específicas toorun. Si desea toobe de requisitos previos instalado en todos los nodos con independencia de las tareas de Hola que se ejecutan en él, puede usar hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propiedad al agregar un grupo. Puede usar Hola después de la definición de la tarea de preparación para la referencia.
>
>

Una tarea de preparación se especifica durante el envío de Hola de proceso por lotes de Azure. A continuación se Hola parámetros de configuración de preparación de la tarea:

* **Id. de**: un identificador único para la tarea de preparación de hello
* **la línea de comandos**: tarea de hello tooexecute de línea de comandos ejecutable
* **resourceFiles**: matriz de objetos que proporcionan los detalles de los archivos necesarios toobe descargado para este toorun de tarea.  Las opciones son
    - blobSource: Hola URI de archivo hello SAS
    - filePath: toodownload de ruta de acceso Local y guarde el archivo hello
    - fileMode: fileMode solo es aplicable para nodos de Linux, está en formato octal con un valor predeterminado de 0770
* **waitForSuccess**: si no se ejecuta set tootrue, tarea hello en errores de tareas de preparación
* **runElevated**: establecer tootrue si privilegios elevados tarea de hello toorun necesarios.

Fragmento de código siguiente muestra el ejemplo de configuración de script de Hola preparación de la tarea:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Si no hay ningún toobe de requisitos previos instalado para su toorun de tareas, puede omitir las tareas de preparación de Hola. El código siguiente crea un trabajo con el nombre para mostrar "process csv files" (procesar archivos CSV).

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Paso 5: Envío de tareas de Azure Batch para un trabajo

Una vez creado el trabajo para procesar archivos CSV, se crearán las tareas para dicho trabajo. Suponiendo que tenemos cuatro contenedores, tenemos toocreate cuatro tareas, uno para cada contenedor.

Si miramos hello [script de Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), acepta dos parámetros:

* nombre del contenedor: Hola archivos de toodownload de contenedor de almacenamiento de
* pattern: (patrón) parámetro opcional de un patrón de nombre de archivo

Suponiendo que tenemos cuatro contenedores "con1", "con2", "con3", "con4" siguiente código muestra enviar para tareas toohello Azure batch trabajo "proceso csv" hemos creado con anterioridad.

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

código de Hello agrega grupo de toohello de varias tareas. Y cada una de las tareas de Hola se ejecuta en un nodo de grupo de Hola de máquinas virtuales que se creó. Si número Hola de tareas supera el número de Hola de máquinas virtuales en una propiedad de grupo o hello maxTasksPerNode, tareas de hello esperan hasta que un nodo se pone a disposición. Azure Batch controla esta orquestación de un modo automático.

portal de Hello, detallaron vistas sobre las tareas de Hola y Estados de trabajo. También puede usar la lista de Hola y obtener funciones en hello SDK de nodo de Azure. Se proporcionan detalles en la documentación de hello [vínculo](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Pasos siguientes

- Hola de revisión [características de información general de Azure Batch](batch-api-basics.md) artículo, que se recomienda si dispone de un nuevo servicio de toohello.
- Vea hello [Node.js de lote referencia](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore Hola API de lote.

