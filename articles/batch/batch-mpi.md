---
title: tareas de varias instancias de aaaUse aplicaciones de MPI toorun - Azure Batch | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de interfaz de paso de mensajes (MPI) tooexecute mediante la tarea de varias instancias de hello escriban en el lote de Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Usar las aplicaciones de interfaz de paso de mensajes (MPI) de toorun de tareas de varias instancias de lote

Tareas de varias instancias le permiten toorun una tarea de lote de Azure en varios nodos de ejecución al mismo tiempo. Estas tareas permiten escenarios de informática de alto rendimiento como las aplicaciones de interfaz de paso de mensajes (MPI) en Lote. En este artículo, aprenderá cómo Hola mediante las tareas de varias instancias de tooexecute [.NET de lotes] [ api_net] biblioteca.

> [!NOTE]
> Aunque los ejemplos de hello en este artículo se centran en .NET de lotes, MS-MPI, y nodos de proceso de Windows, conceptos de tarea de varias instancias de Hola que se tratan aquí son tooother aplicables plataformas y tecnologías (Python y Intel MPI en nodos de Linux, por ejemplo).
>
>

## <a name="multi-instance-task-overview"></a>Información general de las tareas de instancias múltiples
En el lote, cada tarea suele ejecutar en un nodo de proceso único--que envíe varias tareas tooa trabajo y Hola servicio por lotes programa cada tarea para su ejecución en un nodo. Sin embargo, mediante la configuración de una tarea **configuración de varias instancias**, puede indicar a lote tooinstead crear una tarea principal y varias subtareas que, a continuación, se ejecutan en varios nodos.

![Información general de las tareas de instancias múltiples][1]

Cuando se envía una tarea de trabajo de tooa de configuración de varias instancias, lote realiza varias tareas de instancia única de toomulti de pasos:

1. Hola servicio por lotes crea una **principal** y varios **subtareas** en función de la configuración de varias instancias de Hola. número total de Hola de tareas (principales además de todas las subtareas) coincide con número de Hola de **instancias** (nodos de proceso) especificados en la configuración de varias instancias de Hola.
2. Lote designa uno de hello nodos de proceso como hello **maestro**, y programaciones Hola tooexecute tarea principal en el patrón de Hola. Programa hello subtareas tooexecute en el resto de Hola de tarea de hello proceso nodos toohello asignado varias instancias, una subtarea por nodo.
3. Hola principal y todas las subtareas descargar cualquiera **archivos de recursos comunes** especificados en la configuración de varias instancias de Hola.
4. Después de que se han descargado los archivos de recursos comunes de hello, hello principal y subtareas ejecutan hello **comando coordinación** especificados en la configuración de varias instancias de Hola. comando de coordinación de Hello es nodos tooprepare normalmente se usan para ejecutar la tarea hello. Esto puede incluir a partir de servicios de fondo (como [Microsoft MPI][msmpi_msdn]del `smpd.exe`) y comprobar que los nodos de hello son mensajes de tooprocess listo entre nodos.
5. tarea principal de Hello ejecuta hello **comando de la aplicación** en el nodo principal de hello *después* comando de coordinación de Hola se ha completado correctamente por hello principal y todas las subtareas. comando de la aplicación Hello es Hola de línea de comandos de la propia tarea de varias instancias hello y se ejecuta solo por la tarea principal de hello. En una solución basada en [MS-MPI][msmpi_msdn], se trata del lugar donde ejecuta la aplicación habilitada para MPI mediante `mpiexec.exe`.

> [!NOTE]
> Aunque es funcionalmente distinto, Hola "tarea de varias instancias" no es un tipo de tarea único como hello [StartTask] [ net_starttask] o [JobPreparationTask] [ net_jobprep]. tarea de varias instancias de Hello es simplemente una tarea de lote estándar ([CloudTask] [ net_task] en .NET de lote) se configuró cuya configuración de varias instancias. En este artículo, nos referiremos toothis como hello **tareas varias instancias**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Requisitos de las tareas de instancias múltiples
Las tareas de múltiples instancias requieren un grupo con la **comunicación ente nodos habilitada** y la **ejecución simultánea de tareas deshabilitada**. ejecución de tareas simultáneas toodisable, conjunto hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 de propiedad.

Este fragmento de código muestra cómo toocreate un grupo de instancias múltiples tareas utilizando la biblioteca de .NET de lotes de Hola.

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> Si intentas toorun deshabilitada una tarea de varias instancias en un grupo con la comunicación entre nodos, o con un *maxTasksPerNode* valor mayor que 1, nunca se programa la tarea hello--indefinidamente permanece en estado de "activo" Hola. 
>
> Se podrán ejecutar tareas de varias instancias solo en nodos de los grupos creados después del 14 de diciembre de 2015.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>Usar un tooinstall StartTask MPI
aplicaciones de MPI toorun con una tarea de varias instancias, primero debe tooinstall una implementación de MPI en nodos de proceso de hello en el grupo de hello (MS-MPI o MPI de Intel, por ejemplo). Se trata de un buen momento toouse una [StartTask][net_starttask], que se ejecuta cada vez que un nodo une a un grupo o se ha reiniciado. Este fragmento de código crea un StartTask que especifica el paquete de instalación de hello MS-MPI como un [archivo de recursos][net_resourcefile]. línea de comandos de la tarea de inicio de Hola se ejecuta después de archivo de recursos de hello es nodo toohello descargado. En este caso, la línea de comandos de hello realiza una instalación desatendida de MS-MPI.

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a>Acceso directo a memoria remota (RDMA)
Cuando se elige un [tamaño compatibles con RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como A9 para hello nodos de cálculo en el grupo de lote, la aplicación de MPI puede aprovechar las ventajas de alto rendimiento, latencia baja memoria directa remota (RDMA) de acceso de red de Azure.

Busque los tamaños de hello especificados como "Capacidad RDMA" Hola siguientes artículos:

* Grupos de **CloudServiceConfiguration**

  * [Tamaños de Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (solo Windows)
* Grupos de **VirtualMachineConfiguration**

  * [Tamaños de las máquinas virtuales en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Tamaños de las máquinas virtuales en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> tootake aprovechar RDMA en [nodos de proceso de Linux](batch-linux-nodes.md), debe usar **MPI Intel** en nodos de Hola. Para obtener más información acerca de los grupos CloudServiceConfiguration y VirtualMachineConfiguration, vea Hola sección Pool de hello [Introducción a la característica por lotes](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Creación de una tarea de instancias múltiples con .NET de Lote
Ahora que hemos analizado los requisitos de grupo de hello e instalación de paquete MPI, vamos a crear la tarea de varias instancias de hello. En este fragmento de código, creamos una instancia de [CloudTask][net_task] estándar y luego configuramos su propiedad [MultiInstanceSettings][net_multiinstance_prop]. Como se mencionó anteriormente, tarea de varias instancias de hello no es un tipo de tarea distintos, pero una tarea por lotes estándar configurado con la configuración de varias instancias.

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a>Tarea principal y subtareas
Cuando creas Hola configuración de varias instancias de una tarea, especifique número Hola de nodos de proceso que son tareas de hello tooexecute. Cuando se envía el trabajo de la tarea tooa hello, Hola servicio por lotes crea una **principal** tareas y suficientes **subtareas** que coincidan conjuntamente con número de Hola de nodos especificado.

Estas tareas se asignan un identificador entero del intervalo de hello 0 demasiado*numberOfInstances* - 1. tarea de Hello con Id. 0 es tarea principal de hello y todos los otros identificadores son subtareas. Por ejemplo, si creas Hola después de la configuración de varias instancias de una tarea, tarea principal de hello tendría un identificador de 0 y Hola subtareas tendría identificadores del 1 al 9.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Nodo maestro
Cuando se envía una tarea de varias instancias, Hola servicio por lotes designa uno de hello nodos de proceso como nodo de "maestro" hello y programaciones Hola tooexecute tarea principal en el nodo principal de Hola. Hola subtareas son tooexecute programada del resto de nodos de hello asignado la tarea de varias instancias de toohello Hola.

## <a name="coordination-command"></a>comando de coordinación
Hola **comando coordinación** se ejecuta Hola principal y las subtareas.

está bloqueando la invocación de Hola de comando de coordinación de hello--por lotes no ejecutan el comando de la aplicación hello hasta que el comando de coordinación de hello ha devuelto correctamente para todas las subtareas. comando de coordinación de Hello, por tanto, debe iniciar los servicios de fondo requerido, compruebe que están listas para su uso y, a continuación, salir. Por ejemplo, este comando de coordinación en una solución mediante MS-MPI versión 7 inicia el servicio SMPD de hello en el nodo de hello, entonces se cierra:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Tenga en cuenta uso Hola de `start` en este comando de coordinación. Esto es necesario porque hello `smpd.exe` aplicación no se devuelve inmediatamente después de la ejecución. Sin usar Hola Hola [iniciar] [ cmd_start] de comandos, este comando de coordinación no devolvería y, por tanto, bloquearían Hola aplicación ejecución del comando.

## <a name="application-command"></a>Comando de aplicación
Una vez que la tarea principal de hello y todas las subtareas han terminado de ejecutar el comando de coordinación de hello, línea de comandos de la tarea de varias instancias de Hola se ejecuta por la tarea principal de hello *sólo*. Llamamos a este hello **comando aplicación** toodistinguish de comando de coordinación de Hola.

Para las aplicaciones de MS-MPI, use Hola aplicación comando tooexecute una aplicación habilitada para MPI con `mpiexec.exe`. Por ejemplo, este es un comando de aplicación para una solución mediante la versión 7 de MS-MPI:

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Dado que MS-MPI `mpiexec.exe` usa Hola `CCP_NODES` variable de forma predeterminada (vea [variables de entorno](#environment-variables)) hello (ejemplo) se excluye la línea de comandos de la aplicación anterior.
>
>

## <a name="environment-variables"></a>Variables de entorno
Proceso por lotes crea varios [variables de entorno] [ msdn_env_var] tareas toomulti-instancia específica en hello nodos asignan la tarea de varias instancias de tooa de proceso. Las líneas de comando de coordinación y la aplicación puede hacer referencia a estas variables de entorno, como puede Hola scripts y programas que se ejecutan.

Hello siguientes variables de entorno se crean Hola servicio por lotes para su uso por las tareas de varias instancias:

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Para obtener detalles completos sobre estos y Hola otras variables de entorno de proceso por lotes proceso nodo, incluido su contenido y la visibilidad, vea [variables de entorno de nodo de proceso][msdn_env_var].

> [!TIP]
> ejemplo de código de Hello MPI de Linux de lote contiene un ejemplo de cómo se pueden utilizar algunas de estas variables de entorno. Hola [coordinación cmd] [ coord_cmd_example] Bash script descarga la aplicación comunes y los archivos de entrada desde el almacenamiento de Azure, permite a un recurso compartido de Network File System (NFS) en el nodo principal de Hola y configura Hola otros nodos asignar tareas de varias instancias de toohello como clientes NFS.
>
>

## <a name="resource-files"></a>Archivos de recursos
Hay dos conjuntos de tooconsider de archivos de recursos para tareas de varias instancias: **archivos de recursos comunes** que *todos los* descargar tareas (ambos principal y subtareas), hello y **dearchivosderecursos** especificado para hello varias instancias de tareas, que *sólo Hola principal* descargas de tareas.

Puede especificar uno o varios **archivos de recursos comunes** en la configuración de varias instancias de Hola para una tarea. Estos archivos de recursos comunes se descargan desde [el almacenamiento de Azure](../storage/common/storage-introduction.md) en cada nodo **directorio compartido de tarea** Hola principal y todas las subtareas. Puede tener acceso a directorio compartido de hello tareas de líneas de comandos de la aplicación y la coordinación mediante hello `AZ_BATCH_TASK_SHARED_DIR` variable de entorno. Hola `AZ_BATCH_TASK_SHARED_DIR` ruta de acceso es idéntico en cada tarea de varias instancias de nodo toohello asignado, lo que puede compartir un comando único coordinación entre Hola principal y todas las subtareas. Lote no "compartir" directorio de hello en un sentido de acceso remoto, pero puede usar como un montaje o compartir punto tal y como se mencionó anteriormente en la sugerencia de hello en variables de entorno.

Archivos de recursos que especifique para la propia tarea de varias instancias hello son directorio de trabajo de la tarea de toohello descargado, `AZ_BATCH_TASK_WORKING_DIR`, de forma predeterminada. Tal y como se ha mencionado, en cambio toocommon archivos de recursos, solo tarea principal de hello descarga archivos de recursos especificados para la propia tarea de varias instancias Hola.

> [!IMPORTANT]
> Utilice siempre las variables de entorno de hello `AZ_BATCH_TASK_SHARED_DIR` y `AZ_BATCH_TASK_WORKING_DIR` directorios de toothese toorefer en las líneas de comando. No intente manualmente las rutas de acceso de tooconstruct Hola.
>
>

## <a name="task-lifetime"></a>Duración de la tarea
duración de Hola de duración de hello tarea principal controles Hola de tarea de hello todo varias instancias. Cuando se cierra Hola principal, se terminan todas Hola subtareas. código de salida de Hello de hello principal es el código de salida de hello de tarea hello y es, por tanto, toodetermine usado Hola éxito o error de tarea de Hola para fines de reintento.

Si se produce un error en cualquiera de las subtareas hello, salir con un código de retorno distinto de cero, por ejemplo, hello todo varias instancias tarea genera un error. tarea de varias instancias de Hello, a continuación, se terminan y se vuelve a intentar la tooits límite de reintentos.

Cuando se elimina una tarea de varias instancias, también se eliminan por servicio por lotes de Hola Hola principal y todas las subtareas. Todos los directorios de subtarea y sus archivos se eliminan de los nodos de proceso de hello, como ocurre con una tarea estándar.

[TaskConstraints] [ net_taskconstraints] para una tarea de varias instancias, como hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], y [RetentionTime] [ net_taskconstraint_retention] se respetan las propiedades, como son para una tarea estándar y aplicar toohello principal y todas las subtareas. Sin embargo, si cambia hello [RetentionTime] [ net_taskconstraint_retention] propiedad después de agregar el trabajo de toohello tarea hello varias instancias, este cambio es tarea principal toohello solo aplicada. Todas las subtareas de hello contribuyen toouse Hola original [RetentionTime][net_taskconstraint_retention].

Lista de tareas recientes de un nodo de proceso refleja identificador hello de una subtarea si tareas recientes Hola formaba parte de una tarea de varias instancias.

## <a name="obtain-information-about-subtasks"></a>Obtención de información sobre las subtareas
información de tooobtain en subtareas mediante .NET de lote Hola biblioteca, llamada hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] método. Este método devuelve información sobre todas las subtareas y obtener información acerca de hello proceso nodo que ejecuta tareas de Hola. De esta información, puede determinar el directorio de raíz de cada subtarea, Id. de grupo de hello, su estado actual, código de salida y mucho más. Esta información se puede utilizar en combinación con hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] archivos de subtarea de método tooobtain Hola. Tenga en cuenta que este método no devuelve información de la tarea principal de hello (Id. 0).

> [!NOTE]
> A menos que se indique lo contrario, los métodos de .NET de lotes que operan en Hola varias instancias [CloudTask] [ net_task] propio aplicar *sólo* toohello de tarea principal. Por ejemplo, cuando se llama a hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] método en una tarea de varias instancias, se devuelven únicamente los archivos de la tarea principal de Hola.
>
>

Hello fragmento de código siguiente muestra cómo tooobtain subtarea información, así como contenido del archivo de solicitud de nodos de hello en el que ejecuta.

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a>Código de ejemplo
Hola [MultiInstanceTasks] [ github_mpi] ejemplo de código en GitHub muestra cómo toouse una instancia de varias tareas toorun una [MS-MPI] [ msmpi_msdn] aplicación de nodos de proceso por lotes. Siga los pasos de hello en [preparación](#preparation) y [ejecución](#execution) ejemplo de Hola a toorun.

### <a name="preparation"></a>Preparación
1. Siga los dos primeros pasos de hello en [cómo toocompile y ejecutar un programa sencillo de MS-MPI][msmpi_howto]. Esto cumple hello prerequesites para hello siguiendo el paso.
2. Crear un *versión* versión de hello [MPIHelloWorld] [ helloworld_proj] programa de MPI de ejemplo. Se trata de un programa hello que se ejecutará en los nodos de proceso mediante la tarea de varias instancias de hello.
3. Cree un archivo zip que contenga `MPIHelloWorld.exe` (creado en el paso 2) y `MSMpiSetup.exe` (descargado en el paso 1). Cargue este archivo zip como un paquete de aplicación en el paso siguiente de saludo.
4. Hola de uso [portal de Azure] [ portal] toocreate un lote [aplicación](batch-application-packages.md) denominado "MPIHelloWorld" y especifique el archivo zip de hello creado en el paso anterior de hello como versión "1.0" de paquete de aplicación Hola. Para más información, consulte [Carga y administración de aplicaciones](batch-application-packages.md#upload-and-manage-applications).

> [!TIP]
> Crear un *versión* versión de `MPIHelloWorld.exe` para que no tengan tooinclude las dependencias adicionales (por ejemplo, `msvcp140d.dll` o `vcruntime140d.dll`) en el paquete de aplicación.
>
>

### <a name="execution"></a>Ejecución
1. Descargar hello [ejemplos de lote de azure] [ github_samples_zip] desde GitHub.
2. Abra hello MultiInstanceTasks **solución** en Visual Studio 2015 o versiones más recientes. Hola `MultiInstanceTasks.sln` archivo de solución se encuentra en:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Escriba sus credenciales de cuenta de lote y el almacenamiento en `AccountSettings.settings` en hello **Microsoft.Azure.Batch.Samples.Common** proyecto.
4. **Compilar y ejecutar** el aplicación de ejemplo de Hola MultiInstanceTasks solución tooexecute Hola MPI en nodos de cálculo en un grupo de lote.
5. *Opcional*: Hola de uso [portal de Azure] [ portal] o hello [Explorer lote] [ batch_explorer] tooexamine grupo de ejemplo de Hola, trabajo, y tarea ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") antes de eliminar los recursos de Hola.

> [!TIP]
> Si no tiene Visual Studio, puede descargar gratis [Visual Studio Community][visual_studio].
>
>

Resultado de `MultiInstanceTasks.exe` es similar siguiente toohello:

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Pasos siguientes
* blog del equipo de lote de Azure y Microsoft HPC Hola describe [MPI compatibilidad con Linux en Azure Batch][blog_mpi_linux]e incluye información sobre el uso de [OpenFOAM] [ openfoam] con el lote. Puede encontrar ejemplos de código de Python para hello [ejemplo OpenFOAM en GitHub][github_mpi].
* Obtenga información acerca de cómo demasiado[crear grupos de nodos de proceso de Linux](batch-linux-nodes.md) para su uso en sus soluciones de MPI de lote de Azure.

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Información general de instancias múltiples"
