---
title: aaaGet a trabajar con almacenamiento de tabla de Azure mediante .NET | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="1ae68-103">Introducción al Almacenamiento de tablas de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="1ae68-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="1ae68-104">El almacenamiento de tabla es un servicio que almacena NoSQL estructurado con un diseño schemaless del almacén de datos en la nube de hello, que proporciona un atributo de clave.</span><span class="sxs-lookup"><span data-stu-id="1ae68-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="1ae68-105">Dado que el almacenamiento de tabla es schemaless, resulta fácil tooadapt necesidades de los datos como Hola de evolucionar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ae68-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="1ae68-106">Acceder a los datos de almacenamiento tooTable es rápido y rentable para muchos tipos de aplicaciones y es normalmente menores costo SQL tradicional para similar volúmenes de datos.</span><span class="sxs-lookup"><span data-stu-id="1ae68-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="1ae68-107">Puede usar la tabla almacenamiento toostore flexible los conjuntos de datos como datos de usuario para aplicaciones web, libretas de direcciones, información de dispositivo u otros tipos de metadatos que se requiere el servicio.</span><span class="sxs-lookup"><span data-stu-id="1ae68-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="1ae68-108">Puede almacenar cualquier número de entidades en una tabla y una cuenta de almacenamiento puede contener cualquier número de tablas, una toohello el límite de capacidad de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="1ae68-109">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="1ae68-109">About this tutorial</span></span>
<span data-ttu-id="1ae68-110">Este tutorial muestra cómo hello toouse [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) en algunos escenarios comunes de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae68-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="1ae68-111">Estos escenarios se presentan con ejemplos de C# para crear y eliminar una tabla, e insertar, actualizar, eliminar y consultar datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="1ae68-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ae68-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1ae68-112">Prerequisites</span></span>

<span data-ttu-id="1ae68-113">Se necesita Hola siguientes toocomplete este tutorial correctamente:</span><span class="sxs-lookup"><span data-stu-id="1ae68-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="1ae68-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ae68-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="1ae68-115">Biblioteca de cliente de Almacenamiento de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="1ae68-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="1ae68-116">Administrador de configuración Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="1ae68-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="1ae68-117">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1ae68-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="1ae68-118">Más ejemplos</span><span class="sxs-lookup"><span data-stu-id="1ae68-118">More samples</span></span>
<span data-ttu-id="1ae68-119">Para más ejemplos de uso de Almacenamiento de tablas, consulte [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Introducción a Almacenamiento de tablas de Azure en .NET).</span><span class="sxs-lookup"><span data-stu-id="1ae68-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="1ae68-120">Puede descargar la aplicación de ejemplo de Hola y ejecutarlo o examinar el código de hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="1ae68-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="1ae68-121">Adición de directivas using</span><span class="sxs-lookup"><span data-stu-id="1ae68-121">Add using directives</span></span>
<span data-ttu-id="1ae68-122">Agregue Hola siguiente **con** arriba toohello de directivas de hello `Program.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="1ae68-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="1ae68-123">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="1ae68-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="1ae68-124">Crear el cliente del servicio tabla Hola</span><span class="sxs-lookup"><span data-stu-id="1ae68-124">Create hello Table service client</span></span>
<span data-ttu-id="1ae68-125">Hola [CloudTableClient] [ dotnet_CloudTableClient] clase le permite tooretrieve tablas y entidades almacenadas en almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="1ae68-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="1ae68-126">Este es el cliente del servicio de tabla de una manera toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="1ae68-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="1ae68-127">Ahora está listo toowrite código que lee datos de y escribe tooTable almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="1ae68-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1ae68-128">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="1ae68-128">Create a table</span></span>
<span data-ttu-id="1ae68-129">Este ejemplo se muestra cómo toocreate una tabla si aún no existe:</span><span class="sxs-lookup"><span data-stu-id="1ae68-129">This example shows how toocreate a table if it does not already exist:</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="1ae68-130">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="1ae68-130">Add an entity tooa table</span></span>
<span data-ttu-id="1ae68-131">Las entidades asignan objetos tooC # mediante el uso de una clase personalizada derivada de [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="1ae68-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="1ae68-132">tooadd una tabla de tooa de entidad, cree una clase que define las propiedades de saludo de la entidad.</span><span class="sxs-lookup"><span data-stu-id="1ae68-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="1ae68-133">Hello código siguiente define una clase de entidad que utiliza el nombre del cliente de hello como clave de fila de Hola y last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="1ae68-134">Juntos, partición de una entidad y la clave de fila identifican singularmente en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="1ae68-135">Claves de partición de entidades con la misma clave de partición se puede consultar con más rapidez que las entidades con diferentes de hello, pero el uso de las claves de partición diversos permite para una mayor escalabilidad de operaciones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="1ae68-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="1ae68-136">Debe ser toobe de entidades que se almacenan en tablas de un tipo compatible, por ejemplo derivado Hola [TableEntity] [ dotnet_TableEntity] clase.</span><span class="sxs-lookup"><span data-stu-id="1ae68-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="1ae68-137">Propiedades de la entidad que desea que toostore en una tabla deben ser propiedades públicas de tipo hello y admitir obtener y establecer valores de.</span><span class="sxs-lookup"><span data-stu-id="1ae68-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="1ae68-138">Además, el tipo de entidad *must* expone un constructor sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="1ae68-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

```csharp
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
```

<span data-ttu-id="1ae68-139">Las operaciones de tabla que implican las entidades se realizan a través de hello [CloudTable] [ dotnet_CloudTable] objeto que creó anteriormente en la sección "Crear una tabla" de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="1ae68-140">Hello toobe operación realiza representado por un [TableOperation] [ dotnet_TableOperation] objeto.</span><span class="sxs-lookup"><span data-stu-id="1ae68-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="1ae68-141">Hello ejemplo de código siguiente muestra hello creación de hello [CloudTable] [ dotnet_CloudTable] objeto y, a continuación, un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="1ae68-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="1ae68-142">operación de hello tooprepare, un [TableOperation] [ dotnet_TableOperation] objeto se crea la entidad customer ya tooinsert hello en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="1ae68-143">Por último, se ejecuta la operación de hello mediante una llamada a [CloudTable][dotnet_CloudTable].[ Ejecutar][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="1ae68-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="1ae68-144">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="1ae68-144">Insert a batch of entities</span></span>
<span data-ttu-id="1ae68-145">Puede insertar un lote de entidades en una tabla mediante una operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="1ae68-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="1ae68-146">Otras notas acerca de las operaciones por lotes:</span><span class="sxs-lookup"><span data-stu-id="1ae68-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="1ae68-147">Puede realizar actualizaciones, eliminaciones e inserciones en hello mismo única operación por lotes.</span><span class="sxs-lookup"><span data-stu-id="1ae68-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="1ae68-148">Una única operación por lotes puede incluir una too100 entidades.</span><span class="sxs-lookup"><span data-stu-id="1ae68-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="1ae68-149">Todas las entidades de una operación por lotes solo deben tener Hola misma clave de partición.</span><span class="sxs-lookup"><span data-stu-id="1ae68-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="1ae68-150">Aunque es posible tooperform una consulta como una operación por lotes, debe ser única operación de hello en lote Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="1ae68-151">crea dos objetos entidad Hello siguiente ejemplo de código y agrega cada demasiado[TableBatchOperation] [ dotnet_TableBatchOperation] mediante el uso de hello [insertar] [ dotnet_TableBatchOperation_Insert] método.</span><span class="sxs-lookup"><span data-stu-id="1ae68-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="1ae68-152">A continuación, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] se denomina operación de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="1ae68-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

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
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="1ae68-153">todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="1ae68-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="1ae68-154">tooquery una tabla para todas las entidades de una partición, use un [TableQuery] [ dotnet_TableQuery] objeto.</span><span class="sxs-lookup"><span data-stu-id="1ae68-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="1ae68-155">Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="1ae68-156">Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="1ae68-157">Recuperación de un rango de entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="1ae68-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="1ae68-158">Si no desea tooquery todas las entidades de una partición, puede especificar un intervalo mediante la combinación de filtro de clave de partición de hello con un filtro de clave de fila.</span><span class="sxs-lookup"><span data-stu-id="1ae68-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="1ae68-159">Hello ejemplo de código siguiente utiliza dos tooget filtros todas las entidades de partición "Smith" donde hello fila clave (nombre) empieza por una letra antes 'E' alfabeto hello, a continuación, imprime los resultados de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="1ae68-160">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="1ae68-160">Retrieve a single entity</span></span>
<span data-ttu-id="1ae68-161">Puede escribir una consulta tooretrieve una entidad única, específica.</span><span class="sxs-lookup"><span data-stu-id="1ae68-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="1ae68-162">Hola siguiente de código usa [TableOperation] [ dotnet_TableOperation] cliente de hello toospecify "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="1ae68-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="1ae68-163">Este método devuelve una sola entidad en lugar de una colección y Hola devolvió el valor en [TableResult][dotnet_TableResult].[ Resultado] [ dotnet_TableResult_Result] es un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="1ae68-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="1ae68-164">Especificar claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una sola entidad de servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="1ae68-165">una entidad</span><span class="sxs-lookup"><span data-stu-id="1ae68-165">Replace an entity</span></span>
<span data-ttu-id="1ae68-166">tooupdate una entidad, recuperar del servicio de tabla de hello, modificar el objeto de entidad de hello y, a continuación, guardar los cambios de hello hacer copia de servicio de la tabla de toohello.</span><span class="sxs-lookup"><span data-stu-id="1ae68-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="1ae68-167">Hello código siguiente cambia número de teléfono de un cliente existente.</span><span class="sxs-lookup"><span data-stu-id="1ae68-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="1ae68-168">En lugar de llamar a [Insert][dotnet_TableOperation_Insert], este código utiliza [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="1ae68-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="1ae68-169">[Reemplace] [ dotnet_TableOperation_Replace] causas Hola toobe entidad reemplazado totalmente en el servidor de hello, a menos que la entidad de hello en servidor hello ha cambiado desde que se recuperó, en cuyo caso se producirá un error de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="1ae68-170">Este error es tooprevent la aplicación se ha sobrescrito accidentalmente un cambio realizado entre Hola recuperación y actualizar por otro componente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ae68-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="1ae68-171">Hello control correcto de este error es tooretrieve Hola entidad nuevo, realice los cambios (si todavía es válido) y, a continuación, realizar otra [reemplazar] [ dotnet_TableOperation_Replace] operación.</span><span class="sxs-lookup"><span data-stu-id="1ae68-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="1ae68-172">Hola siguiente sección le mostrará cómo toooverride este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="1ae68-172">hello next section will show you how toooverride this behavior.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="1ae68-173">Inserción o reemplazo de una entidad</span><span class="sxs-lookup"><span data-stu-id="1ae68-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="1ae68-174">[Reemplace] [ dotnet_TableOperation_Replace] operaciones generarán un error si la entidad de Hola se ha modificado desde que se recuperó del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="1ae68-175">Además, debe recuperar primero entidad Hola desde servidor hello en orden para hello [reemplazar] [ dotnet_TableOperation_Replace] toobe de operación correcta.</span><span class="sxs-lookup"><span data-stu-id="1ae68-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="1ae68-176">A veces, sin embargo, no sabe si entidad Hola existe en el servidor de Hola y valores actuales de hello almacenados en ella son irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="1ae68-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="1ae68-177">La actualización debe sobrescribir todos.</span><span class="sxs-lookup"><span data-stu-id="1ae68-177">Your update should overwrite them all.</span></span> <span data-ttu-id="1ae68-178">tooaccomplish, usaría un [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operación.</span><span class="sxs-lookup"><span data-stu-id="1ae68-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="1ae68-179">Esta operación inserta la entidad de hello si no existe, o lo reemplaza si lo hace, sin tener en cuenta cuando se realizó la última actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="1ae68-180">En el siguiente ejemplo de código de hello, una entidad customer para 'Fred Jones' se crea y se inserta en la tabla de hello 'usuarios'.</span><span class="sxs-lookup"><span data-stu-id="1ae68-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="1ae68-181">A continuación, usamos hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operación toosave una entidad con hello mismo (Jones) de clave de partición y fila de clave server de toohello (Fred), esta vez con un valor diferente para hello PhoneNumber propiedad.</span><span class="sxs-lookup"><span data-stu-id="1ae68-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="1ae68-182">Dado que se ha usado [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], se reemplazan todos los valores de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="1ae68-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="1ae68-183">Sin embargo, si una entidad 'Fred Jones' no se había ya existía en la tabla de hello, habría que ha insertado.</span><span class="sxs-lookup"><span data-stu-id="1ae68-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="1ae68-184">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="1ae68-184">Query a subset of entity properties</span></span>
<span data-ttu-id="1ae68-185">Una consulta de tabla puede recuperar solo unas pocas propiedades de una entidad en lugar de todas las propiedades de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="1ae68-186">Esta técnica, denominada proyección, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="1ae68-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="1ae68-187">consulta de Hello en el siguiente código de hello devuelve solo direcciones de correo electrónico de Hola de entidades de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="1ae68-188">Esto se consigue utilizando una consulta de [DynamicTableEntity][dotnet_DynamicTableEntity] y también [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="1ae68-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="1ae68-189">Puede aprender más acerca de la proyección en hello [entrada de blog Introducción Upsert y proyección de consultas][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="1ae68-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="1ae68-190">Proyección no es compatible con el emulador de almacenamiento de hello, este código se ejecuta sólo cuando se está utilizando una cuenta de servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="1ae68-191">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="1ae68-191">Delete an entity</span></span>
<span data-ttu-id="1ae68-192">Puede eliminar fácilmente una entidad después de que se han recuperado mediante el uso de hello mismo patrón que se muestra para la actualización de una entidad.</span><span class="sxs-lookup"><span data-stu-id="1ae68-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="1ae68-193">Hola siguiente código recupera y elimina una entidad customer.</span><span class="sxs-lookup"><span data-stu-id="1ae68-193">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="1ae68-194">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="1ae68-194">Delete a table</span></span>
<span data-ttu-id="1ae68-195">Por último, Hola ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1ae68-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="1ae68-196">Una tabla que se ha eliminado estará disponible toobe vuelve a crear durante un período de tiempo tras la eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae68-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="1ae68-197">Recuperación de entidades en páginas de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="1ae68-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="1ae68-198">Si está leyendo un gran número de entidades, y desea tooprocess/mostrar entidades como recuperarlos en lugar de esperar a todos los tooreturn, puede recuperar entidades mediante una consulta segmentada.</span><span class="sxs-lookup"><span data-stu-id="1ae68-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="1ae68-199">Este ejemplo muestra cómo tooreturn resultados en páginas mediante el patrón de hello asincrónicas Await para que la ejecución no se bloquea mientras se están esperando un gran conjunto de resultados tooreturn.</span><span class="sxs-lookup"><span data-stu-id="1ae68-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="1ae68-200">Para obtener más detalles sobre el uso de hello patrón Async y Await en. NET, consulte [programación asincrónica con Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ae68-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="1ae68-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ae68-201">Next steps</span></span>
<span data-ttu-id="1ae68-202">Ahora que conoce los fundamentos de hello del almacenamiento de tabla, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="1ae68-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="1ae68-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="1ae68-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="1ae68-204">Consulte más ejemplos de uso de Almacenamiento de tablas en [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="1ae68-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="1ae68-205">Ver la documentación de referencia de servicio de tabla de Hola para obtener información detallada acerca de las API disponibles:</span><span class="sxs-lookup"><span data-stu-id="1ae68-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="1ae68-206">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="1ae68-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="1ae68-207">Referencia de API de REST</span><span class="sxs-lookup"><span data-stu-id="1ae68-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="1ae68-208">Obtenga información acerca de cómo código de hello toosimplify escribir toowork con el almacenamiento de Azure mediante el uso de hello [SDK de WebJobs de Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1ae68-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="1ae68-209">Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae68-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="1ae68-210">[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore datos no estructurados.</span><span class="sxs-lookup"><span data-stu-id="1ae68-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="1ae68-211">[Conectar tooSQL base de datos mediante el uso de .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="1ae68-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
