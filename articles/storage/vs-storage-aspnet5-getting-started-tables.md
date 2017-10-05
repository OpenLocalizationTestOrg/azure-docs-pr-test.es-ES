---
title: "Introducción a Table Storage y los servicios conectados de Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Introducción a Azure Table Storage en un proyecto de ASP.NET Core en Visual Studio después de conectarse a una cuenta de almacenamiento mediante los servicios conectados de Visual Studio"
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
ms.openlocfilehash: b64d4f7e55977c7ce144987f7600e5ddcb25596c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="3aca6-103">Introducción al almacenamiento Tabla de Azure y los servicios conectados de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3aca6-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="3aca6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="3aca6-104">Overview</span></span>
<span data-ttu-id="3aca6-105">En este artículo se describe cómo empezar a usar Azure Table Storage en Visual Studio después de crear una cuenta de Azure Storage en un proyecto de ASP.NET Core mediante el cuadro de diálogo **Add Connected Services** (Agregar servicios conectados) de Visual Studio, o después de hacer referencia a una.</span><span class="sxs-lookup"><span data-stu-id="3aca6-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="3aca6-106">El servicio de almacenamiento de tabla de Azure permite almacenar una gran cantidad de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="3aca6-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="3aca6-107">El servicio es un almacén de datos NoSQL que acepta llamadas autenticadas desde dentro y fuera de la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aca6-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="3aca6-108">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="3aca6-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="3aca6-109">La operación **Agregar servicios conectados** instala los paquetes de NuGet adecuados para tener acceso al almacenamiento de Azure en el proyecto y agrega la cadena de conexión para la cuenta de almacenamiento a los archivos de configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3aca6-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="3aca6-110">Para más información general sobre el uso de Almacenamiento de tablas de Azure, consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="3aca6-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="3aca6-111">Para comenzar, necesita crear una tabla en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3aca6-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="3aca6-112">Le mostraremos cómo crear una tabla de Azure en el código.</span><span class="sxs-lookup"><span data-stu-id="3aca6-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="3aca6-113">También le mostraremos cómo realizar operaciones básicas de tabla y de entidad, como agregar, modificar, leer y leer entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="3aca6-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="3aca6-114">Los ejemplos están escritos en código C\# y usan la biblioteca del cliente de Azure Storage para .NET.</span><span class="sxs-lookup"><span data-stu-id="3aca6-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="3aca6-115">**NOTA**: Algunas de las API que realizan llamadas a Azure Storage en ASP.NET Core son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="3aca6-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="3aca6-116">Consulte [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3aca6-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="3aca6-117">El código siguiente supone que se están utilizando métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="3aca6-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="3aca6-118">Acceso a tablas en código</span><span class="sxs-lookup"><span data-stu-id="3aca6-118">Access tables in code</span></span>
<span data-ttu-id="3aca6-119">Para obtener acceso a las tablas de los proyectos de ASP.NET Core, deberá incluir los elementos siguientes en los archivos de origen de C# que acceden a Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="3aca6-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="3aca6-120">Asegúrese de que las declaraciones del espacio de nombres de la parte superior del archivo de C# incluyen estas instrucciones **using** .</span><span class="sxs-lookup"><span data-stu-id="3aca6-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="3aca6-121">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3aca6-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="3aca6-122">Use el código siguiente para obtener la cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de la configuración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aca6-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="3aca6-123">**NOTA** : use todo el código anterior delante del código que aparece en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="3aca6-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="3aca6-124">Obtenga un objeto **CloudTableClient** para hacer referencia a los objetos de tabla de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3aca6-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="3aca6-125">Obtenga un objeto de referencia **CloudTable** para hacer referencia a una tabla y a entidades específicas.</span><span class="sxs-lookup"><span data-stu-id="3aca6-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="3aca6-126">Crear una tabla en el código</span><span class="sxs-lookup"><span data-stu-id="3aca6-126">Create a table in code</span></span>
<span data-ttu-id="3aca6-127">Para crear la tabla de Azure, solo tiene que agregar una llamada a **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="3aca6-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="3aca6-128">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="3aca6-128">Add an entity to a table</span></span>
<span data-ttu-id="3aca6-129">Para agregar una entidad a una tabla, cree una clase que defina las propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="3aca6-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="3aca6-130">El código siguiente define una clase de entidad llamada **CustomerEntity** que usa el nombre del cliente como clave de fila y el apellido como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="3aca6-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

<span data-ttu-id="3aca6-131">Las operaciones de tablas que afectan a las entidades se realizan con el objeto **CloudTable** que se creó anteriormente en el apartado "Acceso a tablas en código".</span><span class="sxs-lookup"><span data-stu-id="3aca6-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="3aca6-132">El objeto **TableOperation** representa la operación que se va a realizar.</span><span class="sxs-lookup"><span data-stu-id="3aca6-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="3aca6-133">En el ejemplo de código siguiente se muestra cómo crear un objeto **CloudTable** y un objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="3aca6-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="3aca6-134">Para preparar la operación, se crea un objeto **TableOperation** para insertar la entidad de cliente en la tabla.</span><span class="sxs-lookup"><span data-stu-id="3aca6-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="3aca6-135">Por último, la operación se ejecuta llamando a CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="3aca6-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="3aca6-136">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="3aca6-136">Insert a batch of entities</span></span>
<span data-ttu-id="3aca6-137">Puede insertar varias entidades en una tabla mediante una única operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="3aca6-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="3aca6-138">En el ejemplo de código siguiente se crean dos objetos de entidad ("Jeff Smith" y "Ben Smith") que se agregan a un objeto **TableBatchOperation** mediante el método Insert y, a continuación, se inicia la operación llamando a **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="3aca6-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

    // Create the batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it to the table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities to the batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute the batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="3aca6-139">Obtención de todas las entidades en una partición</span><span class="sxs-lookup"><span data-stu-id="3aca6-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="3aca6-140">Para consultar una tabla a fin de obtener todas las entidades de una partición, use un objeto **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="3aca6-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="3aca6-141">El ejemplo de código siguiente especifica un filtro para las entidades en las que “Smith” es la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="3aca6-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="3aca6-142">En este ejemplo, los campos de cada entidad se imprimen en la consola, como parte de los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="3aca6-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
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

## <a name="get-a-single-entity"></a><span data-ttu-id="3aca6-143">Obtención de una sola entidad</span><span class="sxs-lookup"><span data-stu-id="3aca6-143">Get a single entity</span></span>
<span data-ttu-id="3aca6-144">Puede escribir una consulta para obtener una sola entidad concreta.</span><span class="sxs-lookup"><span data-stu-id="3aca6-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="3aca6-145">El código siguiente utiliza un objeto **TableOperation** para especificar el cliente llamado "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="3aca6-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="3aca6-146">Este método devuelve solo una entidad, en lugar de una colección, y el valor devuelto en **TableResult.Result** es un objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="3aca6-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="3aca6-147">La forma más rápida de recuperar una sola entidad del servicio **Tabla** es especificar claves tanto de partición como de fila en las consultas.</span><span class="sxs-lookup"><span data-stu-id="3aca6-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="3aca6-148">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="3aca6-148">Delete an entity</span></span>
<span data-ttu-id="3aca6-149">Puede eliminar fácilmente una entidad después de haberla encontrado.</span><span class="sxs-lookup"><span data-stu-id="3aca6-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="3aca6-150">El código siguiente busca una entidad de cliente denominada "Ben Smith" y, si la encuentra, la elimina.</span><span class="sxs-lookup"><span data-stu-id="3aca6-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="3aca6-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3aca6-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

