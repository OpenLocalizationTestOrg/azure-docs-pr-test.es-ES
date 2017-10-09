---
title: aaaGet a trabajar con el almacenamiento de tabla y Visual Studio servicios conectados (servicios en la nube) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de tabla de Azure en un proyecto de servicio de nube en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="206d2-103">Introducción al almacenamiento de tablas de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)</span><span class="sxs-lookup"><span data-stu-id="206d2-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="206d2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="206d2-104">Overview</span></span>
<span data-ttu-id="206d2-105">Este artículo describe cómo tooget iniciado mediante el almacenamiento de tabla de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de servicios de nube mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo .</span><span class="sxs-lookup"><span data-stu-id="206d2-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="206d2-106">Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.</span><span class="sxs-lookup"><span data-stu-id="206d2-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="206d2-107">Hola servicio de almacenamiento de tabla de Azure permite toostore grandes cantidades de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="206d2-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="206d2-108">servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="206d2-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="206d2-109">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="206d2-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="206d2-110">tooget iniciado, primero debe toocreate una tabla en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="206d2-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="206d2-111">Le mostraremos cómo tabla toocreate un Azure en el código y cómo tabla básica tooperform y operaciones de entidad, como agregar, modificar, leer y leer la tabla de entidades.</span><span class="sxs-lookup"><span data-stu-id="206d2-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="206d2-112">Hola ejemplos están escritos en C\# código y utilizar hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="206d2-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="206d2-113">**Nota:** algunas de las API que realizan llamadas tooAzure almacenamiento hello son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="206d2-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="206d2-114">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="206d2-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="206d2-115">código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="206d2-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="206d2-116">Consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](../storage/storage-dotnet-how-to-use-tables.md) para más información sobre la manipulación de tablas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="206d2-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="206d2-117">Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="206d2-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="206d2-118">Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="206d2-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="206d2-119">Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="206d2-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="206d2-120">Acceso a tablas en código</span><span class="sxs-lookup"><span data-stu-id="206d2-120">Access tables in code</span></span>
<span data-ttu-id="206d2-121">tooaccess tablas en proyectos de servicios de nube, debe hello tooinclude siguientes archivos de origen de tooany C# de elementos que tienen acceso a almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="206d2-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="206d2-122">Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.</span><span class="sxs-lookup"><span data-stu-id="206d2-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="206d2-123">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="206d2-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="206d2-124">Usar hello siguientes código tooget Hola almacenamiento conexión cadena y almacenamiento de información de la cuenta de configuración de servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="206d2-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="206d2-125">Use todos Hola encima código frente a código de hello en los siguientes ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="206d2-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="206d2-126">Obtener un **CloudTableClient** tooreference Hola tabla objetos en la cuenta de almacenamiento de objetos.</span><span class="sxs-lookup"><span data-stu-id="206d2-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="206d2-127">Obtener un **CloudTable** hacen referencia a una tabla específica del objeto tooreference y entidades.</span><span class="sxs-lookup"><span data-stu-id="206d2-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="206d2-128">Crear una tabla en el código</span><span class="sxs-lookup"><span data-stu-id="206d2-128">Create a table in code</span></span>
<span data-ttu-id="206d2-129">Hola toocreate tabla de Azure, basta con agregar una llamada demasiado**CreateIfNotExistsAsync** toohello después de obtener un **CloudTable** objeto tal y como se describe en la sección de "Acceso a tablas en el código" Hola.</span><span class="sxs-lookup"><span data-stu-id="206d2-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="206d2-130">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="206d2-130">Add an entity tooa table</span></span>
<span data-ttu-id="206d2-131">tooadd una tabla de tooa de entidad, cree una clase que define las propiedades de saludo de la entidad.</span><span class="sxs-lookup"><span data-stu-id="206d2-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="206d2-132">Hello código siguiente define una clase de entidad denominada **CustomerEntity** que usa Hola nombre del cliente como clave de fila de Hola y Hola last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="206d2-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="206d2-133">Operaciones de tabla que implican las entidades se realizan mediante hello **CloudTable** objeto que creó anteriormente en "Acceso a las tablas en el código".</span><span class="sxs-lookup"><span data-stu-id="206d2-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="206d2-134">Hola **TableOperation** objeto representa Hola operación toobe realizada.</span><span class="sxs-lookup"><span data-stu-id="206d2-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="206d2-135">Hola siguiendo el ejemplo de código muestra cómo toocreate una **CloudTable** objeto y un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="206d2-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="206d2-136">operación de hello tooprepare, un **TableOperation** se crea la entidad customer ya tooinsert hello en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="206d2-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="206d2-137">Por último, se ejecuta la operación de hello mediante una llamada a **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="206d2-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="206d2-138">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="206d2-138">Insert a batch of entities</span></span>
<span data-ttu-id="206d2-139">Puede insertar varias entidades en una tabla mediante una única operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="206d2-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="206d2-140">Hello ejemplo de código siguiente crea dos objetos de entidad ("Jeff Smith" y "Ben Smith"), se agrega tooa **TableBatchOperation** objeto mediante Hola método Insert y, a continuación, inicia Hola operación mediante una llamada a  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="206d2-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="206d2-141">Obtener todas las entidades de hello en una partición</span><span class="sxs-lookup"><span data-stu-id="206d2-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="206d2-142">tooquery una tabla para todas las entidades de hello en una partición, use un **TableQuery** objeto.</span><span class="sxs-lookup"><span data-stu-id="206d2-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="206d2-143">Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="206d2-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="206d2-144">Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="206d2-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="206d2-145">Obtención de una sola entidad</span><span class="sxs-lookup"><span data-stu-id="206d2-145">Get a single entity</span></span>
<span data-ttu-id="206d2-146">Puede escribir una consulta tooget una entidad única, específica.</span><span class="sxs-lookup"><span data-stu-id="206d2-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="206d2-147">Hola siguiente de código utiliza un **TableOperation** toospecify un cliente llamado "Ben Smith" del objeto.</span><span class="sxs-lookup"><span data-stu-id="206d2-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="206d2-148">Este método devuelve una sola entidad, en lugar de una colección y Hola devolvió el valor en **TableResult.Result** es un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="206d2-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="206d2-149">La especificación de claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una entidad única desde hello **tabla** servicio.</span><span class="sxs-lookup"><span data-stu-id="206d2-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="206d2-150">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="206d2-150">Delete an entity</span></span>
<span data-ttu-id="206d2-151">Puede eliminar fácilmente una entidad después de haberla encontrado.</span><span class="sxs-lookup"><span data-stu-id="206d2-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="206d2-152">Hello código siguiente busca una entidad de cliente denominada "Ben Smith" y, si lo encuentra, elimina.</span><span class="sxs-lookup"><span data-stu-id="206d2-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="206d2-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="206d2-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

