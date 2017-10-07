---
title: aaaHow tooget a trabajar con el almacenamiento de tabla y Visual Studio servicios conectados (ASP.NET Core) | Documentos de Microsoft
description: "Forma en que tooget se inicia con el almacenamiento de tabla de Azure en un proyecto de ASP.NET Core en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 6a8fb6aa085d78a087fcd14adbc765a0d59e0308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="5816e-103">¿Cómo tooget a trabajar con el almacenamiento de tabla de Azure y Visual Studio servicios conectados</span><span class="sxs-lookup"><span data-stu-id="5816e-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="5816e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5816e-104">Overview</span></span>
<span data-ttu-id="5816e-105">Este artículo se describe cómo obtener se hayan iniciado mediante la tabla de Azure Hola almacenamiento en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET Core mediante Visual Studio **agregar servicios conectados** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5816e-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="5816e-106">Hola servicio de almacenamiento de tabla de Azure permite toostore grandes cantidades de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="5816e-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="5816e-107">servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="5816e-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="5816e-108">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="5816e-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="5816e-109">Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.</span><span class="sxs-lookup"><span data-stu-id="5816e-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="5816e-110">Para más información general sobre el uso de Almacenamiento de tablas de Azure, consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5816e-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="5816e-111">tooget iniciado, primero debe toocreate una tabla en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5816e-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="5816e-112">Le mostraremos cómo tabla toocreate un Azure en el código.</span><span class="sxs-lookup"><span data-stu-id="5816e-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="5816e-113">También le mostraremos cómo tabla básica tooperform y operaciones de entidad, como agregar, modificar, leer y leer la tabla de entidades.</span><span class="sxs-lookup"><span data-stu-id="5816e-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="5816e-114">Hola ejemplos están escritos en C\# código y utilizar Hola biblioteca de cliente de almacenamiento de Azure para. NET.</span><span class="sxs-lookup"><span data-stu-id="5816e-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="5816e-115">**Tenga en cuenta** -algunas de las API que realizan llamadas tooAzure almacenamiento en ASP.NET Core Hola son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="5816e-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="5816e-116">Consulte [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="5816e-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="5816e-117">código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="5816e-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="5816e-118">Acceso a tablas en código</span><span class="sxs-lookup"><span data-stu-id="5816e-118">Access tables in code</span></span>
<span data-ttu-id="5816e-119">tooaccess tablas en proyectos de ASP.NET Core, deberá hello tooinclude siguientes archivos de origen de tooany C# de elementos que tienen acceso a almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="5816e-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="5816e-120">Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.</span><span class="sxs-lookup"><span data-stu-id="5816e-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="5816e-121">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5816e-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5816e-122">Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="5816e-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="5816e-123">**Tenga en cuenta** -los Hola encima código frente a código de hello usan en hello siguiendo los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="5816e-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="5816e-124">Obtener un **CloudTableClient** tooreference Hola tabla objetos en la cuenta de almacenamiento de objetos.</span><span class="sxs-lookup"><span data-stu-id="5816e-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="5816e-125">Obtener un **CloudTable** hacen referencia a una tabla específica del objeto tooreference y entidades.</span><span class="sxs-lookup"><span data-stu-id="5816e-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="5816e-126">Crear una tabla en el código</span><span class="sxs-lookup"><span data-stu-id="5816e-126">Create a table in code</span></span>
<span data-ttu-id="5816e-127">Hola toocreate tabla de Azure, basta con agregar una llamada demasiado**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="5816e-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="5816e-128">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="5816e-128">Add an entity tooa table</span></span>
<span data-ttu-id="5816e-129">tooadd una tabla de tooa de entidad se crea una clase que define las propiedades de saludo de la entidad.</span><span class="sxs-lookup"><span data-stu-id="5816e-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="5816e-130">Hello código siguiente define una clase de entidad denominada **CustomerEntity** que usa Hola nombre del cliente como clave de fila de Hola y last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="5816e-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }

        public string PhoneNumber { get; set; }
    }

<span data-ttu-id="5816e-131">Operaciones de tabla que implican las entidades se realizan mediante hello **CloudTable** objeto que creó anteriormente en "Acceso a las tablas en el código".</span><span class="sxs-lookup"><span data-stu-id="5816e-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="5816e-132">Hola **TableOperation** objeto representa Hola operación toobe realizada.</span><span class="sxs-lookup"><span data-stu-id="5816e-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="5816e-133">Hola siguiendo el ejemplo de código muestra cómo toocreate una **CloudTable** objeto y un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="5816e-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="5816e-134">operación de hello tooprepare, un **TableOperation** se crea la entidad customer ya tooinsert hello en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="5816e-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="5816e-135">Por último, la operación de Hola se ejecuta mediante una llamada a CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="5816e-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="5816e-136">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="5816e-136">Insert a batch of entities</span></span>
<span data-ttu-id="5816e-137">Puede insertar varias entidades en una tabla mediante una única operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="5816e-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="5816e-138">Hello ejemplo de código siguiente crea dos objetos de entidad ("Jeff Smith" y "Ben Smith"), se agrega tooa **TableBatchOperation** objeto mediante hello **insertar** método y, a continuación, inicia Hola operación CloudTable.ExecuteBatchAsync que realiza la llamada.</span><span class="sxs-lookup"><span data-stu-id="5816e-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

    // Create hello batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it toohello table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities toohello batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute hello batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="5816e-139">Obtener todas las entidades de hello en una partición</span><span class="sxs-lookup"><span data-stu-id="5816e-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="5816e-140">tooquery una tabla para todas las entidades de hello en una partición, use un **TableQuery** objeto.</span><span class="sxs-lookup"><span data-stu-id="5816e-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="5816e-141">Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="5816e-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="5816e-142">Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5816e-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="5816e-143">Obtención de una sola entidad</span><span class="sxs-lookup"><span data-stu-id="5816e-143">Get a single entity</span></span>
<span data-ttu-id="5816e-144">Puede escribir una consulta tooget una entidad única, específica.</span><span class="sxs-lookup"><span data-stu-id="5816e-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="5816e-145">Hola siguiente de código utiliza un **TableOperation** toospecify un cliente llamado "Ben Smith" del objeto.</span><span class="sxs-lookup"><span data-stu-id="5816e-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="5816e-146">Este método devuelve una sola entidad, en lugar de una colección y Hola devolvió el valor en **TableResult.Result** es un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="5816e-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="5816e-147">La especificación de claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una entidad única desde hello **tabla** servicio.</span><span class="sxs-lookup"><span data-stu-id="5816e-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="5816e-148">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="5816e-148">Delete an entity</span></span>
<span data-ttu-id="5816e-149">Puede eliminar fácilmente una entidad después de haberla encontrado.</span><span class="sxs-lookup"><span data-stu-id="5816e-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="5816e-150">Hello código siguiente busca una entidad de cliente denominada "Ben Smith" y si lo encuentra, elimina.</span><span class="sxs-lookup"><span data-stu-id="5816e-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="5816e-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5816e-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

