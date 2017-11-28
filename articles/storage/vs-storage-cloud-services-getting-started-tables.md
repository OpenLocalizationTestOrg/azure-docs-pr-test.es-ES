---
title: "Introducción al almacenamiento de tablas y los servicios conectados de Visual Studio (servicios en la nube) | Microsoft Docs"
description: "Cómo empezar a usar el almacenamiento de tablas de Azure en un proyecto de servicio en la nube en Visual Studio después de conectarse a una cuenta de almacenamiento mediante los servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3208ddb1a1246a5ff25d272bfc7d8ba842348a36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="e320b-103">Introducción al almacenamiento de tablas de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)</span><span class="sxs-lookup"><span data-stu-id="e320b-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="e320b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e320b-104">Overview</span></span>
<span data-ttu-id="e320b-105">En este artículo se describe cómo empezar a usar el almacenamiento de tablas de Azure en Visual Studio después de haber creado o hecho referencia a una cuenta de almacenamiento de Azure en un proyecto de servicios en la nube mediante el cuadro de diálogo **Agregar servicios conectados** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e320b-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="e320b-106">La operación **Agregar servicios conectados** instala los paquetes de NuGet adecuados para tener acceso al almacenamiento de Azure en el proyecto y agrega la cadena de conexión de la cuenta de almacenamiento a los archivos de configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e320b-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="e320b-107">El servicio de almacenamiento de tabla de Azure permite almacenar una gran cantidad de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="e320b-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="e320b-108">El servicio es un almacén de datos NoSQL que acepta llamadas autenticadas desde dentro y fuera de la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="e320b-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="e320b-109">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="e320b-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="e320b-110">Para comenzar, necesita crear una tabla en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e320b-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="e320b-111">También le mostraremos cómo crear una tabla de Azure en código, además de cómo realizar operaciones básicas de tabla y de entidad, como agregar, modificar y leer entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="e320b-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="e320b-112">Los ejemplos están escritos en código C\# y usan la [biblioteca del cliente de Microsoft Azure Storage para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="e320b-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="e320b-113">**NOTA:** algunas de las API que realizan llamadas al almacenamiento de Azure son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="e320b-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="e320b-114">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="e320b-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="e320b-115">El código siguiente supone que se están utilizando métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="e320b-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="e320b-116">Consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md) para más información sobre la manipulación de tablas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e320b-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="e320b-117">Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e320b-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="e320b-118">Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="e320b-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="e320b-119">Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e320b-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="e320b-120">Acceso a tablas en código</span><span class="sxs-lookup"><span data-stu-id="e320b-120">Access tables in code</span></span>
<span data-ttu-id="e320b-121">Para obtener acceso a las tablas en los proyectos de servicios en la nube, deberá incluir los elementos siguientes en los archivos de origen C# que acceden al almacenamiento Tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e320b-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="e320b-122">Asegúrese de que las declaraciones del espacio de nombres de la parte superior del archivo de C# incluyen estas instrucciones **using** .</span><span class="sxs-lookup"><span data-stu-id="e320b-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="e320b-123">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e320b-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e320b-124">Use el código siguiente para obtener la cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de la configuración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="e320b-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="e320b-125">Use todo el código anterior delante del código que aparece en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="e320b-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="e320b-126">Obtenga un objeto **CloudTableClient** para hacer referencia a los objetos de tabla de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e320b-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="e320b-127">Obtenga un objeto de referencia **CloudTable** para hacer referencia a una tabla y a entidades específicas.</span><span class="sxs-lookup"><span data-stu-id="e320b-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="e320b-128">Crear una tabla en el código</span><span class="sxs-lookup"><span data-stu-id="e320b-128">Create a table in code</span></span>
<span data-ttu-id="e320b-129">Para crear la tabla de Azure, basta con que agregue una llamada a **CreateIfNotExistsAsync** después de obtener el objeto **CloudTable**, tal como se describe en la sección "Acceso a tablas en código".</span><span class="sxs-lookup"><span data-stu-id="e320b-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e320b-130">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="e320b-130">Add an entity to a table</span></span>
<span data-ttu-id="e320b-131">Para agregar una entidad a una tabla, cree una clase que defina las propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="e320b-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="e320b-132">El código siguiente define una clase de entidad llamada **CustomerEntity** que usa el nombre del cliente como clave de fila y el apellido como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="e320b-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="e320b-133">Las operaciones de tablas que afectan a las entidades se realizan con el objeto **CloudTable** que se creó anteriormente en el apartado "Acceso a tablas en código".</span><span class="sxs-lookup"><span data-stu-id="e320b-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="e320b-134">El objeto **TableOperation** representa la operación que se va a realizar.</span><span class="sxs-lookup"><span data-stu-id="e320b-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="e320b-135">En el ejemplo de código siguiente se muestra cómo crear un objeto **CloudTable** y un objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e320b-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="e320b-136">Para preparar la operación, se crea un objeto **TableOperation** para insertar la entidad de cliente en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e320b-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="e320b-137">Por último, la operación se ejecuta llamando a **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="e320b-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="e320b-138">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="e320b-138">Insert a batch of entities</span></span>
<span data-ttu-id="e320b-139">Puede insertar varias entidades en una tabla mediante una única operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="e320b-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="e320b-140">En el ejemplo de código siguiente se crean dos objetos de entidad ("Jeff Smith" y "Ben Smith") que se agregan a un objeto **TableBatchOperation** mediante el método Insert y, a continuación, se inicia la operación llamando a **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="e320b-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="e320b-141">Obtención de todas las entidades en una partición</span><span class="sxs-lookup"><span data-stu-id="e320b-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="e320b-142">Para consultar una tabla a fin de obtener todas las entidades de una partición, use un objeto **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="e320b-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="e320b-143">El ejemplo de código siguiente especifica un filtro para las entidades en las que “Smith” es la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="e320b-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="e320b-144">En este ejemplo, los campos de cada entidad se imprimen en la consola, como parte de los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="e320b-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="e320b-145">Obtención de una sola entidad</span><span class="sxs-lookup"><span data-stu-id="e320b-145">Get a single entity</span></span>
<span data-ttu-id="e320b-146">Puede escribir una consulta para obtener una sola entidad concreta.</span><span class="sxs-lookup"><span data-stu-id="e320b-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="e320b-147">El código siguiente utiliza un objeto **TableOperation** para especificar el cliente llamado "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="e320b-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="e320b-148">Este método devuelve solo una entidad, en lugar de una colección, y el valor devuelto en **TableResult.Result** es un objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e320b-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="e320b-149">La forma más rápida de recuperar una sola entidad del servicio **Tabla** es especificar claves tanto de partición como de fila en las consultas.</span><span class="sxs-lookup"><span data-stu-id="e320b-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="e320b-150">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="e320b-150">Delete an entity</span></span>
<span data-ttu-id="e320b-151">Puede eliminar fácilmente una entidad después de haberla encontrado.</span><span class="sxs-lookup"><span data-stu-id="e320b-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="e320b-152">El código siguiente busca una entidad de cliente denominada "Ben Smith" y, si la encuentra, la elimina.</span><span class="sxs-lookup"><span data-stu-id="e320b-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e320b-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e320b-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

