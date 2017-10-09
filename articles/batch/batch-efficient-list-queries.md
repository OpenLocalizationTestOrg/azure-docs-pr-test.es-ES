---
title: las consultas de la lista eficaz de aaaDesign - Azure Batch | Documentos de Microsoft
description: "Mejore el rendimiento filtrando las consultas cuando solicite información en recursos de Batch, como grupos, trabajos, tareas y nodos de proceso."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Crear consultas de recursos de proceso por lotes toolist eficazmente

Aquí aprenderá cómo tooincrease rendimiento de su aplicación de Azure Batch reduciendo la cantidad de Hola de datos devuelto por el servicio de hello al consultar los trabajos, tareas y los nodos de proceso con hello [.NET de lotes] [ api_net] biblioteca.

Casi todas las aplicaciones de lote necesitan tooperform algún tipo de supervisión u otra operación que consulta al servicio de lote de hello, a menudo a intervalos regulares. Por ejemplo, toodetermine si hay cualquier tarea en cola restante en un trabajo, debe obtener datos en todas las tareas en el trabajo de Hola. estado de hello toodetermine de nodos en el grupo, debe obtener datos en cada nodo de grupo de Hola. Este artículo explica cómo tooexecute por ejemplo, las consultas en hello forma más eficaz.

> [!NOTE]
> Hola servicio por lotes proporciona compatibilidad de API especial para el escenario común de Hola de recuento de tareas en un trabajo. En lugar de usar una consulta de lista para ello, puede llamar a hello [obtener recuentos de tarea] [ rest_get_task_counts] operación. Get Task Counts indica cuántas tareas están pendientes, en ejecución o completadas, y cuántas finalizaron correctamente o con errores. Esta operación es más eficaz que una consulta de lista. Para más información, consulte [Recuento de tareas de un trabajo por estado (versión preliminar)](batch-get-task-counts.md). 
>
> Hola operación obtener recuentos de tarea no está disponible en las versiones de servicio de lote anteriores a 2017-06-01.5.1. Si está utilizando una versión anterior del servicio de hello, a continuación, utilice una lista de tareas de toocount de consulta en un trabajo en su lugar.
>
> 

## <a name="meet-hello-detaillevel"></a>Cumplir hello DetailLevel
En una aplicación de lote de producción, las entidades como trabajos, tareas y nodos de proceso pueden numerar Hola miles. Cuando se solicita información acerca de estos recursos, una cantidad potencialmente grande de datos debe "se transfieren entre conexión Hola" aplicación de tooyour de servicio de lote de hello en cada consulta. Al limitar el número de Hola de elementos y el tipo de información devuelta por una consulta, puede aumentar la velocidad de Hola de las consultas y Hola, por tanto, el rendimiento de la aplicación.

Esto [.NET de lotes] [ api_net] listas de fragmento de código de API *cada* tarea que está asociado con un trabajo, junto con *todos los* de propiedades de Hola de cada uno tarea:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

Puede realizar una consulta de lista mucho más eficaz, sin embargo, mediante la aplicación de una consulta de tooyour "nivel de detalle". Para ello, proporcionando un [ODATADetailLevel] [ odata] objeto toohello [JobOperations.ListTasks] [ net_list_tasks] método. Este fragmento de código devuelve sólo identificador hello, línea de comandos y propiedades de información de nodo de proceso de las tareas completadas:

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

En este escenario de ejemplo, si hay miles de tareas trabajo hello, resultados de Hola de segunda consulta de hello normalmente será mucho más rápido que Hola devuelve en primer lugar. Para obtener más información sobre el uso de ODATADetailLevel cuando se enumeran los elementos con hello API de .NET de lote se incluye [a continuación](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> Es muy recomendable que se *siempre* proporcione una lista de API de .NET ODATADetailLevel tooyour de objeto llama tooensure la máxima eficiencia y el rendimiento de la aplicación. Al especificar un nivel de detalle, puede ayudar a toolower procesar por lotes los tiempos de respuesta de servicio, mejorar la utilización de la red y minimizar el uso de memoria por las aplicaciones cliente.
> 
> 

## <a name="filter-select-and-expand"></a>Filtrado, selección y expansión
Hola [.NET de lotes] [ api_net] y [REST de lote] [ api_rest] API proporcionan Hola capacidad tooreduce ambos en número de elementos que se devuelven en una lista, Hola así como Hola cantidad de información que se devuelve para cada uno. Para ello, debe especificar **filter**, **select** y **expand strings** cuando realice consultas de lista.

### <a name="filter"></a>Filtrar
cadena de filtro de Hello es una expresión que reduce el número de Hola de elementos que se devuelven. Por ejemplo, lista solo hello las tareas para un trabajo o solo nodos de proceso de lista que están listos toorun tareas en ejecución.

* cadena de filtro de Hello consta de una o varias expresiones, con una expresión que consta de un nombre de propiedad, un operador y un valor. propiedades de Hola que pueden especificarse son tipo de entidad tooeach específico que realiza una consulta, como operadores de Hola que se admiten para cada propiedad.
* Se pueden combinar varias expresiones mediante operadores lógicos de hello `and` y `or`.
* En este ejemplo filtrar listas de cadena solo Hola ejecutando "representación" tareas: `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Seleccionar
cadena seleccione Hola limita los valores de propiedad de Hola que se devuelven para cada elemento. Especifica una lista de nombres de propiedad, y se devuelven únicamente los valores de propiedad para los elementos de hello en los resultados de la consulta de Hola.

* cadena de select Hola consta de una lista separada por comas de nombres de propiedad. Puede especificar cualquiera de las propiedades de Hola Hola tipo de entidad que está consultando.
* Esta cadena select de ejemplo especifica que solo se deben devolver tres valores de propiedades para cada tarea: `id, state, stateTransitionTime`.

### <a name="expand"></a>Expanda
Hola expanda cadena reduce el número de Hola de llamadas API que son necesario tooobtain cierta información. Cuando se utiliza una cadena expand, se puede obtener más información sobre cada elemento con una sola llamada API. En lugar de la primera lista de hello obtención de entidades y, a continuación, solicitar información para cada elemento de lista de hello, utilice una cadena de expansión tooobtain Hola la misma información en una sola llamada API. Menos llamadas API supone un rendimiento mayor.

* Cadena de select toohello similar, Hola expandir controles de cadena si determinados datos se incluyen en los resultados de la consulta de lista.
* Hola expanda cadena solo se admite cuando se usa en la lista de trabajos, programaciones de trabajos, tareas y grupos. En la actualidad, solo admite información estadística.
* Cuando todas las propiedades son necesarias y no se especifica ninguna cadena de select, Hola expanda cadena *debe* tooget usa información de estadísticas. Si una cadena de selección es tooobtain usa un subconjunto de propiedades, a continuación, `stats` puede especificarse en la cadena de selección de Hola y Hola expanda cadena no es necesario toobe especificado.
* En este ejemplo expanda cadena especifica que se debe devolver información de estadísticas para cada elemento de lista de hello: `stats`.

> [!NOTE]
> Al construir cualquiera de hello tres tipos de cadena de consulta (filtrar, seleccione y expanda), debe asegurarse de que los nombres de propiedad de Hola y caso de coincidan con sus homólogos de elemento de la API de REST. Por ejemplo, cuando se trabaja con Hola .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) (clase), debe especificar **estado** en lugar de **estado**, incluso aunque Hola propiedad .NET [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Ver tablas de Hola por debajo de las asignaciones de propiedad entre Hola .NET y las API de REST.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Reglas de las cadenas filter, select y expand
* Nombres de propiedades de filtro, seleccione y expanda las cadenas deben aparecer como lo hacen en hello [REST de lote] [ api_rest] API, aunque se usen [.NET de lotes] [ api_net] o uno de Hola otros SDK de lote.
* Todos los nombres de propiedades distinguen mayúsculas y minúsculas, pero los valores de propiedad no lo hacen.
* Las cadenas de fecha y hora pueden tener uno de los dos formatos y deben ir precedidas por `DateTime`.
  
  * Ejemplo de formato W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * Ejemplo de formato RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Las cadenas booleanas son `true` o `false`.
* Si se especifica una propiedad o un operador no válidos, aparecerá el error `400 (Bad Request)` .

## <a name="efficient-querying-in-batch-net"></a>Consultas eficaces en .NET de Batch
Dentro de hello [.NET de lotes] [ api_net] API, hello [ODATADetailLevel] [ odata] clase se usa para suministrar el filtro, seleccione y expanda cadenas operaciones de toolist. Hola ODataDetailLevel clase tiene tres propiedades de cadena pública que pueden especificados en el constructor de hello, o establecer directamente en el objeto de Hola. , A continuación, pasa hello ODataDetailLevel objeto como un parámetro toohello varias operaciones de lista como [ListPools][net_list_pools], [ListJobs][net_list_jobs], y [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: limitar el número de Hola de elementos que se devuelven.
* [ODATADetailLevel.SelectClause][odata].[SelectClause][odata_select]: especifica los valores de propiedad devueltos con cada elemento.
* [ODATADetailLevel][odata].[ExpandClause][odata_expand]: recupera datos para todos los elementos en una sola llamada API en lugar de en llamadas independientes para cada elemento.

Hello fragmento de código siguiente usa Hola API de .NET de lote tooefficiently consulta Hola lote servicio para las estadísticas de Hola de un conjunto específico de grupos. En este escenario, el usuario de lote de hello tiene grupos de prueba y producción. grupo de prueba de Hello identificadores van precedidas por "test" y grupo de producción de hello identificadores tienen el prefijo "prod". En el fragmento de código de hello, *myBatchClient* es una instancia inicializada correctamente de hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) clase.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> Una instancia de [ODATADetailLevel] [ odata] que está configurado con Select y Expand cláusulas pueden también se pueden pasar como métodos de Get tooappropriate, [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , cantidad de hello toolimit de datos que se devuelven.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Asignaciones de API de REST too.NET de lote
Los nombres de propiedades en las cadenas filter, select y expand *deben* reflejar sus homólogos en la API de REST, tanto en el nombre en sí como en el uso de mayúsculas y minúsculas. tablas de Hello siguientes proporcionan las asignaciones entre Hola .NET y homólogos de la API de REST.

### <a name="mappings-for-filter-strings"></a>Asignaciones de las cadenas filter
* **Métodos de la lista de .NET**: cada uno de los métodos de la API de .NET de hello en esta columna acepta un [ODATADetailLevel] [ odata] objeto como parámetro.
* **Lista de solicitudes de REST**: API de REST de cada página vinculado tooin esta columna contiene una tabla que especifica las propiedades de Hola y las operaciones que se permite en *filtro* cadenas. Estos nombres de propiedad y estas operaciones se usarán al construir una cadena [ODATADetailLevel.FilterClause][odata_filter].

| Métodos de lista de .NET | Solicitudes de lista de REST |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Lista de certificados de hello en una cuenta][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Enumerar archivos de hello asociados a una tarea][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Mostrar hello estado de preparación del trabajo hello y tareas de la versión de trabajo para un trabajo][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Lista de trabajos de hello en una cuenta][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Enumerar archivos de hello en un nodo][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Lista de tareas de hello asociado a un trabajo][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Lista de programaciones de trabajos de hello en una cuenta][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Enumerar trabajos de hello asociados con una programación de trabajo][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Hola lista nodos en un grupo de proceso][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Lista de grupos de Hola de una cuenta][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Asignaciones de las cadenas select
* **Tipos de .NET de Batch**: tipos de la API de .NET para Batch.
* **Entidades de la API de REST**: cada página de esta columna contiene una o más tablas que enumeran los nombres de propiedad de API de REST de hello para el tipo de saludo. Estos nombres de propiedades se usan al construir cadenas *select* . Estos mismos nombres se usarán al construir una cadena [ODATADetailLevel.SelectClause][odata_select].

| Tipos de .NET de Batch | Entidades de la API de REST |
| --- | --- |
| [Certificate][net_cert] |[Obtención de información sobre un certificado][rest_get_cert] |
| [CloudJob][net_job] |[Obtención de información sobre un trabajo][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Obtención de información sobre una programación de trabajo][rest_get_schedule] |
| [ComputeNode][net_node] |[Obtención de información sobre un nodo][rest_get_node] |
| [CloudPool][net_pool] |[Obtención de información sobre un grupo][rest_get_pool] |
| [CloudTask][net_task] |[Obtención de información sobre una tarea][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Ejemplo: construcción de una cadena filter
Cuando se construye una cadena de filtro para [ODATADetailLevel.FilterClause][odata_filter], consulte la tabla Hola anteriormente en "Asignaciones de las cadenas de filtro" toofind Hola API de REST página de documentación que corresponde operación de lista de toohello que desea tooperform. Encontrará las propiedades filtrables hello y sus operadores admitidos en la primera tabla de varias filas hello en la página. Si desea tooretrieve todas las tareas cuyo código de salida es distinto de cero, por ejemplo, esta fila en [la lista de tareas de hello asociadas a un trabajo] [ rest_list_tasks] especifica la cadena de propiedad aplicable de Hola y operadores permitidos:

| Propiedad | Operaciones permitidas | Tipo |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Por lo tanto, sería la cadena de filtro de Hola para enumerar todas las tareas con un código de salida distinto de cero:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Ejemplo: construcción de una cadena select
tooconstruct [ODATADetailLevel.SelectClause][odata_select], consulte la tabla Hola anteriormente en "Asignaciones para las cadenas seleccionadas" y navegar por página de API de REST de toohello correspondiente toohello tipo de entidad que enumerar. Encontrará propiedades seleccionable de Hola y sus operadores admitidos en la primera tabla de varias filas hello en la página. Si desea tooretrieve solo Hola Id. y línea de comandos para cada tarea en una lista, por ejemplo, encontrará estas filas de tabla procede de hello en [obtener información acerca de una tarea][rest_get_task]:

| Propiedad | Tipo | Notas |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

cadena de select de Hola para incluir sólo identificador hello y línea de comandos con cada tarea de la lista, a continuación, podría ser:

`id, commandLine`

## <a name="code-samples"></a>Ejemplos de código
### <a name="efficient-list-queries-code-sample"></a>Código de ejemplo de consultas de lista eficaces
Extraer del repositorio hello [EfficientListQueries] [ efficient_query_sample] proyecto de ejemplo en GitHub toosee lo eficaces consultas de lista pueden afectar al rendimiento en una aplicación. Esta aplicación de consola de C# crea y agrega una gran cantidad de trabajo de tooa de tareas. A continuación, realiza varias de las llamadas toohello [JobOperations.ListTasks] [ net_list_tasks] método y pasa [ODATADetailLevel] [ odata] objetos configurar con otro nombre de propiedad valores toovary Hola mucha toobe datos devuelto. Produce el siguiente toohello similar de salida:

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Como se muestra en el el tiempo transcurrido hello, puede reducir en gran medida tiempos de respuesta de consulta mediante la limitación de propiedades de Hola y número de Hola de elementos que se devuelven. Puede encontrar este y otros proyectos de ejemplo Hola [ejemplos de lote de azure] [ github_samples] repositorio en GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>Biblioteca y código de ejemplo de BatchMetrics
Además toohello EfficientListQueries ejemplo de código anterior, puede encontrar Hola [BatchMetrics] [ batch_metrics] proyecto Hola [ejemplos de lote de azure] [ github_samples] Repositorio de GitHub. proyecto de ejemplo de Hola BatchMetrics muestra cómo supervisar el progreso del trabajo por lotes de Azure mediante la API de lote de hello tooefficiently.

Hola [BatchMetrics] [ batch_metrics] ejemplo incluye un proyecto de biblioteca de clases de .NET que puede incorporar en sus propios proyectos y una línea de comandos sencilla programa tooexercise y mostrar el uso de Hola de Hola biblioteca.

aplicación de ejemplo de Hola en proyecto de hello muestra hello las siguientes operaciones:

1. Seleccionar atributos específicos en orden toodownload solo hello las propiedades que necesite
2. Solo filtrado en los tiempos de transición de estado en toodownload de orden de los cambios desde la última consulta de Hola

Por ejemplo, hello siguiendo el método aparece en hello BatchMetrics biblioteca. Devuelve un ODATADetailLevel que especifica que solo hello `id` y `state` propiedades deben obtenerse para entidades de Hola que se consultan. También especifica que solo las entidades cuyo estado ha cambiado desde Hola especificado `DateTime` parámetro se debe devolver.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Pasos siguientes
### <a name="parallel-node-tasks"></a>Tareas paralelas de nodo
[Maximizar el uso de recursos de proceso por lotes de Azure con las tareas de nodo simultáneos](batch-parallel-node-tasks.md) es otro artículo relacionado con el rendimiento de la aplicación tooBatch. Algunos tipos de cargas de trabajo pueden beneficiarse de la ejecución de tareas paralelas en una menor cantidad de nodos de proceso que, sin embargo, sean de mayor tamaño. Extraer del repositorio hello [escenario de ejemplo](batch-parallel-node-tasks.md#example-scenario) en el artículo de Hola para obtener detalles sobre este escenario.

### <a name="batch-forum"></a>Foro de Batch
Hola [foro de lote de Azure] [ forum] en MSDN es una gran colocar toodiscuss por lotes y formular preguntas acerca del servicio de Hola. Lea los mensajes útiles publicados y envíe sus preguntas a medida que surjan mientras compila sus soluciones del servicio Batch.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

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

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job