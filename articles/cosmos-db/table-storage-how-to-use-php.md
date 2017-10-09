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
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="5eb15-103">Cómo toouse tabla almacenamiento de PHP</span><span class="sxs-lookup"><span data-stu-id="5eb15-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="5eb15-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5eb15-104">Overview</span></span>
<span data-ttu-id="5eb15-105">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb15-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="5eb15-106">ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="5eb15-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="5eb15-107">Hello escenarios descritos se incluyen **crear y eliminar una tabla e Insertar, eliminar y consultar entidades de una tabla**.</span><span class="sxs-lookup"><span data-stu-id="5eb15-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="5eb15-108">Para obtener más información sobre Hola servicio tabla de Azure, vea hello [pasos siguientes](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="5eb15-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5eb15-109">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="5eb15-109">Create a PHP application</span></span>
<span data-ttu-id="5eb15-110">Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de la tabla de Azure de hello es hello las referencias de las clases de hello Azure SDK para PHP desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="5eb15-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="5eb15-111">Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación, incluso el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="5eb15-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="5eb15-112">En esta guía, utilizará características del servicio Tabla a las que se puede llamar desde una aplicación PHP localmente, o bien mediante código que se ejecuta en un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb15-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="5eb15-113">Obtener Hola bibliotecas de cliente de Azure</span><span class="sxs-lookup"><span data-stu-id="5eb15-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="5eb15-114">Configurar el servicio de tabla de aplicación tooaccess Hola</span><span class="sxs-lookup"><span data-stu-id="5eb15-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="5eb15-115">toouse hello Azure API del servicio tabla, debe:</span><span class="sxs-lookup"><span data-stu-id="5eb15-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="5eb15-116">Archivo de referencia hello cargador automático con hello [require_once] [ require_once] (instrucción), y</span><span class="sxs-lookup"><span data-stu-id="5eb15-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="5eb15-117">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="5eb15-117">Reference any classes you might use.</span></span>

<span data-ttu-id="5eb15-118">Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServicesBuilder** clase.</span><span class="sxs-lookup"><span data-stu-id="5eb15-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="5eb15-119">ejemplos de Hello en este artículo se supone que ha instalado Hola bibliotecas de cliente de PHP para Azure mediante el compositor.</span><span class="sxs-lookup"><span data-stu-id="5eb15-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5eb15-120">Si ha instalado manualmente las bibliotecas de hello, necesita hello tooreference <code>WindowsAzure.php</code> archivo cargador automático.</span><span class="sxs-lookup"><span data-stu-id="5eb15-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="5eb15-121">En los siguientes ejemplos de hello, Hola `require_once` siempre se muestra la instrucción, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5eb15-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5eb15-122">Configuración de una conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5eb15-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="5eb15-123">tooinstantiate un cliente del servicio tabla de Azure, primero debe tener una cadena de conexión válida.</span><span class="sxs-lookup"><span data-stu-id="5eb15-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="5eb15-124">formato Hola Hola cadena de conexión de servicio de tabla es:</span><span class="sxs-lookup"><span data-stu-id="5eb15-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="5eb15-125">Para obtener acceso a un servicio en directo:</span><span class="sxs-lookup"><span data-stu-id="5eb15-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="5eb15-126">Para acceder al almacenamiento de emulador de hello:</span><span class="sxs-lookup"><span data-stu-id="5eb15-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="5eb15-127">toocreate cualquier cliente de servicio de Azure, necesita hello toouse **ServicesBuilder** clase.</span><span class="sxs-lookup"><span data-stu-id="5eb15-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="5eb15-128">Puede:</span><span class="sxs-lookup"><span data-stu-id="5eb15-128">You can:</span></span>

* <span data-ttu-id="5eb15-129">Pasar Hola conexión cadena directamente tooit o</span><span class="sxs-lookup"><span data-stu-id="5eb15-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="5eb15-130">Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="5eb15-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="5eb15-131">de manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="5eb15-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="5eb15-132">Puede agregar nuevos orígenes de extendiendo hello **ConnectionStringSource** (clase)</span><span class="sxs-lookup"><span data-stu-id="5eb15-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="5eb15-133">Para obtener ejemplos de hello descritos a continuación, cadena de conexión de Hola se pasará directamente.</span><span class="sxs-lookup"><span data-stu-id="5eb15-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="5eb15-134">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="5eb15-134">Create a table</span></span>
<span data-ttu-id="5eb15-135">A **TableRestProxy** objeto le permite crear una tabla con hello **createTable** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="5eb15-136">Al crear una tabla, puede establecer el tiempo de espera del servicio de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5eb15-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="5eb15-137">(Para obtener más información sobre el tiempo de espera del servicio de tabla de hello, consulte [los tiempos de espera de configuración para las operaciones de servicio de tabla][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="5eb15-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="5eb15-138">Para obtener información acerca de las restricciones en los nombres de tabla, vea [Hola de entender el modelo de datos del servicio de tabla][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="5eb15-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="5eb15-139">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="5eb15-139">Add an entity tooa table</span></span>
<span data-ttu-id="5eb15-140">tooadd una tabla de tooa de entidad, cree un nuevo **entidad** objeto y pasarlo demasiado**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="5eb15-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="5eb15-141">Tenga en cuenta que al crear una entidad, es necesario especificar los valores de `PartitionKey` y `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="5eb15-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="5eb15-142">Estos son identificadores únicos de una entidad de Hola y son valores que se pueden consultar mucho más rápido que otras propiedades de entidad.</span><span class="sxs-lookup"><span data-stu-id="5eb15-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="5eb15-143">sistema de Hello usa `PartitionKey` tooautomatically distribuir las entidades de la tabla de hello sobre muchos nodos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5eb15-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="5eb15-144">Las entidades con Hola mismo `PartitionKey` se almacenan en hello mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="5eb15-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="5eb15-145">(Las operaciones en varias entidades que se almacenan en hello realizar el mismo nodo mejor que en las entidades almacenadas en distintos nodos.) Hola `RowKey` es Hola identificador único de una entidad dentro de una partición.</span><span class="sxs-lookup"><span data-stu-id="5eb15-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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

<span data-ttu-id="5eb15-146">Para obtener información sobre propiedades de tabla y los tipos, vea [Hola de entender el modelo de datos del servicio de tabla][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="5eb15-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="5eb15-147">Hola **TableRestProxy** clase ofrece dos métodos alternativos para insertar las entidades: **insertOrMergeEntity** y **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="5eb15-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="5eb15-148">toouse estos métodos, cree un nuevo **entidad** y pasarla como un método de tooeither de parámetro.</span><span class="sxs-lookup"><span data-stu-id="5eb15-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="5eb15-149">Cada método insertará entidad Hola si no existe.</span><span class="sxs-lookup"><span data-stu-id="5eb15-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="5eb15-150">Si ya existe una entidad de hello, **insertOrMergeEntity** actualiza valores de propiedad si ya existen propiedades de Hola y agrega propiedades de nueva si no existen, mientras que **insertOrReplaceEntity** completamente reemplaza una entidad existente.</span><span class="sxs-lookup"><span data-stu-id="5eb15-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="5eb15-151">Hola siguiente ejemplo se muestra cómo toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="5eb15-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="5eb15-152">Si Hola entidad con `PartitionKey` "tasksSeattle" y `RowKey` "1" no existe ya, se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="5eb15-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="5eb15-153">Sin embargo, si previamente se ha insertado (tal y como se muestra en el ejemplo de Hola anterior), Hola `DueDate` propiedad se actualizará y Hola `Status` se agregará la propiedad.</span><span class="sxs-lookup"><span data-stu-id="5eb15-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="5eb15-154">Hola `Description` y `Location` propiedades también se actualizan, pero con valores que eficazmente o dejarlos intactos.</span><span class="sxs-lookup"><span data-stu-id="5eb15-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="5eb15-155">Si estas dos últimas propiedades no se agrega como se muestra en el ejemplo de Hola, pero existía en la entidad de destino de hello, sus valores existentes se mantendría sin cambios.</span><span class="sxs-lookup"><span data-stu-id="5eb15-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="5eb15-156">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="5eb15-156">Retrieve a single entity</span></span>
<span data-ttu-id="5eb15-157">Hola **TableRestProxy -> getEntity** método le permite tooretrieve una única entidad mediante una consulta para su `PartitionKey` y `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="5eb15-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="5eb15-158">En el siguiente ejemplo de Hola, Hola clave de partición `tasksSeattle` y clave de fila `1` se pasan toohello **getEntity** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="5eb15-159">todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="5eb15-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="5eb15-160">Las consultas a entidades se basan en filtros (para obtener más información, consulte [Consultar tablas y entidades][filters]).</span><span class="sxs-lookup"><span data-stu-id="5eb15-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="5eb15-161">tooretrieve todas las entidades en una partición, use el filtro de Hola "eq PartitionKey *partición*".</span><span class="sxs-lookup"><span data-stu-id="5eb15-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="5eb15-162">Hola siguiente ejemplo se muestra cómo tooretrieve todas las entidades de hello `tasksSeattle` partición pasando un filtro toohello **queryEntities** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="5eb15-163">un subconjunto de entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="5eb15-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="5eb15-164">Hola mismo patrón que se utiliza en el ejemplo anterior de hello puede ser cualquier subconjunto de las entidades de una partición de tooretrieve usado.</span><span class="sxs-lookup"><span data-stu-id="5eb15-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="5eb15-165">subconjunto de Hola de entidades que recupera vienen determinados por filtro de hello usas (para obtener más información, consulte [consultar tablas y entidades][filters]) .hello siguiente ejemplo se muestra cómo toouse una tooretrieve de filtro todas las entidades con un valor concreto `Location` y un `DueDate` menor que una fecha especificada.</span><span class="sxs-lookup"><span data-stu-id="5eb15-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="5eb15-166">un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="5eb15-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="5eb15-167">Es posible recuperar un subconjunto de propiedades de las entidades mediante una consulta.</span><span class="sxs-lookup"><span data-stu-id="5eb15-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="5eb15-168">Esta técnica, denominada *proyección*, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="5eb15-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="5eb15-169">recupera de una propiedad toobe toospecify, pasar nombre Hola de hello propiedad toohello **consulta -> addSelectField** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="5eb15-170">Puede llamar a este método varias veces tooadd más propiedades.</span><span class="sxs-lookup"><span data-stu-id="5eb15-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="5eb15-171">Después de ejecutar **TableRestProxy -> queryEntities**, Hola devuelve entidades solo tendrán propiedades Hola seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5eb15-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="5eb15-172">(Si desea tooreturn un subconjunto de las entidades de tabla, utilice un filtro como se muestra en las consultas de hello anteriores.)</span><span class="sxs-lookup"><span data-stu-id="5eb15-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

## <a name="update-an-entity"></a><span data-ttu-id="5eb15-173">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="5eb15-173">Update an entity</span></span>
<span data-ttu-id="5eb15-174">Se puede actualizar una entidad existente mediante el uso de hello **Entity -> setProperty** y **Entity -> addProperty** métodos en la entidad de hello y, a continuación, llamar a **TableRestProxy -> updateEntity** .</span><span class="sxs-lookup"><span data-stu-id="5eb15-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="5eb15-175">Hello en el ejemplo siguiente se recupera una entidad, modifica una propiedad, quita otra propiedad y agrega una nueva propiedad.</span><span class="sxs-lookup"><span data-stu-id="5eb15-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="5eb15-176">Tenga en cuenta que puede quitar una propiedad estableciendo su valor demasiado**null**.</span><span class="sxs-lookup"><span data-stu-id="5eb15-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="5eb15-177">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="5eb15-177">Delete an entity</span></span>
<span data-ttu-id="5eb15-178">toodelete una entidad, pase el nombre de la tabla de Hola y la entidad de hello `PartitionKey` y `RowKey` toohello **TableRestProxy -> deleteEntity** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="5eb15-179">Tenga en cuenta que para las comprobaciones de simultaneidad, se puede establecer hello Etag para un toobe de entidad eliminado mediante el uso de hello **DeleteEntityOptions -> setEtag** Hola de método y pasar **DeleteEntityOptions** objeto demasiado**deleteEntity** como cuarto parámetro.</span><span class="sxs-lookup"><span data-stu-id="5eb15-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="5eb15-180">operaciones de tabla</span><span class="sxs-lookup"><span data-stu-id="5eb15-180">Batch table operations</span></span>
<span data-ttu-id="5eb15-181">Hola **TableRestProxy -> lote** método le permite tooexecute varias operaciones en una sola solicitud.</span><span class="sxs-lookup"><span data-stu-id="5eb15-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="5eb15-182">Hello patrón aquí implica agregar operaciones demasiado**BatchRequest** objeto y, a continuación, pasar hello **BatchRequest** objeto toohello **TableRestProxy -> lote** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="5eb15-183">una operación tooa tooadd **BatchRequest** objeto, puede llamar a cualquiera de hello siguiendo métodos varias veces:</span><span class="sxs-lookup"><span data-stu-id="5eb15-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="5eb15-184">**addInsertEntity** (agrega una operación insertEntity)</span><span class="sxs-lookup"><span data-stu-id="5eb15-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="5eb15-185">**addUpdateEntity** (agrega una operación updateEntity)</span><span class="sxs-lookup"><span data-stu-id="5eb15-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="5eb15-186">**addMergeEntity** (agrega una operación mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="5eb15-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="5eb15-187">**addInsertOrReplaceEntity** (agrega una operación insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="5eb15-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="5eb15-188">**addInsertOrMergeEntity** (agrega una operación insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="5eb15-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="5eb15-189">**addDeleteEntity** (agrega una operación deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="5eb15-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="5eb15-190">Hola siguiente ejemplo se muestra cómo tooexecute **insertEntity** y **deleteEntity** operaciones en una sola solicitud:</span><span class="sxs-lookup"><span data-stu-id="5eb15-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

<span data-ttu-id="5eb15-191">Para obtener más información sobre el procesamiento por lotes de las operaciones de tabla, consulte [Realizar transacciones con grupos de entidades][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="5eb15-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="5eb15-192">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="5eb15-192">Delete a table</span></span>
<span data-ttu-id="5eb15-193">Por último, toodelete una tabla, pase toohello de nombre de tabla de hello **TableRestProxy -> deleteTable** método.</span><span class="sxs-lookup"><span data-stu-id="5eb15-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5eb15-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5eb15-194">Next steps</span></span>
<span data-ttu-id="5eb15-195">Ahora que conoce los fundamentos de Hola de hello servicio tabla de Azure, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5eb15-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="5eb15-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="5eb15-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="5eb15-197">[Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5eb15-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
