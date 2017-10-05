---
title: Uso de Azure Table Storage con Python | Microsoft Docs
description: "Almacene datos estructurados en la nube con el Almacenamiento de tablas de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 0c46f04786ba4b62bd7ca22c5e25643123e6e136
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="b35f9-103">Uso de Table Storage en Python</span><span class="sxs-lookup"><span data-stu-id="b35f9-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="b35f9-104">En esta guía se explica cómo realizar escenarios comunes de Azure Table Storage en Python con la [SDK de Microsoft Azure Storage para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="b35f9-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="b35f9-105">Entre los escenarios descritos se incluyen la creación y eliminación de una tabla, la inserción y la consulta de entidades.</span><span class="sxs-lookup"><span data-stu-id="b35f9-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="b35f9-106">Mientras trabaja con los escenarios de este tutorial, puede que desee consultar la [referencia de SDK de Azure Storage para la API de Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="b35f9-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="b35f9-107">Instalación del SDK de Azure Storage para Python</span><span class="sxs-lookup"><span data-stu-id="b35f9-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="b35f9-108">Una vez que ha creado una cuenta de almacenamiento, el paso siguiente consiste en instalar el [SDK de Microsoft Azure Storage para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="b35f9-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="b35f9-109">Para más información acerca de la instalación del SDK, consulte el archivo [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) del SDK de Storage del repositorio de Python en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b35f9-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="b35f9-110">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="b35f9-110">Create a table</span></span>

<span data-ttu-id="b35f9-111">Para trabajar con Azure Table Service en Python, debe importar el módulo [TableService][py_TableService].</span><span class="sxs-lookup"><span data-stu-id="b35f9-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="b35f9-112">Dado que trabajará con entidades de Table, también se necesitará la clase [Entidad][py_Entity].</span><span class="sxs-lookup"><span data-stu-id="b35f9-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="b35f9-113">Agregue este código cerca de la parte superior del archivo de Python para importar ambos:</span><span class="sxs-lookup"><span data-stu-id="b35f9-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="b35f9-114">Cree un objeto [TableService][py_TableService] mediante la transmisión del nombre de la cuenta de almacenamiento y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="b35f9-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="b35f9-115">Reemplace `myaccount` y `mykey` por su nombre y clave de cuenta, y llame a [create_table][py_create_table] para crear la tabla en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b35f9-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="b35f9-116">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="b35f9-116">Add an entity to a table</span></span>

<span data-ttu-id="b35f9-117">Para agregar una entidad, cree primero un objeto que represente a la entidad y, a continuación, pase el objeto al método [TableService][py_TableService].[insert_entity][py_insert_entity].</span><span class="sxs-lookup"><span data-stu-id="b35f9-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="b35f9-118">El objeto de la entidad puede ser un diccionario o un objeto del tipo [Entidad][py_Entity] y define los nombres de propiedad y los valores de la entidad.</span><span class="sxs-lookup"><span data-stu-id="b35f9-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="b35f9-119">Cada entidad debe incluir las propiedades [PartitionKey y RowKey](#partitionkey-and-rowkey) necesarias, además de cualquier otra propiedad que se defina para la entidad.</span><span class="sxs-lookup"><span data-stu-id="b35f9-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="b35f9-120">En este ejemplo se crea un objeto de diccionario que representa a una entidad y, a continuación, lo pasa al método [insert_entity][py_insert_entity] para agregarlo a la tabla:</span><span class="sxs-lookup"><span data-stu-id="b35f9-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="b35f9-121">En este ejemplo se crea un objeto de [Entidad][py_Entity] y, a continuación, lo pasa al método [insert_entity][py_insert_entity] para agregarlo a la tabla:</span><span class="sxs-lookup"><span data-stu-id="b35f9-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="b35f9-122">PartitionKey y RowKey</span><span class="sxs-lookup"><span data-stu-id="b35f9-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="b35f9-123">Para cada entidad debe especificar una propiedad **PartitionKey** y **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="b35f9-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="b35f9-124">Estos son los identificadores únicos de las entidades y juntos forman la clave principal de una entidad.</span><span class="sxs-lookup"><span data-stu-id="b35f9-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="b35f9-125">Puede realizar consultas mediante estos valores de forma mucho más rápida que si consulta cualquier otra propiedad de la entidad ya que estas propiedades son las únicas que se indexan.</span><span class="sxs-lookup"><span data-stu-id="b35f9-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="b35f9-126">Table Service usa **PartitionKey** para distribuir de forma inteligente las entidades de tabla entre los nodos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b35f9-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="b35f9-127">Las entidades con la misma **PartitionKey** se almacenan en el mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="b35f9-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="b35f9-128">**RowKey** es el identificador exclusivo de la entidad de la partición a la que pertenece.</span><span class="sxs-lookup"><span data-stu-id="b35f9-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="b35f9-129">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="b35f9-129">Update an entity</span></span>

<span data-ttu-id="b35f9-130">Para actualizar todos los valores de propiedad de una entidad, llame al método [update_entity][py_update_entity].</span><span class="sxs-lookup"><span data-stu-id="b35f9-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="b35f9-131">Este ejemplo muestra cómo reemplazar una entidad existente con una versión actualizada:</span><span class="sxs-lookup"><span data-stu-id="b35f9-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="b35f9-132">Si la entidad que se está actualizando no existe, la operación de actualización generará un error.</span><span class="sxs-lookup"><span data-stu-id="b35f9-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="b35f9-133">Si desea almacenar una entidad independientemente de si existe o no, use [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="b35f9-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="b35f9-134">En el siguiente ejemplo, la primera llamada reemplazará la entidad existente.</span><span class="sxs-lookup"><span data-stu-id="b35f9-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="b35f9-135">La segunda llamada insertará una nueva entidad, debido a que en la tabla no existe ninguna entidad con PartitionKey y RowKey especificados.</span><span class="sxs-lookup"><span data-stu-id="b35f9-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="b35f9-136">El método [update_entity][py_update_entity] reemplaza todas las propiedades y valores de una entidad existente y también se puede usar para quitar las propiedades de otra de ellas.</span><span class="sxs-lookup"><span data-stu-id="b35f9-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="b35f9-137">Puede usar el método [merge_entity][py_merge_entity] para actualizar una entidad existente con valores de propiedad nuevos o modificados sin reemplazar completamente la entidad.</span><span class="sxs-lookup"><span data-stu-id="b35f9-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="b35f9-138">Modificación de varias entidades</span><span class="sxs-lookup"><span data-stu-id="b35f9-138">Modify multiple entities</span></span>

<span data-ttu-id="b35f9-139">Para garantizar el procesamiento atómico de una solicitud por parte de Table Service, puede enviar varias operaciones en un lote.</span><span class="sxs-lookup"><span data-stu-id="b35f9-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="b35f9-140">En primer lugar, use la clase [TableBatch][py_TableBatch] para agregar varias operaciones a un único lote.</span><span class="sxs-lookup"><span data-stu-id="b35f9-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="b35f9-141">A continuación, llame a [TableService][py_TableService].[commit_batch][py_commit_batch] para enviar las operaciones de una operación atómica.</span><span class="sxs-lookup"><span data-stu-id="b35f9-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="b35f9-142">Todas las entidades que desea modificar del lote deben estar en la misma partición.</span><span class="sxs-lookup"><span data-stu-id="b35f9-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="b35f9-143">En este ejemplo se agregan dos entidades juntas en un lote:</span><span class="sxs-lookup"><span data-stu-id="b35f9-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="b35f9-144">Los lotes también pueden usarse con la sintaxis de administrador de contexto:</span><span class="sxs-lookup"><span data-stu-id="b35f9-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="b35f9-145">Consulta de una entidad</span><span class="sxs-lookup"><span data-stu-id="b35f9-145">Query for an entity</span></span>

<span data-ttu-id="b35f9-146">Para consultar una entidad de una tabla, pase sus propiedades PartitionKey y RowKey al método [TableService][py_TableService].[get_entity][py_get_entity].</span><span class="sxs-lookup"><span data-stu-id="b35f9-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="b35f9-147">Consulta de un conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="b35f9-147">Query a set of entities</span></span>

<span data-ttu-id="b35f9-148">Puede consultar un conjunto de entidades proporcionando una cadena de filtro con el parámetro **filter**.</span><span class="sxs-lookup"><span data-stu-id="b35f9-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="b35f9-149">En este ejemplo se buscan todas las tareas en Seattle mediante la aplicación de un filtro en PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="b35f9-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="b35f9-150">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="b35f9-150">Query a subset of entity properties</span></span>

<span data-ttu-id="b35f9-151">También puede restringir qué propiedades se devuelven para cada entidad en una consulta.</span><span class="sxs-lookup"><span data-stu-id="b35f9-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="b35f9-152">Esta técnica, denominada *proyección*, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades o conjuntos de resultados de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="b35f9-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="b35f9-153">Use el parámetro **select** y pase los nombres de las propiedades que desea que se devuelvan al cliente.</span><span class="sxs-lookup"><span data-stu-id="b35f9-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="b35f9-154">La consulta del código siguiente devuelve solo las descripciones de las entidades de la tabla.</span><span class="sxs-lookup"><span data-stu-id="b35f9-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="b35f9-155">El siguiente fragmento de código funciona solo con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b35f9-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="b35f9-156">Esto no es compatible con el emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b35f9-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="b35f9-157">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="b35f9-157">Delete an entity</span></span>

<span data-ttu-id="b35f9-158">Elimine una entidad pasando sus propiedades PartitionKey y RowKey al método [delete_entity][py_delete_entity].</span><span class="sxs-lookup"><span data-stu-id="b35f9-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="b35f9-159">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="b35f9-159">Delete a table</span></span>

<span data-ttu-id="b35f9-160">Si ya no necesita una tabla ni ninguna de las entidades dentro de ella, llame al método [delete_table][py_delete_table] para eliminar permanentemente la tabla de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b35f9-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="b35f9-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b35f9-161">Next steps</span></span>

* [<span data-ttu-id="b35f9-162">Referencia del SDK de Azure Storage para la API de Python</span><span class="sxs-lookup"><span data-stu-id="b35f9-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="b35f9-163">SDK de Azure Storage para Python</span><span class="sxs-lookup"><span data-stu-id="b35f9-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="b35f9-164">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="b35f9-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="b35f9-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): una aplicación gratuita y multiplataforma para trabajar visualmente con datos de Azure Storage en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="b35f9-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
