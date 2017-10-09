---
title: aaaHow toouse almacenamiento de tabla (C++) | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>¿Cómo toouse almacenamiento de tablas de C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes al usar Hola servicio de almacenamiento de tabla de Azure. ejemplos de Hello están escritos en C++ y usar hello [biblioteca de cliente de almacenamiento de Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello escenarios descritos se incluyen **crear y eliminar una tabla** y **trabajar con entidades de tabla**.

> [!NOTE]
> Destinos de esta guía Hola biblioteca de cliente de almacenamiento de Azure para C++ versión 1.0.0 y versiones posteriores. Hola recomienda versión es la biblioteca de cliente de almacenamiento 2.2.0, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Creación de una aplicación de C++
En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++. toodo por lo tanto, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.  

Hola tooinstall biblioteca de cliente de almacenamiento de Azure para C++, puede usar Hola siguientes métodos:

* **Linux:** siga las instrucciones de hello proporcionadas en hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.  
* **Windows:** en Visual Studio, haga clic en **Herramientas &gt; Administrador de paquetes de NuGet &gt; Consola del Administrador de paquetes**. Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione ENTRAR.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurar el almacenamiento de tabla tooaccess de aplicación
Agregar siguiente Hola incluir parte superior de toohello de las instrucciones del archivo de C++ de Hola donde se desea que las tablas de tooaccess de las API de toouse Hola almacenamiento de Azure:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de Almacenamiento de Azure
Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos. Cuando se ejecuta una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato. Usar el nombre de su almacenamiento hello y cuenta de almacenamiento clave de acceso para la cuenta de almacenamiento de Hola Hola enumerados en hello [Portal de Azure](https://portal.azure.com) para hello *AccountName* y *AccountKey* valores. Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md). Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest la aplicación en el equipo local basado en Windows, puede usar hello Azure [emulador de almacenamiento](../storage/common/storage-use-emulator.md) que se instala con hello [Azure SDK](https://azure.microsoft.com/downloads/). emulador de almacenamiento de Hello es una utilidad que simula los servicios de Azure Blob, cola y tabla de hello disponibles en el equipo de desarrollo local. Hello en el ejemplo siguiente se muestra cómo se puede declarar un emulador de almacenamiento local de campo estático toohold Hola conexión cadena tooyour:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart Hola emulador de almacenamiento de Azure, haga clic en hello **iniciar** o presionen clave de Windows hello. Comience a escribir **emulador de almacenamiento de Azure**y, a continuación, seleccione **emulador de almacenamiento de Microsoft Azure** de lista de Hola de aplicaciones.  

Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.  

## <a name="retrieve-your-connection-string"></a>Recuperación de la cadena de conexión
Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento. tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede usar el método de análisis de hello.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

A continuación, obtener una referencia tooa **cloud_table_client** de la clase, que le permite obtener objetos de referencia para las tablas y entidades almacenan dentro de hello servicio de almacenamiento de tabla. Hello código siguiente se crea un **cloud_table_client** objeto utilizando el objeto de cuenta de almacenamiento Hola recuperamos anteriormente:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Creación de una tabla
Los objetos **cloud_table_client** le permiten obtener objetos de referencia para tablas y entidades. Hello código siguiente se crea un **cloud_table_client** objeto y lo usa toocreate una nueva tabla.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
tooadd una tabla de tooa de entidad, cree un nuevo **table_entity** objeto y pasarlo demasiado**table_operation:: insert_entity**. Hello código siguiente usa nombre del cliente de hello como clave de fila de Hola y last name como clave de partición de Hola. Juntos, partición de una entidad y la clave de fila identifican entidad de hello en la tabla de Hola. Entidades con hello misma clave de partición se puede consultar con más rapidez que las que tienen diferentes claves de partición, pero el uso de las claves de partición diversos permite para una mayor escalabilidad de la operación paralela. Para obtener más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Almacenamiento de Microsoft Azure](../storage/common/storage-performance-checklist.md).

Hello código siguiente crea una nueva instancia de **table_entity** con algunos toobe de datos del cliente almacenado. Hola de código siguiente llama **table_operation:: insert_entity** toocreate una **table_operation** tooinsert una entidad del objeto en una tabla, y asocia Hola nueva entidad de tabla con él. Por último, llamadas código Hola Hola ejecutar el método en hello **cloud_table** objeto. Hello nueva y **table_operation** envía una entidad de cliente nueva de tabla servicio tooinsert hello toohello de solicitud en la tabla de Hola "personas".  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Inserción de un lote de entidades
Puede insertar un lote de entidades toohello servicio tabla en una sola operación de escritura. Hello código siguiente se crea un **table_batch_operation** objeto y, a continuación, agrega tres tooit de operaciones de inserción. Cada operación de inserción se agrega mediante la creación de un nuevo objeto de entidad, establecer sus valores, y, a continuación, llamar a Hola insert (método) en hello **table_batch_operation** entidad de hello tooassociate de objeto con una nueva operación de inserción. A continuación, **cloud_table.execute** se denomina operación de hello tooexecute.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Algunos toonote cosas en operaciones por lotes:  

* Puede realizar una too100 insert, delete, merge, replace, operaciones insert o merge y cuadro de diálogo Insertar o reemplazar en cualquier combinación en un único lote.  
* Una operación por lotes puede tener una operación de recuperación, si es la única operación de hello en el lote de Hola.  
* Todas las entidades de una operación por lotes solo deben tener Hola misma clave de partición.  
* Una operación por lotes es la carga de datos de 4 MB de tooa limitado.  

## <a name="retrieve-all-entities-in-a-partition"></a>todas las entidades de una partición
tooquery una tabla para todas las entidades de una partición, use un **table_query** objeto. Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola. Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

consulta de Hello en este ejemplo hace que todas las entidades de Hola que coinciden con los criterios de filtro de Hola. Si tiene tablas grandes y necesita entidades de tabla de hello toodownload a menudo, se recomienda que los datos se almacenan en blobs de almacenamiento de Azure en su lugar.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Recuperación de un rango de entidades de una partición
Si no desea tooquery todas las entidades de hello en una partición, puede especificar un intervalo mediante la combinación de filtro de clave de partición de hello con un filtro de clave de fila. Hello ejemplo de código siguiente utiliza dos tooget filtros todas las entidades de partición "Smith" donde clave de fila (nombre) de hello empieza por una letra anterior a 'E' alfabeto hello y, a continuación, imprime resultados de la consulta de Hola.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>una sola entidad
Puede escribir una consulta tooretrieve una entidad única, específica. Hola siguiente de código usa **table_operation:: retrieve_entity** cliente de hello toospecify "Jeff Smith". Este método devuelve una sola entidad, en lugar de una colección y hello valor devuelto está en **table_result**. Especificar claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una sola entidad de servicio de la tabla de Hola.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>una entidad
tooreplace una entidad, recuperar del servicio de tabla de hello, modificar el objeto de entidad de hello y, a continuación, guardar los cambios de hello hacer copia de servicio de la tabla de toohello. Hello código siguiente cambia dirección de correo electrónico y número de teléfono de un cliente existente. En lugar de llamar a **table_operation::insert_entity**, este código usa **table_operation::replace_entity**. Esto hace que Hola entidad toobe reemplazado totalmente en el servidor de hello, a menos que la entidad de hello en servidor hello ha cambiado desde que se recuperó, en cuyo caso se producirá un error de operación de Hola. Este error es tooprevent la aplicación se ha sobrescrito accidentalmente un cambio realizado entre Hola recuperación y actualizar por otro componente de la aplicación. Hello control correcto de este error es tooretrieve Hola entidad nuevo, realice los cambios (si todavía es válido) y, a continuación, realizar otra **table_operation:: replace_entity** operación. Hola siguiente sección le mostrará cómo toooverride este comportamiento.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Inserción o reemplazo de una entidad
**table_operation:: replace_entity** operaciones generarán un error si la entidad de Hola se ha modificado desde que se recuperó del servidor de Hola. Además, debe recuperar entidad Hola desde servidor hello primero en orden para **table_operation:: replace_entity** toobe correcta. A veces, sin embargo, no sabe si entidad Hola existe en el servidor de Hola y valores actuales de hello almacenados en ella son irrelevantes: la actualización debe sobrescribir todos ellos. tooaccomplish, usaría un **table_operation:: insert_or_replace_entity** operación. Esta operación inserta la entidad de hello si no existe, o lo reemplaza si lo hace, sin tener en cuenta cuando se realizó la última actualización de Hola. En el siguiente ejemplo de código de hello, todavía se recupera la entidad customer de Hola para Jeff Smith, pero, a continuación, se guarda servidor toohello atrás a través de **table_operation:: insert_or_replace_entity**. Se sobrescribirá cualquier actualización realizada entidad toohello entre una operación de recuperación y actualización Hola.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Consulta de un subconjunto de propiedades de las entidades
Una tabla de tooa de consulta puede recuperar solo unas pocas propiedades de una entidad. la consulta en el siguiente código de hello Hello utiliza hello **table_query:: set_select_columns** método tooreturn solo Hola direcciones de correo electrónico las entidades de tabla de Hola.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> Consultar una serie de propiedades de una entidad es una operación más eficaz que recuperar todas las propiedades.
> 
> 

## <a name="delete-an-entity"></a>Eliminación de una entidad
Puede eliminar fácilmente una entidad después de que la haya recuperado. Una vez que se recupera la entidad de hello, llame a **table_operation:: delete_entity** con hello entidad toodelete. A continuación, llamar a hello **cloud_table.execute** método. Hello siguiente código recupera y elimina una entidad con una clave de partición "Smith" y una clave de fila de "Juan".  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Eliminación de una tabla
Por último, Hola ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento. Una tabla que se ha eliminado estará disponible toobe vuelve a crear durante un período de tiempo tras la eliminación de Hola.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de hello del almacenamiento de tabla, siga estos toolearn de vínculos más sobre el almacenamiento de Azure:  

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* [¿Cómo toouse almacenamiento de blobs de C++](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de cola desde C++](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [Enumeración de los recursos de Almacenamiento de Azure en C++](../storage/common/storage-c-plus-plus-enumeration.md)
* [Referencia de la biblioteca de clientes de almacenamiento para C++](http://azure.github.io/azure-storage-cpp)
* [Documentación de Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/)
