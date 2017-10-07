---
title: aaaGetting iniciado con el almacenamiento de Azure y servicios conectados de Visual Studio (proyectos de trabajo Web)
description: "Cómo tooget iniciado mediante el almacenamiento de tabla de Azure en un proyecto de trabajos Web de Azure en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="d6138-103">Introducción a Almacenamiento de Azure (proyectos de WebJobs de Azure)</span><span class="sxs-lookup"><span data-stu-id="d6138-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="d6138-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d6138-104">Overview</span></span>
<span data-ttu-id="d6138-105">Este artículo se proporcionan ejemplos de código de C# que muestran muestran cómo toouse Hola versión del SDK de WebJobs de Azure 1.x con hello servicio de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6138-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="d6138-106">ejemplos de código de Hello usan hello [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="d6138-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="d6138-107">Hola servicio de almacenamiento de tabla de Azure permite toostore grandes cantidades de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="d6138-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="d6138-108">servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6138-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="d6138-109">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="d6138-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="d6138-110">Consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) para más información.</span><span class="sxs-lookup"><span data-stu-id="d6138-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="d6138-111">Algunos de los fragmentos de código de hello mostrar hello **tabla** atributo utilizado en las funciones que se llaman manualmente, es decir, no con uno de los atributos de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6138-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="d6138-112">La tabla de tooadd entidades tooa</span><span class="sxs-lookup"><span data-stu-id="d6138-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="d6138-113">tabla de tooa tooadd entidades, use hello **tabla** atributo con un **ICollector<T>**  o **IAsyncCollector<T>**  parámetro donde **T** especifica el esquema de Hola de entidades de hello desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="d6138-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="d6138-114">constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre de Hola de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6138-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="d6138-115">Hello siguiente ejemplo de código agrega **persona** tabla de entidades tooa denominada *entrada*.</span><span class="sxs-lookup"><span data-stu-id="d6138-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="d6138-116">Hola normalmente el tipo que se utiliza con **ICollector** deriva **TableEntity** o implementa **ITableEntity**, pero no es necesario.</span><span class="sxs-lookup"><span data-stu-id="d6138-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="d6138-117">Cualquiera de los siguientes hello **persona** clases con código de hello mostrado en hello anterior **entrada** método.</span><span class="sxs-lookup"><span data-stu-id="d6138-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="d6138-118">Si desea que toowork directamente con hello API de almacenamiento de Azure, puede agregar un **CloudStorageAccount** firma del método toohello parámetro.</span><span class="sxs-lookup"><span data-stu-id="d6138-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="d6138-119">Supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="d6138-119">Real-time monitoring</span></span>
<span data-ttu-id="d6138-120">Dado que las funciones de entrada de datos a menudo procesan grandes volúmenes de datos, panel de SDK de WebJobs Hola proporciona datos de supervisión en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="d6138-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="d6138-121">Hola **invocación registro** sección indica si la función hello se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="d6138-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Función de entrada en ejecución](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="d6138-123">Hola **detalles de invocación** página informes Hola progreso de la función (número de entidades que escriben) mientras se está ejecutando y proporciona una oportunidad tooabort lo.</span><span class="sxs-lookup"><span data-stu-id="d6138-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Función de entrada en ejecución](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="d6138-125">Cuando función hello finalice, hello **detalles de invocación** página notifica el número de Hola de filas escritas.</span><span class="sxs-lookup"><span data-stu-id="d6138-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Función de entrada finalizada](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="d6138-127">¿Cómo tooread varias entidades de una tabla</span><span class="sxs-lookup"><span data-stu-id="d6138-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="d6138-128">tooread una tabla, utilice hello **tabla** atributo con un **IQueryable<T>**  parámetro donde escribir **T** deriva **TableEntity**o implementa **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d6138-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="d6138-129">lee Hello siguiente ejemplo de código y registros de todas las filas de hello **entrada** tabla:</span><span class="sxs-lookup"><span data-stu-id="d6138-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="d6138-130">¿Cómo tooread una sola entidad de una tabla</span><span class="sxs-lookup"><span data-stu-id="d6138-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="d6138-131">Hay un **tabla** constructor de atributo con dos parámetros adicionales que le permiten especificar la clave de partición de Hola y clave de fila cuando se desea toobind tooa tabla única entidad.</span><span class="sxs-lookup"><span data-stu-id="d6138-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="d6138-132">ejemplo de código siguiente Hello lee una fila de tabla para una **persona** entidad en función de clave y la fila de claves de partición recibidos en un mensaje de cola:</span><span class="sxs-lookup"><span data-stu-id="d6138-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="d6138-133">Hola **persona** clase en este ejemplo no tiene tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d6138-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="d6138-134">¿Cómo toouse Hola API de almacenamiento de .NET directamente toowork con una tabla</span><span class="sxs-lookup"><span data-stu-id="d6138-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="d6138-135">También puede usar hello **tabla** atributo con un **CloudTable** objeto para una mayor flexibilidad cuando se trabaja con una tabla.</span><span class="sxs-lookup"><span data-stu-id="d6138-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="d6138-136">usos de ejemplo de código siguiente Hola un **CloudTable** objeto tooadd una sola entidad toohello *entrada* tabla.</span><span class="sxs-lookup"><span data-stu-id="d6138-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="d6138-137">Para obtener más información acerca de cómo hello toouse **CloudTable** de objetos, consulte [Introducción al almacenamiento de tabla de Azure mediante .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d6138-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="d6138-138">Temas relacionados cubiertos por las colas de hello cómo-tooarticle</span><span class="sxs-lookup"><span data-stu-id="d6138-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="d6138-139">Para obtener información acerca de cómo el procesamiento de tabla toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no procesar, consulte específica tootable [Introducción al almacenamiento de cola de Azure y Visual Studio conectado servicios (proyectos de trabajo Web) ](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d6138-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6138-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6138-140">Next steps</span></span>
<span data-ttu-id="d6138-141">En este artículo ha proporcionado el código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6138-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="d6138-142">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d6138-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

