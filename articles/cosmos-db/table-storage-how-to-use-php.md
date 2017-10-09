---
title: almacenamiento de tablas de aaaHow toouse de PHP | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola servicio tabla de PHP toocreate y eliminar una tabla y la inserción, la eliminación y la tabla de Hola de consulta."
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 5b7c92221069d1c2a6ca951c06ae8eea8bb8478c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Cómo toouse tabla almacenamiento de PHP
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio tabla de Azure. ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP][download]. Hello escenarios descritos se incluyen **crear y eliminar una tabla e Insertar, eliminar y consultar entidades de una tabla**. Para obtener más información sobre Hola servicio tabla de Azure, vea hello [pasos siguientes](#next-steps) sección.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Creación de una aplicación PHP
Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de la tabla de Azure de hello es hello las referencias de las clases de hello Azure SDK para PHP desde dentro del código. Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación, incluso el Bloc de notas.

En esta guía, utilizará características del servicio Tabla a las que se puede llamar desde una aplicación PHP localmente, o bien mediante código que se ejecuta en un rol web, rol de trabajo o sitio web de Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtener Hola bibliotecas de cliente de Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Configurar el servicio de tabla de aplicación tooaccess Hola
toouse hello Azure API del servicio tabla, debe:

1. Archivo de referencia hello cargador automático con hello [require_once] [ require_once] (instrucción), y
2. Hacer referencia a todas las clases que utilice.

Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServicesBuilder** clase.

> [!NOTE]
> ejemplos de Hello en este artículo se supone que ha instalado Hola bibliotecas de cliente de PHP para Azure mediante el compositor. Si ha instalado manualmente las bibliotecas de hello, necesita hello tooreference <code>WindowsAzure.php</code> archivo cargador automático.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

En los siguientes ejemplos de hello, Hola `require_once` siempre se muestra la instrucción, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de Almacenamiento de Azure
tooinstantiate un cliente del servicio tabla de Azure, primero debe tener una cadena de conexión válida. formato Hola Hola cadena de conexión de servicio de tabla es:

Para obtener acceso a un servicio en directo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para acceder al almacenamiento de emulador de hello:

```php
UseDevelopmentStorage=true
```

toocreate cualquier cliente de servicio de Azure, necesita hello toouse **ServicesBuilder** clase. Puede:

* Pasar Hola conexión cadena directamente tooit o
* Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:
  * de manera predeterminada, admite un origen externo: variables de entorno.
  * Puede agregar nuevos orígenes de extendiendo hello **ConnectionStringSource** (clase)

Para obtener ejemplos de hello descritos a continuación, cadena de conexión de Hola se pasará directamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Creación de una tabla
A **TableRestProxy** objeto le permite crear una tabla con hello **createTable** método. Al crear una tabla, puede establecer el tiempo de espera del servicio de tabla de Hola. (Para obtener más información sobre el tiempo de espera del servicio de tabla de hello, consulte [los tiempos de espera de configuración para las operaciones de servicio de tabla][table-service-timeouts].)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

Para obtener información acerca de las restricciones en los nombres de tabla, vea [Hola de entender el modelo de datos del servicio de tabla][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
tooadd una tabla de tooa de entidad, cree un nuevo **entidad** objeto y pasarlo demasiado**TableRestProxy -> insertEntity**. Tenga en cuenta que al crear una entidad, es necesario especificar los valores de `PartitionKey` y `RowKey`. Estos son identificadores únicos de una entidad de Hola y son valores que se pueden consultar mucho más rápido que otras propiedades de entidad. sistema de Hello usa `PartitionKey` tooautomatically distribuir las entidades de la tabla de hello sobre muchos nodos de almacenamiento. Las entidades con Hola mismo `PartitionKey` se almacenan en hello mismo nodo. (Las operaciones en varias entidades que se almacenan en hello realizar el mismo nodo mejor que en las entidades almacenadas en distintos nodos.) Hola `RowKey` es Hola identificador único de una entidad dentro de una partición.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

Para obtener información sobre propiedades de tabla y los tipos, vea [Hola de entender el modelo de datos del servicio de tabla][table-data-model].

Hola **TableRestProxy** clase ofrece dos métodos alternativos para insertar las entidades: **insertOrMergeEntity** y **insertOrReplaceEntity**. toouse estos métodos, cree un nuevo **entidad** y pasarla como un método de tooeither de parámetro. Cada método insertará entidad Hola si no existe. Si ya existe una entidad de hello, **insertOrMergeEntity** actualiza valores de propiedad si ya existen propiedades de Hola y agrega propiedades de nueva si no existen, mientras que **insertOrReplaceEntity** completamente reemplaza una entidad existente. Hola siguiente ejemplo se muestra cómo toouse **insertOrMergeEntity**. Si Hola entidad con `PartitionKey` "tasksSeattle" y `RowKey` "1" no existe ya, se va a insertar. Sin embargo, si previamente se ha insertado (tal y como se muestra en el ejemplo de Hola anterior), Hola `DueDate` propiedad se actualizará y Hola `Status` se agregará la propiedad. Hola `Description` y `Location` propiedades también se actualizan, pero con valores que eficazmente o dejarlos intactos. Si estas dos últimas propiedades no se agrega como se muestra en el ejemplo de Hola, pero existía en la entidad de destino de hello, sus valores existentes se mantendría sin cambios.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>una sola entidad
Hola **TableRestProxy -> getEntity** método le permite tooretrieve una única entidad mediante una consulta para su `PartitionKey` y `RowKey`. En el siguiente ejemplo de Hola, Hola clave de partición `tasksSeattle` y clave de fila `1` se pasan toohello **getEntity** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>todas las entidades de una partición
Las consultas a entidades se basan en filtros (para obtener más información, consulte [Consultar tablas y entidades][filters]). tooretrieve todas las entidades en una partición, use el filtro de Hola "eq PartitionKey *partición*". Hola siguiente ejemplo se muestra cómo tooretrieve todas las entidades de hello `tasksSeattle` partición pasando un filtro toohello **queryEntities** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>un subconjunto de entidades de una partición
Hola mismo patrón que se utiliza en el ejemplo anterior de hello puede ser cualquier subconjunto de las entidades de una partición de tooretrieve usado. subconjunto de Hola de entidades que recupera vienen determinados por filtro de hello usas (para obtener más información, consulte [consultar tablas y entidades][filters]) .hello siguiente ejemplo se muestra cómo toouse una tooretrieve de filtro todas las entidades con un valor concreto `Location` y un `DueDate` menor que una fecha especificada.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>un subconjunto de propiedades de las entidades
Es posible recuperar un subconjunto de propiedades de las entidades mediante una consulta. Esta técnica, denominada *proyección*, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño. recupera de una propiedad toobe toospecify, pasar nombre Hola de hello propiedad toohello **consulta -> addSelectField** método. Puede llamar a este método varias veces tooadd más propiedades. Después de ejecutar **TableRestProxy -> queryEntities**, Hola devuelve entidades solo tendrán propiedades Hola seleccionado. (Si desea tooreturn un subconjunto de las entidades de tabla, utilice un filtro como se muestra en las consultas de hello anteriores.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Actualización de una entidad
Se puede actualizar una entidad existente mediante el uso de hello **Entity -> setProperty** y **Entity -> addProperty** métodos en la entidad de hello y, a continuación, llamar a **TableRestProxy -> updateEntity** . Hello en el ejemplo siguiente se recupera una entidad, modifica una propiedad, quita otra propiedad y agrega una nueva propiedad. Tenga en cuenta que puede quitar una propiedad estableciendo su valor demasiado**null**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>Eliminación de una entidad
toodelete una entidad, pase el nombre de la tabla de Hola y la entidad de hello `PartitionKey` y `RowKey` toohello **TableRestProxy -> deleteEntity** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Tenga en cuenta que para las comprobaciones de simultaneidad, se puede establecer hello Etag para un toobe de entidad eliminado mediante el uso de hello **DeleteEntityOptions -> setEtag** Hola de método y pasar **DeleteEntityOptions** objeto demasiado**deleteEntity** como cuarto parámetro.

## <a name="batch-table-operations"></a>operaciones de tabla
Hola **TableRestProxy -> lote** método le permite tooexecute varias operaciones en una sola solicitud. Hello patrón aquí implica agregar operaciones demasiado**BatchRequest** objeto y, a continuación, pasar hello **BatchRequest** objeto toohello **TableRestProxy -> lote** método. una operación tooa tooadd **BatchRequest** objeto, puede llamar a cualquiera de hello siguiendo métodos varias veces:

* **addInsertEntity** (agrega una operación insertEntity)
* **addUpdateEntity** (agrega una operación updateEntity)
* **addMergeEntity** (agrega una operación mergeEntity)
* **addInsertOrReplaceEntity** (agrega una operación insertOrReplaceEntity)
* **addInsertOrMergeEntity** (agrega una operación insertOrMergeEntity)
* **addDeleteEntity** (agrega una operación deleteEntity)

Hola siguiente ejemplo se muestra cómo tooexecute **insertEntity** y **deleteEntity** operaciones en una sola solicitud:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Para obtener más información sobre el procesamiento por lotes de las operaciones de tabla, consulte [Realizar transacciones con grupos de entidades][entity-group-transactions].

## <a name="delete-a-table"></a>Eliminación de una tabla
Por último, toodelete una tabla, pase toohello de nombre de tabla de hello **TableRestProxy -> deleteTable** método.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de hello servicio tabla de Azure, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.

* [Centro para desarrolladores de PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
