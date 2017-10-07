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
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>¿Cómo tooget a trabajar con el almacenamiento de tabla de Azure y Visual Studio servicios conectados
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Información general
Este artículo se describe cómo obtener se hayan iniciado mediante la tabla de Azure Hola almacenamiento en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET Core mediante Visual Studio **agregar servicios conectados** cuadro de diálogo.

Hola servicio de almacenamiento de tabla de Azure permite toostore grandes cantidades de datos estructurados. servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure. Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.

Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.

Para más información general sobre el uso de Almacenamiento de tablas de Azure, consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md).

tooget iniciado, primero debe toocreate una tabla en la cuenta de almacenamiento. Le mostraremos cómo tabla toocreate un Azure en el código. También le mostraremos cómo tabla básica tooperform y operaciones de entidad, como agregar, modificar, leer y leer la tabla de entidades. Hola ejemplos están escritos en C\# código y utilizar Hola biblioteca de cliente de almacenamiento de Azure para. NET.

**Tenga en cuenta** -algunas de las API que realizan llamadas tooAzure almacenamiento en ASP.NET Core Hola son asincrónicas. Consulte [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para obtener más información. código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.

## <a name="access-tables-in-code"></a>Acceso a tablas en código
tooaccess tablas en proyectos de ASP.NET Core, deberá hello tooinclude siguientes archivos de origen de tooany C# de elementos que tienen acceso a almacenamiento de tabla de Azure.

1. Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Tenga en cuenta** -los Hola encima código frente a código de hello usan en hello siguiendo los ejemplos.
3. Obtener un **CloudTableClient** tooreference Hola tabla objetos en la cuenta de almacenamiento de objetos.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Obtener un **CloudTable** hacen referencia a una tabla específica del objeto tooreference y entidades.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Crear una tabla en el código
Hola toocreate tabla de Azure, basta con agregar una llamada demasiado**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
tooadd una tabla de tooa de entidad se crea una clase que define las propiedades de saludo de la entidad. Hello código siguiente define una clase de entidad denominada **CustomerEntity** que usa Hola nombre del cliente como clave de fila de Hola y last name como clave de partición de Hola.

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

Operaciones de tabla que implican las entidades se realizan mediante hello **CloudTable** objeto que creó anteriormente en "Acceso a las tablas en el código". Hola **TableOperation** objeto representa Hola operación toobe realizada. Hola siguiendo el ejemplo de código muestra cómo toocreate una **CloudTable** objeto y un **CustomerEntity** objeto. operación de hello tooprepare, un **TableOperation** se crea la entidad customer ya tooinsert hello en tabla Hola. Por último, la operación de Hola se ejecuta mediante una llamada a CloudTable.ExecuteAsync.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Inserción de un lote de entidades
Puede insertar varias entidades en una tabla mediante una única operación de escritura. Hello ejemplo de código siguiente crea dos objetos de entidad ("Jeff Smith" y "Ben Smith"), se agrega tooa **TableBatchOperation** objeto mediante hello **insertar** método y, a continuación, inicia Hola operación CloudTable.ExecuteBatchAsync que realiza la llamada.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Obtener todas las entidades de hello en una partición
tooquery una tabla para todas las entidades de hello en una partición, use un **TableQuery** objeto. Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola. Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.

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

## <a name="get-a-single-entity"></a>Obtención de una sola entidad
Puede escribir una consulta tooget una entidad única, específica. Hola siguiente de código utiliza un **TableOperation** toospecify un cliente llamado "Ben Smith" del objeto. Este método devuelve una sola entidad, en lugar de una colección y Hola devolvió el valor en **TableResult.Result** es un **CustomerEntity** objeto. La especificación de claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una entidad única desde hello **tabla** servicio.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Eliminación de una entidad
Puede eliminar fácilmente una entidad después de haberla encontrado. Hello código siguiente busca una entidad de cliente denominada "Ben Smith" y si lo encuentra, elimina.

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

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

