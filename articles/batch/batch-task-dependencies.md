---
title: "tareas de toorun de dependencias de tarea aaaUse se basan en la realización de Hola de otras tareas - Azure Batch | Documentos de Microsoft"
description: "Crear tareas que dependen de finalización de Hola de otras tareas para procesar estilo MapReduce y grandes cantidades de datos similar cargas de trabajo en el lote de Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Crear tareas de toorun que dependen de otras tareas de las dependencias entre tareas

Puede definir tareas dependencias toorun una tarea o un conjunto de tareas solo después de que se ha completado una tarea primaria. A continuación se indican algunos escenarios donde las dependencias de tareas son útiles:

* Cargas de trabajo de estilo MapReduce en la nube de Hola.
* Trabajos cuyas tareas de procesamiento de datos se pueden expresar como un gráfico acíclico dirigido (DAG).
* Procesos de representación anterior y posterior a la representación, donde cada tarea debe completar para poder iniciar la tarea siguiente de hello.
* Cualquier otro trabajo en la que dependen de tareas de nivel inferiores en la salida de hello de tareas de nivel superior.

Con las dependencias de tareas de lote, puede crear tareas que están programadas para ejecutarse en nodos de proceso después de finalizar las tareas primarias de uno o más Hola. Por ejemplo, puede crear un trabajo que represente cada fotograma de una película 3D con una tarea independiente y paralela. tarea final de Hello: Hola "tarea de mezcla--" hello representa fotogramas en hello toda la película sólo después de que todos los marcos de combinaciones se han correctamente representado.

De forma predeterminada, las tareas dependientes están programadas para ejecutarse solo después de hello primario tarea se ha completado correctamente. Puede especificar un comportamiento predeterminado de dependencia acción toooverride hello y ejecutar tareas cuando se produce un error en la tarea primaria de Hola. Vea hello [acciones de dependencia](#dependency-actions) sección para obtener más información.  

Puede crear tareas que dependan de otras en una relación de una a una o una a varias. También puede crear una dependencia de intervalo que depende una tarea en la realización de Hola de un grupo de tareas dentro de un intervalo de Id. de tarea especificado. Puede combinar estas relaciones de varios a varios de tres escenarios básicos toocreate.

## <a name="task-dependencies-with-batch-net"></a>Dependencias de tareas con Lote de .NET
En este artículo se describe cómo tooconfigure las dependencias de tareas mediante el uso de Hola [.NET de lotes] [ net_msdn] biblioteca. En primer lugar le mostraremos cómo demasiado[habilitar la dependencia de la tarea](#enable-task-dependencies) en los trabajos y, a continuación, se muestra cómo demasiado[configurar una tarea con dependencias](#create-dependent-tasks). También se describe cómo toospecify una dependencia acción toorun tareas dependientes si primario Hola se produce un error. Por último, analizamos hello [escenarios de dependencia](#dependency-scenarios) admitido por lote.

## <a name="enable-task-dependencies"></a>Habilitación de dependencias de tareas
toouse las dependencias de tareas en la aplicación de lote, primero debe configurar las dependencias de tareas de hello trabajo toouse. En .NET de lote, habilitarla en su [CloudJob] [ net_cloudjob] estableciendo su [UsesTaskDependencies] [ net_usestaskdependencies] propiedad demasiado`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

Hola anterior fragmento de código, "batchClient" es una instancia de hello [BatchClient] [ net_batchclient] clase.

## <a name="create-dependent-tasks"></a>Creación de tareas dependientes
toocreate una tarea que depende de una o varias tareas de elemento primario de finalización de hello, puede especificar que Hola tarea "depende" hello otras tareas. En .NET de lote, configurar hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] propiedad con una instancia de hello [TaskDependencies] [ net_taskdependencies] clase:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Este fragmento de código crea una tarea dependiente con el identificador de tarea "Flowers". Hello "Flores" tarea depende de las tareas "Raicilla" y "Sun". Tarea "Flores" estará toorun programada en un nodo de proceso solo después de las tareas "Raicilla" y "Sun" se han completado correctamente.

> [!NOTE]
> Una tarea se considera toobe completó correctamente cuando se encuentra en hello **completado** estado y su **código de salida** es `0`. En .NET de lotes, esto significa un [CloudTask][net_cloudtask].[ Estado] [ net_taskstate] valor de propiedad de `Completed` y Hola del CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] es el valor de la propiedad `0`.
> 
> 

## <a name="dependency-scenarios"></a>escenarios de dependencia
Hay tres escenarios de dependencia de tareas básicos que puede usar en Lote de Azure: uno a uno, uno a varios y la dependencia de intervalo de identificadores de tarea. Puede tratarse de combinado tooprovide un cuarto escenario, varios a varios.

| Escenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Ejemplo |  |
|:---:| --- | --- |
|  [Uno a uno](#one-to-one) |*taskB* depende de *taskA* <p/> Se programará que *taskB* no se ejecute hasta que *taskA* se haya completado correctamente |![Diagrama: dependencia de la tarea uno a uno][1] |
|  [Uno a varios](#one-to-many) |*taskC* depende de*taskA* y *taskB*. <p/> Se programará que *taskC* no se ejecute hasta que *taskA* y *taskB* se hayan completado correctamente |![Diagrama: dependencia de la tarea uno a varios][2] |
|  [Intervalo de id. de tarea](#task-id-range) |*taskD* depende de una serie de tareas <p/> *taskD* no se programará para su ejecución hasta que las tareas de hello con identificadores *1* a través de *10* se han completado correctamente |![Diagrama: dependencia de intervalo de id. de tarea][3] |

> [!TIP]
> Puede crear **-to-many** relaciones, como donde tareas C, D, E y F cada dependen de las tareas A y B. Esto es útil, por ejemplo, en escenarios de procesamiento paralelo que dependen de las tareas de nivel inferiores en la salida de hello de varias tareas de nivel superior.
> 
> En los ejemplos de hello en esta sección, se ejecuta una tarea dependiente solo después de que las tareas primarias de Hola se completan correctamente. Este comportamiento es el comportamiento predeterminado de Hola para una tarea dependiente. Puede ejecutar una tarea dependiente después de que se produce un error en una tarea primaria especificando un comportamiento predeterminado de dependencia acción toooverride Hola. Vea hello [acciones de dependencia](#dependency-actions) sección para obtener más información.

### <a name="one-to-one"></a>Uno a uno
En una relación uno a uno, una tarea depende de la finalización correcta de Hola de tarea de un elemento primario. toocreate Hola dependencia, proporcione un toohello de Id. de tarea única [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] método estático al rellenar hello [DependsOn] [ net_dependson] propiedad de [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Uno a varios
En una relación uno a varios, una tarea depende de finalización de Hola de varias tareas de elemento primario. toocreate Hola dependencia, proporcionar una serie de tareas identificadores toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] método estático al rellenar hello [DependsOn] [ net_dependson] propiedad de [CloudTask] [ net_cloudtask].

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a>Intervalo de id. de tarea
Una dependencia en un intervalo de las tareas primarias, una tarea depende de la finalización de Hola de Hola de tareas cuyos identificadores se encuentran dentro de un intervalo.
dependencia de hello toocreate, proporcionar hello en primer lugar y última tarea con identificadores de hello intervalo toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] método estático al rellenar hello [DependsOn] [ net_dependson] propiedad de [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Cuando utiliza intervalos de Id. de tarea para sus dependencias, Hola identificadores de tarea en el intervalo de hello *debe* ser representaciones de cadena de valores enteros.
> 
> Cada tarea en el intervalo de hello debe satisfacer dependencia hello, completando correctamente o completando con un error de acción de la dependencia de tooa asignado establecida demasiado**satisfacción**. Vea hello [acciones de dependencia](#dependency-actions) sección para obtener más información.
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a>Acciones de dependencia

De forma predeterminada, una tarea dependiente o un conjunto de tareas se ejecuta solo después de que una tarea principal se haya completado correctamente. En algunos escenarios, puede que desee tareas dependientes toorun incluso si se produce un error en la tarea primaria de Hola. Puede invalidar el comportamiento predeterminado de hello mediante la especificación de una acción de dependencia. Una acción de dependencia especifica si una tarea dependiente es toorun apto, en función de hello éxito o fracaso de la tarea primaria de Hola. 

Por ejemplo, suponga que una tarea dependiente está esperando los datos desde la finalización de Hola de tarea de nivel superior de hello. Si se produce un error en la tarea de nivel superior de hello, tarea dependiente Hola todavía puede ser capaz de toorun con los datos más antiguos. En este caso, una acción de dependencia puede especificar que dicha tarea dependiente de hello es elegible toorun a pesar del error Hola de tarea principal de Hola.

Una acción de dependencia se basa en una condición de salida para la tarea primaria de Hola. Puede especificar una acción de dependencia para cualquiera de hello después de condiciones de salida; para. NET, vea hello [ExitConditions] [ net_exitconditions] clase para obtener más información:

- Cuando se produce un error de procesamiento previo.
- Cuando se produce un error de carga de archivo. Si tarea hello finaliza con un código de salida que se especificó mediante **exitCodes** o **exitCodeRanges**y, a continuación, encuentra un error de carga de archivo, la acción de hello especificado por el código de hello salida tiene prioridad.
- Cuando termina la tarea hello con un código de salida definido por hello **ExitCodes** propiedad.
- Cuando finaliza la tarea hello con un código de salida que se encuentra dentro de un intervalo especificado por hello **ExitCodeRanges** propiedad.
- Hola caso predeterminado, si la tarea hello finaliza con un código de salida no definido en **ExitCodes** o **ExitCodeRanges**, o si la tarea hello finaliza con un error y Hola previa al procesamiento **PreProcessingError**  propiedad no está establecida o si hello se produce un error de tarea con un archivo carga hello y error **FileUploadError** propiedad no está establecida. 

una acción de dependencia en. NET, conjunto hello toospecify [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] propiedad Hola condición de salida. Hola **DependencyAction** propiedad toma uno de dos valores:

- Hola configuración **DependencyAction** propiedad demasiado**satisfacción** indica que las tareas dependientes son elegible toorun si la tarea primaria de Hola se cierra con un error especificado.
- Hola configuración **DependencyAction** propiedad demasiado**bloque** indica que las tareas dependientes no están toorun elegible.

Hola configuración predeterminada de hello **DependencyAction** propiedad es **satisfacción** para código de salida 0, y **bloque** para todas las demás condiciones de salida.

Hello fragmento de código siguiente establece hello **DependencyAction** propiedad para una tarea primaria. Si tarea primaria de Hola se cierra con un error de procesamiento previo o con Hola Hola dependientes códigos de error especificado, la tarea se bloquea. Si la tarea primaria de hello finaliza con cualquier otro error distinto de cero, tarea dependiente hello es toorun elegible.

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a>Código de ejemplo
Hola [TaskDependencies] [ github_taskdependencies] proyecto de ejemplo es uno de hello [ejemplos de código de Azure Batch] [ github_samples] en GitHub. Esta solución de Visual Studio muestra:

- ¿Cómo tooenable tareas depende de un trabajo
- ¿Cómo toocreate las tareas que dependen de otras tareas
- ¿Cómo tooexecute las tareas en un grupo de nodos de proceso.

## <a name="next-steps"></a>Pasos siguientes
### <a name="application-deployment"></a>Implementación de la aplicación
Hola [paquetes de aplicación](batch-application-packages.md) característica de lote proporciona una manera fácil de implementar tooboth y la versión nodos de aplicaciones de Hola que se ejecutan las tareas en ejecución.

### <a name="installing-applications-and-staging-data"></a>Instalación de aplicaciones y datos de ensayo
Vea [nodos de proceso de instalación de aplicaciones y datos en lotes de almacenamiento provisional] [ forum_post] en el foro de Azure Batch Hola para obtener información general de métodos para preparar los nodos toorun tareas. Escrito por uno de los miembros del equipo de Azure Batch de hello, que esta entrada es un buen manual en las aplicaciones de toocopy de maneras diferentes de Hola, datos de entrada de tarea y otro archivos tooyour nodos de ejecución.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagrama: dependencia uno a uno"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagrama: dependencia uno a varios"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagrama: dependencia de intervalo de id. de tarea"
