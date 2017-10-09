---
title: aaaGet a trabajar con el almacenamiento de tabla y Visual Studio servicios conectados (servicios en la nube) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de tabla de Azure en un proyecto de servicio de nube en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
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
ms.openlocfilehash: efb16953e05764cb162cbdae4d0eab57f781682d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introducción al almacenamiento de tablas de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Información general
Este artículo describe cómo tooget iniciado mediante el almacenamiento de tabla de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de servicios de nube mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo . Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.

Hola servicio de almacenamiento de tabla de Azure permite toostore grandes cantidades de datos estructurados. servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure. Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.

tooget iniciado, primero debe toocreate una tabla en la cuenta de almacenamiento. Le mostraremos cómo tabla toocreate un Azure en el código y cómo tabla básica tooperform y operaciones de entidad, como agregar, modificar, leer y leer la tabla de entidades. Hola ejemplos están escritos en C\# código y utilizar hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

**Nota:** algunas de las API que realizan llamadas tooAzure almacenamiento hello son asincrónicas. Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información. código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.

* Consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md) para más información sobre la manipulación de tablas mediante programación.
* Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.
* Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.
* Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.

## <a name="access-tables-in-code"></a>Acceso a tablas en código
tooaccess tablas en proyectos de servicios de nube, debe hello tooinclude siguientes archivos de origen de tooany C# de elementos que tienen acceso a almacenamiento de tabla de Azure.

1. Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Usar hello siguientes código tooget Hola almacenamiento conexión cadena y almacenamiento de información de la cuenta de configuración de servicio de Azure Hola.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > Use todos Hola encima código frente a código de hello en los siguientes ejemplos de hello.
   > 
   > 
3. Obtener un **CloudTableClient** tooreference Hola tabla objetos en la cuenta de almacenamiento de objetos.
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Obtener un **CloudTable** hacen referencia a una tabla específica del objeto tooreference y entidades.
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Crear una tabla en el código
Hola toocreate tabla de Azure, basta con agregar una llamada demasiado**CreateIfNotExistsAsync** toohello después de obtener un **CloudTable** objeto tal y como se describe en la sección de "Acceso a tablas en el código" Hola.

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
tooadd una tabla de tooa de entidad, cree una clase que define las propiedades de saludo de la entidad. Hello código siguiente define una clase de entidad denominada **CustomerEntity** que usa Hola nombre del cliente como clave de fila de Hola y Hola last name como clave de partición de Hola.

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

Operaciones de tabla que implican las entidades se realizan mediante hello **CloudTable** objeto que creó anteriormente en "Acceso a las tablas en el código". Hola **TableOperation** objeto representa Hola operación toobe realizada. Hola siguiendo el ejemplo de código muestra cómo toocreate una **CloudTable** objeto y un **CustomerEntity** objeto. operación de hello tooprepare, un **TableOperation** se crea la entidad customer ya tooinsert hello en tabla Hola. Por último, se ejecuta la operación de hello mediante una llamada a **CloudTable.ExecuteAsync**.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a>Inserción de un lote de entidades
Puede insertar varias entidades en una tabla mediante una única operación de escritura. Hello ejemplo de código siguiente crea dos objetos de entidad ("Jeff Smith" y "Ben Smith"), se agrega tooa **TableBatchOperation** objeto mediante Hola método Insert y, a continuación, inicia Hola operación mediante una llamada a  **CloudTable.ExecuteBatchAsync**.

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
Puede eliminar fácilmente una entidad después de haberla encontrado. Hello código siguiente busca una entidad de cliente denominada "Ben Smith" y, si lo encuentra, elimina.

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

