---
title: aaaHow toouse almacenamiento de tabla de Azure con hello SDK de WebJobs
description: "Obtenga información acerca de cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs. Crear tablas, agregar entidades tootables y leer las tablas existentes."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="02876-104">Cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="02876-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="02876-105">Información general</span><span class="sxs-lookup"><span data-stu-id="02876-105">Overview</span></span>
<span data-ttu-id="02876-106">Esta guía proporcionan ejemplos de código de C# que muestran cómo tablas tooread y escritura de almacenamiento de Azure mediante el uso de [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="02876-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="02876-107">Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o demasiado[varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="02876-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="02876-108">Algunos de los fragmentos de código de hello mostrar hello `Table` atributo utilizado en las funciones que son [llama manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), es decir, no mediante uno de los atributos de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="02876-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="02876-109"><a id="ingress"></a>La tabla de tooadd entidades tooa</span><span class="sxs-lookup"><span data-stu-id="02876-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="02876-110">tabla de tooa tooadd entidades, use hello `Table` atributo con un `ICollector<T>` o `IAsyncCollector<T>` parámetro donde `T` especifica el esquema de Hola de entidades de hello desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="02876-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="02876-111">constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre de Hola de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="02876-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="02876-112">Hello siguiente ejemplo de código agrega `Person` tabla de entidades tooa denominada *entrada*.</span><span class="sxs-lookup"><span data-stu-id="02876-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="02876-113">Hola normalmente el tipo que se utiliza con `ICollector` deriva `TableEntity` o implementa `ITableEntity`, pero no es necesario.</span><span class="sxs-lookup"><span data-stu-id="02876-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="02876-114">Cualquiera de los siguientes hello `Person` clases con código de hello mostrado en hello anterior `Ingress` método.</span><span class="sxs-lookup"><span data-stu-id="02876-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="02876-115">Si desea que toowork directamente con hello API de almacenamiento de Azure, puede agregar un `CloudStorageAccount` firma del método toohello parámetro.</span><span class="sxs-lookup"><span data-stu-id="02876-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="02876-116"><a id="monitor"></a> Supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="02876-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="02876-117">Dado que las funciones de entrada de datos a menudo procesan grandes volúmenes de datos, panel de SDK de WebJobs Hola proporciona datos de supervisión en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="02876-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="02876-118">Hola **invocación registro** sección indica si la función hello se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="02876-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Función de entrada en ejecución](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="02876-120">Hola **detalles de invocación** página informes Hola progreso de la función (número de entidades que escriben) mientras se está ejecutando y proporciona una oportunidad tooabort lo.</span><span class="sxs-lookup"><span data-stu-id="02876-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Función de entrada en ejecución](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="02876-122">Cuando función hello finalice, hello **detalles de invocación** página notifica el número de Hola de filas escritas.</span><span class="sxs-lookup"><span data-stu-id="02876-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Función de entrada finalizada](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="02876-124"><a id="multiple"></a>¿Cómo tooread varias entidades de una tabla</span><span class="sxs-lookup"><span data-stu-id="02876-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="02876-125">tooread una tabla, utilice hello `Table` atributo con un `IQueryable<T>` parámetro donde escribir `T` deriva `TableEntity` o que implemente `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="02876-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="02876-126">lee Hello siguiente ejemplo de código y registros de todas las filas de hello `Ingress` tabla:</span><span class="sxs-lookup"><span data-stu-id="02876-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="02876-127"><a id="readone"></a>¿Cómo tooread una sola entidad de una tabla</span><span class="sxs-lookup"><span data-stu-id="02876-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="02876-128">Hay un `Table` constructor de atributo con dos parámetros adicionales que le permiten especificar la clave de partición de Hola y clave de fila cuando se desea toobind tooa tabla única entidad.</span><span class="sxs-lookup"><span data-stu-id="02876-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="02876-129">ejemplo de código siguiente Hello lee una fila de tabla para una `Person` entidad en función de clave y la fila de claves de partición recibidos en un mensaje de cola:</span><span class="sxs-lookup"><span data-stu-id="02876-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="02876-130">Hola `Person` clase en este ejemplo no tiene tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="02876-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="02876-131"><a id="storageapi"></a>¿Cómo toouse Hola API de almacenamiento de .NET directamente toowork con una tabla</span><span class="sxs-lookup"><span data-stu-id="02876-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="02876-132">También puede usar hello `Table` atribuir a un `CloudTable` objeto para una mayor flexibilidad cuando se trabaja con una tabla.</span><span class="sxs-lookup"><span data-stu-id="02876-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="02876-133">usos de ejemplo de código siguiente Hola un `CloudTable` objeto tooadd una sola entidad toohello *entrada* tabla.</span><span class="sxs-lookup"><span data-stu-id="02876-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="02876-134">Para obtener más información acerca de cómo hello toouse `CloudTable` de objetos, consulte [cómo toouse almacenamiento de tablas de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="02876-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="02876-135"><a id="queues"></a>Temas relacionados cubiertos por las colas de hello cómo-tooarticle</span><span class="sxs-lookup"><span data-stu-id="02876-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="02876-136">Para obtener información acerca de cómo el procesamiento de tabla toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no procesar, consulte específica tootable [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="02876-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="02876-137">Los temas tratados en dicho artículo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="02876-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="02876-138">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="02876-138">Async functions</span></span>
* <span data-ttu-id="02876-139">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="02876-139">Multiple instances</span></span>
* <span data-ttu-id="02876-140">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="02876-140">Graceful shutdown</span></span>
* <span data-ttu-id="02876-141">Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="02876-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="02876-142">Establecer las cadenas de conexión de SDK de hello en el código</span><span class="sxs-lookup"><span data-stu-id="02876-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="02876-143">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="02876-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="02876-144">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="02876-144">Trigger a function manually</span></span>
* <span data-ttu-id="02876-145">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="02876-145">Write logs</span></span>

## <span data-ttu-id="02876-146"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02876-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="02876-147">Esta guía proporciona código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="02876-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="02876-148">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="02876-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

