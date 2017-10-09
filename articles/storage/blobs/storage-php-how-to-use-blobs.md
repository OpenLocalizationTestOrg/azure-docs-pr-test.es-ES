---
title: almacenamiento de blobs de toouse aaaHow (almacenamiento de objetos) de PHP | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="5262f-103">¿Cómo toouse blob almacenamiento de PHP</span><span class="sxs-lookup"><span data-stu-id="5262f-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="5262f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5262f-104">Overview</span></span>
<span data-ttu-id="5262f-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="5262f-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="5262f-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5262f-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="5262f-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="5262f-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="5262f-108">Esta guía le mostrará cómo tooperform escenarios comunes con hello Azure el servicio de blob.</span><span class="sxs-lookup"><span data-stu-id="5262f-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="5262f-109">ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="5262f-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="5262f-110">Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="5262f-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="5262f-111">Para obtener más información sobre los blobs, vea hello [pasos siguientes](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="5262f-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5262f-112">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="5262f-112">Create a PHP application</span></span>
<span data-ttu-id="5262f-113">Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de blobs de Azure de hello es hello las referencias de las clases de hello Azure SDK para PHP desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="5262f-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="5262f-114">Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación, incluso el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="5262f-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="5262f-115">En esta guía, usará funciones del servicio a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5262f-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="5262f-116">Obtener Hola bibliotecas de cliente de Azure</span><span class="sxs-lookup"><span data-stu-id="5262f-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="5262f-117">Configurar el servicio de blob de aplicación tooaccess Hola</span><span class="sxs-lookup"><span data-stu-id="5262f-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="5262f-118">toouse hello Azure API del servicio blob, debe:</span><span class="sxs-lookup"><span data-stu-id="5262f-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="5262f-119">Archivo de referencia hello cargador automático con hello [require_once] (instrucción), y</span><span class="sxs-lookup"><span data-stu-id="5262f-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="5262f-120">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="5262f-120">Reference any classes you might use.</span></span>

<span data-ttu-id="5262f-121">Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServicesBuilder** clase.</span><span class="sxs-lookup"><span data-stu-id="5262f-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="5262f-122">ejemplos de Hello en este artículo se supone que ha instalado Hola bibliotecas de cliente de PHP para Azure mediante el compositor.</span><span class="sxs-lookup"><span data-stu-id="5262f-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5262f-123">Si ha instalado manualmente las bibliotecas de hello, necesita hello tooreference `WindowsAzure.php` archivo cargador automático.</span><span class="sxs-lookup"><span data-stu-id="5262f-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="5262f-124">En los siguientes ejemplos de hello, Hola `require_once` instrucción se muestran siempre, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262f-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5262f-125">Configuración de una conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5262f-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="5262f-126">tooinstantiate un cliente de servicios de blobs de Azure, primero debe tener una cadena de conexión válida.</span><span class="sxs-lookup"><span data-stu-id="5262f-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="5262f-127">Hola formato de cadena de conexión de servicio de blob de hello es:</span><span class="sxs-lookup"><span data-stu-id="5262f-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="5262f-128">Para obtener acceso a un servicio en directo:</span><span class="sxs-lookup"><span data-stu-id="5262f-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="5262f-129">Para tener acceso a emulador de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="5262f-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="5262f-130">toocreate cualquier cliente de servicio de Azure, necesita hello toouse **ServicesBuilder** clase.</span><span class="sxs-lookup"><span data-stu-id="5262f-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="5262f-131">Puede:</span><span class="sxs-lookup"><span data-stu-id="5262f-131">You can:</span></span>

* <span data-ttu-id="5262f-132">Pasar Hola conexión cadena directamente tooit o</span><span class="sxs-lookup"><span data-stu-id="5262f-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="5262f-133">Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="5262f-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="5262f-134">de manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="5262f-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="5262f-135">Puede agregar nuevos orígenes de extendiendo hello **ConnectionStringSource** clase.</span><span class="sxs-lookup"><span data-stu-id="5262f-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="5262f-136">Para obtener ejemplos de hello descritos a continuación, cadena de conexión de Hola se pasará directamente.</span><span class="sxs-lookup"><span data-stu-id="5262f-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="5262f-137">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="5262f-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="5262f-138">A **BlobRestProxy** objeto le permite crear un contenedor de blobs con hello **createContainer** método.</span><span class="sxs-lookup"><span data-stu-id="5262f-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="5262f-139">Al crear un contenedor, puede establecer opciones en el contenedor de hello, pero al hacerlo, por lo tanto, no es necesario.</span><span class="sxs-lookup"><span data-stu-id="5262f-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="5262f-140">(ejemplo de Hola siguiente muestra cómo contenedor de hello tooset tener acceso a la lista de control (ACL) y metadatos del contenedor).</span><span class="sxs-lookup"><span data-stu-id="5262f-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5262f-141">Al llamar a **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOBS)** hace Hola datos del contenedor y blob accesibles a través de las solicitudes anónimas.</span><span class="sxs-lookup"><span data-stu-id="5262f-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="5262f-142">Si llama a **setPublicAccess(PublicAccessType::BLOBS_ONLY)**, solo los datos de los blobs pasan a ser accesibles mediante solicitudes anónimas.</span><span class="sxs-lookup"><span data-stu-id="5262f-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="5262f-143">Para obtener más información sobre las ACL del contenedor, consulte [Set container ACL (API de REST)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="5262f-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="5262f-144">Para obtener más información sobre los códigos de error del servicio BLOB, consulte [Códigos de error de Blob Service][error-codes].</span><span class="sxs-lookup"><span data-stu-id="5262f-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5262f-145">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="5262f-145">Upload a blob into a container</span></span>
<span data-ttu-id="5262f-146">un archivo como un blob, use hello tooupload **BlobRestProxy -> createBlockBlob** método.</span><span class="sxs-lookup"><span data-stu-id="5262f-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="5262f-147">Esta operación crea blob Hola si no existe, o lo sobrescribe si lo hace.</span><span class="sxs-lookup"><span data-stu-id="5262f-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="5262f-148">Hello ejemplo de código siguiente supone que el contenedor de hello ya se ha creado y utiliza [fopen] [ fopen] tooopen archivo de hello como una secuencia.</span><span class="sxs-lookup"><span data-stu-id="5262f-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5262f-149">Tenga en cuenta que Hola anterior ejemplo carga un blob como una secuencia.</span><span class="sxs-lookup"><span data-stu-id="5262f-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="5262f-150">Sin embargo, un blob también se puede cargar como una cadena que se usa, por ejemplo, hello [archivo\_obtener\_contenido] [ file_get_contents] (función).</span><span class="sxs-lookup"><span data-stu-id="5262f-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="5262f-151">toodo este ejemplo de Hola a anterior, cambie `$content = fopen("c:\myfile.txt", "r");` demasiado`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="5262f-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="5262f-152">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="5262f-152">List hello blobs in a container</span></span>
<span data-ttu-id="5262f-153">blobs de hello toolist en un contenedor, use hello **BlobRestProxy -> listBlobs** método con un **foreach** tooloop a través del resultado de hello en bucle.</span><span class="sxs-lookup"><span data-stu-id="5262f-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="5262f-154">Hello código siguiente muestra el nombre de Hola de cada blob como salida en un contenedor y muestra su explorador toohello URI.</span><span class="sxs-lookup"><span data-stu-id="5262f-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="5262f-155">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="5262f-155">Download a blob</span></span>
<span data-ttu-id="5262f-156">toodownload un blob, llamada hello **BlobRestProxy -> getBlob** método y, a continuación, llamada hello **getContentStream** método en hello resultante **GetBlobResult** objeto.</span><span class="sxs-lookup"><span data-stu-id="5262f-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5262f-157">Tenga en cuenta que ese ejemplo Hola anterior obtiene un objeto binario como un recurso de secuencia (comportamiento predeterminado de hello).</span><span class="sxs-lookup"><span data-stu-id="5262f-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="5262f-158">Sin embargo, puede usar hello [flujo\_obtener\_contenido] [ stream-get-contents] Hola de función tooconvert devolvió la cadena de tooa de secuencia.</span><span class="sxs-lookup"><span data-stu-id="5262f-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="5262f-159">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="5262f-159">Delete a blob</span></span>
<span data-ttu-id="5262f-160">toodelete un blob, pase el nombre del contenedor de Hola y el nombre de blob demasiado**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="5262f-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="5262f-161">un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="5262f-161">Delete a blob container</span></span>
<span data-ttu-id="5262f-162">Por último, toodelete un contenedor de blobs, pase el nombre del contenedor de hello demasiado**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="5262f-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="5262f-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5262f-163">Next steps</span></span>
<span data-ttu-id="5262f-164">Ahora que conoce los fundamentos de Hola de hello servicio blob de Azure, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5262f-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="5262f-165">Visite hello [blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="5262f-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="5262f-166">Vea hello [ejemplo de blob de bloque PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="5262f-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="5262f-167">Vea hello [ejemplo de blob de página PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="5262f-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="5262f-168">Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola</span><span class="sxs-lookup"><span data-stu-id="5262f-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="5262f-169">Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5262f-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
