---
title: Uso de Azure Table Storage en Node.js | Microsoft Docs
description: "Almacene datos estructurados en la nube con el Almacenamiento de tablas de Azure, un almacén de datos NoSQL."
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
ms.openlocfilehash: 539212c6abe7738c022d67245f8992516f0899ff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="133d0-103">Uso del almacenamiento de tablas de Azure en Node.js</span><span class="sxs-lookup"><span data-stu-id="133d0-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="133d0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="133d0-104">Overview</span></span>
<span data-ttu-id="133d0-105">Este tema muestra cómo realizar algunas tareas comunes a través del servicio Tabla de Azure en una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="133d0-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="133d0-106">En los ejemplos de código de este tema se considera que ya tiene una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="133d0-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="133d0-107">Para información sobre cómo crear una aplicación Node.js en Azure, consulte alguno de estos temas:</span><span class="sxs-lookup"><span data-stu-id="133d0-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="133d0-108">Creación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="133d0-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="133d0-109">Creación e implementación de una aplicación web Node.js en Azure con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="133d0-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="133d0-110">[Compilación e implementación de una aplicación Node.js en un Servicio en la nube de Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (con Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="133d0-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="133d0-111">Configuración de la aplicación para obtener acceso al almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="133d0-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="133d0-112">Para usar Almacenamiento de Azure necesitará el SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de útiles bibliotecas que se comunican con los servicios REST de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="133d0-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="133d0-113">Uso del Administrador de paquetes para Node (NPM) para instalar el paquete</span><span class="sxs-lookup"><span data-stu-id="133d0-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="133d0-114">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix) y vaya a la carpeta donde creó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="133d0-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="133d0-115">Escriba **npm install azure-storage** en la ventana de comandos.</span><span class="sxs-lookup"><span data-stu-id="133d0-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="133d0-116">La salida del comando es similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="133d0-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="133d0-117">Puede ejecutar manualmente el comando **ls** para comprobar si se ha creado la carpeta **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="133d0-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="133d0-118">Dentro de dicha carpeta, encontrará el paquete **azure-storage** , que contiene las bibliotecas necesarias para el acceso al almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="133d0-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="133d0-119">Importación del paquete</span><span class="sxs-lookup"><span data-stu-id="133d0-119">Import the package</span></span>
<span data-ttu-id="133d0-120">Agregue el código siguiente a la parte superior del archivo **server.js** de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="133d0-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="133d0-121">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="133d0-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="133d0-122">El módulo azure leerá las variables de entorno AZURE\_STORAGE\_ACCOUNT y AZURE\_STORAGE\_ACCESS\_KEY o AZURE\_STORAGE\_CONNECTION\_STRING para obtener información necesaria para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="133d0-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="133d0-123">Si no se configuran estas variables de entorno, debe especificar la información de la cuenta al llamar a **TableService**.</span><span class="sxs-lookup"><span data-stu-id="133d0-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="133d0-124">Para ver un ejemplo de cómo configurar las variables de entorno de [Azure Portal](https://portal.azure.com) para un sitio web de Azure, consulte [Aplicación web de Node.js con Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="133d0-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="133d0-125">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="133d0-125">Create a table</span></span>
<span data-ttu-id="133d0-126">El código siguiente crea un objeto **TableService** que usa para crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="133d0-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="133d0-127">Agregue lo siguiente cerca de la parte superior de **server.js**.</span><span class="sxs-lookup"><span data-stu-id="133d0-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="133d0-128">La llamada a **createTableIfNotExists** creará una nueva tabla con el nombre especificado si no existe ya.</span><span class="sxs-lookup"><span data-stu-id="133d0-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="133d0-129">El ejemplo siguiente crea una tabla llamada "mytable", si es que no existe todavía:</span><span class="sxs-lookup"><span data-stu-id="133d0-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="133d0-130">El `result.created` será `true` si se crea una nueva tabla y `false` si la tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="133d0-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="133d0-131">La `response` contendrá información sobre la solicitud.</span><span class="sxs-lookup"><span data-stu-id="133d0-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="133d0-132">Filtros</span><span class="sxs-lookup"><span data-stu-id="133d0-132">Filters</span></span>
<span data-ttu-id="133d0-133">Las operaciones opcionales de filtrado se pueden aplicar a las operaciones realizadas usando **TableService**.</span><span class="sxs-lookup"><span data-stu-id="133d0-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="133d0-134">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con la firma:</span><span class="sxs-lookup"><span data-stu-id="133d0-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="133d0-135">Después de realizar el preprocesamiento en las opciones de solicitud, el método tiene que llamar a "next" pasando una devolución de llamada con la firma siguiente:</span><span class="sxs-lookup"><span data-stu-id="133d0-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="133d0-136">En esta devolución de llamada y después de procesar returnObject (la respuesta de la solicitud al servidor), la devolución de llamada tiene que invocar a next, si existe, para continuar procesando otros filtros, o bien simplemente invocar a finalCallback para finalizar la invocación del servicio.</span><span class="sxs-lookup"><span data-stu-id="133d0-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="133d0-137">Se incluyen dos filtros que implementan la lógica de reintento con el SDK de Azure para Node.js: **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="133d0-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="133d0-138">Lo siguiente crea un objeto **TableService** que usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="133d0-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="133d0-139">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="133d0-139">Add an entity to a table</span></span>
<span data-ttu-id="133d0-140">Para agregar una entidad, primero cree un objeto que defina las propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="133d0-141">Todas las entidades tienen que contener un valor para **PartitionKey** y **RowKey**, que son identificadores únicos de la entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="133d0-142">**PartitionKey** : determina la partición en la que se almacena la entidad</span><span class="sxs-lookup"><span data-stu-id="133d0-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="133d0-143">**RowKey** : identifica de forma única la entidad dentro de la partición</span><span class="sxs-lookup"><span data-stu-id="133d0-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="133d0-144">Tanto **PartitionKey** como **RowKey** tiene que ser valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="133d0-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="133d0-145">Para obtener más información, consulte [Descripción del modelo de datos del servicio Tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="133d0-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="133d0-146">Este es un ejemplo de la definición de una entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="133d0-147">Tenga en cuenta que **dueDate** se define como un tipo de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="133d0-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="133d0-148">La especificación del tipo es opcional, y los tipos se deducen si no se especifican.</span><span class="sxs-lookup"><span data-stu-id="133d0-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="133d0-149">Hay también un campo **Timestamp** para cada registro; Azure lo establece cuando se inserta o actualiza una entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="133d0-150">También puede usar **entityGenerator** para crear entidades.</span><span class="sxs-lookup"><span data-stu-id="133d0-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="133d0-151">En el siguiente ejemplo se crea la misma entidad de tarea mediante **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="133d0-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="133d0-152">Para agregar una entidad a su tabla, pase el objeto de la entidad al método **insertEntity** .</span><span class="sxs-lookup"><span data-stu-id="133d0-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="133d0-153">Si la operación se realiza correctamente, `result` contendrá la etiqueta [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) del registro insertado y `response` contendrá información sobre la operación.</span><span class="sxs-lookup"><span data-stu-id="133d0-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="133d0-154">Respuesta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="133d0-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="133d0-155">De forma predeterminada, el elemento **insertEntity** no devuelve la entidad insertada como parte de la información de `response`.</span><span class="sxs-lookup"><span data-stu-id="133d0-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="133d0-156">Si tiene pensado realizar otras operaciones en esta entidad o desea almacenar en caché la información, puede ser útil que la devuelva como parte de `result`.</span><span class="sxs-lookup"><span data-stu-id="133d0-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="133d0-157">Para ello, puede habilitar **echoContent** de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="133d0-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="133d0-158">Actualización de una entidad</span><span class="sxs-lookup"><span data-stu-id="133d0-158">Update an entity</span></span>
<span data-ttu-id="133d0-159">Hay varios métodos para actualizar una entidad existente:</span><span class="sxs-lookup"><span data-stu-id="133d0-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="133d0-160">**replaceEntity** : actualiza una entidad que ya existe reemplazándola.</span><span class="sxs-lookup"><span data-stu-id="133d0-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="133d0-161">**mergeEntity** : actualiza una entidad que ya existe combinando los valores de las nuevas propiedades con la entidad existente</span><span class="sxs-lookup"><span data-stu-id="133d0-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="133d0-162">**insertOrReplaceEntity** : actualiza una entidad existente reemplazándola.</span><span class="sxs-lookup"><span data-stu-id="133d0-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="133d0-163">Si no hay entidades, se insertará una nueva.</span><span class="sxs-lookup"><span data-stu-id="133d0-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="133d0-164">**insertOrMergeEntity** : actualiza una entidad que ya existe combinando los valores de las nuevas propiedades con los existentes.</span><span class="sxs-lookup"><span data-stu-id="133d0-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="133d0-165">Si no hay entidades, se insertará una nueva.</span><span class="sxs-lookup"><span data-stu-id="133d0-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="133d0-166">En el ejemplo siguiente se demuestra cómo actualizar una entidad usando **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="133d0-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="133d0-167">De manera predeterminada, al actualizar una entidad no se comprueba si otro proceso ha modificado anteriormente los datos que se actualizan.</span><span class="sxs-lookup"><span data-stu-id="133d0-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="133d0-168">Para permitir las actualizaciones simultáneas:</span><span class="sxs-lookup"><span data-stu-id="133d0-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="133d0-169">Obtenga la etiqueta ETag del objeto que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="133d0-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="133d0-170">Esta se devuelve como parte del valor de `response` para cualquier operación relacionada con entidades y se puede recuperar a través de `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="133d0-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="133d0-171">Al realizar una operación de actualización en una entidad, agregue la información de ETag anteriormente recuperada a la nueva entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="133d0-172">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="133d0-172">For example:</span></span>
>
>       <span data-ttu-id="133d0-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="133d0-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="133d0-174">Realice la operación de actualización.</span><span class="sxs-lookup"><span data-stu-id="133d0-174">Perform the update operation.</span></span> <span data-ttu-id="133d0-175">Si la entidad se modificó desde que recuperara el valor de ETag, como por ejemplo, otra instancia de la aplicación, se devolverá un `error` indicando que la condición de actualización especificada en la solicitud no se ha satisfecho.</span><span class="sxs-lookup"><span data-stu-id="133d0-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="133d0-176">Con **replaceEntity** y **mergeEntity**, si la entidad que se está actualizando no existe, se producirá un error en la operación de actualización.</span><span class="sxs-lookup"><span data-stu-id="133d0-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="133d0-177">Por lo tanto, si desea almacenar una entidad independientemente de la que ya existe, use **insertOrReplaceEntity** o **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="133d0-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="133d0-178">El `result` de operaciones de actualización correctas contendrá la etiqueta **Etag** de la entidad actualizada.</span><span class="sxs-lookup"><span data-stu-id="133d0-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="133d0-179">Trabajo con grupos de entidades</span><span class="sxs-lookup"><span data-stu-id="133d0-179">Work with groups of entities</span></span>
<span data-ttu-id="133d0-180">A veces resulta útil enviar varias operaciones juntas en un lote a fin de garantizar el procesamiento atómico por parte del servidor.</span><span class="sxs-lookup"><span data-stu-id="133d0-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="133d0-181">Para ello, use la clase **TableBatch** para crear un lote y, a continuación, use el método **executeBatch** de **TableService** para realizar las operaciones por lotes.</span><span class="sxs-lookup"><span data-stu-id="133d0-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="133d0-182">El ejemplo siguiente demuestra cómo enviar dos entidades en un lote:</span><span class="sxs-lookup"><span data-stu-id="133d0-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
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

<span data-ttu-id="133d0-183">En las operaciones por lotes realizadas correctamente, `result` contendrá información de cada operación del lote.</span><span class="sxs-lookup"><span data-stu-id="133d0-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="133d0-184">Trabajar con operaciones por lotes</span><span class="sxs-lookup"><span data-stu-id="133d0-184">Work with batched operations</span></span>
<span data-ttu-id="133d0-185">Las operaciones agregadas a un lote se pueden inspeccionar mirando la propiedad `operations` .</span><span class="sxs-lookup"><span data-stu-id="133d0-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="133d0-186">También se pueden usar los siguientes métodos para trabajar con operaciones.</span><span class="sxs-lookup"><span data-stu-id="133d0-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="133d0-187">**clear** : borra todas las operaciones de un lote</span><span class="sxs-lookup"><span data-stu-id="133d0-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="133d0-188">**getOperations** : obtiene una operación del lote</span><span class="sxs-lookup"><span data-stu-id="133d0-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="133d0-189">**hasOperations** : devuelve true si el lote contiene operaciones</span><span class="sxs-lookup"><span data-stu-id="133d0-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="133d0-190">**removeOperations** : quita una operación.</span><span class="sxs-lookup"><span data-stu-id="133d0-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="133d0-191">**size** : devuelve el número de operaciones del lote</span><span class="sxs-lookup"><span data-stu-id="133d0-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="133d0-192">Recuperación de una entidad por clave</span><span class="sxs-lookup"><span data-stu-id="133d0-192">Retrieve an entity by key</span></span>
<span data-ttu-id="133d0-193">Para devolver una entidad específica basada en los valores de **PartitionKey** y **RowKey**, use el método **retrieveEntity**.</span><span class="sxs-lookup"><span data-stu-id="133d0-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="133d0-194">Después de completar esta operación, `result` contendrá la entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="133d0-195">Consulta de un conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="133d0-195">Query a set of entities</span></span>
<span data-ttu-id="133d0-196">Para consultar una tabla, use el objeto **TableQuery** para compilar una expresión de consulta mediante las siguientes cláusulas:</span><span class="sxs-lookup"><span data-stu-id="133d0-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="133d0-197">**select** : son los campos que va a devolver la consulta</span><span class="sxs-lookup"><span data-stu-id="133d0-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="133d0-198">**where** : la cláusula where.</span><span class="sxs-lookup"><span data-stu-id="133d0-198">**where** - the where clause</span></span>

  * <span data-ttu-id="133d0-199">**and**: es una condición where `and`</span><span class="sxs-lookup"><span data-stu-id="133d0-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="133d0-200">**or**: es una condición where `or`</span><span class="sxs-lookup"><span data-stu-id="133d0-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="133d0-201">**top** : es el número de elementos que se obtendrán</span><span class="sxs-lookup"><span data-stu-id="133d0-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="133d0-202">En el siguiente ejemplo se crea una consulta que devolverá los cinco elementos principales con un valor de PartitionKey de 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="133d0-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="133d0-203">Dado que **select** no se usa, se devolverán todos los campos.</span><span class="sxs-lookup"><span data-stu-id="133d0-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="133d0-204">Para realizar la consulta en una tabla, use **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="133d0-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="133d0-205">En el siguiente ejemplo se usa esta consulta para devolver entidades de 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="133d0-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="133d0-206">Si la operación se realiza correctamente, `result.entries` contendrá una matriz de entidades que coinciden con la consulta.</span><span class="sxs-lookup"><span data-stu-id="133d0-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="133d0-207">Si la consulta no puede devolver todas las entidades, `result.continuationToken` será non-*null* y se puede usar como el tercer parámetro de **queryEntities** para recuperar más resultados.</span><span class="sxs-lookup"><span data-stu-id="133d0-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="133d0-208">Para la consulta inicial, use *null* para el tercer parámetro.</span><span class="sxs-lookup"><span data-stu-id="133d0-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="133d0-209">Consulta de un subconjunto de propiedades de las entidades</span><span class="sxs-lookup"><span data-stu-id="133d0-209">Query a subset of entity properties</span></span>
<span data-ttu-id="133d0-210">Una consulta de tabla puede recuperar solo algunos campos de una entidad.</span><span class="sxs-lookup"><span data-stu-id="133d0-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="133d0-211">Esto reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="133d0-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="133d0-212">Use la cláusula **select** y pase los nombres de los campos que se van a devolver.</span><span class="sxs-lookup"><span data-stu-id="133d0-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="133d0-213">Por ejemplo, la siguiente consulta solo devolverá los campos **description** y **dueDate**.</span><span class="sxs-lookup"><span data-stu-id="133d0-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="133d0-214">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="133d0-214">Delete an entity</span></span>
<span data-ttu-id="133d0-215">Puede eliminar una entidad usando sus claves de partición y fila.</span><span class="sxs-lookup"><span data-stu-id="133d0-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="133d0-216">En este ejemplo, el objeto **task1** contiene los valores **RowKey** y **PartitionKey** de la entidad que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="133d0-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="133d0-217">A continuación, el objeto pasa al método **deleteEntity** .</span><span class="sxs-lookup"><span data-stu-id="133d0-217">Then the object is passed to the **deleteEntity** method.</span></span>

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
> <span data-ttu-id="133d0-218">Cuando elimine elementos, debería considerar el uso de etiquetas ETag para garantizar que otro proceso no haya modificado el elemento.</span><span class="sxs-lookup"><span data-stu-id="133d0-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="133d0-219">Consulte [Actualización de una entidad](#update-an-entity) para obtener información sobre el uso de etiquetas ETag.</span><span class="sxs-lookup"><span data-stu-id="133d0-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="133d0-220">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="133d0-220">Delete a table</span></span>
<span data-ttu-id="133d0-221">El código siguiente elimina una tabla de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="133d0-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="133d0-222">Si no está seguro de si existe la tabla, use **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="133d0-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="133d0-223">Usar tokens de continuación</span><span class="sxs-lookup"><span data-stu-id="133d0-223">Use continuation tokens</span></span>
<span data-ttu-id="133d0-224">Cuando consulte tablas para grandes cantidades de resultados, busque tokens de continuación.</span><span class="sxs-lookup"><span data-stu-id="133d0-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="133d0-225">Puede haber grandes cantidades de datos disponibles para su consulta de los que podría no darse cuenta si no crear para reconocer cuando hay un token de continuación presente.</span><span class="sxs-lookup"><span data-stu-id="133d0-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="133d0-226">El objeto de resultados devuelto al consultar los conjuntos de entidades, establece una propiedad `continuationToken` cuando hay un token de este tipo presente.</span><span class="sxs-lookup"><span data-stu-id="133d0-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="133d0-227">Entonces, podrá usarlo al realizar una consulta para continuar moviéndose por las entidades de tabla y partición.</span><span class="sxs-lookup"><span data-stu-id="133d0-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="133d0-228">Al consultar, se puede proporcionar un parámetro continuationToken entre la instancia de objeto de consulta y la función de devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="133d0-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

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

<span data-ttu-id="133d0-229">Si inspecciona el objeto `continuationToken`, encontrará propiedades como `nextPartitionKey`, `nextRowKey` y `targetLocation`, que puede usar para iterar en todos los resultados.</span><span class="sxs-lookup"><span data-stu-id="133d0-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="133d0-230">También hay un ejemplo de continuación en el repositorio de Node.js de Almacenamiento de Azure en GitHub.</span><span class="sxs-lookup"><span data-stu-id="133d0-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="133d0-231">Busque `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="133d0-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="133d0-232">Trabajo con firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="133d0-232">Work with shared access signatures</span></span>
<span data-ttu-id="133d0-233">Las firmas de acceso compartido (SAS) constituyen una manera segura de ofrecer acceso granular a las tablas sin proporcionar el nombre o las claves de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="133d0-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="133d0-234">Las SAS se usan con frecuencia para proporcionar acceso limitado a sus datos, por ejemplo, para permitir que una aplicación móvil consulte registros.</span><span class="sxs-lookup"><span data-stu-id="133d0-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="133d0-235">Una aplicación de confianza, como por ejemplo un servicio basado en la nube, genera una SAS mediante el valor **generateSharedAccessSignature** del elemento **TableService** y se lo proporciona a una aplicación en la que no se confía o en la que se confía parcialmente, como una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="133d0-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="133d0-236">La SAS se genera usando una directiva que describe las fechas de inicio y de finalización durante las cuales la SAS es válida, junto con el nivel de acceso otorgado al titular de la SAS.</span><span class="sxs-lookup"><span data-stu-id="133d0-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="133d0-237">En el siguiente ejemplo se genera una nueva directiva de acceso compartido que permitirá al titular de la SAS consultar ('r') la tabla, y que expira 100 minutos después de la hora en que se crea.</span><span class="sxs-lookup"><span data-stu-id="133d0-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="133d0-238">Tenga en cuenta que también se debe proporcionar la información del host, puesto que es necesaria cuando el titular de la SAS intenta acceder a la tabla.</span><span class="sxs-lookup"><span data-stu-id="133d0-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="133d0-239">La aplicación cliente usa entonces la SAS con **TableServiceWithSAS** para realizar operaciones en la tabla.</span><span class="sxs-lookup"><span data-stu-id="133d0-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="133d0-240">En el siguiente ejemplo se realiza la conexión a la tabla y se realiza una consulta.</span><span class="sxs-lookup"><span data-stu-id="133d0-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="133d0-241">Dado que la SAS se generó solo con acceso de consulta, si se realizara un intento para insertar, actualizar o eliminar entidades, se devolvería un error.</span><span class="sxs-lookup"><span data-stu-id="133d0-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="133d0-242">Listas de control de acceso</span><span class="sxs-lookup"><span data-stu-id="133d0-242">Access Control Lists</span></span>
<span data-ttu-id="133d0-243">Se puede usar una lista de control de acceso (ACL) para definir la directiva de acceso para una SAS.</span><span class="sxs-lookup"><span data-stu-id="133d0-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="133d0-244">Esto es útil si desea permitir que varios clientes accedan a la tabla, pero cada uno con directivas de acceso diferentes.</span><span class="sxs-lookup"><span data-stu-id="133d0-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="133d0-245">Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva.</span><span class="sxs-lookup"><span data-stu-id="133d0-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="133d0-246">En los siguientes ejemplos se definen dos directivas; una para "user1" y otra para "user2":</span><span class="sxs-lookup"><span data-stu-id="133d0-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="133d0-247">En el siguiente ejemplo se obtiene la ACL actual para la tabla **hometasks** y luego se agregan las nuevas directivas mediante **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="133d0-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="133d0-248">Este enfoque permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="133d0-248">This approach allows:</span></span>

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

<span data-ttu-id="133d0-249">Después de establecer una ACL, puede crear luego una SAS basada en el Id. de una directiva.</span><span class="sxs-lookup"><span data-stu-id="133d0-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="133d0-250">En el siguiente ejemplo se crea una nueva SAS para 'user2':</span><span class="sxs-lookup"><span data-stu-id="133d0-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="133d0-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="133d0-251">Next steps</span></span>
<span data-ttu-id="133d0-252">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="133d0-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="133d0-253">El [Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente y gratuita de Microsoft que permite trabajar visualmente con los datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="133d0-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="133d0-254">[SDK de almacenamiento de Azure para Node.js](https://github.com/Azure/azure-storage-node) en GitHub</span><span class="sxs-lookup"><span data-stu-id="133d0-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="133d0-255">Centro para desarrolladores de Node.js</span><span class="sxs-lookup"><span data-stu-id="133d0-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="133d0-256">Creación e implementación de una aplicación Node.js en un sitio web de Azure</span><span class="sxs-lookup"><span data-stu-id="133d0-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)