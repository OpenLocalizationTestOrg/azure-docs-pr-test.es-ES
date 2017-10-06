---
title: aaaCreate tareas tooprepare trabajos y tareas completadas en nodos de proceso - Azure Batch | Documentos de Microsoft
description: "Usar datos de toominimize de tareas de preparación de nivel de trabajo transferir nodos de proceso por lotes de tooAzure y tareas de limpieza de nodo a la conclusión del trabajo de la versión."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Ejecución de tareas de preparación y liberación de trabajos en nodos de proceso de Batch

 A menudo, Azure Batch requiere algún tipo de configuración antes de ejecutar sus tareas y un mantenimiento posterior al trabajo una vez completadas sus tareas. Tal vez necesite toodownload comunes tarea datos de entrada tooyour proceso nodos, o se puede cargar tooAzure de datos de salida de tareas almacenamiento una vez completado el trabajo de Hola. Puede usar **preparación del trabajo** y **trabajo versión** tareas tooperform estas operaciones.

## <a name="what-are-job-preparation-and-release-tasks"></a>Tareas de preparación y liberación de trabajos
Antes de ejecutarán las tareas de un trabajo, tarea de preparación del trabajo de hello ejecuta en todos los toorun programada nodos de proceso al menos una tarea. Una vez que se complete el trabajo de hello, tarea de liberación del trabajo de Hola se ejecuta en cada nodo de grupo de Hola que ejecuta al menos una tarea. Al igual que con las tareas normales de lote, puede especificar un toobe de línea de comandos que se invoca cuando una preparación del trabajo o se ejecuta la tarea de liberación.

Las tareas de preparación y liberación ofrecen características de tareas de Batch familiares, como la descarga de archivos ([archivos de recursos][net_job_prep_resourcefiles]), la ejecución con elevación de privilegios, las variables de entorno personalizadas, la duración máxima de ejecución, el número de reintentos y el tiempo de retención de archivos.

Hola siguientes secciones, aprenderá cómo hello toouse [JobPreparationTask] [ net_job_prep] y [JobReleaseTask] [ net_job_release] clases se encuentran en hello [.NET de lotes] [ api_net] biblioteca.

> [!TIP]
> Las tareas de preparación y liberación de trabajos son especialmente útiles en entornos de "grupo compartido", en los que un grupo de nodos de proceso persiste entre ejecuciones de trabajo y muchos trabajos lo usan.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Cuando toouse preparación del trabajo y tareas de la versión
Preparación del trabajo y tareas de la versión de trabajo son una buena elección para hello siguientes situaciones:

**Descarga de datos de tareas comunes**

Trabajos por lotes requieren a menudo un conjunto común de datos como entrada para las tareas del trabajo de Hola. Por ejemplo, en los cálculos de análisis de riesgos diaria, datos de mercado son específicos del trabajo, pero common tareas tooall trabajo de Hola. Estos datos de mercado, a menudo varios gigabytes de tamaño, deben ser una sola vez tooeach descargado de nodos de proceso que puede utilizar cualquier tarea que se ejecuta en el nodo de Hola. Use un **tareas de preparación del trabajo** toodownload este nodo de tooeach datos antes ejecución Hola de trabajo de Hola de otras tareas.

**Trabajo persistente y resultado de la tarea**

En un entorno compartido» grupo", donde los nodos de proceso del grupo no están dado de baja entre los trabajos, puede ser necesario toodelete datos del trabajo entre ejecuciones. Es posible que tenga tooconserve espacio en disco en los nodos de Hola o cumplir las directivas de seguridad de su organización. Use un **tarea de liberación del trabajo** datos toodelete descargados por una tarea de preparación del trabajo, o generados durante la ejecución de la tarea.

**Retención de registro**

Puede ser conveniente tookeep una copia de archivos de registro que generan las tareas, o quizás archivos de volcado que se pueden generar aplicaciones con errores. Use un **tarea de liberación del trabajo** en tales casos toocompress y cargar este tooan datos [el almacenamiento de Azure] [ azure_storage] cuenta.

> [!TIP]
> Toopersist de otra manera datos se toouse Hola de salida de registros y otros trabajos y tareas [convenciones de archivos por lotes de Azure](batch-task-output.md) biblioteca.
> 
> 

## <a name="job-preparation-task"></a>tarea de preparación del trabajo
Antes de la ejecución de tareas de un trabajo, lote ejecuta la tarea de preparación del trabajo de hello en cada nodo de proceso que está programada toorun una tarea. De manera predeterminada, Hola servicio por lotes espera toobe de tareas de preparación Hola trabajo completado antes de ejecutar tooexecute de hello tareas programadas en el nodo de Hola. Sin embargo, puede configurar el servicio de hello no toowait. Si se reinicia el nodo de hello, tarea de preparación de hello trabajo se ejecuta de nuevo, pero también se puede deshabilitar este comportamiento.

se ejecuta la tarea de preparación del trabajo de Hello solo en nodos que estén programada toorun una tarea. Esto impide la ejecución innecesarios de Hola de una tarea de preparación en caso de que un nodo no está asignado a una tarea. Esto puede ocurrir cuando número Hola de tareas para un trabajo es menor que el número de Hola de nodos en un grupo. También se aplica cuando [ejecución de tareas simultáneas](batch-parallel-node-tasks.md) está habilitada, lo que deja a algunos nodos inactivo si recuento de tareas de hello es inferior a tareas simultáneas posibles total Hola. No ejecutando tarea de preparación del trabajo de hello en nodos inactivos, puede ahorrar dinero en gastos de transferencia de datos.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] difiere de [CloudPool.StartTask] [ pool_starttask] en que JobPreparationTask se ejecuta en el inicio de Hola de cada trabajo, mientras que StartTask se ejecuta solo cuando un nodo de proceso en primer lugar une a un grupo o se reinicia.
> 
> 

## <a name="job-release-task"></a>tarea de liberación del trabajo
Una vez que un trabajo está marcado como completada, la tarea de liberación del trabajo de Hola se ejecuta en cada nodo de grupo de Hola que ejecuta al menos una tarea. El trabajo se marca como completado mediante la emisión de una solicitud de finalización. Hola servicio por lotes, a continuación, Establece Hola estado del trabajo demasiado*terminación*, finaliza las tareas activas o en ejecución asociadas con el trabajo de Hola y ejecuta la tarea de liberación del trabajo de Hola. trabajo de Hello, a continuación, mueve toohello *completado* estado.

> [!NOTE]
> Eliminación de trabajo también ejecuta la tarea de liberación del trabajo de Hola. Sin embargo, si ya ha finalizado un trabajo, tarea de liberación de hello no se ejecuta una segunda vez si más adelante se elimina el trabajo de Hola.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Tareas de preparación y liberación de trabajos con Lote para .NET
asignar una tarea de preparación del trabajo, toouse una [JobPreparationTask] [ net_job_prep] del trabajo de objeto tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propiedad . Inicializar de forma similar, un [JobReleaseTask] [ net_job_release] y asígnele el nombre del trabajo de tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset de propiedad tarea de liberación del trabajo.

En este fragmento de código, `myBatchClient` es una instancia de [BatchClient][net_batch_client], y `myPool` es un grupo existente dentro de hello cuenta de lote.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Tal y como se mencionó anteriormente, la tarea de versión de Hola se ejecuta cuando se finaliza o se elimina un trabajo. Finalice un trabajo con [JobOperations.TerminateJobAsync][net_job_terminate]. Elimine un trabajo con [JobOperations.DeleteJobAsync][net_job_delete]. Normalmente un trabajo se termina o elimina cuando se han completado sus tareas o cuando se ha alcanzado el tiempo de espera que haya definido.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Código de ejemplo en GitHub
las tareas de preparación y la versión del trabajo de toosee en acción, visite hello [JobPrepRelease] [ job_prep_release_sample] proyecto de ejemplo en GitHub. Esta aplicación de consola Hola siguientes:

1. Crea un grupo con dos nodos "pequeños".
2. Crea un trabajo con las tareas de preparación y de liberación del trabajo, además de las estándar.
3. Se ejecuta Hola tarea de preparación del trabajo, que escribe primero el archivo de texto de tooa de Id. de nodo de hello en el directorio "compartido" de un nodo.
4. Ejecuta una tarea en cada nodo que escribe su toohello de Id. de tarea mismo archivo de texto.
5. Una vez que se completan todas las tareas (o se alcanza el tiempo de espera de hello), imprime el contenido de Hola de consola de toohello de archivos de texto de cada nodo.
6. Cuando se completa el trabajo de hello, ejecuta archivo de hello trabajo versión tarea toodelete Hola de nodo de Hola.
7. Hola imprime códigos de preparación del trabajo Hola de salida y las tareas para cada nodo en el que ejecuta la versión.
8. Confirmación de tooallow de la ejecución de las pausas de eliminación de trabajo o grupo.

Resultado de la aplicación de ejemplo de Hola es siguiente de toohello similar:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> Pagar toohello variable creación y hora de inicio de nodos en un grupo nuevo (algunos nodos no están listos para tareas antes que otras), puede ver un resultado diferente. En concreto, dado que las tareas de hello completan rápidamente, uno de los nodos del grupo de hello puede ejecutar todas las tareas del trabajo de Hola de. Si esto ocurre, observará que Hola prep del trabajo y tareas de la versión no existe para el nodo de Hola que no ejecutar ninguna tarea.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Inspeccionar la preparación del trabajo y las tareas de la versión de Hola portal de Azure
Cuando se ejecuta la aplicación de ejemplo de Hola, puede usar hello [portal de Azure] [ portal] tooview Hola propiedades del trabajo de Hola y sus tareas, o incluso descargar archivo de texto compartida hello modificado por tareas del trabajo de Hola.

Hola de captura de pantalla siguiente muestra hello **hoja de tareas de preparación** en el portal de Azure después de una ejecución de la aplicación de ejemplo de Hola Hola. Navegue toohello *JobPrepReleaseSampleJob* propiedades después de han completado las tareas (pero antes de eliminar el trabajo y grupo) y haga clic en **tareas de preparación** o **versión tareas** tooview sus propiedades.

![Propiedades de preparación del trabajo en el Portal de Azure][1]

## <a name="next-steps"></a>Pasos siguientes
### <a name="application-packages"></a>paquetes de aplicación
En la tarea de preparación de suma toohello trabajo, también puede utilizar hello [paquetes de aplicación](batch-application-packages.md) nodos para la ejecución de la tarea de ejecución de la característica de tooprepare de lote. Esta característica es especialmente útil para implementar aplicaciones que no requieren que se ejecute un instalador, aplicaciones que contienen muchos archivos (más de 100) o aplicaciones que requieren un control estricto de la versión.

### <a name="installing-applications-and-staging-data"></a>Instalación de aplicaciones y datos de ensayo
Este foro de MSDN proporciona información general de varios métodos de preparación de los nodos para la ejecución de tareas:

[Installing applications and staging data on Batch compute nodes][forum_post] (Instalación de aplicaciones y datos de ensayo en nodos de proceso de Batch)

Escrito por uno de los miembros del equipo de Azure Batch de hello, describe varias técnicas que puede usar los nodos de toocompute de aplicaciones y datos de toodeploy.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
