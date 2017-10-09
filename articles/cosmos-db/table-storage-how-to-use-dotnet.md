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
# <a name="get-started-with-azure-table-storage-using-net"></a>Introducción al Almacenamiento de tablas de Azure mediante .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

El almacenamiento de tabla es un servicio que almacena NoSQL estructurado con un diseño schemaless del almacén de datos en la nube de hello, que proporciona un atributo de clave. Dado que el almacenamiento de tabla es schemaless, resulta fácil tooadapt necesidades de los datos como Hola de evolucionar de la aplicación. Acceder a los datos de almacenamiento tooTable es rápido y rentable para muchos tipos de aplicaciones y es normalmente menores costo SQL tradicional para similar volúmenes de datos.

Puede usar la tabla almacenamiento toostore flexible los conjuntos de datos como datos de usuario para aplicaciones web, libretas de direcciones, información de dispositivo u otros tipos de metadatos que se requiere el servicio. Puede almacenar cualquier número de entidades en una tabla y una cuenta de almacenamiento puede contener cualquier número de tablas, una toohello el límite de capacidad de la cuenta de almacenamiento de Hola.

### <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial muestra cómo hello toouse [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) en algunos escenarios comunes de almacenamiento de tabla de Azure. Estos escenarios se presentan con ejemplos de C# para crear y eliminar una tabla, e insertar, actualizar, eliminar y consultar datos de la tabla.

## <a name="prerequisites"></a>Requisitos previos

Se necesita Hola siguientes toocomplete este tutorial correctamente:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteca de cliente de Almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Administrador de configuración Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Más ejemplos
Para más ejemplos de uso de Almacenamiento de tablas, consulte [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Introducción a Almacenamiento de tablas de Azure en .NET). Puede descargar la aplicación de ejemplo de Hola y ejecutarlo o examinar el código de hello en GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adición de directivas using
Agregue Hola siguiente **con** arriba toohello de directivas de hello `Program.cs` archivo:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Analizar la cadena de conexión de Hola
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Crear el cliente del servicio tabla Hola
Hola [CloudTableClient] [ dotnet_CloudTableClient] clase le permite tooretrieve tablas y entidades almacenadas en almacenamiento de tabla. Este es el cliente del servicio de tabla de una manera toocreate hello:

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Ahora está listo toowrite código que lee datos de y escribe tooTable almacenamiento de datos.

## <a name="create-a-table"></a>Creación de una tabla
Este ejemplo se muestra cómo toocreate una tabla si aún no existe:

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

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
Las entidades asignan objetos tooC # mediante el uso de una clase personalizada derivada de [TableEntity][dotnet_TableEntity]. tooadd una tabla de tooa de entidad, cree una clase que define las propiedades de saludo de la entidad. Hello código siguiente define una clase de entidad que utiliza el nombre del cliente de hello como clave de fila de Hola y last name como clave de partición de Hola. Juntos, partición de una entidad y la clave de fila identifican singularmente en tabla Hola. Claves de partición de entidades con la misma clave de partición se puede consultar con más rapidez que las entidades con diferentes de hello, pero el uso de las claves de partición diversos permite para una mayor escalabilidad de operaciones en paralelo. Debe ser toobe de entidades que se almacenan en tablas de un tipo compatible, por ejemplo derivado Hola [TableEntity] [ dotnet_TableEntity] clase. Propiedades de la entidad que desea que toostore en una tabla deben ser propiedades públicas de tipo hello y admitir obtener y establecer valores de. Además, el tipo de entidad *must* expone un constructor sin parámetros.

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

Las operaciones de tabla que implican las entidades se realizan a través de hello [CloudTable] [ dotnet_CloudTable] objeto que creó anteriormente en la sección "Crear una tabla" de Hola. Hello toobe operación realiza representado por un [TableOperation] [ dotnet_TableOperation] objeto. Hello ejemplo de código siguiente muestra hello creación de hello [CloudTable] [ dotnet_CloudTable] objeto y, a continuación, un **CustomerEntity** objeto. operación de hello tooprepare, un [TableOperation] [ dotnet_TableOperation] objeto se crea la entidad customer ya tooinsert hello en tabla Hola. Por último, se ejecuta la operación de hello mediante una llamada a [CloudTable][dotnet_CloudTable].[ Ejecutar][dotnet_CloudTable_Execute].

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

## <a name="insert-a-batch-of-entities"></a>Inserción de un lote de entidades
Puede insertar un lote de entidades en una tabla mediante una operación de escritura. Otras notas acerca de las operaciones por lotes:

* Puede realizar actualizaciones, eliminaciones e inserciones en hello mismo única operación por lotes.
* Una única operación por lotes puede incluir una too100 entidades.
* Todas las entidades de una operación por lotes solo deben tener Hola misma clave de partición.
* Aunque es posible tooperform una consulta como una operación por lotes, debe ser única operación de hello en lote Hola.

crea dos objetos entidad Hello siguiente ejemplo de código y agrega cada demasiado[TableBatchOperation] [ dotnet_TableBatchOperation] mediante el uso de hello [insertar] [ dotnet_TableBatchOperation_Insert] método. A continuación, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] se denomina operación de hello tooexecute.

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

## <a name="retrieve-all-entities-in-a-partition"></a>todas las entidades de una partición
tooquery una tabla para todas las entidades de una partición, use un [TableQuery] [ dotnet_TableQuery] objeto. Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola. Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Recuperación de un rango de entidades de una partición
Si no desea tooquery todas las entidades de una partición, puede especificar un intervalo mediante la combinación de filtro de clave de partición de hello con un filtro de clave de fila. Hello ejemplo de código siguiente utiliza dos tooget filtros todas las entidades de partición "Smith" donde hello fila clave (nombre) empieza por una letra antes 'E' alfabeto hello, a continuación, imprime los resultados de la consulta de Hola.

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

## <a name="retrieve-a-single-entity"></a>una sola entidad
Puede escribir una consulta tooretrieve una entidad única, específica. Hola siguiente de código usa [TableOperation] [ dotnet_TableOperation] cliente de hello toospecify "Ben Smith". Este método devuelve una sola entidad en lugar de una colección y Hola devolvió el valor en [TableResult][dotnet_TableResult].[ Resultado] [ dotnet_TableResult_Result] es un **CustomerEntity** objeto. Especificar claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una sola entidad de servicio de la tabla de Hola.

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

## <a name="replace-an-entity"></a>una entidad
tooupdate una entidad, recuperar del servicio de tabla de hello, modificar el objeto de entidad de hello y, a continuación, guardar los cambios de hello hacer copia de servicio de la tabla de toohello. Hello código siguiente cambia número de teléfono de un cliente existente. En lugar de llamar a [Insert][dotnet_TableOperation_Insert], este código utiliza [Replace][dotnet_TableOperation_Replace]. [Reemplace] [ dotnet_TableOperation_Replace] causas Hola toobe entidad reemplazado totalmente en el servidor de hello, a menos que la entidad de hello en servidor hello ha cambiado desde que se recuperó, en cuyo caso se producirá un error de operación de Hola. Este error es tooprevent la aplicación se ha sobrescrito accidentalmente un cambio realizado entre Hola recuperación y actualizar por otro componente de la aplicación. Hello control correcto de este error es tooretrieve Hola entidad nuevo, realice los cambios (si todavía es válido) y, a continuación, realizar otra [reemplazar] [ dotnet_TableOperation_Replace] operación. Hola siguiente sección le mostrará cómo toooverride este comportamiento.

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

## <a name="insert-or-replace-an-entity"></a>Inserción o reemplazo de una entidad
[Reemplace] [ dotnet_TableOperation_Replace] operaciones generarán un error si la entidad de Hola se ha modificado desde que se recuperó del servidor de Hola. Además, debe recuperar primero entidad Hola desde servidor hello en orden para hello [reemplazar] [ dotnet_TableOperation_Replace] toobe de operación correcta. A veces, sin embargo, no sabe si entidad Hola existe en el servidor de Hola y valores actuales de hello almacenados en ella son irrelevantes. La actualización debe sobrescribir todos. tooaccomplish, usaría un [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operación. Esta operación inserta la entidad de hello si no existe, o lo reemplaza si lo hace, sin tener en cuenta cuando se realizó la última actualización de Hola.

En el siguiente ejemplo de código de hello, una entidad customer para 'Fred Jones' se crea y se inserta en la tabla de hello 'usuarios'. A continuación, usamos hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operación toosave una entidad con hello mismo (Jones) de clave de partición y fila de clave server de toohello (Fred), esta vez con un valor diferente para hello PhoneNumber propiedad. Dado que se ha usado [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], se reemplazan todos los valores de la propiedad. Sin embargo, si una entidad 'Fred Jones' no se había ya existía en la tabla de hello, habría que ha insertado.

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

## <a name="query-a-subset-of-entity-properties"></a>Consulta de un subconjunto de propiedades de las entidades
Una consulta de tabla puede recuperar solo unas pocas propiedades de una entidad en lugar de todas las propiedades de entidad de Hola. Esta técnica, denominada proyección, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño. consulta de Hello en el siguiente código de hello devuelve solo direcciones de correo electrónico de Hola de entidades de tabla de Hola. Esto se consigue utilizando una consulta de [DynamicTableEntity][dotnet_DynamicTableEntity] y también [EntityResolver][dotnet_EntityResolver]. Puede aprender más acerca de la proyección en hello [entrada de blog Introducción Upsert y proyección de consultas][blog_post_upsert]. Proyección no es compatible con el emulador de almacenamiento de hello, este código se ejecuta sólo cuando se está utilizando una cuenta de servicio de la tabla de Hola.

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

## <a name="delete-an-entity"></a>Eliminación de una entidad
Puede eliminar fácilmente una entidad después de que se han recuperado mediante el uso de hello mismo patrón que se muestra para la actualización de una entidad. Hola siguiente código recupera y elimina una entidad customer.

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

## <a name="delete-a-table"></a>Eliminación de una tabla
Por último, Hola ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento. Una tabla que se ha eliminado estará disponible toobe vuelve a crear durante un período de tiempo tras la eliminación de Hola.

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

## <a name="retrieve-entities-in-pages-asynchronously"></a>Recuperación de entidades en páginas de forma asincrónica
Si está leyendo un gran número de entidades, y desea tooprocess/mostrar entidades como recuperarlos en lugar de esperar a todos los tooreturn, puede recuperar entidades mediante una consulta segmentada. Este ejemplo muestra cómo tooreturn resultados en páginas mediante el patrón de hello asincrónicas Await para que la ejecución no se bloquea mientras se están esperando un gran conjunto de resultados tooreturn. Para obtener más detalles sobre el uso de hello patrón Async y Await en. NET, consulte [programación asincrónica con Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

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

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de hello del almacenamiento de tabla, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento:

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* Consulte más ejemplos de uso de Almacenamiento de tablas en [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)
* Ver la documentación de referencia de servicio de tabla de Hola para obtener información detallada acerca de las API disponibles:
* [Referencia de la biblioteca de clientes de almacenamiento para .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Referencia de API de REST](http://msdn.microsoft.com/library/azure/dd179355)
* Obtenga información acerca de cómo código de hello toosimplify escribir toowork con el almacenamiento de Azure mediante el uso de hello [SDK de WebJobs de Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.
* [Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore datos no estructurados.
* [Conectar tooSQL base de datos mediante el uso de .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore de datos relacionales.

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
