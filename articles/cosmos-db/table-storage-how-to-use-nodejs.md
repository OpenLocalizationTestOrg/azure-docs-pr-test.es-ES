---
title: almacenamiento de tablas de Azure de Node.js del aaaHow toouse | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="eda0c-103">¿Cómo toouse almacenamiento de tablas de Azure de Node.js</span><span class="sxs-lookup"><span data-stu-id="eda0c-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="eda0c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="eda0c-104">Overview</span></span>
<span data-ttu-id="eda0c-105">Este tema muestra cómo service tooperform escenarios comunes con hello tabla de Azure en una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="eda0c-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="eda0c-106">ejemplos de código de Hello en este tema se suponen que ya tiene una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="eda0c-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="eda0c-107">Para obtener información acerca de cómo toocreate una aplicación Node.js en Azure, vea cualquiera de estos temas:</span><span class="sxs-lookup"><span data-stu-id="eda0c-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="eda0c-108">Creación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="eda0c-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="eda0c-109">Compilar e implementar un tooAzure de aplicación web de Node.js mediante WebMatrix</span><span class="sxs-lookup"><span data-stu-id="eda0c-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="eda0c-110">[Compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (uso de Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="eda0c-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="eda0c-111">Configurar el almacenamiento de Azure tooaccess de aplicación</span><span class="sxs-lookup"><span data-stu-id="eda0c-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="eda0c-112">toouse almacenamiento de Azure, necesitará Hola SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="eda0c-113">Usar el Administrador de paquetes de nodo (NPM) tooinstall Hola paquete</span><span class="sxs-lookup"><span data-stu-id="eda0c-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="eda0c-114">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix) y desplazarse por las carpetas de toohello en la que creó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eda0c-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="eda0c-115">Tipo de **npm instalar almacenamiento de azure** en la ventana de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="eda0c-116">Salida de comando de hello es similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="eda0c-116">Output from hello command is similar toohello following example.</span></span>

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="eda0c-117">También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta.</span><span class="sxs-lookup"><span data-stu-id="eda0c-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="eda0c-118">Dentro de esa carpeta, encontrará hello **almacenamiento de azure** paquete, que contiene las bibliotecas de Hola que necesita almacenamiento tooaccess.</span><span class="sxs-lookup"><span data-stu-id="eda0c-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="eda0c-119">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="eda0c-119">Import hello package</span></span>
<span data-ttu-id="eda0c-120">Agregar Hola después de la parte superior de toohello de código de hello **server.js** archivo en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="eda0c-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="eda0c-121">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="eda0c-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="eda0c-122">módulo de Hello azure leerá variables de entorno de hello AZURE\_almacenamiento\_cuenta y AZURE\_almacenamiento\_acceso\_clave o AZURE\_almacenamiento\_conexión \_Cadena para la información necesaria tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="eda0c-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="eda0c-123">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a **TableService**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="eda0c-124">Para obtener un ejemplo de establecer las variables de entorno de hello en hello [portal de Azure](https://portal.azure.com) para un sitio Web de Azure, consulte [aplicación web de Node.js con Hola servicio tabla de Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="eda0c-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="eda0c-125">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="eda0c-125">Create a table</span></span>
<span data-ttu-id="eda0c-126">Hello código siguiente se crea un **TableService** objeto y lo usa toocreate una nueva tabla.</span><span class="sxs-lookup"><span data-stu-id="eda0c-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="eda0c-127">Agregue Hola siguiente cerca de la parte superior de Hola de **server.js**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="eda0c-128">Hola llamada demasiado**createTableIfNotExists** creará una nueva tabla con el nombre especificado de hello si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="eda0c-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="eda0c-129">Hello en el ejemplo siguiente se crea una nueva tabla denominada "mytable" Si aún no existe:</span><span class="sxs-lookup"><span data-stu-id="eda0c-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="eda0c-130">Hola `result.created` será `true` si se crea una nueva tabla, y `false` si Hola tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="eda0c-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="eda0c-131">Hola `response` contendrá información sobre la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="eda0c-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="eda0c-132">Filtros</span><span class="sxs-lookup"><span data-stu-id="eda0c-132">Filters</span></span>
<span data-ttu-id="eda0c-133">Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **TableService**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="eda0c-134">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:</span><span class="sxs-lookup"><span data-stu-id="eda0c-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="eda0c-135">Después de realizar su procesamiento previo en Opciones de solicitud de hello, método hello necesita toocall "siguiente", pasando una devolución de llamada con hello siguiente firma:</span><span class="sxs-lookup"><span data-stu-id="eda0c-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="eda0c-136">En esta devolución de llamada y, después de procesar hello returnObject (respuesta Hola Hola solicitud enviada toohello al servidor), la devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o simplemente invocar finalCallback en caso contrario hello tooend invocación de servicio.</span><span class="sxs-lookup"><span data-stu-id="eda0c-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="eda0c-137">Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="eda0c-138">Hola siguiente crea un **TableService** objeto que usa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="eda0c-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="eda0c-139">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="eda0c-139">Add an entity tooa table</span></span>
<span data-ttu-id="eda0c-140">tooadd una entidad, primero cree un objeto que define las propiedades de entidad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="eda0c-141">Todas las entidades deben contener una **PartitionKey** y **RowKey**, que son identificadores únicos de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="eda0c-142">**PartitionKey** -determina la partición de Hola Hola entidad se almacena en</span><span class="sxs-lookup"><span data-stu-id="eda0c-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="eda0c-143">**RowKey** : de forma única identifica la entidad de hello en partición de Hola</span><span class="sxs-lookup"><span data-stu-id="eda0c-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="eda0c-144">Tanto **PartitionKey** como **RowKey** tiene que ser valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="eda0c-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="eda0c-145">Para obtener más información, consulte [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="eda0c-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="eda0c-146">Hola aquí te mostramos un ejemplo de definición de una entidad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="eda0c-147">Tenga en cuenta que **dueDate** se define como un tipo de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="eda0c-148">Especificar tipo de hello es opcional y tipos se pueden inferir si no se especifica.</span><span class="sxs-lookup"><span data-stu-id="eda0c-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="eda0c-149">Hay también un campo **Timestamp** para cada registro; Azure lo establece cuando se inserta o actualiza una entidad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="eda0c-150">También puede usar hello **entityGenerator** toocreate entidades.</span><span class="sxs-lookup"><span data-stu-id="eda0c-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="eda0c-151">Hello en el ejemplo siguiente se crea Hola misma entidad tarea utilizando hello **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="eda0c-152">tooadd una tabla de tooyour de entidad, pasar toohello de objeto de entidad de hello **insertEntity** método.</span><span class="sxs-lookup"><span data-stu-id="eda0c-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="eda0c-153">Si es correcta, la operación de hello `result` contendrá hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de hello registro insertado y `response` contendrá información sobre la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="eda0c-154">Respuesta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eda0c-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="eda0c-155">De forma predeterminada, **insertEntity** no devuelve entidades Hola insertado como parte del programa Hola `response` información.</span><span class="sxs-lookup"><span data-stu-id="eda0c-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="eda0c-156">Si la intención de realizar otras operaciones en esta entidad, o desea obtener información de hello toocache, puede ser útil toohave devuelve como parte del programa Hola a `result`.</span><span class="sxs-lookup"><span data-stu-id="eda0c-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="eda0c-157">Para ello, puede habilitar **echoContent** de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="eda0c-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="eda0c-158">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="eda0c-158">Update an entity</span></span>
<span data-ttu-id="eda0c-159">Hay varios métodos a disponible tooupdate una entidad existente:</span><span class="sxs-lookup"><span data-stu-id="eda0c-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="eda0c-160">**replaceEntity** : actualiza una entidad que ya existe reemplazándola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="eda0c-161">**mergeEntity** -actualiza una entidad existente mediante la combinación de nuevos valores de propiedad de entidad existente Hola</span><span class="sxs-lookup"><span data-stu-id="eda0c-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="eda0c-162">**insertOrReplaceEntity** : actualiza una entidad existente reemplazándola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="eda0c-163">Si no hay entidades, se insertará una nueva.</span><span class="sxs-lookup"><span data-stu-id="eda0c-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="eda0c-164">**insertOrMergeEntity** -actualiza una entidad existente mediante la combinación de nuevos valores de propiedad Hola existente.</span><span class="sxs-lookup"><span data-stu-id="eda0c-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="eda0c-165">Si no hay entidades, se insertará una nueva.</span><span class="sxs-lookup"><span data-stu-id="eda0c-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="eda0c-166">Hello en el ejemplo siguiente se muestra cómo actualizar una entidad utilizando **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="eda0c-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="eda0c-167">De forma predeterminada, actualizar una entidad no comprueba toosee si anteriormente se han modificado los datos de Hola que se está actualizados en otro proceso.</span><span class="sxs-lookup"><span data-stu-id="eda0c-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="eda0c-168">toosupport actualizaciones simultáneas:</span><span class="sxs-lookup"><span data-stu-id="eda0c-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="eda0c-169">Obtener Hola ETag del objeto de Hola que se está actualizando.</span><span class="sxs-lookup"><span data-stu-id="eda0c-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="eda0c-170">Esto se devuelve como parte del programa Hola a `response` para todas las operaciones relacionadas con la entidad y se pueden recuperar mediante `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="eda0c-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="eda0c-171">Al realizar una operación de actualización en una entidad, agregue información de ETag Hola recuperado previamente toohello nueva entidad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="eda0c-172">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eda0c-172">For example:</span></span>
>
>       <span data-ttu-id="eda0c-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="eda0c-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="eda0c-174">Realizar la operación de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-174">Perform hello update operation.</span></span> <span data-ttu-id="eda0c-175">Si se ha modificado la entidad de hello puesto que recuperar el valor de ETag de hello, como otra instancia de la aplicación, un `error` se devolverán que indica que no se cumple la condición de actualización de hello especificado en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="eda0c-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="eda0c-176">Con **replaceEntity** y **mergeEntity**, si no existe la entidad Hola que se está actualizando, se producirá un error en la operación de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="eda0c-177">Por lo tanto, si desea toostore una entidad, independientemente de si ya existe, utilice **insertOrReplaceEntity** o **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="eda0c-178">Hola `result` para actualización correcta operaciones contendrá hello **Etag** de hello Actualizar entidad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="eda0c-179">Trabajo con grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="eda0c-179">Work with groups of entities</span></span>
<span data-ttu-id="eda0c-180">A veces tiene sentido toosubmit varias operaciones juntos en un lote tooensure atómica de procesamiento por servidor hello.</span><span class="sxs-lookup"><span data-stu-id="eda0c-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="eda0c-181">tooaccomplish que usar hello **TableBatch** clase toocreate un lote y, a continuación, usar hello **executeBatch** método **TableService** operaciones por lotes tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="eda0c-182">Hola de ejemplo siguiente se muestra cómo enviar dos entidades en un lote:</span><span class="sxs-lookup"><span data-stu-id="eda0c-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="eda0c-183">Realizó correctamente las operaciones por lotes, `result` contendrá información de cada operación de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="eda0c-184">Trabajar con operaciones por lotes</span><span class="sxs-lookup"><span data-stu-id="eda0c-184">Work with batched operations</span></span>
<span data-ttu-id="eda0c-185">Agregar operaciones por lotes tooa pueden ser inspeccionado por ver hello `operations` propiedad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="eda0c-186">También puede usar Hola siguiendo métodos toowork con operaciones:</span><span class="sxs-lookup"><span data-stu-id="eda0c-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="eda0c-187">**clear** : borra todas las operaciones de un lote</span><span class="sxs-lookup"><span data-stu-id="eda0c-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="eda0c-188">**getOperations** -Obtiene una operación del lote de Hola</span><span class="sxs-lookup"><span data-stu-id="eda0c-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="eda0c-189">**hasOperations** -devuelve true si el lote de hello contiene operaciones</span><span class="sxs-lookup"><span data-stu-id="eda0c-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="eda0c-190">**removeOperations** : quita una operación.</span><span class="sxs-lookup"><span data-stu-id="eda0c-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="eda0c-191">**tamaño** -devuelve Hola número de operaciones en lote Hola</span><span class="sxs-lookup"><span data-stu-id="eda0c-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="eda0c-192">Recuperación de una entidad por clave</span><span class="sxs-lookup"><span data-stu-id="eda0c-192">Retrieve an entity by key</span></span>
<span data-ttu-id="eda0c-193">tooreturn una entidad específica en función de hello **PartitionKey** y **RowKey**, usar hello **retrieveEntity** método.</span><span class="sxs-lookup"><span data-stu-id="eda0c-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="eda0c-194">Una vez completada, esta operación `result` contendrá entidad Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="eda0c-195">Consulta de un conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="eda0c-195">Query a set of entities</span></span>
<span data-ttu-id="eda0c-196">tooquery una tabla, utilice hello **TableQuery** toobuild una expresión de consulta mediante Hola después de las cláusulas de objeto:</span><span class="sxs-lookup"><span data-stu-id="eda0c-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="eda0c-197">**Seleccione** -Hola campos toobe procedentes de la consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="eda0c-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="eda0c-198">**donde** : hello donde cláusula</span><span class="sxs-lookup"><span data-stu-id="eda0c-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="eda0c-199">**and**: es una condición where `and`</span><span class="sxs-lookup"><span data-stu-id="eda0c-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="eda0c-200">**or**: es una condición where `or`</span><span class="sxs-lookup"><span data-stu-id="eda0c-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="eda0c-201">**parte superior** -Hola número de elementos toofetch</span><span class="sxs-lookup"><span data-stu-id="eda0c-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="eda0c-202">Hello en el ejemplo siguiente se genera una consulta que devolverá Hola superiores cinco elementos con un PartitionKey de 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="eda0c-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="eda0c-203">Dado que **select** no se usa, se devolverán todos los campos.</span><span class="sxs-lookup"><span data-stu-id="eda0c-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="eda0c-204">consulta de Hola de tooperform en una tabla, utilice **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="eda0c-205">Hello en el ejemplo siguiente se usa este tooreturn consultar entidades de "mytable".</span><span class="sxs-lookup"><span data-stu-id="eda0c-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="eda0c-206">Si se realiza correctamente, `result.entries` contendrá una matriz de entidades que coinciden con la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="eda0c-207">Si la consulta de hello era tooreturn no se puede todas las entidades, `result.continuationToken` será no son*null* y puede utilizarse como Hola tercer parámetro del **queryEntities** tooretrieve más resultados.</span><span class="sxs-lookup"><span data-stu-id="eda0c-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="eda0c-208">Para la consulta inicial de hello, use *null* para el tercer parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="eda0c-209">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="eda0c-209">Query a subset of entity properties</span></span>
<span data-ttu-id="eda0c-210">Una tabla de tooa de consulta puede recuperar solo unos cuantos campos de una entidad.</span><span class="sxs-lookup"><span data-stu-id="eda0c-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="eda0c-211">Esto reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="eda0c-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="eda0c-212">Hola de uso **seleccione** devuelven los nombres de Hola de cláusula y pase de hello campos toobe.</span><span class="sxs-lookup"><span data-stu-id="eda0c-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="eda0c-213">Por ejemplo, hello siguiente consulta devolverá solo hello **descripción** y **dueDate** campos.</span><span class="sxs-lookup"><span data-stu-id="eda0c-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="eda0c-214">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="eda0c-214">Delete an entity</span></span>
<span data-ttu-id="eda0c-215">Puede eliminar una entidad usando sus claves de partición y fila.</span><span class="sxs-lookup"><span data-stu-id="eda0c-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="eda0c-216">En este ejemplo, Hola **Tarea1** objeto contiene Hola **RowKey** y **PartitionKey** valores de hello entidad toobe eliminado.</span><span class="sxs-lookup"><span data-stu-id="eda0c-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="eda0c-217">A continuación, se pasa el objeto de hello toohello **deleteEntity** método.</span><span class="sxs-lookup"><span data-stu-id="eda0c-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="eda0c-218">Considere el uso de valores de eTag al eliminar elementos, tooensure que Hola de elemento no se haya modificado por otro proceso.</span><span class="sxs-lookup"><span data-stu-id="eda0c-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="eda0c-219">Consulte [Actualización de una entidad](#update-an-entity) para obtener información sobre el uso de etiquetas ETag.</span><span class="sxs-lookup"><span data-stu-id="eda0c-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="eda0c-220">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="eda0c-220">Delete a table</span></span>
<span data-ttu-id="eda0c-221">Hola siguiente código elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eda0c-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="eda0c-222">Si no está seguro de si existe la tabla de hello, use **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="eda0c-223">Usar tokens de continuación</span><span class="sxs-lookup"><span data-stu-id="eda0c-223">Use continuation tokens</span></span>
<span data-ttu-id="eda0c-224">Cuando consulte tablas para grandes cantidades de resultados, busque tokens de continuación.</span><span class="sxs-lookup"><span data-stu-id="eda0c-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="eda0c-225">Puede haber grandes cantidades de datos disponibles para la consulta que no es posible que consiga si no genere toorecognize cuando hay un token de continuación.</span><span class="sxs-lookup"><span data-stu-id="eda0c-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="eda0c-226">resultados de Hello objeto devuelto durante consultar conjuntos de entidades un `continuationToken` propiedad cuando está presente un token de este tipo.</span><span class="sxs-lookup"><span data-stu-id="eda0c-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="eda0c-227">A continuación, puede usar al realizar una toomove de toocontinue de consulta en las entidades de partición y la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="eda0c-228">Al realizar una consulta, puede proporcionarse un parámetro de continuationToken entre la instancia de objeto de consulta de Hola y función de devolución de llamada de hello:</span><span class="sxs-lookup"><span data-stu-id="eda0c-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="eda0c-229">Si examina hello `continuationToken` objeto, encontrará propiedades como `nextPartitionKey`, `nextRowKey` y `targetLocation`, lo que puede ser usado tooiterate a través de todos los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="eda0c-230">También hay un ejemplo de continuación en el repositorio de hello Node.js de almacenamiento de Azure en GitHub.</span><span class="sxs-lookup"><span data-stu-id="eda0c-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="eda0c-231">Busque `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="eda0c-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="eda0c-232">Trabajo con firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="eda0c-232">Work with shared access signatures</span></span>
<span data-ttu-id="eda0c-233">Firmas de acceso compartido (SAS) son un tootables de acceso granular de tooprovide de forma segura sin tener que proporcionar el nombre de la cuenta de almacenamiento o claves.</span><span class="sxs-lookup"><span data-stu-id="eda0c-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="eda0c-234">SAS son a menudo utilizados tooprovide limitado acceder a tooyour los datos, como permitir que una aplicación móvil tooquery registros.</span><span class="sxs-lookup"><span data-stu-id="eda0c-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="eda0c-235">Una aplicación de confianza, como un servicio basado en la nube genera una SAS con hello **generatesharedaccesssignature tal** de hello **TableService**y proporciona tooan aplicación de confianza o de confianza parcial Por ejemplo, una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="eda0c-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="eda0c-236">Hola SAS se genera mediante una directiva, que describe el inicio de Hola y fechas de finalización durante qué Hola SAS es válido, así como Hola titular SAS toohello concedidos nivel de acceso.</span><span class="sxs-lookup"><span data-stu-id="eda0c-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="eda0c-237">Hello en el ejemplo siguiente se genera una nueva directiva de acceso compartido que le permitirá hello tooquery ("r") de la tabla de hello SAS titular y expira 100 minutos tarde Hola se crea.</span><span class="sxs-lookup"><span data-stu-id="eda0c-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="eda0c-238">Recuerde que debe ser información de host de hello siempre también, tal y como se requiere cuando titular SAS de hello intentos de tabla de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="eda0c-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="eda0c-239">Hola aplicación cliente, a continuación, utiliza Hola SAS con **TableServiceWithSAS** tooperform operaciones contra la tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="eda0c-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="eda0c-240">Hola siguiente ejemplo conecta la tabla toohello y realiza una consulta.</span><span class="sxs-lookup"><span data-stu-id="eda0c-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="eda0c-241">Dado que hello SAS se genera con acceso de consulta solo si se realiza un intento tooinsert, actualizar o eliminar entidades, se devolvería un error.</span><span class="sxs-lookup"><span data-stu-id="eda0c-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="eda0c-242">Listas de control de acceso</span><span class="sxs-lookup"><span data-stu-id="eda0c-242">Access Control Lists</span></span>
<span data-ttu-id="eda0c-243">También puede usar una directiva de acceso de Hola de tooset de lista de Control de acceso (ACL) para una SAS.</span><span class="sxs-lookup"><span data-stu-id="eda0c-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="eda0c-244">Esto es útil si desea tooallow varias tablas de hello tooaccess de los clientes, pero proporcionar las directivas de acceso diferente para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="eda0c-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="eda0c-245">Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva.</span><span class="sxs-lookup"><span data-stu-id="eda0c-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="eda0c-246">Hola siguiente ejemplo define dos directivas, uno para "user1" y otro para el usuario '2':</span><span class="sxs-lookup"><span data-stu-id="eda0c-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="eda0c-247">Hola siguiendo el ejemplo se obtiene Hola ACL actual para hello **hometasks** de tabla y, a continuación, agrega nuevas directivas de hello mediante **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="eda0c-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="eda0c-248">Este enfoque permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eda0c-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="eda0c-249">Una vez se ha establecido la ACL de hello, puede crear una SAS basada en Id. de Hola para una directiva.</span><span class="sxs-lookup"><span data-stu-id="eda0c-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="eda0c-250">Hola de ejemplo siguiente crea una nueva SAS para el usuario '2':</span><span class="sxs-lookup"><span data-stu-id="eda0c-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="eda0c-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eda0c-251">Next steps</span></span>
<span data-ttu-id="eda0c-252">Para obtener más información, vea Hola recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="eda0c-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="eda0c-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="eda0c-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="eda0c-254">[SDK de almacenamiento de Azure para Node.js](https://github.com/Azure/azure-storage-node) en GitHub</span><span class="sxs-lookup"><span data-stu-id="eda0c-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="eda0c-255">Centro para desarrolladores de Node.js</span><span class="sxs-lookup"><span data-stu-id="eda0c-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="eda0c-256">Crear e implementar un tooan de aplicación Node.js sitio Web de Azure</span><span class="sxs-lookup"><span data-stu-id="eda0c-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
