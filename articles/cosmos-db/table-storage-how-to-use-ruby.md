---
title: aaaHow toouse almacenamiento de tablas de Azure de Ruby | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="8b99c-103">¿Cómo toouse almacenamiento de tablas de Azure de Ruby</span><span class="sxs-lookup"><span data-stu-id="8b99c-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="8b99c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8b99c-104">Overview</span></span>
<span data-ttu-id="8b99c-105">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b99c-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="8b99c-106">ejemplos de Hola se escriben con hello API Ruby.</span><span class="sxs-lookup"><span data-stu-id="8b99c-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="8b99c-107">Hello escenarios descritos se incluyen **crear y eliminar una tabla, insertar y consultar entidades de una tabla**.</span><span class="sxs-lookup"><span data-stu-id="8b99c-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="8b99c-108">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="8b99c-108">Create a Ruby application</span></span>
<span data-ttu-id="8b99c-109">Para obtener instrucciones de cómo toocreate una aplicación Ruby, consulte [Ruby en la aplicación Web de raíles en una máquina virtual de Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b99c-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="8b99c-110">Configurar el almacenamiento de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="8b99c-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="8b99c-111">toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquetes de azure que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios de REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="8b99c-112">Use el paquete de RubyGems tooobtain Hola</span><span class="sxs-lookup"><span data-stu-id="8b99c-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="8b99c-113">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="8b99c-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="8b99c-114">Tipo de **azure de la instalación de indicador** en el indicador de hello comando ventana tooinstall hello y dependencias.</span><span class="sxs-lookup"><span data-stu-id="8b99c-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="8b99c-115">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="8b99c-115">Import hello package</span></span>
<span data-ttu-id="8b99c-116">Utilice el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="8b99c-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="8b99c-117">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8b99c-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="8b99c-118">Hello azure módulo leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_acceso\_clave**para obtener información necesaria la cuenta de almacenamiento de Azure de tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b99c-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="8b99c-119">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::TableService** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8b99c-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="8b99c-120">tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="8b99c-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="8b99c-121">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b99c-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8b99c-122">Navegar por cuenta de almacenamiento toohello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="8b99c-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="8b99c-123">En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="8b99c-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="8b99c-124">En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="8b99c-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="8b99c-125">Puede usar cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="8b99c-125">You can use either of these.</span></span>
5. <span data-ttu-id="8b99c-126">Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="8b99c-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="8b99c-127">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="8b99c-127">Create a table</span></span>
<span data-ttu-id="8b99c-128">Hola **Azure::TableService** objeto le permite trabajar con tablas y entidades.</span><span class="sxs-lookup"><span data-stu-id="8b99c-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="8b99c-129">toocreate una tabla, utilice hello **crear\_table()** método.</span><span class="sxs-lookup"><span data-stu-id="8b99c-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="8b99c-130">Hello en el ejemplo siguiente se crea una tabla o imprime Hola error si no hay ninguno.</span><span class="sxs-lookup"><span data-stu-id="8b99c-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="8b99c-131">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="8b99c-131">Add an entity tooa table</span></span>
<span data-ttu-id="8b99c-132">tooadd una entidad, primero cree un objeto de hash que define las propiedades de entidad.</span><span class="sxs-lookup"><span data-stu-id="8b99c-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="8b99c-133">Tenga en cuenta que para cada entidad debe especificar valores en **PartitionKey** y **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="8b99c-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="8b99c-134">Estos son identificadores únicos de las entidades de Hola y son valores que se pueden consultar mucho más rápidamente que las otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="8b99c-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="8b99c-135">Almacenamiento de Azure usa **PartitionKey** tooautomatically distribuir las entidades de la tabla de hello sobre muchos nodos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8b99c-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="8b99c-136">Las entidades con Hola mismo **PartitionKey** se almacenan en hello mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="8b99c-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="8b99c-137">Hola **RowKey** es Hola identificador único de entidad de hello dentro de la partición de Hola que pertenece.</span><span class="sxs-lookup"><span data-stu-id="8b99c-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="8b99c-138">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="8b99c-138">Update an entity</span></span>
<span data-ttu-id="8b99c-139">Hay varios métodos a disponible tooupdate una entidad existente:</span><span class="sxs-lookup"><span data-stu-id="8b99c-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="8b99c-140">**update\_entity():** actualiza una entidad existente reemplazándola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="8b99c-141">**mezcla\_entity():** actualiza una entidad existente mediante la combinación de nuevos valores de propiedad de entidad existente Hola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="8b99c-142">**insert\_or\_merge\_entity():** actualiza una entidad existente reemplazándola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="8b99c-143">Si no hay entidades, se insertará una nueva.</span><span class="sxs-lookup"><span data-stu-id="8b99c-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="8b99c-144">**Insertar\_o\_reemplazar\_entity():** actualiza una entidad existente mediante la combinación de nuevos valores de propiedad de entidad existente Hola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="8b99c-145">Si no hay entidades, se insertará una nueva.</span><span class="sxs-lookup"><span data-stu-id="8b99c-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="8b99c-146">Hello en el ejemplo siguiente se muestra cómo actualizar una entidad utilizando **actualizar\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="8b99c-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="8b99c-147">Con **actualizar\_entity()** y **mezcla\_entity()**, si no existe la entidad de Hola que va a actualizar, a continuación, se producirá un error en la operación de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="8b99c-148">Por lo tanto, si desea toostore una entidad, independientemente de si ya existe, deberían usar **insertar\_o\_reemplazar\_entity()** o **insertar\_o \_mezcla\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="8b99c-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="8b99c-149">Trabajo con grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="8b99c-149">Work with groups of entities</span></span>
<span data-ttu-id="8b99c-150">A veces tiene sentido toosubmit varias operaciones juntos en un lote tooensure atómica de procesamiento por servidor hello.</span><span class="sxs-lookup"><span data-stu-id="8b99c-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="8b99c-151">tooaccomplish, crear primero un **lote** objeto y, a continuación, usar hello **ejecutar\_batch()** método en **TableService**.</span><span class="sxs-lookup"><span data-stu-id="8b99c-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="8b99c-152">Hello en el ejemplo siguiente se muestra cómo enviar dos entidades con RowKey 2 y 3 en un lote.</span><span class="sxs-lookup"><span data-stu-id="8b99c-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="8b99c-153">Observe que solo funciona para las entidades con Hola misma PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="8b99c-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="8b99c-154">Consulta de una entidad</span><span class="sxs-lookup"><span data-stu-id="8b99c-154">Query for an entity</span></span>
<span data-ttu-id="8b99c-155">una entidad en una tabla, use hello tooquery **obtener\_entity()** método, pasando el nombre de la tabla de hello, **PartitionKey** y **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="8b99c-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="8b99c-156">Consulta de un conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="8b99c-156">Query a set of entities</span></span>
<span data-ttu-id="8b99c-157">tooquery un conjunto de entidades en una tabla, cree un objeto de hash de consulta y usar hello **consulta\_entities()** método.</span><span class="sxs-lookup"><span data-stu-id="8b99c-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="8b99c-158">Hello en el ejemplo siguiente se muestra cómo obtener todas las entidades de hello con hello mismo **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="8b99c-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="8b99c-159">Si el conjunto de resultados de hello es demasiado grande para una única consulta tooreturn, se devolverá un token de continuación que se puede utilizar las páginas siguientes tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="8b99c-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="8b99c-160">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="8b99c-160">Query a subset of entity properties</span></span>
<span data-ttu-id="8b99c-161">Una tabla de tooa de consulta puede recuperar solo unas pocas propiedades de una entidad.</span><span class="sxs-lookup"><span data-stu-id="8b99c-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="8b99c-162">Esta técnica, denominada "proyección", reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="8b99c-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="8b99c-163">Cláusula select Hola de uso y los nombres de Hola de paso de Hola propiedades le gustaría toobring sobre toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="8b99c-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="8b99c-164">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="8b99c-164">Delete an entity</span></span>
<span data-ttu-id="8b99c-165">toodelete una entidad, use hello **eliminar\_entity()** método.</span><span class="sxs-lookup"><span data-stu-id="8b99c-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="8b99c-166">Debe toopass en nombre de Hola de tabla de Hola que contiene la entidad de hello, hello PartitionKey y RowKey de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b99c-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="8b99c-167">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="8b99c-167">Delete a table</span></span>
<span data-ttu-id="8b99c-168">toodelete una tabla, utilice hello **eliminar\_table()** método y pase el nombre de Hola de Hola tabla desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="8b99c-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="8b99c-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b99c-169">Next steps</span></span>

* <span data-ttu-id="8b99c-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="8b99c-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="8b99c-171">[SDK de Azure para Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub</span><span class="sxs-lookup"><span data-stu-id="8b99c-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

