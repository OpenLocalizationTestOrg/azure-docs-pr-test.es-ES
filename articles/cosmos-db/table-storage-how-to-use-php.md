---
title: Uso de Table Storage en PHP | Microsoft Docs
description: Aprenda a utilizar el servicio Tabla de Azure de PHP para crear y eliminar una tabla e insertar, eliminar y consultar la tabla.
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
ms.openlocfilehash: 7a48446a11c5c6db0c9f4fdd8872b1e3c12e85c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="dc8e9-103">Uso del almacenamiento de tablas de PHP</span><span class="sxs-lookup"><span data-stu-id="dc8e9-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="dc8e9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="dc8e9-104">Overview</span></span>
<span data-ttu-id="dc8e9-105">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio Tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="dc8e9-106">Los ejemplos están escritos en PHP y utilizan el [SDK de Azure para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="dc8e9-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="dc8e9-107">Entre los escenarios descritos se incluyen la **creación y eliminación de una tabla, y la inserción, eliminación y consulta de entidades de una tabla**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="dc8e9-108">Para obtener más información acerca del servicio Tabla de Azure, vea la sección [Pasos siguientes](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="dc8e9-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="dc8e9-109">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="dc8e9-109">Create a PHP application</span></span>
<span data-ttu-id="dc8e9-110">El único requisito a la hora de crear una aplicación PHP para obtener acceso al servicio Tabla de Azure es que el código haga referencia a clases del SDK de Azure para PHP.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="dc8e9-111">Puede utilizar cualquier herramienta de desarrollo para crear la aplicación, incluido el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="dc8e9-112">En esta guía, utilizará características del servicio Tabla a las que se puede llamar desde una aplicación PHP localmente, o bien mediante código que se ejecuta en un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="dc8e9-113">Obtención de las bibliotecas de clientes de Azure</span><span class="sxs-lookup"><span data-stu-id="dc8e9-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="dc8e9-114">Configuración de la aplicación para obtener acceso al servicio Tabla</span><span class="sxs-lookup"><span data-stu-id="dc8e9-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="dc8e9-115">Para utilizar las API del servicio Tabla de Azure, necesita:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="dc8e9-116">Hacer referencia al archivo autocargador mediante la instrucción [require_once][require_once] y</span><span class="sxs-lookup"><span data-stu-id="dc8e9-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="dc8e9-117">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-117">Reference any classes you might use.</span></span>

<span data-ttu-id="dc8e9-118">En el siguiente ejemplo se muestra cómo incluir el archivo autocargador y hacer referencia a la clase **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="dc8e9-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="dc8e9-119">En los ejemplos de este artículo, se da por hecho que ha instalado las bibliotecas de clientes PHP para Azure mediante el compositor.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="dc8e9-120">Si las instaló manualmente, debe hacer referencia al archivo del cargador automático <code>WindowsAzure.php</code> .</span><span class="sxs-lookup"><span data-stu-id="dc8e9-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="dc8e9-121">En los ejemplos que aparecen a continuación, la instrucción `require_once` aparecerá siempre, pero solo se hará referencia a las clases necesarias para la ejecución del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="dc8e9-122">Configuración de una conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="dc8e9-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="dc8e9-123">Para crear una instancia de un cliente del servicio Tabla de Azure, primero debe disponer de una cadena de conexión válida.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="dc8e9-124">El formato de las cadenas de conexión del servicio Tabla es:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="dc8e9-125">Para obtener acceso a un servicio en directo:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="dc8e9-126">Para obtener acceso al emulador de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="dc8e9-127">Para crear un cliente de cualquier servicio de Azure, debe usar la clase **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="dc8e9-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="dc8e9-128">Puede:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-128">You can:</span></span>

* <span data-ttu-id="dc8e9-129">pasarle directamente la cadena de conexión, o bien</span><span class="sxs-lookup"><span data-stu-id="dc8e9-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="dc8e9-130">usar **CloudConfigurationManager (CCM)** para buscar la cadena de conexión en varios orígenes externos:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="dc8e9-131">de manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="dc8e9-132">para agregar nuevos orígenes, amplíe la clase **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="dc8e9-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="dc8e9-133">En los ejemplos descritos aquí, la cadena de conexión se pasará directamente.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="dc8e9-134">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="dc8e9-134">Create a table</span></span>
<span data-ttu-id="dc8e9-135">Puede crear una tabla con un objeto A **TableRestProxy** con el método **createTable**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="dc8e9-136">Al crear una tabla, puede establecer un tiempo de espera para el servicio Tabla.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="dc8e9-137">(Para obtener más información sobre el tiempo de espera de Table Service, consulte [Establecer los tiempos de espera para las operaciones de Table Service][table-service-timeouts]).</span><span class="sxs-lookup"><span data-stu-id="dc8e9-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="dc8e9-138">Para obtener más información sobre las restricciones que se aplican a los nombres de las tablas, consulte [Introducción al modelo de datos de Table Service][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="dc8e9-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="dc8e9-139">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="dc8e9-139">Add an entity to a table</span></span>
<span data-ttu-id="dc8e9-140">Para agregar una entidad a una tabla, cree un nuevo objeto **Entity** y páselo a **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="dc8e9-141">Tenga en cuenta que al crear una entidad, es necesario especificar los valores de `PartitionKey` y `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="dc8e9-142">Estos valores son los identificadores exclusivos de la entidad y se pueden consultar más rápidamente que las demás propiedades.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="dc8e9-143">El sistema usa `PartitionKey` para distribuir automáticamente las entidades de la tabla entre numerosos nodos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="dc8e9-144">Las entidades con la misma `PartitionKey` se almacenan en el mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="dc8e9-145">(Las operaciones que afecten a entidades almacenadas en el mismo nodo se realizarán mejor que aquellas que afecten a entidades almacenadas en nodos distintos). `RowKey` es el identificador exclusivo de una entidad dentro de una partición.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
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

<span data-ttu-id="dc8e9-146">Para obtener más información sobre las propiedades y los tipos de tabla, consulte [Introducción al modelo de datos de Table Service][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="dc8e9-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="dc8e9-147">La clase **TableRestProxy** ofrece dos métodos alternativos para insertar entidades: **insertOrMergeEntity** y **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="dc8e9-148">Para usar estos métodos, cree una nueva **Entity** y pásela como un parámetro para cualquiera de los métodos.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="dc8e9-149">Ambos métodos insertarán la entidad si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="dc8e9-150">Si ya existe la entidad, **insertOrMergeEntity** actualizará los valores de las propiedades existentes y agregará las propiedades que no existan, mientras que **insertOrReplaceEntity** reemplazará por completo la entidad existente.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="dc8e9-151">En el siguiente ejemplo se muestra cómo usar el método **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="dc8e9-152">Si todavía no existe ninguna entidad con `PartitionKey` "tasksSeattle" y `RowKey` "1", se insertará.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="dc8e9-153">Sin embargo, si ya se insertó previamente (como se muestra en el ejemplo anterior), se actualizará la propiedad `DueDate` y se agregará la propiedad `Status`.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="dc8e9-154">Las propiedades `Description` y `Location` también se actualizan, pero con valores que a efectos prácticos no provocarán ningún cambio en ellas.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="dc8e9-155">Si estas dos últimas propiedades no se agregaron como se muestra en el ejemplo, sino que existían en la entidad objetivo, sus valores actuales permanecerán invariables.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="dc8e9-156">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="dc8e9-156">Retrieve a single entity</span></span>
<span data-ttu-id="dc8e9-157">El método **TableRestProxy->getEntity** permite recuperar una sola entidad consultando sus valores de `PartitionKey` y `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="dc8e9-158">En el ejemplo siguiente, la clave de partición `tasksSeattle` y la clave de fila `1` se pasan al método **getEntity**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="dc8e9-159">todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="dc8e9-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="dc8e9-160">Las consultas a entidades se basan en filtros (para obtener más información, consulte [Consultar tablas y entidades][filters]).</span><span class="sxs-lookup"><span data-stu-id="dc8e9-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="dc8e9-161">Para recuperar todas las entidades de una partición, utilice el filtro "PartitionKey eq *partition_name*".</span><span class="sxs-lookup"><span data-stu-id="dc8e9-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="dc8e9-162">En el siguiente ejemplo se muestra cómo recuperar todas las entidades de la partición `tasksSeattle` pasando un filtro al método **queryEntities** .</span><span class="sxs-lookup"><span data-stu-id="dc8e9-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="dc8e9-163">un subconjunto de entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="dc8e9-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="dc8e9-164">El mismo patrón utilizado en el ejemplo anterior se puede aplicar a la recuperación de cualquier subconjunto de entidades de una partición.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="dc8e9-165">El subconjunto de entidades que recupere dependerá del filtro que utilice (para más información, consulte [Consultar tablas y entidades][filters]). En el siguiente ejemplo se muestra cómo usar un filtro para recuperar todas las entidades con un valor concreto para `Location` y un valor para `DueDate` anterior a una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="dc8e9-166">un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="dc8e9-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="dc8e9-167">Es posible recuperar un subconjunto de propiedades de las entidades mediante una consulta.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="dc8e9-168">Esta técnica, denominada *proyección*, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="dc8e9-169">Para especificar la propiedad que desea recuperar, pase el nombre de la propiedad al método **Query->addSelectField**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="dc8e9-170">Puede llamar a este método varias veces para agregar más propiedades.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="dc8e9-171">Tras ejecutar **TableRestProxy->queryEntities**, las entidades que se recuperen solo presentarán las propiedades seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="dc8e9-172">(Si desea recuperar un subconjunto de entidades de tabla, utilice un filtro tal y como se muestra en las consultas anteriores).</span><span class="sxs-lookup"><span data-stu-id="dc8e9-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

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

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="dc8e9-173">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="dc8e9-173">Update an entity</span></span>
<span data-ttu-id="dc8e9-174">Es posible actualizar una entidad existente con los métodos **Entity->setProperty** y **Entity->addProperty** en la entidad y, a continuación, con una llamada a **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="dc8e9-175">En el siguiente ejemplo se recupera una entidad, se modifica una propiedad, se elimina otra propiedad y se agrega una nueva propiedad.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="dc8e9-176">Tenga en cuenta que para eliminar una propiedad debe establecer su valor en **null**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-176">Note that you can remove a property by setting its value to **null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="dc8e9-177">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="dc8e9-177">Delete an entity</span></span>
<span data-ttu-id="dc8e9-178">Para eliminar una entidad, pase el nombre de la tabla y los valores `PartitionKey` y `RowKey` de la entidad al método **TableRestProxy->deleteEntity**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="dc8e9-179">Tenga en cuenta que en las comprobaciones de simultaneidad puede determinar que se elimine la propiedad Etag de una entidad utilizando el método **DeleteEntityOptions->setEtag** y pasando el objeto **DeleteEntityOptions** a **deleteEntity** como cuarto parámetro.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="dc8e9-180">operaciones de tabla</span><span class="sxs-lookup"><span data-stu-id="dc8e9-180">Batch table operations</span></span>
<span data-ttu-id="dc8e9-181">El método **TableRestProxy->batch** permite ejecutar varias operaciones en una única solicitud.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="dc8e9-182">Este patrón consiste en agregar operaciones al objeto **BatchRequest** y, a continuación, pasar el objeto **BatchRequest** al método **TableRestProxy->batch**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="dc8e9-183">Para agregar una operación a un objeto **BatchRequest** , puede llamar a cualquiera de los siguientes métodos varias veces:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="dc8e9-184">**addInsertEntity** (agrega una operación insertEntity)</span><span class="sxs-lookup"><span data-stu-id="dc8e9-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="dc8e9-185">**addUpdateEntity** (agrega una operación updateEntity)</span><span class="sxs-lookup"><span data-stu-id="dc8e9-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="dc8e9-186">**addMergeEntity** (agrega una operación mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="dc8e9-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="dc8e9-187">**addInsertOrReplaceEntity** (agrega una operación insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="dc8e9-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="dc8e9-188">**addInsertOrMergeEntity** (agrega una operación insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="dc8e9-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="dc8e9-189">**addDeleteEntity** (agrega una operación deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="dc8e9-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="dc8e9-190">En el siguiente ejemplo se muestra cómo ejecutar las operaciones **insertEntity** y **deleteEntity** en una única solicitud:</span><span class="sxs-lookup"><span data-stu-id="dc8e9-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
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

<span data-ttu-id="dc8e9-191">Para obtener más información sobre el procesamiento por lotes de las operaciones de tabla, consulte [Realizar transacciones con grupos de entidades][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="dc8e9-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="dc8e9-192">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="dc8e9-192">Delete a table</span></span>
<span data-ttu-id="dc8e9-193">Finalmente, para eliminar una tabla, pase su nombre al método **TableRestProxy->deleteTable**.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dc8e9-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc8e9-194">Next steps</span></span>
<span data-ttu-id="dc8e9-195">Ahora que está familiarizado con los aspectos básicos de Azure Table service, use estos vínculos para obtener más información sobre tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="dc8e9-196">El [Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente y gratuita de Microsoft que permite trabajar visualmente con los datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="dc8e9-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="dc8e9-197">[Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="dc8e9-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
