---
title: almacenamiento de blobs de Node.js del aaaHow toouse | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
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
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="7d3d0-103">¿Cómo toouse almacenamiento de blobs de Node.js</span><span class="sxs-lookup"><span data-stu-id="7d3d0-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="7d3d0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7d3d0-104">Overview</span></span>
<span data-ttu-id="7d3d0-105">Este artículo muestra cómo tooperform escenarios comunes con almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="7d3d0-106">ejemplos de Hola se escriben a través de la API Node.js Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="7d3d0-107">escenarios de Hello descritos incluyen cómo tooupload, enumerar, descargar y eliminar los blobs.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="7d3d0-108">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="7d3d0-108">Create a Node.js application</span></span>
<span data-ttu-id="7d3d0-109">Para obtener instrucciones sobre cómo toocreate una aplicación Node.js, vea [creación de una aplicación web de Node.js en el servicio de aplicación de Azure], [compilar e implementar un tooan de aplicación servicio de nube de Azure de Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) --con Windows PowerShell, o [de compilación y implementar un tooAzure de aplicación web de Node.js mediante Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="7d3d0-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="7d3d0-110">Configurar el almacenamiento de tooaccess de aplicación</span><span class="sxs-lookup"><span data-stu-id="7d3d0-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="7d3d0-111">toouse almacenamiento de Azure, necesitará Hola SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="7d3d0-112">Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete</span><span class="sxs-lookup"><span data-stu-id="7d3d0-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="7d3d0-113">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), toonavigate toohello carpeta en la que creó el ejemplo aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="7d3d0-114">Tipo de **npm instalar almacenamiento de azure** en la ventana de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="7d3d0-115">Salida de comando de hello es toohello similar el ejemplo de código siguiente.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="7d3d0-116">También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="7d3d0-117">Dentro de esa carpeta, busque hello **almacenamiento de azure** paquete, que contiene las bibliotecas de Hola que necesita almacenamiento tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="7d3d0-118">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="7d3d0-118">Import hello package</span></span>
<span data-ttu-id="7d3d0-119">Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello donde piensa toouse almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="7d3d0-120">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7d3d0-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="7d3d0-121">Hello Azure módulo leerá las variables de entorno de hello `AZURE_STORAGE_ACCOUNT` y `AZURE_STORAGE_ACCESS_KEY`, o `AZURE_STORAGE_CONNECTION_STRING`, para obtener información necesaria tooconnect tooyour cuenta de almacenamiento Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7d3d0-122">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="7d3d0-123">Para obtener un ejemplo de establecer las variables de entorno de hello en hello [portal de Azure](https://portal.azure.com) para una aplicación web de Azure, consulte [aplicación web de Node.js con Hola servicio tabla de Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="7d3d0-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="7d3d0-124">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="7d3d0-124">Create a container</span></span>
<span data-ttu-id="7d3d0-125">Hola **BlobService** objeto le permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="7d3d0-126">Hello código siguiente se crea un **BlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="7d3d0-127">Agregue Hola siguiente cerca de la parte superior de Hola de **server.js**:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="7d3d0-128">Se puede tener acceso a un blob de forma anónima mediante el uso de **createBlobServiceAnonymous** y proporcionar la dirección de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="7d3d0-129">Por ejemplo, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="7d3d0-130">toocreate un nuevo contenedor, use **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="7d3d0-131">Hello ejemplo de código siguiente crea un nuevo contenedor denominado 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="7d3d0-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="7d3d0-132">Si se acaba de crear el contenedor de hello, `result.created` es true.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="7d3d0-133">Si ya existe un contenedor de hello, `result.created` es false.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="7d3d0-134">`response`contiene información acerca de la operación de hello, incluida la información de ETag de hello para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="7d3d0-135">Seguridad del contenedor</span><span class="sxs-lookup"><span data-stu-id="7d3d0-135">Container security</span></span>
<span data-ttu-id="7d3d0-136">De forma predeterminada, los nuevos contenedores son privados, así que no se puede acceder a ellos de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="7d3d0-137">contenedor de hello toomake pública para que se pueda acceder de forma anónima, puede establecer nivel de acceso del contenedor de hello demasiado**blob** o **contenedor**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="7d3d0-138">**BLOB** -permite acceso de lectura anónimo tooblob contenido y metadatos dentro de este contenedor, pero no los metadatos de toocontainer como enumerar todos los blobs dentro de un contenedor</span><span class="sxs-lookup"><span data-stu-id="7d3d0-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="7d3d0-139">**contenedor** -permite acceso de lectura anónimo tooblob contenido y metadatos, así como metadatos del contenedor</span><span class="sxs-lookup"><span data-stu-id="7d3d0-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="7d3d0-140">Hello ejemplo de código siguiente muestra el nivel de acceso de configuración Hola demasiado**blob**:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="7d3d0-141">Como alternativa, puede modificar el nivel de acceso de Hola de un contenedor mediante el uso de **setContainerAcl** nivel de acceso de toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="7d3d0-142">Hola siguiente de código toocontainer de nivel de acceso de Hola de cambios de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="7d3d0-143">resultado hello contiene información acerca de la operación de hello, incluida la corriente de hello **ETag** para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="7d3d0-144">Filtros</span><span class="sxs-lookup"><span data-stu-id="7d3d0-144">Filters</span></span>
<span data-ttu-id="7d3d0-145">Puede aplicar opcional filtrado operaciones toooperations realizadas utilizando **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="7d3d0-146">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="7d3d0-147">Después de realizar su procesamiento previo en Opciones de solicitud de hello, método hello necesita toocall "siguiente", pasando una devolución de llamada con hello siguiente firma:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="7d3d0-148">En esta devolución de llamada y, después de procesar hello returnObject (respuesta Hola Hola solicitud enviada toohello al servidor), la devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o simplemente invocar el servicio de finalCallback tooend Hola invocación.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="7d3d0-149">Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="7d3d0-150">Hola siguiente crea un **BlobService** objeto que usa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="7d3d0-151">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="7d3d0-151">Upload a blob into a container</span></span>
<span data-ttu-id="7d3d0-152">Hay tres tipos de blobs: blobs en bloques, blobs en páginas y blobs en anexos.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="7d3d0-153">Los blobs en bloques permiten toomore eficazmente cargar datos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="7d3d0-154">Los blobs en anexos están optimizados para las operaciones de anexión.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="7d3d0-155">Los blobs en páginas están optimizados para las operaciones de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="7d3d0-156">Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d3d0-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="7d3d0-157">Blobs en bloques</span><span class="sxs-lookup"><span data-stu-id="7d3d0-157">Block blobs</span></span>
<span data-ttu-id="7d3d0-158">tooupload datos tooa blob en bloques, Hola de uso siguientes:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="7d3d0-159">**createBlockBlobFromLocalFile** : crea un nuevo blob en bloques y carga el contenido de Hola de un archivo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="7d3d0-160">**createBlockBlobFromStream** : crea un nuevo blob en bloques y carga el contenido de Hola de un flujo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="7d3d0-161">**createBlockBlobFromText** : crea un nuevo blob en bloques y carga el contenido de Hola de una cadena</span><span class="sxs-lookup"><span data-stu-id="7d3d0-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="7d3d0-162">**createWriteStreamToBlockBlob** -proporciona un blob en bloques escritura flujo tooa</span><span class="sxs-lookup"><span data-stu-id="7d3d0-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="7d3d0-163">Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **myblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="7d3d0-164">Hola `result` estos métodos devuelven contiene información sobre el funcionamiento de hello, como hello **ETag** de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="7d3d0-165">Blobs en anexos</span><span class="sxs-lookup"><span data-stu-id="7d3d0-165">Append blobs</span></span>
<span data-ttu-id="7d3d0-166">tooupload datos tooa nueva anexar blob, utilice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="7d3d0-167">**createAppendBlobFromLocalFile** : crea un nuevo blob en anexos y carga el contenido de Hola de un archivo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="7d3d0-168">**createAppendBlobFromStream** : crea un nuevo blob en anexos y carga el contenido de Hola de un flujo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="7d3d0-169">**createAppendBlobFromText** : crea un nuevo blob en anexos y carga el contenido de Hola de una cadena</span><span class="sxs-lookup"><span data-stu-id="7d3d0-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="7d3d0-170">**createWriteStreamToNewAppendBlob** : crea un nuevo blob en anexos y, a continuación, proporciona un tooit de toowrite de secuencia</span><span class="sxs-lookup"><span data-stu-id="7d3d0-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="7d3d0-171">Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="7d3d0-172">tooappend un bloque existente de tooan anexar blob, Hola de uso siguientes:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="7d3d0-173">**appendFromLocalFile** -anexar Hola contenido de un archivo tooan existente anexar blob</span><span class="sxs-lookup"><span data-stu-id="7d3d0-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="7d3d0-174">**appendFromStream** -anexar Hola contenido de una secuencia tooan existente anexar blob</span><span class="sxs-lookup"><span data-stu-id="7d3d0-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="7d3d0-175">**appendFromText** -anexar Hola contenido de una cadena tooan existente anexar blob</span><span class="sxs-lookup"><span data-stu-id="7d3d0-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="7d3d0-176">**appendBlockFromStream** -anexar Hola contenido de una secuencia tooan existente anexar blob</span><span class="sxs-lookup"><span data-stu-id="7d3d0-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="7d3d0-177">**appendBlockFromText** -anexar Hola contenido de una cadena tooan existente anexar blob</span><span class="sxs-lookup"><span data-stu-id="7d3d0-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="7d3d0-178">appendFromXXX API realizará algunas llamadas de validación del lado cliente toofail tooavoid rápido innecesario del servidor.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="7d3d0-179">appendBlockFromXXX no.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="7d3d0-180">Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="7d3d0-181">Blobs en páginas</span><span class="sxs-lookup"><span data-stu-id="7d3d0-181">Page blobs</span></span>
<span data-ttu-id="7d3d0-182">tooupload datos tooa blob en páginas, Hola de uso siguientes:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="7d3d0-183">**createPageBlob** : crea un nuevo blob en páginas de una longitud especificada.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="7d3d0-184">**createPageBlobFromLocalFile** : crea un nuevo blob en páginas y carga el contenido de Hola de un archivo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="7d3d0-185">**createPageBlobFromStream** : crea un nuevo blob en páginas y carga el contenido de Hola de un flujo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="7d3d0-186">**createWriteStreamToExistingPageBlob** -proporciona un escritura flujo tooan blob en páginas existente</span><span class="sxs-lookup"><span data-stu-id="7d3d0-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="7d3d0-187">**createWriteStreamToNewPageBlob** : crea un nuevo blob en páginas y, a continuación, proporciona un tooit de toowrite de secuencia</span><span class="sxs-lookup"><span data-stu-id="7d3d0-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="7d3d0-188">Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="7d3d0-189">Los blobs en páginas constan de 'páginas' de 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="7d3d0-190">Al cargar datos con un tamaño que no sea múltiplo de 512 recibirá un error.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="7d3d0-191">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="7d3d0-191">List hello blobs in a container</span></span>
<span data-ttu-id="7d3d0-192">blobs de hello toolist en un contenedor, use hello **listBlobsSegmented** método.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="7d3d0-193">Si desea que tooreturn blobs con un prefijo concreto, utilice **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="7d3d0-194">Hola `result` contiene un `entries` colección, que es una matriz de objetos que describen cada blob.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="7d3d0-195">Si no se puede devolver todos los blobs, Hola `result` también proporciona un `continuationToken`, que se puede utilizar como entradas adicionales de hello segundo parámetro tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="7d3d0-196">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="7d3d0-196">Download blobs</span></span>
<span data-ttu-id="7d3d0-197">datos de toodownload de un blob, use siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="7d3d0-198">**getBlobToLocalFile** -escribe Hola blob contenido toofile</span><span class="sxs-lookup"><span data-stu-id="7d3d0-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="7d3d0-199">**getBlobToStream** -escribe Hola blob contenido tooa secuencia</span><span class="sxs-lookup"><span data-stu-id="7d3d0-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="7d3d0-200">**getBlobToText** -escribe el contenido de blob de hello tooa cadena</span><span class="sxs-lookup"><span data-stu-id="7d3d0-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="7d3d0-201">**createReadStream** -proporciona un tooread de flujo de blob de Hola</span><span class="sxs-lookup"><span data-stu-id="7d3d0-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="7d3d0-202">Hello ejemplo de código siguiente muestra cómo utilizar **getBlobToStream** contenido de hello toodownload de hello **myblob** blob y almacenar toohello **output.txt** un archivo utilizando un secuencia:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="7d3d0-203">Hola `result` contiene información sobre el blob de hello, incluidos los **ETag** información.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="7d3d0-204">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="7d3d0-204">Delete a blob</span></span>
<span data-ttu-id="7d3d0-205">Por último, llame un blob, toodelete **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="7d3d0-206">Hola el siguiente ejemplo de código elimina Hola blob denominado **myblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="7d3d0-207">simultáneo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-207">Concurrent access</span></span>
<span data-ttu-id="7d3d0-208">blob en tooa toosupport acceso simultáneo de varios clientes o varias instancias de proceso, puede usar **ETags** o **concesiones**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="7d3d0-209">**ETag** -proporciona un toodetect de manera que Hola blob o contenedor ha sido modificado por otro proceso</span><span class="sxs-lookup"><span data-stu-id="7d3d0-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="7d3d0-210">**Concesión** : proporciona una manera tooobtain exclusivo renovable, escritura o eliminar el blob de tooa de acceso para un período de tiempo</span><span class="sxs-lookup"><span data-stu-id="7d3d0-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="7d3d0-211">ETag</span><span class="sxs-lookup"><span data-stu-id="7d3d0-211">ETag</span></span>
<span data-ttu-id="7d3d0-212">Usar ETags si necesita tooallow varios clientes o instancias toowrite toohello bloque Blob o página Blob simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="7d3d0-213">Hello ETag permite toodetermine si hello contenedor o blob se ha modificado desde que inicialmente lee o crearla, lo que permite tooavoid sobrescriba los cambios confirmados por otro proceso o cliente.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="7d3d0-214">Puede establecer condiciones de ETag mediante Hola opcional `options.accessConditions` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="7d3d0-215">Hello ejemplo de código siguiente solo carga hello **test.txt** contiene archivos si blob Hola ya existe y tiene el valor de ETag hello `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="7d3d0-216">Cuando se usa ETags, patrón general de hello es:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="7d3d0-217">Obtener Hola ETag como resultado de hello de crear, la lista o la operación get.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="7d3d0-218">Realizar una acción, comprobación de ese valor de ETag hello no se ha modificado.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="7d3d0-219">Si se ha modificado el valor de hello, esto indica que otro cliente o instancia modificado Hola blob o contenedor desde que obtuvo el valor de ETag Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="7d3d0-220">Concesión</span><span class="sxs-lookup"><span data-stu-id="7d3d0-220">Lease</span></span>
<span data-ttu-id="7d3d0-221">Puede adquirir una nueva concesión mediante hello **acquireLease** método, especificando el blob de Hola o un contenedor que desee tooobtain una concesión en.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="7d3d0-222">Por ejemplo, el siguiente código de hello adquiere una concesión en **myblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="7d3d0-223">Las operaciones subsiguientes en **myblob** debe proporcionar hello `options.leaseId` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="7d3d0-224">concesión de Hello Id. se devuelve como `result.id` de **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="7d3d0-225">De forma predeterminada, la duración de la concesión de hello es infinita.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="7d3d0-226">Puede especificar una duración no infinita (entre 15 y 60 segundos) proporcionando hello `options.leaseDuration` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="7d3d0-227">usar tooremove una concesión, **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="7d3d0-228">toobreak una concesión, pero impedir que otras personas obtengan una nueva concesión hasta que expire la duración original de hello, use **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="7d3d0-229">Trabajo con firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="7d3d0-229">Work with shared access signatures</span></span>
<span data-ttu-id="7d3d0-230">Firmas de acceso compartido (SAS) son un tooblobs de forma segura tooprovide acceso granular y contenedores sin proporcionar el nombre de la cuenta de almacenamiento o claves.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="7d3d0-231">Firmas de acceso compartido con frecuencia son datos de tooyour de acceso de tooprovide uso limitado, como permitir que una aplicación móvil tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="7d3d0-232">Aunque también puede permitir el acceso anónimo tooblobs, firmas de acceso compartido permiten el acceso tooprovide más controlado, como debe generar Hola SAS.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="7d3d0-233">Una aplicación de confianza, como un servicio basado en la nube genera firmas de acceso compartido con hello **generatesharedaccesssignature tal** de hello **BlobService**y le proporciona tooan no es de confianza o aplicación de confianza parcial, como una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="7d3d0-234">Acceso compartido firmas se generan mediante una directiva, que describe el inicio de Hola y fechas de finalización durante qué Hola firmas de acceso compartido son válidas, así como Hola tener acceso a nivel titular de firmas de acceso compartido toohello concedidos.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="7d3d0-235">ejemplo de código siguiente Hello genera una nueva directiva de acceso compartido que permite Hola compartido acceso firmas titular tooperform operaciones de lectura en hello **myblob** blob y expira 100 minutos tarde Hola se crea.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="7d3d0-236">Tenga en cuenta que la información de host de hello debe estar siempre también, tal y como se requiere cuando el titular de firmas de acceso compartido de Hola intente en el contenedor de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="7d3d0-237">Hola, a continuación, la aplicación cliente usa firmas de acceso compartido con **BlobServiceWithSAS** tooperform operaciones con blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="7d3d0-238">Hello siguiente obtiene información sobre **myblob**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="7d3d0-239">Puesto que las firmas de acceso compartido de hello generadas con acceso de solo lectura, si se realiza un intento de blob de hello toomodify, se devolverá un error.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="7d3d0-240">Listas de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7d3d0-240">Access control lists</span></span>
<span data-ttu-id="7d3d0-241">También puede usar una directiva de acceso (ACL) de la lista tooset Hola de acceso control SAS.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="7d3d0-242">Esto es útil si desea tooallow varios clientes tooaccess un contenedor, pero proporcionar las directivas de acceso diferente para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="7d3d0-243">Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="7d3d0-244">Hola, ejemplo de código siguiente define dos directivas, uno para "user1" y otro para el usuario '2':</span><span class="sxs-lookup"><span data-stu-id="7d3d0-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="7d3d0-245">Hola siguiendo el ejemplo de código obtiene Hola ACL actual para **mycontainer**y, a continuación, agrega nuevas directivas de hello mediante **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="7d3d0-246">Este enfoque permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7d3d0-246">This approach allows:</span></span>

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

<span data-ttu-id="7d3d0-247">Una vez Hola que ACL se establece, puede crear en función de Id. de Hola para una directiva de firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="7d3d0-248">Hola, ejemplo de código siguiente crea nuevas firmas de acceso compartido para el usuario '2':</span><span class="sxs-lookup"><span data-stu-id="7d3d0-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="7d3d0-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7d3d0-249">Next steps</span></span>
<span data-ttu-id="7d3d0-250">Para obtener más información, vea Hola recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="7d3d0-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="7d3d0-251">[Referencia de la API del SDK de Azure Storage para Node][Referencia de la API del SDK de Azure Storage para Node]</span><span class="sxs-lookup"><span data-stu-id="7d3d0-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="7d3d0-252">[Blog del equipo de Azure Storage] [Blog del equipo de Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="7d3d0-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="7d3d0-253">[SDK de Azure Storage para Node.js][Azure Storage SDK for Node] en GitHub</span><span class="sxs-lookup"><span data-stu-id="7d3d0-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="7d3d0-254">Centro para desarrolladores de Node.js</span><span class="sxs-lookup"><span data-stu-id="7d3d0-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="7d3d0-255">Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola</span><span class="sxs-lookup"><span data-stu-id="7d3d0-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="7d3d0-256">[Aplicación web de Node.js con hello servicio tabla de Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="7d3d0-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="7d3d0-257">[Compilar e implementar un tooAzure de aplicación web de Node.js mediante Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="7d3d0-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="7d3d0-258">[Usar Hola REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [portal de Azure]: https://portal.azure.com [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog del equipo de almacenamiento de Azure]: http:// blogs.msdn.com/b/windowsazurestorage/ [almacenamiento de Azure SDK para la referencia de la API de nodo]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="7d3d0-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
