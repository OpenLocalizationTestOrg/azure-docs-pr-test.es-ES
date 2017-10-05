---
title: "Cómo usar el almacenamiento de tablas de Azure con el SDK de WebJobs"
description: "Obtenga información sobre cómo usar el almacenamiento de tablas de Azure con el SDK de WebJobs. Cree tablas, agregue entidades a las tablas y lea tablas existentes."
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
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="4712f-104">Cómo usar el almacenamiento de tablas de Azure con el SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="4712f-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="4712f-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4712f-105">Overview</span></span>
<span data-ttu-id="4712f-106">Esta guía proporciona ejemplos de código C# que muestran cómo leer y escribir tablas de almacenamiento de Azure mediante el [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="4712f-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="4712f-107">En la guía se supone que sabe [cómo crear un proyecto de WebJob en Visual Studio con cadenas de conexión que señalan a su cuenta de almacenamiento](websites-dotnet-webjobs-sdk-get-started.md) o a [varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="4712f-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="4712f-108">Algunos de los fragmentos de código muestran el atributo `Table` usado en funciones que se [llaman manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), es decir, sin usar ninguno de los atributos de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="4712f-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="4712f-109"><a id="ingress"></a> Cómo agregar entidades a una tabla</span><span class="sxs-lookup"><span data-stu-id="4712f-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="4712f-110">Para agregar entidades a una tabla, utilice el atributo `Table` con un parámetro `ICollector<T>` o `IAsyncCollector<T>` donde `T` especifica el esquema de las entidades que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="4712f-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="4712f-111">El constructor de atributo toma un parámetro de cadena que especifica el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="4712f-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="4712f-112">El ejemplo de código siguiente agrega entidades `Person` a una tabla denominada *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="4712f-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="4712f-113">Normalmente, el tipo que usa con `ICollector` deriva de `TableEntity` o implementa `ITableEntity`, pero no es necesario que lo haga.</span><span class="sxs-lookup"><span data-stu-id="4712f-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="4712f-114">Cualquiera de las siguientes clases `Person` funciona con el código que aparece en el método `Ingress` anterior.</span><span class="sxs-lookup"><span data-stu-id="4712f-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

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

<span data-ttu-id="4712f-115">Si desea trabajar directamente con la API de almacenamiento de Azure, puede agregar un parámetro `CloudStorageAccount` a la firma del método.</span><span class="sxs-lookup"><span data-stu-id="4712f-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="4712f-116"><a id="monitor"></a> Supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="4712f-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="4712f-117">Dado que las funciones de entrada de datos a menudo procesan grandes volúmenes de datos, el panel del SDK de WebJobs proporciona datos de supervisión en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4712f-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="4712f-118">La sección **Registro de invocación** indica si la función sigue en ejecución.</span><span class="sxs-lookup"><span data-stu-id="4712f-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Función de entrada en ejecución](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="4712f-120">La página **Detalles de invocación** informa el progreso de la función (la cantidad de entidades escritas) mientras se ejecuta y ofrece la oportunidad de anularla.</span><span class="sxs-lookup"><span data-stu-id="4712f-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Función de entrada en ejecución](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="4712f-122">Cuando finaliza la función, la página **Detalles de invocación** informa la cantidad de filas escritas.</span><span class="sxs-lookup"><span data-stu-id="4712f-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Función de entrada finalizada](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="4712f-124"><a id="multiple"></a> Cómo leer varias entidades desde una tabla</span><span class="sxs-lookup"><span data-stu-id="4712f-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="4712f-125">Para leer una tabla, use el atributo `Table` con un parámetro `IQueryable<T>` donde el tipo `T`  se deriva de `TableEntity` o implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="4712f-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="4712f-126">El ejemplo de código siguiente lee y registra todas las filas de la tabla `Ingress`:</span><span class="sxs-lookup"><span data-stu-id="4712f-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

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

### <span data-ttu-id="4712f-127"><a id="readone"></a> Cómo leer una entidad única de una tabla</span><span class="sxs-lookup"><span data-stu-id="4712f-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="4712f-128">Existe un constructor de atributo `Table` con dos parámetros adicionales que le permiten especificar la clave de partición y la clave de fila cuando desea enlazar a una entidad de tabla única.</span><span class="sxs-lookup"><span data-stu-id="4712f-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="4712f-129">El siguiente ejemplo de código lee una fila de una tabla de una entidad `Person` según los valores de clave de partición y clave de fila recibidos en un mensaje en cola:</span><span class="sxs-lookup"><span data-stu-id="4712f-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="4712f-130">La clase `Person` de este ejemplo no debe implementar `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="4712f-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="4712f-131"><a id="storageapi"></a>Cómo usar la API de almacenamiento .NET directamente para trabajar con una tabla</span><span class="sxs-lookup"><span data-stu-id="4712f-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="4712f-132">También puede usar el atributo `Table` con un objeto `CloudTable` para obtener más flexibilidad en el trabajo con una tabla.</span><span class="sxs-lookup"><span data-stu-id="4712f-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="4712f-133">El siguiente ejemplo de código usa un objeto `CloudTable` para agregar una entidad única a la tabla *Ingress* .</span><span class="sxs-lookup"><span data-stu-id="4712f-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

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

<span data-ttu-id="4712f-134">Para obtener más información acerca de cómo usar el objeto `CloudTable` , consulte [Uso del almacenamiento de tablas de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="4712f-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="4712f-135"><a id="queues"></a>Temas relacionados tratados en el artículo sobre procedimientos de las colas</span><span class="sxs-lookup"><span data-stu-id="4712f-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="4712f-136">Para obtener información sobre cómo controlar el procesamiento de tablas desencadenado por un mensaje de cola o para ver los escenarios de SDK de WebJobs no específicos para el procesamiento de tablas, consulte [Cómo usar el almacenamiento de colas con el SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4712f-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="4712f-137">Entre los temas tratados en este artículo se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="4712f-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="4712f-138">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="4712f-138">Async functions</span></span>
* <span data-ttu-id="4712f-139">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="4712f-139">Multiple instances</span></span>
* <span data-ttu-id="4712f-140">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="4712f-140">Graceful shutdown</span></span>
* <span data-ttu-id="4712f-141">Utilizar atributos del SDK de WebJobs en el cuerpo de una función</span><span class="sxs-lookup"><span data-stu-id="4712f-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="4712f-142">Establecer las cadenas de conexión del SDK en el código.</span><span class="sxs-lookup"><span data-stu-id="4712f-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="4712f-143">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="4712f-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="4712f-144">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="4712f-144">Trigger a function manually</span></span>
* <span data-ttu-id="4712f-145">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="4712f-145">Write logs</span></span>

## <span data-ttu-id="4712f-146"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4712f-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="4712f-147">En esta guía se han proporcionado ejemplos de código que muestran cómo controlar los escenarios comunes para trabajar con tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="4712f-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="4712f-148">Para obtener más información acerca de cómo usar el SDK de WebJobs y WebJobs de Azure, consulte [Recursos de WebJobs de Azure recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="4712f-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

