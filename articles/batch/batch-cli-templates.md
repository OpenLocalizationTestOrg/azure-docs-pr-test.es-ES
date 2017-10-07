---
title: "aaaRun Azure Batch trabajos to-end sin escribir código (versión preliminar) | Documentos de Microsoft"
description: Crear archivos de plantilla para grupos de hello Azure CLI toocreate por lotes, los trabajos y tareas.
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="2df58-103">Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2df58-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="2df58-104">Con hello CLI de Azure es posible toorun los trabajos por lotes sin escribir código.</span><span class="sxs-lookup"><span data-stu-id="2df58-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="2df58-105">Archivos de plantilla se pueden crear y usar con hello CLI de Azure que permiten grupos por lotes, los trabajos y toobe de tareas crea.</span><span class="sxs-lookup"><span data-stu-id="2df58-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="2df58-106">Archivos de entrada de trabajo se pueden cargar fácilmente a cuenta de almacenamiento de hello asociada Hola lote cuenta y trabajo de salida archivos descargados.</span><span class="sxs-lookup"><span data-stu-id="2df58-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="2df58-107">Información general</span><span class="sxs-lookup"><span data-stu-id="2df58-107">Overview</span></span>

<span data-ttu-id="2df58-108">Un toohello de extensión CLI de Azure permite por lotes toobe usa-to-end por los usuarios que no son programadores.</span><span class="sxs-lookup"><span data-stu-id="2df58-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="2df58-109">Se puede crear un grupo, cargan los datos de entrada, trabajos y las tareas asociadas que se creó, y Hola resultante salida datos descargados: no se necesita, código Hola CLI que se va a usar directamente o que se integra en las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="2df58-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="2df58-110">Crear plantillas de proceso por lotes en hello [soporte técnico de lote existente en hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) que permite a los archivos JSON toospecify valores de propiedad para la creación de hello de grupos, trabajos, tareas y otros elementos.</span><span class="sxs-lookup"><span data-stu-id="2df58-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="2df58-111">Con las plantillas de proceso por lotes, hello las capacidades siguientes se han agregado sobre lo que es posible con archivos JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="2df58-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="2df58-112">Se pueden definir los parámetros.</span><span class="sxs-lookup"><span data-stu-id="2df58-112">Parameters can be defined.</span></span> <span data-ttu-id="2df58-113">Cuando se usa la plantilla de hello, solo los valores de parámetro de hello son elementos de Hola de toocreate especificado, con otros valores de propiedad de elemento que se especifican en el cuerpo de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="2df58-114">Un usuario que se entiende por lotes y el toobe de las aplicaciones que se ejecutan por lotes puede crear plantillas, especificar el grupo de trabajo y valores de propiedad de la tarea.</span><span class="sxs-lookup"><span data-stu-id="2df58-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="2df58-115">Un usuario menos familiarizados con el proceso por lotes o las aplicaciones solo necesita valores de hello toospecify para los parámetros de hello definido.</span><span class="sxs-lookup"><span data-stu-id="2df58-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="2df58-116">Generadores de tareas de trabajo cree uno o más tareas asociadas a un trabajo, evitar Hola necesitan para muchos toobe de definiciones de tarea creado y simplificar considerablemente el envío de trabajos.</span><span class="sxs-lookup"><span data-stu-id="2df58-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="2df58-117">Archivos de datos de entrada necesitan toobe proporcionado para los trabajos y a menudo se generan archivos de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="2df58-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="2df58-118">Se asocia una cuenta de almacenamiento, de forma predeterminada, con cada lote cuenta y archivos pueden ser tooand fácilmente transferido desde esta cuenta de almacenamiento mediante la CLI, sin codificación y credenciales de almacenamiento no necesitan.</span><span class="sxs-lookup"><span data-stu-id="2df58-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="2df58-119">Por ejemplo, [ffmpeg](http://ffmpeg.org/) es una aplicación popular que procesa archivos de audio y video.</span><span class="sxs-lookup"><span data-stu-id="2df58-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="2df58-120">Hola CLI de lote de Azure puede ser usado tooinvoke ffmpeg tootranscode origen archivos de vídeo toodifferent resoluciones.</span><span class="sxs-lookup"><span data-stu-id="2df58-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="2df58-121">Se crea una plantilla de grupo.</span><span class="sxs-lookup"><span data-stu-id="2df58-121">A pool template is created.</span></span> <span data-ttu-id="2df58-122">usuario de Hello crear plantilla de hello sabe cómo toocall Hola ffmpeg aplicación y a sus requisitos; especifican Hola SO adecuado, la máquina virtual de tamaño, cómo ffmpeg está instalado (de un paquete de aplicación o mediante un administrador de paquetes, por ejemplo) y otros valores de propiedad del grupo.</span><span class="sxs-lookup"><span data-stu-id="2df58-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="2df58-123">Por lo que cuando se usa la plantilla de hello, solo el identificador del grupo de Hola y número de máquinas virtuales necesitan toobe especificado, se crean parámetros.</span><span class="sxs-lookup"><span data-stu-id="2df58-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="2df58-124">Se crea una plantilla de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2df58-124">A job template is created.</span></span> <span data-ttu-id="2df58-125">plantilla de Hola de creación de Hello usuario sabe cómo ffmpeg necesidades toobe invoca otra resolución de tootranscode origen tooa vídeo y especifica la línea de comandos de la tarea de hello; También sabe que hay una carpeta que contiene los archivos de vídeo de origen de hello, con una tarea obligatoria por archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="2df58-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="2df58-126">Un usuario final con un conjunto de archivos de vídeo tootranscode primero crea un grupo mediante la plantilla de grupo de hello, especificar solo Id. de grupo de Hola y el número de máquinas virtuales necesarias.</span><span class="sxs-lookup"><span data-stu-id="2df58-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="2df58-127">A continuación, puede cargar tootranscode de archivos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="2df58-128">A continuación, se puede enviar un trabajo con la plantilla de trabajo de hello, especificando solo Id. de grupo de hello y una ubicación de archivos de origen de hello cargada.</span><span class="sxs-lookup"><span data-stu-id="2df58-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="2df58-129">se crea el trabajo por lotes de Hello, con una tarea por cada archivo de entrada que se está generando.</span><span class="sxs-lookup"><span data-stu-id="2df58-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="2df58-130">Por último, los archivos de salida de hello transcodifica pueden ser descarga.</span><span class="sxs-lookup"><span data-stu-id="2df58-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="2df58-131">Instalación</span><span class="sxs-lookup"><span data-stu-id="2df58-131">Installation</span></span>

<span data-ttu-id="2df58-132">capacidades de transferencia de plantilla y el archivo Hello requieren un toobe de extensión instalada.</span><span class="sxs-lookup"><span data-stu-id="2df58-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="2df58-133">Para obtener instrucciones sobre cómo ver tooinstall hello Azure CLI [instalar Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2df58-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="2df58-134">Una vez Hola que CLI de Azure se ha instalado, Hola lote extensión se puede instalar mediante el siguiente comando CLI:</span><span class="sxs-lookup"><span data-stu-id="2df58-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="2df58-135">Para obtener más información acerca de la extensión de lote de Hola, consulte [Azure de Microsoft CLI de lote extensiones para Windows, Mac y Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="2df58-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="2df58-136">Plantillas</span><span class="sxs-lookup"><span data-stu-id="2df58-136">Templates</span></span>

<span data-ttu-id="2df58-137">Hola CLI de lote de Azure permite elementos como grupos, los trabajos y toobe de tareas que se creó mediante la especificación de un archivo JSON que contiene los valores y nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="2df58-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="2df58-138">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2df58-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="2df58-139">Plantillas de proceso por lotes de Azure son plantillas de administrador de recursos tooAzure similares, en la funcionalidad y la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="2df58-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="2df58-140">Son archivos JSON que contienen los nombres de propiedad de elemento y valores, pero agregar Hola después conceptos principales:</span><span class="sxs-lookup"><span data-stu-id="2df58-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="2df58-141">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="2df58-141">**Parameters**</span></span>

    -   <span data-ttu-id="2df58-142">Permitir toobe de valores de propiedad especificado en una sección de cuerpo, con solo los valores de parámetros que necesitan toobe proporcionado cuando se usa la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="2df58-143">Por ejemplo, podría colocarse hello contiene toda la definición de un grupo en el cuerpo de Hola y solo un parámetro definido para el Id. de grupo; Por tanto, sólo una cadena de identificador de grupo debe toocreate toobe proporcionado un grupo.</span><span class="sxs-lookup"><span data-stu-id="2df58-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="2df58-144">cuerpo de la plantilla de Hello puede crearse alguien con conocimientos del lote y Hola aplicaciones toobe ejecutada por lote; solo los valores de parámetros definidos por el autor de hello deben proporcionarse cuando se usa la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="2df58-145">Un usuario sin Hola lote detallada o conocimiento de las aplicaciones, por tanto, puede usar las plantillas.</span><span class="sxs-lookup"><span data-stu-id="2df58-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="2df58-146">**Variables**</span><span class="sxs-lookup"><span data-stu-id="2df58-146">**Variables**</span></span>

    -   <span data-ttu-id="2df58-147">Permitir toobe de valores de parámetro simples o complejas especificado en un solo lugar y utilizar en uno o varios lugares en el cuerpo de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="2df58-148">Las variables pueden simplificar y reducir el tamaño de Hola de plantilla de hello, así como que sea más fácil de mantener si tiene uno cuyo valor puede cambiar propiedades de ubicación de toochange.</span><span class="sxs-lookup"><span data-stu-id="2df58-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="2df58-149">**Construcciones de nivel superiores**</span><span class="sxs-lookup"><span data-stu-id="2df58-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="2df58-150">Algunas construcciones de nivel superiores están disponibles en la plantilla de Hola que todavía no están disponibles en hello las API de lote.</span><span class="sxs-lookup"><span data-stu-id="2df58-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="2df58-151">Por ejemplo, un generador de tareas puede definirse en una plantilla de trabajo que crea varias tareas de trabajo de hello mediante una definición de tarea común.</span><span class="sxs-lookup"><span data-stu-id="2df58-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="2df58-152">Estas construcciones evitar Hola necesidad toocode para dinámicamente crear varios archivos JSON, por ejemplo, un archivo por cada tarea, así como para crear aplicaciones de tooinstall de archivos a través de un administrador de paquetes, por ejemplo de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="2df58-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="2df58-153">En algún punto, cuando agregan aplicables, que estas construcciones pueden toothe lote servicio y está disponible en hello las API de lote, interfaces de usuario, etcetera.</span><span class="sxs-lookup"><span data-stu-id="2df58-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="2df58-154">Plantillas de grupo</span><span class="sxs-lookup"><span data-stu-id="2df58-154">Pool templates</span></span>

<span data-ttu-id="2df58-155">Además, funciones de plantilla estándar de toohello de parámetros y variables, Hola siguientes construcciones de nivel superiores son compatibles con plantilla de grupo de hello:</span><span class="sxs-lookup"><span data-stu-id="2df58-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="2df58-156">**Referencias de paquetes**</span><span class="sxs-lookup"><span data-stu-id="2df58-156">**Package references**</span></span>

    -   <span data-ttu-id="2df58-157">Opcionalmente, permite software toobe copian toopool nodos mediante paquete administradores.</span><span class="sxs-lookup"><span data-stu-id="2df58-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="2df58-158">Administrador de paquetes de saludo y el Id. de paquete se especifican.</span><span class="sxs-lookup"><span data-stu-id="2df58-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="2df58-159">Que se va a toodeclare capaz de uno o más paquetes evita Hola necesidad toocreate un script que obtiene los paquetes de saludo necesario, Hola script de instalación y ejecutar script de Hola en cada nodo de grupo.</span><span class="sxs-lookup"><span data-stu-id="2df58-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="2df58-160">Hola aquí te mostramos un ejemplo de una plantilla que crea un grupo de máquinas virtuales de Linux con ffmpeg instalada y solo requiere un número de hello y cadena de Id. de grupo de máquinas virtuales toobe proporcionado toouse:</span><span class="sxs-lookup"><span data-stu-id="2df58-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="2df58-161">Si se denomina archivo de plantilla de hello _ffmpeg.json grupo_, a continuación, sería necesario invocar una plantilla de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="2df58-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="2df58-162">Plantillas de trabajo</span><span class="sxs-lookup"><span data-stu-id="2df58-162">Job templates</span></span>

<span data-ttu-id="2df58-163">Además, funciones de plantilla estándar de toohello de parámetros y variables, Hola siguientes construcciones de nivel superiores son compatibles con plantilla de trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="2df58-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="2df58-164">**Fábrica de tareas**</span><span class="sxs-lookup"><span data-stu-id="2df58-164">**Task factory**</span></span>

    -   <span data-ttu-id="2df58-165">Crea varias tareas para un trabajo a partir de una definición de tarea.</span><span class="sxs-lookup"><span data-stu-id="2df58-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="2df58-166">Se admiten tres tipos de fábricas de tareas: barrido paramétrico, tarea por archivo y colección de tareas.</span><span class="sxs-lookup"><span data-stu-id="2df58-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="2df58-167">Hola te mostramos un ejemplo de una plantilla que crea un trabajo que utiliza ffmpeg para transcodificar tooone de archivos de vídeo MP4 de dos resoluciones más bajas, con una tarea creada por el archivo de vídeo de origen:</span><span class="sxs-lookup"><span data-stu-id="2df58-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="2df58-168">Si se denomina archivo de plantilla de hello _ffmpeg.json de trabajo_, a continuación, sería necesario invocar una plantilla de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="2df58-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="2df58-169">Grupos de archivos y transferencia de archivos</span><span class="sxs-lookup"><span data-stu-id="2df58-169">File groups and file transfer</span></span>

<span data-ttu-id="2df58-170">La mayoría de los trabajos y tareas requieren archivos de entrada y generan archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="2df58-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="2df58-171">Ambos archivos de entrada y archivos de salida normalmente necesitan toobe transferido desde el nodo de toohello de cliente de Hola o de cliente de hello nodo toohello.</span><span class="sxs-lookup"><span data-stu-id="2df58-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="2df58-172">Hola extensión de CLI de lote de Azure abstrae la transferencia de archivos de ubicación y utiliza la cuenta de almacenamiento de Hola que se crea de forma predeterminada para cada cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="2df58-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="2df58-173">Un grupo de archivos es el mismo contenedor de tooa que se crea en Hola cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="2df58-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="2df58-174">grupo de archivos de Hello puede tener subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="2df58-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="2df58-175">Hola extensión lote CLI proporciona comandos para cargar archivos del grupo de archivos especificado tooa de cliente y descargar archivos desde el cliente de tooa de grupo de archivo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="2df58-176">Las plantillas de grupo y de trabajo permiten archivos almacenados en toobe de grupos de archivos especificado para la copia en los nodos de grupo o desactivar el grupo de nodos en espera tooa grupo de archivos.</span><span class="sxs-lookup"><span data-stu-id="2df58-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="2df58-177">Por ejemplo, en la plantilla de trabajo que se especificó anteriormente, se especifica los archivo de hello grupo "ffmpeg-entrada" para el generador de tareas de hello como ubicación de los archivos de vídeo de origen de hello copiado en el nodo de hello para la transcodificación; las Hola Hola archivo grupo "ffmpeg-output" se utiliza como ubicación donde se archivos de salida de hello transcodifica hello copia nodo de hello toofrom ejecutando cada tarea.</span><span class="sxs-lookup"><span data-stu-id="2df58-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="2df58-178">Resumen</span><span class="sxs-lookup"><span data-stu-id="2df58-178">Summary</span></span>

<span data-ttu-id="2df58-179">Actualmente se han agregado soporte técnico de transferencia de plantilla y el archivo solo toohello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="2df58-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="2df58-180">objetivo de Hello es público de hello tooexpand que puede usar toousers de lote que no necesitan código toodevelop con hello las API de lote, por ejemplo, los investigadores, los usuarios de TI y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="2df58-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="2df58-181">Sin codificar de forma, los usuarios con conocimientos de Azure, lote y Hola aplicaciones toobe ejecutada por lote pueden crear plantillas para la creación de grupo y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2df58-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="2df58-182">Con parámetros de plantilla, los usuarios sin un conocimiento detallado de las aplicaciones de hello y por lotes pueden utilizar plantillas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2df58-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="2df58-183">Probar Hola extensión de lote para hello Azure CLI y proporcionarnos los comentarios y sugerencias, ya sea hello en los comentarios de este artículo o a través de hello [foro de Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="2df58-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2df58-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2df58-184">Next steps</span></span>

- <span data-ttu-id="2df58-185">Consulte blog de plantillas de proceso por lotes hello: [Hola de trabajos de ejecución por lotes de Azure mediante Azure CLI: no se necesita código](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="2df58-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="2df58-186">Documentación detallada de instalación y uso, ejemplos y código fuente están disponibles en hello [repositorio de GitHub de Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="2df58-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
