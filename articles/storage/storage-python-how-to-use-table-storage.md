---
title: aaaHow toouse almacenamiento de tabla de Azure con Python | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="df258-103">¿Cómo toouse almacenamiento de tablas en Python</span><span class="sxs-lookup"><span data-stu-id="df258-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="df258-104">Esta guía le mostrará cómo tooperform comunes escenarios de almacenamiento de tabla de Azure en Python utilizando Hola [SDK de almacenamiento de Microsoft Azure para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="df258-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="df258-105">escenarios de Hello descritos incluyen crear y eliminar una tabla, insertar y consultar entidades.</span><span class="sxs-lookup"><span data-stu-id="df258-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="df258-106">Mientras se tratan los escenarios de hello en este tutorial, puede ser conveniente toorefer toohello [SDK de almacenamiento de Azure para la referencia de la API de Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="df258-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="df258-107">Instalar Hola SDK de almacenamiento de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="df258-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="df258-108">Una vez que haya creado una cuenta de almacenamiento, el siguiente paso es hello tooinstall [SDK de almacenamiento de Microsoft Azure para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="df258-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="df258-109">Para obtener más información acerca de cómo instalar hello SDK, consulte toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) archivo Hola SDK de almacenamiento para el repositorio de Python en GitHub.</span><span class="sxs-lookup"><span data-stu-id="df258-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="df258-110">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="df258-110">Create a table</span></span>

<span data-ttu-id="df258-111">toowork con hello servicio tabla de Azure de Python, debe importar hello [TableService] [ py_TableService] módulo.</span><span class="sxs-lookup"><span data-stu-id="df258-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="df258-112">Puesto que trabajará con entidades de tabla, también tendrá que hello [entidad] [ py_Entity] clase.</span><span class="sxs-lookup"><span data-stu-id="df258-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="df258-113">Agregue este código cerca de la parte superior de hello su tooimport de archivo Python:</span><span class="sxs-lookup"><span data-stu-id="df258-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="df258-114">Cree un objeto [TableService][py_TableService] mediante la transmisión del nombre de la cuenta de almacenamiento y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="df258-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="df258-115">Reemplace `myaccount` y `mykey` con su nombre de cuenta y la clave y la llamada [create_table] [ py_create_table] toocreate tabla de hello en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="df258-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="df258-116">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="df258-116">Add an entity tooa table</span></span>

<span data-ttu-id="df258-117">tooadd una entidad, se crea primero un objeto que representa la entidad, a continuación, pase Hola objeto toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] método.</span><span class="sxs-lookup"><span data-stu-id="df258-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="df258-118">objeto de entidad de Hello puede ser un diccionario o un objeto de tipo [entidad][py_Entity]y define los nombres de propiedad y valores de la entidad.</span><span class="sxs-lookup"><span data-stu-id="df258-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="df258-119">Cada entidad debe incluir Hola necesario [PartitionKey y RowKey](#partitionkey-and-rowkey) propiedades, en suma tooany otras propiedades se definen para la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="df258-120">Este ejemplo crea un objeto de diccionario que representa una entidad, a continuación, lo pasa toohello [insert_entity] [ py_insert_entity] método tooadd se toohello tabla:</span><span class="sxs-lookup"><span data-stu-id="df258-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="df258-121">Este ejemplo se crea un [entidad] [ py_Entity] objeto, a continuación, pasa toohello [insert_entity] [ py_insert_entity] método tooadd se toohello tabla:</span><span class="sxs-lookup"><span data-stu-id="df258-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="df258-122">PartitionKey y RowKey</span><span class="sxs-lookup"><span data-stu-id="df258-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="df258-123">Para cada entidad debe especificar una propiedad **PartitionKey** y **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="df258-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="df258-124">Estos son identificadores únicos de Hola de las entidades, como juntos forman la clave principal de Hola de una entidad.</span><span class="sxs-lookup"><span data-stu-id="df258-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="df258-125">Puede realizar consultas mediante estos valores de forma mucho más rápida que si consulta cualquier otra propiedad de la entidad ya que estas propiedades son las únicas que se indexan.</span><span class="sxs-lookup"><span data-stu-id="df258-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="df258-126">Hola servicio tabla usa **PartitionKey** toointelligently distribuir las entidades de tabla entre nodos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="df258-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="df258-127">Las entidades que tienen Hola mismo **PartitionKey** se almacenan en hello mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="df258-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="df258-128">**RowKey** es Hola identificador único de entidad de hello dentro de la partición de Hola que pertenece.</span><span class="sxs-lookup"><span data-stu-id="df258-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="df258-129">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="df258-129">Update an entity</span></span>

<span data-ttu-id="df258-130">todos los tooupdate de valores de propiedad de una entidad, llame a hello [update_entity] [ py_update_entity] método.</span><span class="sxs-lookup"><span data-stu-id="df258-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="df258-131">Este ejemplo se muestra cómo tooreplace una entidad existente con una versión actualizada:</span><span class="sxs-lookup"><span data-stu-id="df258-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="df258-132">Si aún no existe la entidad de Hola que se está actualizando, se producirá un error en operación de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="df258-133">Si desea toostore una entidad si existe o no, use [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="df258-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="df258-134">En el siguiente ejemplo de Hola, primera llamada de hello reemplazará entidad existente Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="df258-135">segunda llamada de Hello insertará una nueva entidad, ya que ninguna entidad con hello especificado PartitionKey y RowKey existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="df258-136">Hola [update_entity] [ py_update_entity] método reemplaza todas las propiedades y valores de una entidad existente, que también puede utilizar las propiedades de tooremove de una entidad existente.</span><span class="sxs-lookup"><span data-stu-id="df258-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="df258-137">Puede usar hello [merge_entity] [ py_merge_entity] método tooupdate una entidad existente con valores de propiedad nuevos o modificados sin reemplazar completamente entidad Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="df258-138">Modificación de varias entidades</span><span class="sxs-lookup"><span data-stu-id="df258-138">Modify multiple entities</span></span>

<span data-ttu-id="df258-139">tooensure Hola procesamiento atómico de una solicitud de servicio de la tabla de hello, puede enviar varias operaciones en un lote.</span><span class="sxs-lookup"><span data-stu-id="df258-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="df258-140">En primer lugar, utilice hello [TableBatch] [ py_TableBatch] clase tooadd varias operaciones tooa único por lotes.</span><span class="sxs-lookup"><span data-stu-id="df258-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="df258-141">A continuación, llame a [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit operaciones de hello en una operación atómica.</span><span class="sxs-lookup"><span data-stu-id="df258-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="df258-142">Todos los toobe entidades modificado en el lote debe estar en hello misma partición.</span><span class="sxs-lookup"><span data-stu-id="df258-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="df258-143">En este ejemplo se agregan dos entidades juntas en un lote:</span><span class="sxs-lookup"><span data-stu-id="df258-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="df258-144">Lotes también pueden utilizarse con la sintaxis de administrador de contexto de hello:</span><span class="sxs-lookup"><span data-stu-id="df258-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="df258-145">Consulta de una entidad</span><span class="sxs-lookup"><span data-stu-id="df258-145">Query for an entity</span></span>

<span data-ttu-id="df258-146">tooquery para una entidad en una tabla, pasar su toohello PartitionKey y RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] método.</span><span class="sxs-lookup"><span data-stu-id="df258-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="df258-147">Consulta de un conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="df258-147">Query a set of entities</span></span>

<span data-ttu-id="df258-148">Puede consultar un conjunto de entidades proporcionando una cadena de filtro con hello **filtro** parámetro.</span><span class="sxs-lookup"><span data-stu-id="df258-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="df258-149">En este ejemplo se buscan todas las tareas en Seattle mediante la aplicación de un filtro en PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="df258-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="df258-150">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="df258-150">Query a subset of entity properties</span></span>

<span data-ttu-id="df258-151">También puede restringir qué propiedades se devuelven para cada entidad en una consulta.</span><span class="sxs-lookup"><span data-stu-id="df258-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="df258-152">Esta técnica, denominada *proyección*, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades o conjuntos de resultados de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="df258-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="df258-153">Hola de uso **seleccione** toohello cliente devuelven los nombres de Hola de parámetro y pase de propiedades de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="df258-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="df258-154">consulta de Hello en el siguiente código de hello devuelve solo las descripciones de Hola de entidades de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="df258-155">Hola siguiente fragmento de código funciona sólo con hello almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="df258-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="df258-156">No se admite con el emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="df258-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="df258-157">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="df258-157">Delete an entity</span></span>

<span data-ttu-id="df258-158">Eliminar una entidad pasando su toohello PartitionKey y RowKey [delete_entity] [ py_delete_entity] método.</span><span class="sxs-lookup"><span data-stu-id="df258-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="df258-159">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="df258-159">Delete a table</span></span>

<span data-ttu-id="df258-160">Si ya no necesita una tabla o cualquiera de las entidades de hello dentro de ella, llame a hello [delete_table] [ py_delete_table] método toopermanently Eliminar tabla de Hola desde el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="df258-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="df258-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df258-161">Next steps</span></span>

* [<span data-ttu-id="df258-162">Referencia del SDK de Azure Storage para la API de Python</span><span class="sxs-lookup"><span data-stu-id="df258-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="df258-163">SDK de Azure Storage para Python</span><span class="sxs-lookup"><span data-stu-id="df258-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="df258-164">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="df258-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="df258-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): una aplicación gratuita y multiplataforma para trabajar visualmente con datos de Azure Storage en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="df258-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
