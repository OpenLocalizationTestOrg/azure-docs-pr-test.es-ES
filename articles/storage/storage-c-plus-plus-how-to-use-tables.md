---
title: aaaHow toouse almacenamiento de tabla (C++) | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="8b669-103">¿Cómo toouse almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="8b669-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="8b669-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8b669-104">Overview</span></span>
<span data-ttu-id="8b669-105">Esta guía le mostrará cómo tooperform escenarios comunes al usar Hola servicio de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b669-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="8b669-106">ejemplos de Hello están escritos en C++ y usar hello [biblioteca de cliente de almacenamiento de Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="8b669-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="8b669-107">Hello escenarios descritos se incluyen **crear y eliminar una tabla** y **trabajar con entidades de tabla**.</span><span class="sxs-lookup"><span data-stu-id="8b669-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="8b669-108">Destinos de esta guía Hola biblioteca de cliente de almacenamiento de Azure para C++ versión 1.0.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="8b669-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="8b669-109">Hola recomienda versión es la biblioteca de cliente de almacenamiento 2.2.0, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="8b669-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="8b669-110">Creación de una aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="8b669-110">Create a C++ application</span></span>
<span data-ttu-id="8b669-111">En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.</span><span class="sxs-lookup"><span data-stu-id="8b669-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="8b669-112">toodo por lo tanto, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b669-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="8b669-113">Hola tooinstall biblioteca de cliente de almacenamiento de Azure para C++, puede usar Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="8b669-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="8b669-114">**Linux:** siga las instrucciones de hello proporcionadas en hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="8b669-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="8b669-115">**Windows:** en Visual Studio, haga clic en **Herramientas &gt; Administrador de paquetes de NuGet &gt; Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="8b669-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="8b669-116">Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="8b669-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="8b669-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="8b669-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="8b669-118">Configurar el almacenamiento de tabla tooaccess de aplicación</span><span class="sxs-lookup"><span data-stu-id="8b669-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="8b669-119">Agregar siguiente Hola incluir parte superior de toohello de las instrucciones del archivo de C++ de Hola donde se desea que las tablas de tooaccess de las API de toouse Hola almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="8b669-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8b669-120">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8b669-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="8b669-121">Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="8b669-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8b669-122">Cuando se ejecuta una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="8b669-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="8b669-123">Usar el nombre de su almacenamiento hello y cuenta de almacenamiento clave de acceso para la cuenta de almacenamiento de Hola Hola enumerados en hello [Portal de Azure](https://portal.azure.com) para hello *AccountName* y *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="8b669-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8b669-124">Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8b669-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="8b669-125">Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="8b669-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="8b669-126">tootest la aplicación en el equipo local basado en Windows, puede usar hello Azure [emulador de almacenamiento](storage-use-emulator.md) que se instala con hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8b669-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8b669-127">emulador de almacenamiento de Hello es una utilidad que simula los servicios de Azure Blob, cola y tabla de hello disponibles en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="8b669-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="8b669-128">Hello en el ejemplo siguiente se muestra cómo se puede declarar un emulador de almacenamiento local de campo estático toohold Hola conexión cadena tooyour:</span><span class="sxs-lookup"><span data-stu-id="8b669-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="8b669-129">toostart Hola emulador de almacenamiento de Azure, haga clic en hello **iniciar** o presionen clave de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8b669-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="8b669-130">Comience a escribir **emulador de almacenamiento de Azure**y, a continuación, seleccione **emulador de almacenamiento de Microsoft Azure** de lista de Hola de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8b669-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="8b669-131">Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="8b669-132">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8b669-132">Retrieve your connection string</span></span>
<span data-ttu-id="8b669-133">Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8b669-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="8b669-134">tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede usar el método de análisis de hello.</span><span class="sxs-lookup"><span data-stu-id="8b669-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="8b669-135">A continuación, obtener una referencia tooa **cloud_table_client** de la clase, que le permite obtener objetos de referencia para las tablas y entidades almacenan dentro de hello servicio de almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="8b669-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="8b669-136">Hello código siguiente se crea un **cloud_table_client** objeto utilizando el objeto de cuenta de almacenamiento Hola recuperamos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8b669-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="8b669-137">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="8b669-137">Create a table</span></span>
<span data-ttu-id="8b669-138">Los objetos **cloud_table_client** le permiten obtener objetos de referencia para tablas y entidades.</span><span class="sxs-lookup"><span data-stu-id="8b669-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="8b669-139">Hello código siguiente se crea un **cloud_table_client** objeto y lo usa toocreate una nueva tabla.</span><span class="sxs-lookup"><span data-stu-id="8b669-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

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

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="8b669-140">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="8b669-140">Add an entity tooa table</span></span>
<span data-ttu-id="8b669-141">tooadd una tabla de tooa de entidad, cree un nuevo **table_entity** objeto y pasarlo demasiado**table_operation:: insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="8b669-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="8b669-142">Hello código siguiente usa nombre del cliente de hello como clave de fila de Hola y last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="8b669-143">Juntos, partición de una entidad y la clave de fila identifican entidad de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="8b669-144">Entidades con hello misma clave de partición se puede consultar con más rapidez que las que tienen diferentes claves de partición, pero el uso de las claves de partición diversos permite para una mayor escalabilidad de la operación paralela.</span><span class="sxs-lookup"><span data-stu-id="8b669-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="8b669-145">Para obtener más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Almacenamiento de Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="8b669-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="8b669-146">Hello código siguiente crea una nueva instancia de **table_entity** con algunos toobe de datos del cliente almacenado.</span><span class="sxs-lookup"><span data-stu-id="8b669-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="8b669-147">Hola de código siguiente llama **table_operation:: insert_entity** toocreate una **table_operation** tooinsert una entidad del objeto en una tabla, y asocia Hola nueva entidad de tabla con él.</span><span class="sxs-lookup"><span data-stu-id="8b669-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="8b669-148">Por último, llamadas código Hola Hola ejecutar el método en hello **cloud_table** objeto.</span><span class="sxs-lookup"><span data-stu-id="8b669-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="8b669-149">Hello nueva y **table_operation** envía una entidad de cliente nueva de tabla servicio tooinsert hello toohello de solicitud en la tabla de Hola "personas".</span><span class="sxs-lookup"><span data-stu-id="8b669-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

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

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8b669-150">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="8b669-150">Insert a batch of entities</span></span>
<span data-ttu-id="8b669-151">Puede insertar un lote de entidades toohello servicio tabla en una sola operación de escritura.</span><span class="sxs-lookup"><span data-stu-id="8b669-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="8b669-152">Hello código siguiente se crea un **table_batch_operation** objeto y, a continuación, agrega tres tooit de operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="8b669-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="8b669-153">Cada operación de inserción se agrega mediante la creación de un nuevo objeto de entidad, establecer sus valores, y, a continuación, llamar a Hola insert (método) en hello **table_batch_operation** entidad de hello tooassociate de objeto con una nueva operación de inserción.</span><span class="sxs-lookup"><span data-stu-id="8b669-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="8b669-154">A continuación, **cloud_table.execute** se denomina operación de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="8b669-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

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

<span data-ttu-id="8b669-155">Algunos toonote cosas en operaciones por lotes:</span><span class="sxs-lookup"><span data-stu-id="8b669-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="8b669-156">Puede realizar una too100 insert, delete, merge, replace, operaciones insert o merge y cuadro de diálogo Insertar o reemplazar en cualquier combinación en un único lote.</span><span class="sxs-lookup"><span data-stu-id="8b669-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="8b669-157">Una operación por lotes puede tener una operación de recuperación, si es la única operación de hello en el lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="8b669-158">Todas las entidades de una operación por lotes solo deben tener Hola misma clave de partición.</span><span class="sxs-lookup"><span data-stu-id="8b669-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="8b669-159">Una operación por lotes es la carga de datos de 4 MB de tooa limitado.</span><span class="sxs-lookup"><span data-stu-id="8b669-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="8b669-160">todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="8b669-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="8b669-161">tooquery una tabla para todas las entidades de una partición, use un **table_query** objeto.</span><span class="sxs-lookup"><span data-stu-id="8b669-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="8b669-162">Hello ejemplo de código siguiente especifica un filtro para las entidades donde "Smith" es la clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="8b669-163">Este ejemplo imprime campos Hola de cada entidad en la consola de toohello de resultados de consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

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

<span data-ttu-id="8b669-164">consulta de Hello en este ejemplo hace que todas las entidades de Hola que coinciden con los criterios de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="8b669-165">Si tiene tablas grandes y necesita entidades de tabla de hello toodownload a menudo, se recomienda que los datos se almacenan en blobs de almacenamiento de Azure en su lugar.</span><span class="sxs-lookup"><span data-stu-id="8b669-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="8b669-166">Recuperación de un rango de entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="8b669-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="8b669-167">Si no desea tooquery todas las entidades de hello en una partición, puede especificar un intervalo mediante la combinación de filtro de clave de partición de hello con un filtro de clave de fila.</span><span class="sxs-lookup"><span data-stu-id="8b669-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="8b669-168">Hello ejemplo de código siguiente utiliza dos tooget filtros todas las entidades de partición "Smith" donde clave de fila (nombre) de hello empieza por una letra anterior a 'E' alfabeto hello y, a continuación, imprime resultados de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="8b669-169">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="8b669-169">Retrieve a single entity</span></span>
<span data-ttu-id="8b669-170">Puede escribir una consulta tooretrieve una entidad única, específica.</span><span class="sxs-lookup"><span data-stu-id="8b669-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="8b669-171">Hola siguiente de código usa **table_operation:: retrieve_entity** cliente de hello toospecify "Jeff Smith".</span><span class="sxs-lookup"><span data-stu-id="8b669-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="8b669-172">Este método devuelve una sola entidad, en lugar de una colección y hello valor devuelto está en **table_result**.</span><span class="sxs-lookup"><span data-stu-id="8b669-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="8b669-173">Especificar claves de partición y fila en una consulta es tooretrieve de manera más rápida de hello una sola entidad de servicio de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

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

## <a name="replace-an-entity"></a><span data-ttu-id="8b669-174">una entidad</span><span class="sxs-lookup"><span data-stu-id="8b669-174">Replace an entity</span></span>
<span data-ttu-id="8b669-175">tooreplace una entidad, recuperar del servicio de tabla de hello, modificar el objeto de entidad de hello y, a continuación, guardar los cambios de hello hacer copia de servicio de la tabla de toohello.</span><span class="sxs-lookup"><span data-stu-id="8b669-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="8b669-176">Hello código siguiente cambia dirección de correo electrónico y número de teléfono de un cliente existente.</span><span class="sxs-lookup"><span data-stu-id="8b669-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="8b669-177">En lugar de llamar a **table_operation::insert_entity**, este código usa **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="8b669-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="8b669-178">Esto hace que Hola entidad toobe reemplazado totalmente en el servidor de hello, a menos que la entidad de hello en servidor hello ha cambiado desde que se recuperó, en cuyo caso se producirá un error de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="8b669-179">Este error es tooprevent la aplicación se ha sobrescrito accidentalmente un cambio realizado entre Hola recuperación y actualizar por otro componente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b669-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="8b669-180">Hello control correcto de este error es tooretrieve Hola entidad nuevo, realice los cambios (si todavía es válido) y, a continuación, realizar otra **table_operation:: replace_entity** operación.</span><span class="sxs-lookup"><span data-stu-id="8b669-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="8b669-181">Hola siguiente sección le mostrará cómo toooverride este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="8b669-181">hello next section will show you how toooverride this behavior.</span></span>  

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

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="8b669-182">Inserción o reemplazo de una entidad</span><span class="sxs-lookup"><span data-stu-id="8b669-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="8b669-183">**table_operation:: replace_entity** operaciones generarán un error si la entidad de Hola se ha modificado desde que se recuperó del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="8b669-184">Además, debe recuperar entidad Hola desde servidor hello primero en orden para **table_operation:: replace_entity** toobe correcta.</span><span class="sxs-lookup"><span data-stu-id="8b669-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="8b669-185">A veces, sin embargo, no sabe si entidad Hola existe en el servidor de Hola y valores actuales de hello almacenados en ella son irrelevantes: la actualización debe sobrescribir todos ellos.</span><span class="sxs-lookup"><span data-stu-id="8b669-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="8b669-186">tooaccomplish, usaría un **table_operation:: insert_or_replace_entity** operación.</span><span class="sxs-lookup"><span data-stu-id="8b669-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="8b669-187">Esta operación inserta la entidad de hello si no existe, o lo reemplaza si lo hace, sin tener en cuenta cuando se realizó la última actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="8b669-188">En el siguiente ejemplo de código de hello, todavía se recupera la entidad customer de Hola para Jeff Smith, pero, a continuación, se guarda servidor toohello atrás a través de **table_operation:: insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="8b669-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="8b669-189">Se sobrescribirá cualquier actualización realizada entidad toohello entre una operación de recuperación y actualización Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

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

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="8b669-190">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="8b669-190">Query a subset of entity properties</span></span>
<span data-ttu-id="8b669-191">Una tabla de tooa de consulta puede recuperar solo unas pocas propiedades de una entidad.</span><span class="sxs-lookup"><span data-stu-id="8b669-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="8b669-192">la consulta en el siguiente código de hello Hello utiliza hello **table_query:: set_select_columns** método tooreturn solo Hola direcciones de correo electrónico las entidades de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

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
> <span data-ttu-id="8b669-193">Consultar una serie de propiedades de una entidad es una operación más eficaz que recuperar todas las propiedades.</span><span class="sxs-lookup"><span data-stu-id="8b669-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="8b669-194">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="8b669-194">Delete an entity</span></span>
<span data-ttu-id="8b669-195">Puede eliminar fácilmente una entidad después de que la haya recuperado.</span><span class="sxs-lookup"><span data-stu-id="8b669-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="8b669-196">Una vez que se recupera la entidad de hello, llame a **table_operation:: delete_entity** con hello entidad toodelete.</span><span class="sxs-lookup"><span data-stu-id="8b669-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="8b669-197">A continuación, llamar a hello **cloud_table.execute** método.</span><span class="sxs-lookup"><span data-stu-id="8b669-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="8b669-198">Hello siguiente código recupera y elimina una entidad con una clave de partición "Smith" y una clave de fila de "Juan".</span><span class="sxs-lookup"><span data-stu-id="8b669-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

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

## <a name="delete-a-table"></a><span data-ttu-id="8b669-199">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="8b669-199">Delete a table</span></span>
<span data-ttu-id="8b669-200">Por último, Hola ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8b669-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="8b669-201">Una tabla que se ha eliminado estará disponible toobe vuelve a crear durante un período de tiempo tras la eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b669-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="8b669-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b669-202">Next steps</span></span>
<span data-ttu-id="8b669-203">Ahora que conoce los fundamentos de hello del almacenamiento de tabla, siga estos toolearn de vínculos más sobre el almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="8b669-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="8b669-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="8b669-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="8b669-205">¿Cómo toouse almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="8b669-205">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8b669-206">¿Cómo toouse almacenamiento de cola desde C++</span><span class="sxs-lookup"><span data-stu-id="8b669-206">How toouse Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="8b669-207">Enumeración de los recursos de Almacenamiento de Azure en C++</span><span class="sxs-lookup"><span data-stu-id="8b669-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="8b669-208">Referencia de la biblioteca de clientes de almacenamiento para C++</span><span class="sxs-lookup"><span data-stu-id="8b669-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="8b669-209">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8b669-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
