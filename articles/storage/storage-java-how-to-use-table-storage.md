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
# <a name="how-toouse-table-storage-from-java"></a>¿Cómo toouse almacenamiento de tablas de Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio de almacenamiento de tabla de Azure. ejemplos de Hello están escritos en Java y usar hello [almacenamiento de Azure SDK para Java][Azure Storage SDK for Java]. Hello escenarios descritos se incluyen **crear**, **enumerar**, y **eliminar** tablas, así como **insertar**,  **consultar**, **modificar**, y **eliminar** entidades de una tabla. Para obtener más información sobre tablas, vea hello [pasos siguientes](#Next-Steps) sección.

Nota: hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android. Para obtener más información, vea hello [SDK de almacenamiento de Azure para Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Creación de una aplicación Java
En esta guía utilizará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente o bien mediante código a través de un rol web o un rol de trabajo de Azure.

toodo por lo tanto, necesitará tooinstall Hola Java Development Kit (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure. Una vez que lo ha hecho, necesitará tooverify que el sistema de desarrollo cumple los requisitos mínimos de Hola y dependencias que se enumeran en hello [almacenamiento de Azure SDK para Java] [ Azure Storage SDK for Java] repositorio en GitHub. Si su sistema cumple estos requisitos, puede seguir las instrucciones de Hola para descargar e instalar Hola bibliotecas de almacenamiento de Azure para Java en el sistema de ese repositorio. Una vez haya completado estas tareas, será capaz de toocreate una aplicación Java que utiliza los ejemplos de hello en este artículo.

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurar el almacenamiento de tabla tooaccess de aplicación
Agregue Hola después de la parte superior de toohello de instrucciones de importación del archivo de Java de Hola donde desea tablas tooaccess las API de almacenamiento que toouse Microsoft Azure:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de Almacenamiento de Azure
Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos. Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, con nombre de hello de la cuenta de almacenamiento y Hola clave de acceso principal para cuenta de almacenamiento Hola Hola [portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores. Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

En una aplicación en ejecución dentro de un rol en Microsoft Azure, esta cadena puede almacenarse en el archivo de configuración del servicio de hello *ServiceConfiguration.cscfg*y puede tener acceso mediante una llamada a toohello  **RoleEnvironment.getConfigurationSettings** método. Este es un ejemplo de obtención de la cadena de conexión de Hola desde una **configuración** elemento denominado *StorageConnectionString* en el archivo de configuración de servicio de hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.

## <a name="how-to-create-a-table"></a>Cómo crear una tabla
Los objetos **CloudTableClient** le permiten obtener objetos de referencia para tablas y entidades. Hello código siguiente se crea un **CloudTableClient** objeto y lo usa toocreate un nuevo **CloudTable** el objeto que representa una tabla denominada "personas". (Nota: hay otras formas toocreate **CloudStorageAccount** objetos; para obtener más información, vea **CloudStorageAccount** en hello [referencia de SDK de cliente de almacenamiento de Azure].)

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

## <a name="how-to-list-hello-tables"></a>Cómo: mostrar hello tablas
una lista de tablas, llamada hello tooget **CloudTableClient.listTables()** método tooretrieve una lista de nombres de tabla iterable.

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

## <a name="how-to-add-an-entity-tooa-table"></a>Cómo: agregar una tabla de tooa de entidad
Las entidades asignan objetos tooJava con una clase personalizada que implemente **TableEntity**. Para mayor comodidad, Hola **TableServiceEntity** la clase implementa **TableEntity** y propiedades de toomap de reflexión usa métodos establecedor y toogetter con el nombre de Hola propiedades. tooadd una tabla de tooa de entidad, primero cree una clase que define las propiedades de saludo de la entidad. Hello código siguiente define una clase de entidad que utiliza el nombre del cliente de hello como clave de fila de Hola y last name como clave de partición de Hola. Juntos, partición de una entidad y la clave de fila identifican entidad de hello en la tabla de Hola. Entidades con hello misma clave de partición se pueden consultar más rápido que aquellos con las claves de partición diferente.

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

Las operaciones de tabla que afectan a las entidades requieren un objeto **TableOperation** . Este objeto define hello toobe de operación realizada en una entidad, que se puede ejecutar con un **CloudTable** objeto. Hello código siguiente crea una nueva instancia de hello **CustomerEntity** clase con algunos toobe de datos del cliente almacenado. Hola de código siguiente llama **TableOperation.insertOrReplace** toocreate una **TableOperation** tooinsert una entidad del objeto en una tabla, y asocia Hola nuevos **CustomerEntity**con él. Por último, llama a código de hello hello **ejecutar** método en hello **CloudTable** objeto Database, especificando hello nueva y la tabla de "personas" hello **TableOperation**, que, a continuación, envía un solicitar toohello almacenamiento servicio tooinsert Hola nueva entidad customer en la tabla de "personas" hello, o reemplazar entidades Hola si ya existe.

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

## <a name="how-to-insert-a-batch-of-entities"></a>Cómo insertar un lote de entidades
Puede insertar un lote de servicio de tabla toohello de entidades en una sola operación de escritura. Hello código siguiente se crea un **TableBatchOperation** objeto, a continuación, agrega tres tooit de operaciones de inserción. Cada operación de inserción se agrega al crear un nuevo objeto de entidad, establecer sus valores y, a continuación, llamar a hello **insertar** método en hello **TableBatchOperation** objeto entidad de hello tooassociate con un nuevo operación de inserción. Hola, a continuación, llamadas de código **ejecutar** en hello **CloudTable** objeto Database, especificando la tabla de "personas" Hola y Hola **TableBatchOperation** objeto, que envía el lote de Hola de tabla servicio de almacenamiento de toohello de operaciones en una sola solicitud.

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

Algunos toonote cosas en operaciones por lotes:

* Puede realizar una too100 insert, delete, merge, replace, insert o merge e insertar o reemplazar las operaciones en cualquier combinación de en un único lote.
* Una operación por lotes puede tener una operación de recuperación, si es la única operación de hello en el lote de Hola.
* Todas las entidades de una operación por lotes solo deben tener Hola misma clave de partición.
* Una operación por lotes es limitado tooa carga de datos de 4MB.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Cómo recuperar todas las entidades de una partición
tooquery una tabla para entidades de una partición, puede usar un **TableQuery**. Llame a **TableQuery.from** toocreate una consulta en una tabla determinada que devuelve un tipo de resultado especificado. Hello código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola. **TableQuery.generateFilterCondition** es un método auxiliar toocreate filtros para las consultas. Llame a **donde** en referencia de hello devuelta por hello **TableQuery.from** toohello consulta de método tooapply Hola filter. Cuando se ejecuta Hola consulta con una llamada demasiado**ejecutar** en hello **CloudTable** de objeto, devuelve un **iterador** con hello **CustomerEntity**especificado el tipo de resultado. A continuación, puede usar hello **iterador** devuelto en una para cada bucle tooconsume Hola. Este código imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Cómo recuperar un intervalo de entidades de una partición
Si no desea tooquery todas las entidades de hello en una partición, puede especificar un intervalo mediante operadores de comparación en un filtro. Hola después combina código dos filtros tooget todas las entidades de partición "Smith" en clave de fila de hello (nombre) comienza con una letra de too'E' alfabeto Hola. A continuación, imprimen los resultados de la consulta de Hola. Si utiliza la tabla de hello entidades toohello agregada en el lote de hello insertar la sección de esta guía, solo dos entidades se devuelven en este momento (Ben y Denise Smith); Jeff Smith no se incluye.

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

## <a name="how-to-retrieve-a-single-entity"></a>Cómo recuperar una sola entidad
Puede escribir una consulta tooretrieve una entidad única, específica. Hola siguiente código llama **TableOperation.retrieve** con partición clave y fila parámetros clave toospecify Hola cliente "Jeff Smith", en lugar de crear un **TableQuery** y el uso de hello toodo de filtros lo mismo. Cuando se ejecuta, Hola recuperar la operación devuelve una sola entidad, en lugar de una colección. Hola **getResultAsType** método convierte el tipo de destino de asignación de hello, toohello de resultado de hello un **CustomerEntity** objeto. Si este tipo no es compatible con el tipo de hello especificado para la consulta de hello, se producirá una excepción. Se devuelve un valor nulo si no coincide exactamente la clave de fila y de partición de ninguna entidad. Especificar claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una sola entidad de servicio de la tabla de Hola.

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

## <a name="how-to-modify-an-entity"></a>Modificación de una entidad
toomodify una entidad, recuperar del servicio de tabla de hello, hacer cambios toohello entidad objeto y guardar los cambios de hello toohello back-servicio de tabla con una operación de reemplazo o de mezcla. Hello código siguiente cambia número de teléfono de un cliente existente. En lugar de llamar **TableOperation.insert** como hicimos tooinsert, este código llama **TableOperation.replace**. Hola **CloudTable.execute** llamadas de método de servicio de la tabla de Hola y se reemplaza la entidad de hello, a menos que otra aplicación cambiarla en el tiempo de Hola desde esta aplicación recuperó. Cuando esto ocurre, se produce una excepción y entidad Hola se debe recuperar, modificar y guardar de nuevo. Este patrón de reintento de simultaneidad optimista es común en un sistema de almacenamiento distribuido.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>Cómo consultar un subconjunto de las propiedades de entidad
Una tabla de tooa de consulta puede recuperar solo unas pocas propiedades de una entidad. Esta técnica, denominada proyección, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño. la consulta en el siguiente código de hello Hello utiliza hello **seleccione** método tooreturn solo Hola direcciones de correo electrónico las entidades de tabla de Hola. resultados Hello se proyectan una en una colección de **cadena** con ayuda de Hola de un **EntityResolver**, que does Hola conversión de tipos en entidades de hello devuelta por el servidor hello. Puede obtener más información sobre la proyección en [Tablas de Azure: Introducción de Upsert y proyección de consultas][Azure Tables: Introducing Upsert and Query Projection]. Tenga en cuenta que no se admite proyección en el emulador de almacenamiento local de hello, por lo que este código se ejecuta solo cuando utiliza una cuenta de servicio de la tabla de Hola.

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

## <a name="how-to-insert-or-replace-an-entity"></a>Inserción o reemplazo de una entidad
A menudo desea tooadd una tabla de tooa de entidad sin saber si ya existe en la tabla de Hola. Una operación insert o replace permite toomake una única solicitud que se insertará la entidad de Hola si no existe o no Reemplace Hola uno existente si existe. Basándose en los ejemplos anteriores, hello código siguiente inserta o reemplaza la entidad de Hola para "Walter arpa". Después de crear una nueva entidad, este código llama hello **TableOperation.insertOrReplace** método. A continuación, llama a este código **ejecutar** en hello **CloudTable** objeto con insert hello y tabla de Hola o reemplazar la operación de tabla como parámetros de Hola. tooupdate únicamente una parte de una entidad, hello **TableOperation.insertOrMerge** método se puede utilizar en su lugar. Tenga en cuenta que insertar o reemplazar no se admite en el emulador de almacenamiento local de hello, por lo que este código se ejecuta solo cuando utiliza una cuenta de servicio de la tabla de Hola. Puede obtener más información sobre la inserción o reemplazo y la inserción o fusión en [Tablas de Azure: Introducción a Upsert y proyección de consultas][Azure Tables: Introducing Upsert and Query Projection].

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

## <a name="how-to-delete-an-entity"></a>Cómo eliminar una entidad
Puede eliminar fácilmente una entidad después de que la haya recuperado. Una vez que se recupera la entidad de hello, llame a **TableOperation.delete** con hello entidad toodelete. A continuación, llame a **ejecutar** en hello **CloudTable** objeto. Hola siguiente código recupera y elimina una entidad customer.

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

## <a name="how-to-delete-a-table"></a>Cómo eliminar una tabla
Por último, hello siguiente código elimina una tabla de una cuenta de almacenamiento. Una tabla que se ha eliminado estará disponible toobe vuelve a crear durante un período de tiempo tras la eliminación de hello, normalmente menos de 40 segundos.

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

## <a name="next-steps"></a>Pasos siguientes

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* [SDK de Azure Storage para Java][Azure Storage SDK for Java]
* [referencia de SDK de cliente de almacenamiento de Azure][referencia de SDK de cliente de almacenamiento de Azure]
* [API de REST de Azure Storage][Azure Storage REST API]
* [Blog del equipo de Azure Storage][Azure Storage Team Blog]

Para obtener más información, vea también hello [Centro para desarrolladores de Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referencia de SDK de cliente de almacenamiento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
