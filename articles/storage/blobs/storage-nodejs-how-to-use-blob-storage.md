---
title: Uso de Blob Storage en Node.js | Microsoft Docs
description: Almacene datos no estructurados en la nube con Almacenamiento de blobs (objetos) de Azure.
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e83ad647f6b7c70f34ef0c69b5bf322da5b6d60d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="ac4be-103">Uso de almacenamiento de blobs en Node.js</span><span class="sxs-lookup"><span data-stu-id="ac4be-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="ac4be-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ac4be-104">Overview</span></span>
<span data-ttu-id="ac4be-105">En este artículo se muestra cómo realizar algunas tareas comunes con Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="ac4be-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="ac4be-106">Los ejemplos están escritos con la API de Node.js.</span><span class="sxs-lookup"><span data-stu-id="ac4be-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="ac4be-107">Los escenarios descritos incluyen cómo cargar, enumerar, descargar y eliminar blobs.</span><span class="sxs-lookup"><span data-stu-id="ac4be-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="ac4be-108">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="ac4be-108">Create a Node.js application</span></span>
<span data-ttu-id="ac4be-109">Para instrucciones sobre cómo crear una aplicación Node.js, consulte [Creación de una aplicación web Node.js en Azure App Service], [Creación e implementación de una aplicación Node.js en un servicio en la nube de Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) con Windows PowerShell o [Creación e implementación de una aplicación web Node.js en Azure con Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="ac4be-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="ac4be-110">Configuración de la aplicación para acceder al almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ac4be-110">Configure your application to access storage</span></span>
<span data-ttu-id="ac4be-111">Para usar el almacenamiento de Azure necesitará el SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de útiles bibliotecas que se comunican con los servicios REST de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ac4be-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="ac4be-112">Uso del Administrador de paquetes para Node (NPM) para obtener el paquete</span><span class="sxs-lookup"><span data-stu-id="ac4be-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="ac4be-113">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix) para ir a la carpeta donde ha creado la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ac4be-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="ac4be-114">Escriba **npm install azure-storage** en la ventana de comandos.</span><span class="sxs-lookup"><span data-stu-id="ac4be-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="ac4be-115">La salida del comando es similar al ejemplo de código siguiente.</span><span class="sxs-lookup"><span data-stu-id="ac4be-115">Output from the command is similar to the following code example.</span></span>

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
3. <span data-ttu-id="ac4be-116">Puede ejecutar manualmente el comando **ls** para comprobar si se ha creado la carpeta **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="ac4be-117">Dentro de dicha carpeta, busque el paquete **azure-storage** , que contiene las bibliotecas necesarias para el acceso al almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ac4be-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="ac4be-118">Importación del paquete</span><span class="sxs-lookup"><span data-stu-id="ac4be-118">Import the package</span></span>
<span data-ttu-id="ac4be-119">Con el Bloc de notas u otro editor de texto, agregue lo siguiente en la parte superior del archivo **server.js** de la aplicación en la que pretenda usar el almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="ac4be-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="ac4be-120">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ac4be-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="ac4be-121">El módulo de Azure leerá las variables de entorno `AZURE_STORAGE_ACCOUNT` y `AZURE_STORAGE_ACCESS_KEY` o `AZURE_STORAGE_CONNECTION_STRING` para obtener la información necesaria para conectarse a la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac4be-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="ac4be-122">Si no se configuran estas variables de entorno, debe especificar la información de la cuenta llamando a **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="ac4be-123">Para ver un ejemplo de cómo configurar las variables de entorno de [Azure Portal](https://portal.azure.com) para una aplicación web de Azure, consulte [Aplicación web de Node.js con Azure Table service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="ac4be-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ac4be-124">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="ac4be-124">Create a container</span></span>
<span data-ttu-id="ac4be-125">El objeto **BlobService** permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="ac4be-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ac4be-126">El código siguiente crea un objeto **BlobService** .</span><span class="sxs-lookup"><span data-stu-id="ac4be-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="ac4be-127">Agregue lo siguiente cerca de la parte superior de **server.js**:</span><span class="sxs-lookup"><span data-stu-id="ac4be-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="ac4be-128">Puede obtener acceso a un blob de forma anónima mediante **createBlobServiceAnonymous** y proporcionando la dirección del host.</span><span class="sxs-lookup"><span data-stu-id="ac4be-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="ac4be-129">Por ejemplo, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="ac4be-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ac4be-130">Para crear un nuevo contenedor, use **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="ac4be-131">En el siguiente ejemplo de código se crea un nuevo contenedor llamado "mycontainer":</span><span class="sxs-lookup"><span data-stu-id="ac4be-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="ac4be-132">Si se acaba de crear el contenedor, `result.created` es true.</span><span class="sxs-lookup"><span data-stu-id="ac4be-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="ac4be-133">Si el contenedor ya existe, `result.created` es false.</span><span class="sxs-lookup"><span data-stu-id="ac4be-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="ac4be-134">`response` contiene información sobre la operación, incluida la información de ETag del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ac4be-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="ac4be-135">Seguridad del contenedor</span><span class="sxs-lookup"><span data-stu-id="ac4be-135">Container security</span></span>
<span data-ttu-id="ac4be-136">De forma predeterminada, los nuevos contenedores son privados, así que no se puede acceder a ellos de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="ac4be-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="ac4be-137">Para que el contenedor sea público, de modo que pueda tener acceso de forma anónima, puede establecer el nivel de acceso del contenedor en **blob** o en **contenedor**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="ac4be-138">**blob** : permite el acceso de lectura anónimo al contenido del blob y a los metadatos del contenedor, pero no al listado de todos los blobs de un contenedor determinado.</span><span class="sxs-lookup"><span data-stu-id="ac4be-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="ac4be-139">**contenedor** : permite el acceso de lectura anónimo al contenido del blob y los metadatos, incluidos los del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ac4be-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="ac4be-140">En el ejemplo de código siguiente se demuestra cómo configurar el nivel de acceso en **blob**:</span><span class="sxs-lookup"><span data-stu-id="ac4be-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="ac4be-141">También puede modificar el nivel de acceso de un contenedor usando **setContainerAcl** para especificarlo.</span><span class="sxs-lookup"><span data-stu-id="ac4be-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="ac4be-142">En el ejemplo de código siguiente se cambia el nivel de acceso a container:</span><span class="sxs-lookup"><span data-stu-id="ac4be-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="ac4be-143">El resultado contiene información sobre la operación, junto con la información de **ETag** actual del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ac4be-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="ac4be-144">Filtros</span><span class="sxs-lookup"><span data-stu-id="ac4be-144">Filters</span></span>
<span data-ttu-id="ac4be-145">Puede aplicar operaciones de filtrado opcionales a las operaciones realizadas mediante **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="ac4be-146">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con la firma:</span><span class="sxs-lookup"><span data-stu-id="ac4be-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="ac4be-147">Después de realizar el preprocesamiento en las opciones de solicitud, el método tiene que llamar a "next" pasando una devolución de llamada con la firma siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="ac4be-148">En esta devolución de llamada y después de procesar returnObject (la respuesta de la solicitud al servidor), la devolución de llamada tiene que invocar a next, si existe, para continuar procesando otros filtros, o bien simplemente invocar a finalCallback para finalizar la invocación del servicio.</span><span class="sxs-lookup"><span data-stu-id="ac4be-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="ac4be-149">Se incluyen dos filtros que implementan la lógica de reintento con el SDK de Azure para Node.js: **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="ac4be-150">Lo siguiente crea un objeto **BlobService** que usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="ac4be-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ac4be-151">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ac4be-151">Upload a blob into a container</span></span>
<span data-ttu-id="ac4be-152">Hay tres tipos de blobs: blobs en bloques, blobs en páginas y blobs en anexos.</span><span class="sxs-lookup"><span data-stu-id="ac4be-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="ac4be-153">Los blobs en bloques permiten cargar datos de gran tamaño de una forma más eficaz.</span><span class="sxs-lookup"><span data-stu-id="ac4be-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="ac4be-154">Los blobs en anexos están optimizados para las operaciones de anexión.</span><span class="sxs-lookup"><span data-stu-id="ac4be-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="ac4be-155">Los blobs en páginas están optimizados para las operaciones de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="ac4be-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="ac4be-156">Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac4be-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="ac4be-157">Blobs en bloques</span><span class="sxs-lookup"><span data-stu-id="ac4be-157">Block blobs</span></span>
<span data-ttu-id="ac4be-158">Para cargar datos en un blob en bloque, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="ac4be-159">**createBlockBlobFromLocalFile** : crea un nuevo blob en bloques y carga el contenido de un archivo.</span><span class="sxs-lookup"><span data-stu-id="ac4be-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="ac4be-160">**createBlockBlobFromStream** : crea un nuevo blob en bloques y carga el contenido de una secuencia.</span><span class="sxs-lookup"><span data-stu-id="ac4be-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="ac4be-161">**createBlockBlobFromText** : crea un nuevo blob en bloques y carga el contenido de una cadena.</span><span class="sxs-lookup"><span data-stu-id="ac4be-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="ac4be-162">**createWriteStreamToBlockBlob** : proporciona una secuencia de escritura a un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="ac4be-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="ac4be-163">En el siguiente ejemplo de código se carga el contenido del archivo **test.txt** en **myblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="ac4be-164">El `result` que devuelven estos métodos contiene información sobre la operación, como el valor **ETag** del blob.</span><span class="sxs-lookup"><span data-stu-id="ac4be-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="ac4be-165">Blobs en anexos</span><span class="sxs-lookup"><span data-stu-id="ac4be-165">Append blobs</span></span>
<span data-ttu-id="ac4be-166">Para cargar datos en un nuevo blob en anexos, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="ac4be-167">**createAppendBlobFromLocalFile** : crea un nuevo blob en anexos y carga el contenido de un archivo.</span><span class="sxs-lookup"><span data-stu-id="ac4be-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="ac4be-168">**createAppendBlobFromStream** : crea un nuevo blob en anexos y carga el contenido de una transmisión.</span><span class="sxs-lookup"><span data-stu-id="ac4be-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="ac4be-169">**createAppendBlobFromText** : crea un nuevo blob en anexos y carga el contenido de una cadena.</span><span class="sxs-lookup"><span data-stu-id="ac4be-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="ac4be-170">**createWriteStreamToNewAppendBlob** : crea un nuevo blob en anexos y luego proporciona una transmisión para escribir en él.</span><span class="sxs-lookup"><span data-stu-id="ac4be-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="ac4be-171">En el siguiente ejemplo de código se carga el contenido del archivo **test.txt** en **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="ac4be-172">Para anexar un bloque a un blob en anexos existente, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="ac4be-173">**appendFromLocalFile** : anexa el contenido de un archivo a un blob en anexos existente.</span><span class="sxs-lookup"><span data-stu-id="ac4be-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="ac4be-174">**appendFromStream** : anexa el contenido de una transmisión a un blob en anexos existente.</span><span class="sxs-lookup"><span data-stu-id="ac4be-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="ac4be-175">**appendFromText** : anexa el contenido de una cadena a un blob en anexos existente.</span><span class="sxs-lookup"><span data-stu-id="ac4be-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="ac4be-176">**appendBlockFromStream** : anexa el contenido de una transmisión a un blob en anexos existente.</span><span class="sxs-lookup"><span data-stu-id="ac4be-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="ac4be-177">**appendBlockFromText** : anexa el contenido de una cadena a un blob en anexos existente.</span><span class="sxs-lookup"><span data-stu-id="ac4be-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="ac4be-178">Las API appendFromXXX realizarán alguna validación de cliente de errores para evitar llamadas innecesarias al servidor.</span><span class="sxs-lookup"><span data-stu-id="ac4be-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="ac4be-179">appendBlockFromXXX no.</span><span class="sxs-lookup"><span data-stu-id="ac4be-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="ac4be-180">En el siguiente ejemplo de código se carga el contenido del archivo **test.txt** en **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="ac4be-181">Blobs en páginas</span><span class="sxs-lookup"><span data-stu-id="ac4be-181">Page blobs</span></span>
<span data-ttu-id="ac4be-182">Para cargar datos en un blob en página, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="ac4be-183">**createPageBlob** : crea un nuevo blob en páginas de una longitud especificada.</span><span class="sxs-lookup"><span data-stu-id="ac4be-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="ac4be-184">**createPageBlobFromLocalFile** : crea un nuevo blob en páginas y carga el contenido de un archivo.</span><span class="sxs-lookup"><span data-stu-id="ac4be-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="ac4be-185">**createPageBlobFromStream** : crea un nuevo blob en páginas y carga el contenido de una secuencia.</span><span class="sxs-lookup"><span data-stu-id="ac4be-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="ac4be-186">**createWriteStreamToExistingPageBlob** : proporciona una secuencia de escritura a un blob en páginas existente</span><span class="sxs-lookup"><span data-stu-id="ac4be-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="ac4be-187">**createWriteStreamToNewPageBlob** : crea un nuevo blob en páginas y luego proporciona una transmisión para escribir en él.</span><span class="sxs-lookup"><span data-stu-id="ac4be-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="ac4be-188">En el siguiente ejemplo de código se carga el contenido del archivo **test.txt** en **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="ac4be-189">Los blobs en páginas constan de 'páginas' de 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="ac4be-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="ac4be-190">Al cargar datos con un tamaño que no sea múltiplo de 512 recibirá un error.</span><span class="sxs-lookup"><span data-stu-id="ac4be-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="ac4be-191">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="ac4be-191">List the blobs in a container</span></span>
<span data-ttu-id="ac4be-192">Para enumerar los blobs de un contenedor, use el método **listBlobsSegmented** .</span><span class="sxs-lookup"><span data-stu-id="ac4be-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="ac4be-193">Si desea devolver blobs con un prefijo determinado, use **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="ac4be-194">El `result` contiene una colección de `entries`, que es una matriz de objetos que describen cada blob.</span><span class="sxs-lookup"><span data-stu-id="ac4be-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="ac4be-195">Si no se pueden devolver todos los blobs, el `result` proporciona también un `continuationToken`, que puede usar como un segundo parámetro para recuperar entradas adicionales.</span><span class="sxs-lookup"><span data-stu-id="ac4be-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="ac4be-196">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="ac4be-196">Download blobs</span></span>
<span data-ttu-id="ac4be-197">Para descargar datos de un blob, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="ac4be-198">**getBlobToLocalFile** : escribe el contenido del blob en un archivo.</span><span class="sxs-lookup"><span data-stu-id="ac4be-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="ac4be-199">**getBlobToStream** : escribe el contenido del blob en una secuencia.</span><span class="sxs-lookup"><span data-stu-id="ac4be-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="ac4be-200">**getBlobToText** : escribe el contenido del blob en una cadena.</span><span class="sxs-lookup"><span data-stu-id="ac4be-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="ac4be-201">**createReadStream** : proporciona una secuencia para leer del blob.</span><span class="sxs-lookup"><span data-stu-id="ac4be-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="ac4be-202">En el ejemplo de código siguiente se demuestra cómo usar **getBlobToStream** para descargar el contenido del blob **myblob** y almacenarlo en el archivo **output.txt** usando una secuencia:</span><span class="sxs-lookup"><span data-stu-id="ac4be-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="ac4be-203">El `result` contiene información acerca del blob, lo que incluye información de **ETag** .</span><span class="sxs-lookup"><span data-stu-id="ac4be-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="ac4be-204">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="ac4be-204">Delete a blob</span></span>
<span data-ttu-id="ac4be-205">Finalmente, para eliminar un blob, llame a **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="ac4be-206">En el ejemplo de código siguiente se elimina el blob llamado **myblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="ac4be-207">simultáneo</span><span class="sxs-lookup"><span data-stu-id="ac4be-207">Concurrent access</span></span>
<span data-ttu-id="ac4be-208">Para permitir el acceso simultáneo a un blob desde varios clientes o varias instancias de proceso, puede usar etiquetas **ETag** o **concesiones**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="ac4be-209">**Etag** : proporciona una manera de detectar que otro proceso ha modificado el blob o el contenedor</span><span class="sxs-lookup"><span data-stu-id="ac4be-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="ac4be-210">**Concesión** : proporciona una manera de obtener acceso exclusivo y renovable de escritura o eliminación a un blob durante un período de tiempo</span><span class="sxs-lookup"><span data-stu-id="ac4be-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="ac4be-211">ETag</span><span class="sxs-lookup"><span data-stu-id="ac4be-211">ETag</span></span>
<span data-ttu-id="ac4be-212">Use ETag si necesita permitir que varios clientes o instancias escriban en el blob en bloques o en páginas de manera simultánea.</span><span class="sxs-lookup"><span data-stu-id="ac4be-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="ac4be-213">La etiqueta ETag le permite determinar si el contenedor o el blob se modificó desde que inicialmente lo leyera o creara. De esta forma, puede evitar que los cambios efectuados por otro cliente o proceso se sobrescriban.</span><span class="sxs-lookup"><span data-stu-id="ac4be-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="ac4be-214">Puede definir las condiciones de ETag mediante el parámetro opcional `options.accessConditions` .</span><span class="sxs-lookup"><span data-stu-id="ac4be-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="ac4be-215">En el siguiente ejemplo de código solo se carga el archivo **test.txt** si el blob ya existe y tiene el valor ETag contenido por `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="ac4be-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="ac4be-216">El patrón general cuando se usan etiquetas ETag es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="ac4be-217">Obtener la etiqueta ETag como resultado de una operación create, list o get.</span><span class="sxs-lookup"><span data-stu-id="ac4be-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="ac4be-218">Realizar una acción, comprobando que el valor de ETag no se haya modificado.</span><span class="sxs-lookup"><span data-stu-id="ac4be-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="ac4be-219">Si el valor se modificó, significa que otro cliente u otra instancia ha modificado el blob o el contenedor desde que obtuvo el valor de ETag.</span><span class="sxs-lookup"><span data-stu-id="ac4be-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="ac4be-220">Concesión</span><span class="sxs-lookup"><span data-stu-id="ac4be-220">Lease</span></span>
<span data-ttu-id="ac4be-221">Puede adquirir una nueva concesión mediante el método **acquireLease** , especificando el blob o el contenedor sobre el que desea obtenerla.</span><span class="sxs-lookup"><span data-stu-id="ac4be-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="ac4be-222">Por ejemplo, el siguiente código adquiere una concesión sobre **myblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="ac4be-223">Las operaciones sucesivas sobre **myblob** deben proporcionar el parámetro `options.leaseId`.</span><span class="sxs-lookup"><span data-stu-id="ac4be-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="ac4be-224">El id. de concesión se devuelve como `result.id` desde **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="ac4be-225">De manera predeterminada, la duración de la concesión es infinita.</span><span class="sxs-lookup"><span data-stu-id="ac4be-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="ac4be-226">Puede especificar una duración no infinita (entre 15 y 60 segundos) con el parámetro `options.leaseDuration` .</span><span class="sxs-lookup"><span data-stu-id="ac4be-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="ac4be-227">Para eliminar una concesión, use **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="ac4be-228">Para interrumpir una concesión, pero impedir que otros obtengan una nueva concesión hasta que expire la duración original, use **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="ac4be-229">Trabajo con firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="ac4be-229">Work with shared access signatures</span></span>
<span data-ttu-id="ac4be-230">Las firmas de acceso compartido (SAS) constituyen una manera segura de ofrecer acceso granular a blobs y contenedores sin proporcionar el nombre o las claves de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ac4be-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="ac4be-231">Las firmas de acceso compartido se usan con frecuencia para proporcionar acceso limitado a sus datos, por ejemplo, para permitir que una aplicación móvil acceda a los blobs.</span><span class="sxs-lookup"><span data-stu-id="ac4be-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="ac4be-232">Aunque también puede permitir el acceso anónimo a los blobs, las firmas de acceso compartido le permiten proporcionar acceso más controlado, puesto que debe generar la SAS.</span><span class="sxs-lookup"><span data-stu-id="ac4be-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="ac4be-233">Una aplicación de confianza, como un servicio basado en la nube, genera firmas de acceso compartido mediante el valor **generateSharedAccessSignature** del elemento **BlobService** y se lo proporciona a una aplicación en la que no se confía o en la que se confía parcialmente como, por ejemplo, una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="ac4be-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="ac4be-234">Las firmas de acceso compartido se generan usando una directiva que describe las fechas de inicio y finalización durante las que son válidas, junto con el nivel de acceso otorgado al titular de dichas firmas.</span><span class="sxs-lookup"><span data-stu-id="ac4be-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="ac4be-235">En el siguiente ejemplo de código se genera una nueva directiva de acceso compartido que permite al titular de las firmas de acceso compartido realizar operaciones de lectura en el blob **myblob** y que expira 100 minutos después de la hora en que se crea.</span><span class="sxs-lookup"><span data-stu-id="ac4be-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="ac4be-236">Tenga en cuenta que también se debe proporcionar la información del host, puesto que es necesaria cuando el titular de las firmas de acceso compartido intenta acceder al contenedor.</span><span class="sxs-lookup"><span data-stu-id="ac4be-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="ac4be-237">La aplicación cliente usa entonces firmas de acceso compartido con **BlobServiceWithSAS** para realizar operaciones en el blob.</span><span class="sxs-lookup"><span data-stu-id="ac4be-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="ac4be-238">Lo siguiente obtiene información sobre **myblob**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="ac4be-239">Puesto que las firmas de acceso compartido se generaron con acceso de solo lectura, si se intenta modificar el blob, se devolverá un error.</span><span class="sxs-lookup"><span data-stu-id="ac4be-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="ac4be-240">Listas de control de acceso</span><span class="sxs-lookup"><span data-stu-id="ac4be-240">Access control lists</span></span>
<span data-ttu-id="ac4be-241">También se puede usar una lista de control de acceso (ACL) para definir la directiva de acceso para SAS.</span><span class="sxs-lookup"><span data-stu-id="ac4be-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="ac4be-242">Esto es útil si desea permitir que varios clientes accedan a un contenedor, pero cada uno con directivas de acceso diferentes.</span><span class="sxs-lookup"><span data-stu-id="ac4be-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="ac4be-243">Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva.</span><span class="sxs-lookup"><span data-stu-id="ac4be-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="ac4be-244">En el siguiente ejemplo de código se definen dos directivas; una para 'user1' y otra para 'user2':</span><span class="sxs-lookup"><span data-stu-id="ac4be-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="ac4be-245">En el siguiente ejemplo de código se obtiene la ACL actual de **mycontainer** y, a continuación, se agregan las nuevas directivas mediante **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="ac4be-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="ac4be-246">Este enfoque permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac4be-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="ac4be-247">Después de establecer una ACL, puede crear luego firmad de acceso compartido basadas en el id. de una directiva.</span><span class="sxs-lookup"><span data-stu-id="ac4be-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="ac4be-248">En el ejemplo de código siguiente se crean nuevas firmas de acceso compartido para 'user 2':</span><span class="sxs-lookup"><span data-stu-id="ac4be-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="ac4be-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac4be-249">Next steps</span></span>
<span data-ttu-id="ac4be-250">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="ac4be-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="ac4be-251">[Referencia de la API del SDK de Azure Storage para Node][Referencia de la API del SDK de Azure Storage para Node]</span><span class="sxs-lookup"><span data-stu-id="ac4be-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="ac4be-252">[Blog del equipo de Azure Storage] [Blog del equipo de Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="ac4be-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="ac4be-253">[SDK de Azure Storage para Node.js][Azure Storage SDK for Node] en GitHub</span><span class="sxs-lookup"><span data-stu-id="ac4be-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="ac4be-254">Centro para desarrolladores de Node.js</span><span class="sxs-lookup"><span data-stu-id="ac4be-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="ac4be-255">Introducción a la utilidad de línea de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="ac4be-255">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="ac4be-256">[Aplicación web Node.js con Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="ac4be-256">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="ac4be-257">[Creación e implementación de una aplicación web Node.js en Azure con Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="ac4be-257">[Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="ac4be-258">[Se está utilizando la API de REST]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure Portal]: https://portal.azure.com [Creación e implementación de una aplicación Node.js en un servicio en la nube de Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog del equipo de Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/ [SDK de Azure Storage para la referencia de la API de Node]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="ac4be-258">[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
