---
title: aaaHow toouse almacenamiento de tablas de Azure de Ruby | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>¿Cómo toouse almacenamiento de tablas de Azure de Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio tabla de Azure. ejemplos de Hola se escriben con hello API Ruby. Hello escenarios descritos se incluyen **crear y eliminar una tabla, insertar y consultar entidades de una tabla**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Creación de una aplicación de Ruby
Para obtener instrucciones de cómo toocreate una aplicación Ruby, consulte [Ruby en la aplicación Web de raíles en una máquina virtual de Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar el almacenamiento de aplicación tooaccess
toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquetes de azure que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios de REST de almacenamiento de Hola.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use el paquete de RubyGems tooobtain Hola
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Tipo de **azure de la instalación de indicador** en el indicador de hello comando ventana tooinstall hello y dependencias.

### <a name="import-hello-package"></a>Importar paquete de Hola
Utilice el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de almacenamiento de Azure
Hello azure módulo leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_acceso\_clave**para obtener información necesaria la cuenta de almacenamiento de Azure de tooconnect tooyour. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::TableService** con hello siguiente código:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Navegar por cuenta de almacenamiento toohello que desea toouse.
3. En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.
4. En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso. Puede usar cualquiera de estas.
5. Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.

Estos valores desde un almacenamiento clásico tooobtain tenga en cuenta en el portal de Azure clásico hello:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegar por cuenta de almacenamiento toohello que desea toouse.
3. Haga clic en **administrar claves de acceso** final Hola Hola del panel de exploración.
4. En el cuadro de diálogo emergente de hello, verá el nombre de cuenta de almacenamiento de hello, clave de acceso principal y clave de acceso secundaria. Para las claves de acceso, puede usar Hola principal o secundario de Hola.
5. Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.

## <a name="create-a-table"></a>Creación de una tabla
Hola **Azure::TableService** objeto le permite trabajar con tablas y entidades. toocreate una tabla, utilice hello **crear\_table()** método. Hello en el ejemplo siguiente se crea una tabla o imprime Hola error si no hay ninguno.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
tooadd una entidad, primero cree un objeto de hash que define las propiedades de entidad. Tenga en cuenta que para cada entidad debe especificar valores en **PartitionKey** y **RowKey**. Estos son identificadores únicos de las entidades de Hola y son valores que se pueden consultar mucho más rápidamente que las otras propiedades. Almacenamiento de Azure usa **PartitionKey** tooautomatically distribuir las entidades de la tabla de hello sobre muchos nodos de almacenamiento. Las entidades con Hola mismo **PartitionKey** se almacenan en hello mismo nodo. Hola **RowKey** es Hola identificador único de entidad de hello dentro de la partición de Hola que pertenece.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Actualización de una entidad
Hay varios métodos a disponible tooupdate una entidad existente:

* **update\_entity():** actualiza una entidad existente reemplazándola.
* **mezcla\_entity():** actualiza una entidad existente mediante la combinación de nuevos valores de propiedad de entidad existente Hola.
* **insert\_or\_merge\_entity():** actualiza una entidad existente reemplazándola. Si no hay entidades, se insertará una nueva.
* **Insertar\_o\_reemplazar\_entity():** actualiza una entidad existente mediante la combinación de nuevos valores de propiedad de entidad existente Hola. Si no hay entidades, se insertará una nueva.

Hello en el ejemplo siguiente se muestra cómo actualizar una entidad utilizando **actualizar\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Con **actualizar\_entity()** y **mezcla\_entity()**, si no existe la entidad de Hola que va a actualizar, a continuación, se producirá un error en la operación de actualización de Hola. Por lo tanto, si desea toostore una entidad, independientemente de si ya existe, deberían usar **insertar\_o\_reemplazar\_entity()** o **insertar\_o \_mezcla\_entity()**.

## <a name="work-with-groups-of-entities"></a>Trabajo con grupos de entidades
A veces tiene sentido toosubmit varias operaciones juntos en un lote tooensure atómica de procesamiento por servidor hello. tooaccomplish, crear primero un **lote** objeto y, a continuación, usar hello **ejecutar\_batch()** método en **TableService**. Hello en el ejemplo siguiente se muestra cómo enviar dos entidades con RowKey 2 y 3 en un lote. Observe que solo funciona para las entidades con Hola misma PartitionKey.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Consulta de una entidad
una entidad en una tabla, use hello tooquery **obtener\_entity()** método, pasando el nombre de la tabla de hello, **PartitionKey** y **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Consulta de un conjunto de entidades
tooquery un conjunto de entidades en una tabla, cree un objeto de hash de consulta y usar hello **consulta\_entities()** método. Hello en el ejemplo siguiente se muestra cómo obtener todas las entidades de hello con hello mismo **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Si el conjunto de resultados de hello es demasiado grande para una única consulta tooreturn, se devolverá un token de continuación que se puede utilizar las páginas siguientes tooretrieve.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Consulta de un subconjunto de propiedades de las entidades
Una tabla de tooa de consulta puede recuperar solo unas pocas propiedades de una entidad. Esta técnica, denominada "proyección", reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño. Cláusula select Hola de uso y los nombres de Hola de paso de Hola propiedades le gustaría toobring sobre toohello cliente.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Eliminación de una entidad
toodelete una entidad, use hello **eliminar\_entity()** método. Debe toopass en nombre de Hola de tabla de Hola que contiene la entidad de hello, hello PartitionKey y RowKey de entidad de Hola.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Eliminación de una tabla
toodelete una tabla, utilice hello **eliminar\_table()** método y pase el nombre de Hola de Hola tabla desea toodelete.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Pasos siguientes

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* [SDK de Azure para Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub

