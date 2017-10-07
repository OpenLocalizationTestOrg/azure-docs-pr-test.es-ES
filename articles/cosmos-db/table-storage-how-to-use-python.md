---
title: aaaHow toouse almacenamiento de tabla de Azure con Python | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
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
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a>¿Cómo toouse almacenamiento de tablas en Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Esta guía le mostrará cómo tooperform comunes escenarios de almacenamiento de tabla de Azure en Python utilizando Hola [SDK de almacenamiento de Microsoft Azure para Python](https://github.com/Azure/azure-storage-python). escenarios de Hello descritos incluyen crear y eliminar una tabla, insertar y consultar entidades.

Mientras se tratan los escenarios de hello en este tutorial, puede ser conveniente toorefer toohello [SDK de almacenamiento de Azure para la referencia de la API de Python](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Instalar Hola SDK de almacenamiento de Azure para Python

Una vez que haya creado una cuenta de almacenamiento, el siguiente paso es hello tooinstall [SDK de almacenamiento de Microsoft Azure para Python](https://github.com/Azure/azure-storage-python). Para obtener más información acerca de cómo instalar hello SDK, consulte toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) archivo Hola SDK de almacenamiento para el repositorio de Python en GitHub.

## <a name="create-a-table"></a>Creación de una tabla

toowork con hello servicio tabla de Azure de Python, debe importar hello [TableService] [ py_TableService] módulo. Puesto que trabajará con entidades de tabla, también tendrá que hello [entidad] [ py_Entity] clase. Agregue este código cerca de la parte superior de hello su tooimport de archivo Python:

```python
from azure.storage.table import TableService, Entity
```

Cree un objeto [TableService][py_TableService] mediante la transmisión del nombre de la cuenta de almacenamiento y la clave de cuenta. Reemplace `myaccount` y `mykey` con su nombre de cuenta y la clave y la llamada [create_table] [ py_create_table] toocreate tabla de hello en el almacenamiento de Azure.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad

tooadd una entidad, se crea primero un objeto que representa la entidad, a continuación, pase Hola objeto toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] método. objeto de entidad de Hello puede ser un diccionario o un objeto de tipo [entidad][py_Entity]y define los nombres de propiedad y valores de la entidad. Cada entidad debe incluir Hola necesario [PartitionKey y RowKey](#partitionkey-and-rowkey) propiedades, en suma tooany otras propiedades se definen para la entidad de Hola.

Este ejemplo crea un objeto de diccionario que representa una entidad, a continuación, lo pasa toohello [insert_entity] [ py_insert_entity] método tooadd se toohello tabla:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Este ejemplo se crea un [entidad] [ py_Entity] objeto, a continuación, pasa toohello [insert_entity] [ py_insert_entity] método tooadd se toohello tabla:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey y RowKey

Para cada entidad debe especificar una propiedad **PartitionKey** y **RowKey**. Estos son identificadores únicos de Hola de las entidades, como juntos forman la clave principal de Hola de una entidad. Puede realizar consultas mediante estos valores de forma mucho más rápida que si consulta cualquier otra propiedad de la entidad ya que estas propiedades son las únicas que se indexan.

Hola servicio tabla usa **PartitionKey** toointelligently distribuir las entidades de tabla entre nodos de almacenamiento. Las entidades que tienen Hola mismo **PartitionKey** se almacenan en hello mismo nodo. **RowKey** es Hola identificador único de entidad de hello dentro de la partición de Hola que pertenece.

## <a name="update-an-entity"></a>Actualización de una entidad

todos los tooupdate de valores de propiedad de una entidad, llame a hello [update_entity] [ py_update_entity] método. Este ejemplo se muestra cómo tooreplace una entidad existente con una versión actualizada:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Si aún no existe la entidad de Hola que se está actualizando, se producirá un error en operación de actualización de Hola. Si desea toostore una entidad si existe o no, use [insert_or_replace_entity][py_insert_or_replace_entity]. En el siguiente ejemplo de Hola, primera llamada de hello reemplazará entidad existente Hola. segunda llamada de Hello insertará una nueva entidad, ya que ninguna entidad con hello especificado PartitionKey y RowKey existe en la tabla de Hola.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Hola [update_entity] [ py_update_entity] método reemplaza todas las propiedades y valores de una entidad existente, que también puede utilizar las propiedades de tooremove de una entidad existente. Puede usar hello [merge_entity] [ py_merge_entity] método tooupdate una entidad existente con valores de propiedad nuevos o modificados sin reemplazar completamente entidad Hola.

## <a name="modify-multiple-entities"></a>Modificación de varias entidades

tooensure Hola procesamiento atómico de una solicitud de servicio de la tabla de hello, puede enviar varias operaciones en un lote. En primer lugar, utilice hello [TableBatch] [ py_TableBatch] clase tooadd varias operaciones tooa único por lotes. A continuación, llame a [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit operaciones de hello en una operación atómica. Todos los toobe entidades modificado en el lote debe estar en hello misma partición.

En este ejemplo se agregan dos entidades juntas en un lote:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Lotes también pueden utilizarse con la sintaxis de administrador de contexto de hello:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Consulta de una entidad

tooquery para una entidad en una tabla, pasar su toohello PartitionKey y RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] método.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Consulta de un conjunto de entidades

Puede consultar un conjunto de entidades proporcionando una cadena de filtro con hello **filtro** parámetro. En este ejemplo se buscan todas las tareas en Seattle mediante la aplicación de un filtro en PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Consulta de un subconjunto de propiedades de las entidades

También puede restringir qué propiedades se devuelven para cada entidad en una consulta. Esta técnica, denominada *proyección*, reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades o conjuntos de resultados de gran tamaño. Hola de uso **seleccione** toohello cliente devuelven los nombres de Hola de parámetro y pase de propiedades de Hola que desee.

consulta de Hello en el siguiente código de hello devuelve solo las descripciones de Hola de entidades de tabla de Hola.

> [!NOTE]
> Hola siguiente fragmento de código funciona sólo con hello almacenamiento de Azure. No se admite con el emulador de almacenamiento de Hola.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Eliminación de una entidad

Eliminar una entidad pasando su toohello PartitionKey y RowKey [delete_entity] [ py_delete_entity] método.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Eliminación de una tabla

Si ya no necesita una tabla o cualquiera de las entidades de hello dentro de ella, llame a hello [delete_table] [ py_delete_table] método toopermanently Eliminar tabla de Hola desde el almacenamiento de Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Pasos siguientes

* [Referencia del SDK de Azure Storage para la API de Python](https://azure-storage.readthedocs.io/en/latest/index.html)
* [SDK de Azure Storage para Python](https://github.com/Azure/azure-storage-python)
* [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): una aplicación gratuita y multiplataforma para trabajar visualmente con datos de Azure Storage en Windows, Mac OS y Linux.

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
