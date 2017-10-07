---
title: aaaHow toouse almacenamiento de tablas de Java | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="97e96-103">¿Cómo toouse almacenamiento de tablas de Java</span><span class="sxs-lookup"><span data-stu-id="97e96-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="97e96-104">Información general</span><span class="sxs-lookup"><span data-stu-id="97e96-104">Overview</span></span>
<span data-ttu-id="97e96-105">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="97e96-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="97e96-106">ejemplos de Hello están escritos en Java y usar hello [almacenamiento de Azure SDK para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="97e96-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="97e96-107">Hello escenarios descritos se incluyen **crear**, **enumerar**, y **eliminar** tablas, así como **insertar**,  **consultar**, **modificar**, y **eliminar** entidades de una tabla.</span><span class="sxs-lookup"><span data-stu-id="97e96-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="97e96-108">Para obtener más información sobre tablas, vea hello [pasos siguientes](#Next-Steps) sección.</span><span class="sxs-lookup"><span data-stu-id="97e96-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="97e96-109">Nota: hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="97e96-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="97e96-110">Para obtener más información, vea hello [SDK de almacenamiento de Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="97e96-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="97e96-111">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="97e96-111">Create a Java application</span></span>
<span data-ttu-id="97e96-112">En esta guía utilizará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente o bien mediante código a través de un rol web o un rol de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="97e96-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="97e96-113">toodo por lo tanto, necesitará tooinstall Hola Java Development Kit (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="97e96-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="97e96-114">Una vez que lo ha hecho, necesitará tooverify que el sistema de desarrollo cumple los requisitos mínimos de Hola y dependencias que se enumeran en hello [almacenamiento de Azure SDK para Java] [ Azure Storage SDK for Java] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="97e96-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="97e96-115">Si su sistema cumple estos requisitos, puede seguir las instrucciones de Hola para descargar e instalar Hola bibliotecas de almacenamiento de Azure para Java en el sistema de ese repositorio.</span><span class="sxs-lookup"><span data-stu-id="97e96-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="97e96-116">Una vez haya completado estas tareas, será capaz de toocreate una aplicación Java que utiliza los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="97e96-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="97e96-117">Configurar el almacenamiento de tabla tooaccess de aplicación</span><span class="sxs-lookup"><span data-stu-id="97e96-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="97e96-118">Agregue Hola después de la parte superior de toohello de instrucciones de importación del archivo de Java de Hola donde desea tablas tooaccess las API de almacenamiento que toouse Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="97e96-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="97e96-119">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="97e96-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="97e96-120">Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="97e96-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="97e96-121">Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, con nombre de hello de la cuenta de almacenamiento y Hola clave de acceso principal para cuenta de almacenamiento Hola Hola [portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="97e96-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="97e96-122">Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="97e96-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="97e96-123">En una aplicación en ejecución dentro de un rol en Microsoft Azure, esta cadena puede almacenarse en el archivo de configuración del servicio de hello *ServiceConfiguration.cscfg*y puede tener acceso mediante una llamada a toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="97e96-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="97e96-124">Este es un ejemplo de obtención de la cadena de conexión de Hola desde una **configuración** elemento denominado *StorageConnectionString* en el archivo de configuración de servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="97e96-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="97e96-125">Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="97e96-126">Cómo crear una tabla</span><span class="sxs-lookup"><span data-stu-id="97e96-126">How to: Create a table</span></span>
<span data-ttu-id="97e96-127">Los objetos **CloudTableClient** le permiten obtener objetos de referencia para tablas y entidades.</span><span class="sxs-lookup"><span data-stu-id="97e96-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="97e96-128">Hello código siguiente se crea un **CloudTableClient** objeto y lo usa toocreate un nuevo **CloudTable** el objeto que representa una tabla denominada "personas".</span><span class="sxs-lookup"><span data-stu-id="97e96-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="97e96-129">(Nota: hay otras formas toocreate **CloudStorageAccount** objetos; para obtener más información, vea **CloudStorageAccount** en hello [referencia de SDK de cliente de almacenamiento de Azure].)</span><span class="sxs-lookup"><span data-stu-id="97e96-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="97e96-130">Cómo: mostrar hello tablas</span><span class="sxs-lookup"><span data-stu-id="97e96-130">How to: List hello tables</span></span>
<span data-ttu-id="97e96-131">una lista de tablas, llamada hello tooget **CloudTableClient.listTables()** método tooretrieve una lista de nombres de tabla iterable.</span><span class="sxs-lookup"><span data-stu-id="97e96-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="97e96-132">Cómo: agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="97e96-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="97e96-133">Las entidades asignan objetos tooJava con una clase personalizada que implemente **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="97e96-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="97e96-134">Para mayor comodidad, Hola **TableServiceEntity** la clase implementa **TableEntity** y propiedades de toomap de reflexión usa métodos establecedor y toogetter con el nombre de Hola propiedades.</span><span class="sxs-lookup"><span data-stu-id="97e96-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="97e96-135">tooadd una tabla de tooa de entidad, primero cree una clase que define las propiedades de saludo de la entidad.</span><span class="sxs-lookup"><span data-stu-id="97e96-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="97e96-136">Hello código siguiente define una clase de entidad que utiliza el nombre del cliente de hello como clave de fila de Hola y last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="97e96-137">Juntos, partición de una entidad y la clave de fila identifican entidad de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="97e96-138">Entidades con hello misma clave de partición se pueden consultar más rápido que aquellos con las claves de partición diferente.</span><span class="sxs-lookup"><span data-stu-id="97e96-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="97e96-139">Las operaciones de tabla que afectan a las entidades requieren un objeto **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="97e96-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="97e96-140">Este objeto define hello toobe de operación realizada en una entidad, que se puede ejecutar con un **CloudTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="97e96-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="97e96-141">Hello código siguiente crea una nueva instancia de hello **CustomerEntity** clase con algunos toobe de datos del cliente almacenado.</span><span class="sxs-lookup"><span data-stu-id="97e96-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="97e96-142">Hola de código siguiente llama **TableOperation.insertOrReplace** toocreate una **TableOperation** tooinsert una entidad del objeto en una tabla, y asocia Hola nuevos **CustomerEntity**con él.</span><span class="sxs-lookup"><span data-stu-id="97e96-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="97e96-143">Por último, llama a código de hello hello **ejecutar** método en hello **CloudTable** objeto Database, especificando hello nueva y la tabla de "personas" hello **TableOperation**, que, a continuación, envía un solicitar toohello almacenamiento servicio tooinsert Hola nueva entidad customer en la tabla de "personas" hello, o reemplazar entidades Hola si ya existe.</span><span class="sxs-lookup"><span data-stu-id="97e96-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="97e96-144">Cómo insertar un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="97e96-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="97e96-145">Puede insertar un lote de servicio de tabla toohello de entidades en una sola operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="97e96-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="97e96-146">Hello código siguiente se crea un **TableBatchOperation** objeto, a continuación, agrega tres tooit de operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="97e96-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="97e96-147">Cada operación de inserción se agrega al crear un nuevo objeto de entidad, establecer sus valores y, a continuación, llamar a hello **insertar** método en hello **TableBatchOperation** objeto entidad de hello tooassociate con un nuevo operación de inserción.</span><span class="sxs-lookup"><span data-stu-id="97e96-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="97e96-148">Hola, a continuación, llamadas de código **ejecutar** en hello **CloudTable** objeto Database, especificando la tabla de "personas" Hola y Hola **TableBatchOperation** objeto, que envía el lote de Hola de tabla servicio de almacenamiento de toohello de operaciones en una sola solicitud.</span><span class="sxs-lookup"><span data-stu-id="97e96-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="97e96-149">Algunos toonote cosas en operaciones por lotes:</span><span class="sxs-lookup"><span data-stu-id="97e96-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="97e96-150">Puede realizar una too100 insert, delete, merge, replace, insert o merge e insertar o reemplazar las operaciones en cualquier combinación de en un único lote.</span><span class="sxs-lookup"><span data-stu-id="97e96-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="97e96-151">Una operación por lotes puede tener una operación de recuperación, si es la única operación de hello en el lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="97e96-152">Todas las entidades de una operación por lotes solo deben tener Hola misma clave de partición.</span><span class="sxs-lookup"><span data-stu-id="97e96-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="97e96-153">Una operación por lotes es limitado tooa carga de datos de 4MB.</span><span class="sxs-lookup"><span data-stu-id="97e96-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="97e96-154">Cómo recuperar todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="97e96-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="97e96-155">tooquery una tabla para entidades de una partición, puede usar un **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="97e96-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="97e96-156">Llame a **TableQuery.from** toocreate una consulta en una tabla determinada que devuelve un tipo de resultado especificado.</span><span class="sxs-lookup"><span data-stu-id="97e96-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="97e96-157">Hello código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="97e96-158">**TableQuery.generateFilterCondition** es un método auxiliar toocreate filtros para las consultas.</span><span class="sxs-lookup"><span data-stu-id="97e96-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="97e96-159">Llame a **donde** en referencia de hello devuelta por hello **TableQuery.from** toohello consulta de método tooapply Hola filter.</span><span class="sxs-lookup"><span data-stu-id="97e96-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="97e96-160">Cuando se ejecuta Hola consulta con una llamada demasiado**ejecutar** en hello **CloudTable** de objeto, devuelve un **iterador** con hello **CustomerEntity**especificado el tipo de resultado.</span><span class="sxs-lookup"><span data-stu-id="97e96-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="97e96-161">A continuación, puede usar hello **iterador** devuelto en una para cada bucle tooconsume Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="97e96-162">Este código imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="97e96-163">Cómo recuperar un intervalo de entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="97e96-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="97e96-164">Si no desea tooquery todas las entidades de hello en una partición, puede especificar un intervalo mediante operadores de comparación en un filtro.</span><span class="sxs-lookup"><span data-stu-id="97e96-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="97e96-165">Hola después combina código dos filtros tooget todas las entidades de partición "Smith" en clave de fila de hello (nombre) comienza con una letra de too'E' alfabeto Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="97e96-166">A continuación, imprimen los resultados de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-166">Then it prints hello query results.</span></span> <span data-ttu-id="97e96-167">Si utiliza la tabla de hello entidades toohello agregada en el lote de hello insertar la sección de esta guía, solo dos entidades se devuelven en este momento (Ben y Denise Smith); Jeff Smith no se incluye.</span><span class="sxs-lookup"><span data-stu-id="97e96-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="97e96-168">Cómo recuperar una sola entidad</span><span class="sxs-lookup"><span data-stu-id="97e96-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="97e96-169">Puede escribir una consulta tooretrieve una entidad única, específica.</span><span class="sxs-lookup"><span data-stu-id="97e96-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="97e96-170">Hola siguiente código llama **TableOperation.retrieve** con partición clave y fila parámetros clave toospecify Hola cliente "Jeff Smith", en lugar de crear un **TableQuery** y el uso de hello toodo de filtros lo mismo.</span><span class="sxs-lookup"><span data-stu-id="97e96-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="97e96-171">Cuando se ejecuta, Hola recuperar la operación devuelve una sola entidad, en lugar de una colección.</span><span class="sxs-lookup"><span data-stu-id="97e96-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="97e96-172">Hola **getResultAsType** método convierte el tipo de destino de asignación de hello, toohello de resultado de hello un **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="97e96-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="97e96-173">Si este tipo no es compatible con el tipo de hello especificado para la consulta de hello, se producirá una excepción.</span><span class="sxs-lookup"><span data-stu-id="97e96-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="97e96-174">Se devuelve un valor nulo si no coincide exactamente la clave de fila y de partición de ninguna entidad.</span><span class="sxs-lookup"><span data-stu-id="97e96-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="97e96-175">Especificar claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una sola entidad de servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
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
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="97e96-176">Modificación de una entidad</span><span class="sxs-lookup"><span data-stu-id="97e96-176">How to: Modify an entity</span></span>
<span data-ttu-id="97e96-177">toomodify una entidad, recuperar del servicio de tabla de hello, hacer cambios toohello entidad objeto y guardar los cambios de hello toohello back-servicio de tabla con una operación de reemplazo o de mezcla.</span><span class="sxs-lookup"><span data-stu-id="97e96-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="97e96-178">Hello código siguiente cambia número de teléfono de un cliente existente.</span><span class="sxs-lookup"><span data-stu-id="97e96-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="97e96-179">En lugar de llamar **TableOperation.insert** como hicimos tooinsert, este código llama **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="97e96-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="97e96-180">Hola **CloudTable.execute** llamadas de método de servicio de la tabla de Hola y se reemplaza la entidad de hello, a menos que otra aplicación cambiarla en el tiempo de Hola desde esta aplicación recuperó.</span><span class="sxs-lookup"><span data-stu-id="97e96-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="97e96-181">Cuando esto ocurre, se produce una excepción y entidad Hola se debe recuperar, modificar y guardar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="97e96-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="97e96-182">Este patrón de reintento de simultaneidad optimista es común en un sistema de almacenamiento distribuido.</span><span class="sxs-lookup"><span data-stu-id="97e96-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="97e96-183">Cómo consultar un subconjunto de las propiedades de entidad</span><span class="sxs-lookup"><span data-stu-id="97e96-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="97e96-184">Una tabla de tooa de consulta puede recuperar solo unas pocas propiedades de una entidad.</span><span class="sxs-lookup"><span data-stu-id="97e96-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="97e96-185">Esta técnica, denominada proyección, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="97e96-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="97e96-186">la consulta en el siguiente código de hello Hello utiliza hello **seleccione** método tooreturn solo Hola direcciones de correo electrónico las entidades de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="97e96-187">resultados Hello se proyectan una en una colección de **cadena** con ayuda de Hola de un **EntityResolver**, que does Hola conversión de tipos en entidades de hello devuelta por el servidor hello.</span><span class="sxs-lookup"><span data-stu-id="97e96-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="97e96-188">Puede obtener más información sobre la proyección en [Tablas de Azure: Introducción de Upsert y proyección de consultas][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="97e96-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="97e96-189">Tenga en cuenta que no se admite proyección en el emulador de almacenamiento local de hello, por lo que este código se ejecuta solo cuando utiliza una cuenta de servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="97e96-190">Inserción o reemplazo de una entidad</span><span class="sxs-lookup"><span data-stu-id="97e96-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="97e96-191">A menudo desea tooadd una tabla de tooa de entidad sin saber si ya existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="97e96-192">Una operación insert o replace permite toomake una única solicitud que se insertará la entidad de Hola si no existe o no Reemplace Hola uno existente si existe.</span><span class="sxs-lookup"><span data-stu-id="97e96-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="97e96-193">Basándose en los ejemplos anteriores, hello código siguiente inserta o reemplaza la entidad de Hola para "Walter arpa".</span><span class="sxs-lookup"><span data-stu-id="97e96-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="97e96-194">Después de crear una nueva entidad, este código llama hello **TableOperation.insertOrReplace** método.</span><span class="sxs-lookup"><span data-stu-id="97e96-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="97e96-195">A continuación, llama a este código **ejecutar** en hello **CloudTable** objeto con insert hello y tabla de Hola o reemplazar la operación de tabla como parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="97e96-196">tooupdate únicamente una parte de una entidad, hello **TableOperation.insertOrMerge** método se puede utilizar en su lugar.</span><span class="sxs-lookup"><span data-stu-id="97e96-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="97e96-197">Tenga en cuenta que insertar o reemplazar no se admite en el emulador de almacenamiento local de hello, por lo que este código se ejecuta solo cuando utiliza una cuenta de servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="97e96-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="97e96-198">Puede obtener más información sobre la inserción o reemplazo y la inserción o fusión en [Tablas de Azure: Introducción a Upsert y proyección de consultas][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="97e96-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="97e96-199">Cómo eliminar una entidad</span><span class="sxs-lookup"><span data-stu-id="97e96-199">How to: Delete an entity</span></span>
<span data-ttu-id="97e96-200">Puede eliminar fácilmente una entidad después de que la haya recuperado.</span><span class="sxs-lookup"><span data-stu-id="97e96-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="97e96-201">Una vez que se recupera la entidad de hello, llame a **TableOperation.delete** con hello entidad toodelete.</span><span class="sxs-lookup"><span data-stu-id="97e96-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="97e96-202">A continuación, llame a **ejecutar** en hello **CloudTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="97e96-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="97e96-203">Hola siguiente código recupera y elimina una entidad customer.</span><span class="sxs-lookup"><span data-stu-id="97e96-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="97e96-204">Cómo eliminar una tabla</span><span class="sxs-lookup"><span data-stu-id="97e96-204">How to: Delete a table</span></span>
<span data-ttu-id="97e96-205">Por último, hello siguiente código elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97e96-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="97e96-206">Una tabla que se ha eliminado estará disponible toobe vuelve a crear durante un período de tiempo tras la eliminación de hello, normalmente menos de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="97e96-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="97e96-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97e96-207">Next steps</span></span>

* <span data-ttu-id="97e96-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="97e96-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="97e96-209">[SDK de Azure Storage para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="97e96-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="97e96-210">[referencia de SDK de cliente de almacenamiento de Azure][referencia de SDK de cliente de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="97e96-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="97e96-211">[API de REST de Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="97e96-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="97e96-212">[Blog del equipo de Azure Storage][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="97e96-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="97e96-213">Para obtener más información, vea también hello [Centro para desarrolladores de Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="97e96-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referencia de SDK de cliente de almacenamiento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
