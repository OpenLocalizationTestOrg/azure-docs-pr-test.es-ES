---
title: Uso de Table Storage en Java | Microsoft Docs
description: "Almacene datos estructurados en la nube con el Almacenamiento de tablas de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7f92b1e14a514e9eda39f7ca94f63fc761dfdf41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="256c1-103">Uso del almacenamiento de tablas de Java</span><span class="sxs-lookup"><span data-stu-id="256c1-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="256c1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="256c1-104">Overview</span></span>
<span data-ttu-id="256c1-105">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento de tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="256c1-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="256c1-106">Los ejemplos están escritos en Java y utilizan el [SDK de Azure Storage para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="256c1-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="256c1-107">Entre los escenarios descritos se incluyen **crear**, **enumerar** y **eliminar** tablas, así como **insertar**, **consultar**, **modificar** y **eliminar** entidades de una tabla.</span><span class="sxs-lookup"><span data-stu-id="256c1-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="256c1-108">Para obtener más información acerca de las tablas, consulte la sección [Pasos siguientes](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="256c1-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="256c1-109">Nota: hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="256c1-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="256c1-110">Para obtener más información, vea el [SDK de Azure Storage para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="256c1-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="256c1-111">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="256c1-111">Create a Java application</span></span>
<span data-ttu-id="256c1-112">En esta guía utilizará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente o bien mediante código a través de un rol web o un rol de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="256c1-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="256c1-113">Para ello, deberá instalar el Kit de desarrollo de Java (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="256c1-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="256c1-114">Después, deberá verificar que su sistema de desarrollo satisface los requisitos mínimos y las dependencias que se indican en el repositorio del [SDK de Azure Storage para Java][Azure Storage SDK for Java] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="256c1-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="256c1-115">Si su sistema cumple esos requisitos, puede seguir las instrucciones para descargar e instalar las bibliotecas de almacenamiento de Azure para Java en su sistema desde ese repositorio.</span><span class="sxs-lookup"><span data-stu-id="256c1-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="256c1-116">Cuando haya completado esas tareas, podrá crear una aplicación Java que use los ejemplos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="256c1-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="256c1-117">Configuración de la aplicación para acceder al almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="256c1-117">Configure your application to access table storage</span></span>
<span data-ttu-id="256c1-118">Agregue las siguientes instrucciones de importación en la parte superior del archivo Java en el que desea utilizar las API de almacenamiento de Microsoft Azure para obtener acceso a las tablas:</span><span class="sxs-lookup"><span data-stu-id="256c1-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="256c1-119">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="256c1-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="256c1-120">Un cliente de almacenamiento de Azure utiliza una cadena de conexión de almacenamiento para almacenar extremos y credenciales con el fin de obtener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="256c1-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="256c1-121">Al ejecutarse en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento en el siguiente formato, usando el nombre de su cuenta de almacenamiento y la clave de acceso principal de la cuenta de almacenamiento que se muestra en [Azure Portal](https://portal.azure.com) para los valores *AccountName* y *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="256c1-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="256c1-122">En este ejemplo se muestra cómo puede declarar un campo estático para mantener la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="256c1-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="256c1-123">En una aplicación que se esté ejecutando en un rol de Microsoft Azure, esta cadena se puede almacenar en el archivo de configuración de servicio, *ServiceConfiguration.cscfg*, y se puede obtener acceso a él con una llamada al método **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="256c1-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="256c1-124">A continuación se muestra un ejemplo de cómo obtener la cadena de conexión desde un elemento de **configuración** denominado *StorageConnectionString* en el archivo de configuración del servicio:</span><span class="sxs-lookup"><span data-stu-id="256c1-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="256c1-125">En los ejemplos siguientes se supone que usó uno de estos dos métodos para obtener la cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="256c1-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="256c1-126">Cómo crear una tabla</span><span class="sxs-lookup"><span data-stu-id="256c1-126">How to: Create a table</span></span>
<span data-ttu-id="256c1-127">Los objetos **CloudTableClient** le permiten obtener objetos de referencia para tablas y entidades.</span><span class="sxs-lookup"><span data-stu-id="256c1-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="256c1-128">El siguiente código crea un objeto **CloudTableClient** y lo usa para crear un nuevo objeto **CloudTable** que representa una tabla llamada "people".</span><span class="sxs-lookup"><span data-stu-id="256c1-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="256c1-129">(Nota: Hay otras maneras de crear objetos **CloudStorageAccount**. Para más información, consulte **CloudStorageAccount** en la [Referencia del SDK de cliente de Azure Storage]).</span><span class="sxs-lookup"><span data-stu-id="256c1-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="256c1-130">Enumeración de las tablas</span><span class="sxs-lookup"><span data-stu-id="256c1-130">How to: List the tables</span></span>
<span data-ttu-id="256c1-131">Para obtener una lista de las tablas, llame al método **CloudTableClient.listTables()** para recuperar una lista que se puede iterar de nombres de tablas.</span><span class="sxs-lookup"><span data-stu-id="256c1-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="256c1-132">Cómo agregar una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="256c1-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="256c1-133">Las entidades se asignan a objetos de Java utilizando una clase personalizada que implementa **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="256c1-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="256c1-134">Para mayor comodidad, la clase **TableServiceEntity** implementa **TableEntity** y usa la reflexión para asignar propiedades a los métodos de captador y establecedor indicados para las propiedades.</span><span class="sxs-lookup"><span data-stu-id="256c1-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="256c1-135">Para agregar una entidad a una tabla, cree primero una clase que defina las propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="256c1-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="256c1-136">El código siguiente define una clase de entidad que utiliza el nombre de pila del cliente como clave de fila y el apellido como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="256c1-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="256c1-137">En conjunto, la clave de partición y la clave de fila de una entidad la identifican inequívocamente en la tabla.</span><span class="sxs-lookup"><span data-stu-id="256c1-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="256c1-138">Puede realizarse una consulta en las entidades con la misma clave de partición de manera más rápida que en aquellas que tienen claves de partición distintas.</span><span class="sxs-lookup"><span data-stu-id="256c1-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="256c1-139">Las operaciones de tabla que afectan a las entidades requieren un objeto **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="256c1-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="256c1-140">Este objeto define la operación que va a realizarse en una entidad, que puede ejecutarse con un objeto **CloudTable** .</span><span class="sxs-lookup"><span data-stu-id="256c1-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="256c1-141">El código siguiente crea una instancia nueva de la clase **CustomerEntity** con algunos datos de clientes que se van a almacenar.</span><span class="sxs-lookup"><span data-stu-id="256c1-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="256c1-142">El código siguiente llama a **TableOperation.insertOrReplace** para crear un objeto **TableOperation** a fin de insertar una entidad en una tabla y asocia el objeto **CustomerEntity** a ella.</span><span class="sxs-lookup"><span data-stu-id="256c1-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="256c1-143">Por último, el código llama al método **execute** en **CloudTable**, especificando la tabla "people" y el nuevo objeto **TableOperation**, que posteriormente envía una solicitud al servicio de almacenamiento para insertar la nueva entidad de cliente en la tabla "people" o sustituir la entidad si ya existe.</span><span class="sxs-lookup"><span data-stu-id="256c1-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="256c1-144">Cómo insertar un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="256c1-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="256c1-145">Puede insertar un lote de entidades en el servicio Tabla mediante una operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="256c1-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="256c1-146">El siguiente código crea un objeto **TableBatchOperation** y, a continuación, le agrega tres operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="256c1-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="256c1-147">Cada operación de inserción se agrega mediante la creación de un nuevo objeto de entidad, se configuran sus valores y, a continuación, se llama al método **insert** en el objeto **TableBatchOperation** para asociar la entidad a una nueva operación de inserción.</span><span class="sxs-lookup"><span data-stu-id="256c1-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="256c1-148">A continuación, el código llama a **execute** en el objeto **CloudTable**, especificando la tabla "people" y el objeto **TableBatchOperation**, que envía el lote de operaciones de tabla al servicio de almacenamiento en una única solicitud.</span><span class="sxs-lookup"><span data-stu-id="256c1-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="256c1-149">Algunos aspectos que cabe tener en cuenta acerca de las operaciones por lotes:</span><span class="sxs-lookup"><span data-stu-id="256c1-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="256c1-150">Puede ejecutar cualquier combinación de 100 operaciones de inserción, eliminación, combinación, reemplazo, inserción o combinación e inserción o reemplazo en un único lote.</span><span class="sxs-lookup"><span data-stu-id="256c1-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="256c1-151">Una operación por lotes puede tener una operación de recuperación, si es que es la única operación del lote.</span><span class="sxs-lookup"><span data-stu-id="256c1-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="256c1-152">Todas las entidades de la misma operación por lotes deben compartir la misma clave de partición.</span><span class="sxs-lookup"><span data-stu-id="256c1-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="256c1-153">Una operación por lotes se limita a una carga de datos de 4 MB.</span><span class="sxs-lookup"><span data-stu-id="256c1-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="256c1-154">Cómo recuperar todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="256c1-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="256c1-155">Para consultar una tabla a fin de obtener las entidades de una partición, use un objeto **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="256c1-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="256c1-156">Llame a **TableQuery.from** para crear una consulta en una tabla concreta que devuelva un tipo de resultado específico.</span><span class="sxs-lookup"><span data-stu-id="256c1-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="256c1-157">El código siguiente especifica un filtro para las entidades en las que "Smith" es la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="256c1-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="256c1-158">**TableQuery.generateFilterCondition** es un método auxiliar para crear filtros para las consultas.</span><span class="sxs-lookup"><span data-stu-id="256c1-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="256c1-159">Llame a **where** en la referencia devuelta por el método **TableQuery.from** para aplicar el filtro a la consulta.</span><span class="sxs-lookup"><span data-stu-id="256c1-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="256c1-160">Si la consulta se ejecuta con una llamada a **execute** en el objeto **CloudTable**, devuelve un **iterador** con el tipo de resultado **CustomerEntity** especificado.</span><span class="sxs-lookup"><span data-stu-id="256c1-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="256c1-161">A continuación, puede usar el **iterador** devuelto para cada bucle para consumir los resultados.</span><span class="sxs-lookup"><span data-stu-id="256c1-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="256c1-162">En este código, los campos de cada entidad se imprimen en la consola, como parte de los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="256c1-162">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="256c1-163">Cómo recuperar un intervalo de entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="256c1-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="256c1-164">Si no quiere consultar todas las entidades de una partición, puede especificar un rango mediante el uso de operadores de comparación en un filtro.</span><span class="sxs-lookup"><span data-stu-id="256c1-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="256c1-165">El código siguiente combina dos filtros para obtener todas las entidades de la partición "Smith" en las que la clave de fila (nombre de pila) empieza por una letra hasta "E" en el alfabeto.</span><span class="sxs-lookup"><span data-stu-id="256c1-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="256c1-166">A continuación, imprime los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="256c1-166">Then it prints the query results.</span></span> <span data-ttu-id="256c1-167">Si usa las entidades agregadas a la tabla en la sección de inserción por lotes de esta guía, solo se devuelven dos entidades en este momento (Ben y Denise Smith); Jeff Smith no se incluye.</span><span class="sxs-lookup"><span data-stu-id="256c1-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="256c1-168">Cómo recuperar una sola entidad</span><span class="sxs-lookup"><span data-stu-id="256c1-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="256c1-169">Puede enviar una consulta para recuperar una sola entidad concreta.</span><span class="sxs-lookup"><span data-stu-id="256c1-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="256c1-170">El código siguiente llama a **TableOperation.retrieve** con los parámetros de clave de partición y clave de fila para especificar el cliente "Jeff Smith", en lugar de crear un elemento **TableQuery** y usar filtros para realizar la misma operación.</span><span class="sxs-lookup"><span data-stu-id="256c1-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="256c1-171">Cuando se ejecuta, la operación de recuperación devuelve solo una entidad, en lugar de una colección de entidades.</span><span class="sxs-lookup"><span data-stu-id="256c1-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="256c1-172">El método **getResultAsType** convierte el resultado en el tipo de objetivo de asignación, un objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="256c1-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="256c1-173">Si este tipo no es compatible con el tipo especificado para la consulta, se mostrará una excepción.</span><span class="sxs-lookup"><span data-stu-id="256c1-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="256c1-174">Se devuelve un valor nulo si no coincide exactamente la clave de fila y de partición de ninguna entidad.</span><span class="sxs-lookup"><span data-stu-id="256c1-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="256c1-175">La forma más rápida de recuperar una sola entidad del servicio Tabla es especificar claves tanto de partición como de fila en las consultas.</span><span class="sxs-lookup"><span data-stu-id="256c1-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="256c1-176">Modificación de una entidad</span><span class="sxs-lookup"><span data-stu-id="256c1-176">How to: Modify an entity</span></span>
<span data-ttu-id="256c1-177">Para modificar una entidad, recupérela del servicio Tabla, realice los cambios en el objeto de entidad y vuelva a guardar los cambios en dicho servicio con una operación de reemplazo o combinación.</span><span class="sxs-lookup"><span data-stu-id="256c1-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="256c1-178">El código siguiente cambia el número de teléfono de un cliente.</span><span class="sxs-lookup"><span data-stu-id="256c1-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="256c1-179">En lugar de llamar a **TableOperation.insert** como hicimos para la inserción, este código llama a **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="256c1-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="256c1-180">El método **CloudTable.execute** llama al servicio Tabla y la entidad se reemplaza, a no ser que otra aplicación la haya modificado desde que la aplicación la recuperó.</span><span class="sxs-lookup"><span data-stu-id="256c1-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="256c1-181">Cuando se produce esa situación, se muestra una excepción y la entidad debe recuperarse, modificarse y guardarse de nuevo.</span><span class="sxs-lookup"><span data-stu-id="256c1-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="256c1-182">Este patrón de reintento de simultaneidad optimista es común en un sistema de almacenamiento distribuido.</span><span class="sxs-lookup"><span data-stu-id="256c1-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="256c1-183">Cómo consultar un subconjunto de las propiedades de entidad</span><span class="sxs-lookup"><span data-stu-id="256c1-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="256c1-184">Una consulta de tabla puede recuperar solo algunas propiedades de una entidad.</span><span class="sxs-lookup"><span data-stu-id="256c1-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="256c1-185">Esta técnica, denominada proyección, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="256c1-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="256c1-186">La consulta del código siguiente usa el método **select** para devolver solo las direcciones de correo electrónico de las entidades de la tabla.</span><span class="sxs-lookup"><span data-stu-id="256c1-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="256c1-187">Los resultados se proyectan en una colección de propiedades **String** con la ayuda de un objeto **EntityResolver**, que hace la conversión del tipo de entidades que el servidor devuelve.</span><span class="sxs-lookup"><span data-stu-id="256c1-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="256c1-188">Puede obtener más información sobre la proyección en [Tablas de Azure: Introducción de Upsert y proyección de consultas][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="256c1-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="256c1-189">Tenga en cuenta que la proyección no es compatible con el emulador de almacenamiento local, por lo que este código solo se ejecuta cuando se utiliza una cuenta del servicio Tabla.</span><span class="sxs-lookup"><span data-stu-id="256c1-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="256c1-190">Inserción o reemplazo de una entidad</span><span class="sxs-lookup"><span data-stu-id="256c1-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="256c1-191">En ocasiones, es posible que desee agregar una entidad a una tabla sin saber si ya existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="256c1-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="256c1-192">Una operación de inserción o reemplazo le permite realizar una consulta única que insertará la entidad si no existe o que reemplazará la existente si la hubiera.</span><span class="sxs-lookup"><span data-stu-id="256c1-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="256c1-193">Según los ejemplos anteriores, el siguiente código inserta o reemplaza la entidad de "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="256c1-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="256c1-194">Después de crear una nueva entidad, este código llama al método **TableOperation.insertOrReplace** .</span><span class="sxs-lookup"><span data-stu-id="256c1-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="256c1-195">A continuación, este código llama a **execute** en el objeto **CloudTable** con la tabla y las operaciones de inserción o reemplazo de tabla como parámetros.</span><span class="sxs-lookup"><span data-stu-id="256c1-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="256c1-196">Para actualizar solo parte de una entidad, en su lugar, se puede usar el método **TableOperation.insertOrMerge** .</span><span class="sxs-lookup"><span data-stu-id="256c1-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="256c1-197">Tenga en cuenta que la inserción o el reemplazo no son compatibles con el emulador de almacenamiento local, por lo que este código solo se ejecuta cuando se utiliza una cuenta del servicio Tabla.</span><span class="sxs-lookup"><span data-stu-id="256c1-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="256c1-198">Puede obtener más información sobre la inserción o reemplazo y la inserción o fusión en [Tablas de Azure: Introducción a Upsert y proyección de consultas][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="256c1-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="256c1-199">Cómo eliminar una entidad</span><span class="sxs-lookup"><span data-stu-id="256c1-199">How to: Delete an entity</span></span>
<span data-ttu-id="256c1-200">Puede eliminar fácilmente una entidad después de que la haya recuperado.</span><span class="sxs-lookup"><span data-stu-id="256c1-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="256c1-201">Cuando se recupere la entidad, llame a **TableOperation.delete** con la entidad que se eliminará.</span><span class="sxs-lookup"><span data-stu-id="256c1-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="256c1-202">A continuación, llame a **execute** en el objeto **CloudTable**.</span><span class="sxs-lookup"><span data-stu-id="256c1-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="256c1-203">El código siguiente recupera y elimina una entidad de cliente.</span><span class="sxs-lookup"><span data-stu-id="256c1-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="256c1-204">Cómo eliminar una tabla</span><span class="sxs-lookup"><span data-stu-id="256c1-204">How to: Delete a table</span></span>
<span data-ttu-id="256c1-205">Finalmente, el código siguiente elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="256c1-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="256c1-206">Las tablas eliminadas no podrán volver a crearse durante un tiempo tras la eliminación, que normalmente suele ser de menos de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="256c1-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="256c1-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="256c1-207">Next steps</span></span>

* <span data-ttu-id="256c1-208">El [Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente y gratuita de Microsoft que permite trabajar visualmente con los datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="256c1-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="256c1-209">[SDK de Azure Storage para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="256c1-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="256c1-210">[Referencia del SDK de cliente de Azure Storage][Referencia del SDK de cliente de Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="256c1-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="256c1-211">[API de REST de Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="256c1-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="256c1-212">[Blog del equipo de Azure Storage][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="256c1-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="256c1-213">Para más información, visite [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="256c1-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Referencia del SDK de cliente de Azure Storage]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
