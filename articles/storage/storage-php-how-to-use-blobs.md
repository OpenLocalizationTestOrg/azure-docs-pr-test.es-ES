---
title: Uso de Blob Storage (almacenamiento de objetos) en PHP | Microsoft Docs
description: Almacene datos no estructurados en la nube con Almacenamiento de blobs (objetos) de Azure.
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
ms.openlocfilehash: 2c356d7faafa8ef4591087b5b1f949b9374732be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="82bc7-103">Uso del almacenamiento de blobs de PHP</span><span class="sxs-lookup"><span data-stu-id="82bc7-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="82bc7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="82bc7-104">Overview</span></span>
<span data-ttu-id="82bc7-105">Almacenamiento de blobs de Azure es un servicio que almacena datos no estructurados en la nube como objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="82bc7-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="82bc7-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="82bc7-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="82bc7-107">El Almacenamiento de blobs a veces se conoce como "almacenamiento de objetos".</span><span class="sxs-lookup"><span data-stu-id="82bc7-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="82bc7-108">Esta guía muestra cómo realizar algunas tareas comunes a través del servicio BLOB de Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc7-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="82bc7-109">Los ejemplos están escritos en PHP y utilizan el [SDK de Azure para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="82bc7-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="82bc7-110">Entre los escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="82bc7-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="82bc7-111">Para obtener más información acerca de los blobs, consulte la sección [Pasos siguientes](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="82bc7-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="82bc7-112">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="82bc7-112">Create a PHP application</span></span>
<span data-ttu-id="82bc7-113">El único requisito a la hora de crear una aplicación PHP para obtener acceso al servicio BLOB de Azure es que el código haga referencia a clases del SDK de Azure para PHP dentro del código.</span><span class="sxs-lookup"><span data-stu-id="82bc7-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="82bc7-114">Puede utilizar cualquier herramienta de desarrollo para crear la aplicación, incluido el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="82bc7-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="82bc7-115">En esta guía, usará funciones del servicio a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc7-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="82bc7-116">Obtención de las bibliotecas de clientes de Azure</span><span class="sxs-lookup"><span data-stu-id="82bc7-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="82bc7-117">Configuración de la aplicación para obtener acceso al servicio BLOB</span><span class="sxs-lookup"><span data-stu-id="82bc7-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="82bc7-118">Para usar las API del servicio BLOB de Azure, necesita:</span><span class="sxs-lookup"><span data-stu-id="82bc7-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="82bc7-119">Hacer referencia al archivo autocargador mediante la instrucción [require_once] y</span><span class="sxs-lookup"><span data-stu-id="82bc7-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="82bc7-120">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="82bc7-120">Reference any classes you might use.</span></span>

<span data-ttu-id="82bc7-121">En el siguiente ejemplo se muestra cómo incluir el archivo autocargador y hacer referencia a la clase **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="82bc7-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="82bc7-122">En los ejemplos de este artículo, se da por hecho que ha instalado las bibliotecas de clientes PHP para Azure mediante el compositor.</span><span class="sxs-lookup"><span data-stu-id="82bc7-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="82bc7-123">Si las instaló manualmente, debe hacer referencia al archivo del cargador automático `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="82bc7-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="82bc7-124">En los ejemplos que aparecen a continuación, la instrucción `require_once` aparecerá siempre, pero solo se hará referencia a las clases necesarias para la ejecución del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="82bc7-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="82bc7-125">Configuración de una conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="82bc7-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="82bc7-126">Para crear una instancia de un cliente del servicio BLOB de Azure, primero debe disponer de una cadena de conexión válida.</span><span class="sxs-lookup"><span data-stu-id="82bc7-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="82bc7-127">El formato de las cadenas de conexión del servicio BLOB es:</span><span class="sxs-lookup"><span data-stu-id="82bc7-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="82bc7-128">Para obtener acceso a un servicio en directo:</span><span class="sxs-lookup"><span data-stu-id="82bc7-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="82bc7-129">Para obtener acceso al emulador de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="82bc7-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="82bc7-130">Para crear un cliente de cualquier servicio de Azure, debe usar la clase **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="82bc7-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="82bc7-131">Puede:</span><span class="sxs-lookup"><span data-stu-id="82bc7-131">You can:</span></span>

* <span data-ttu-id="82bc7-132">pasarle directamente la cadena de conexión, o bien</span><span class="sxs-lookup"><span data-stu-id="82bc7-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="82bc7-133">usar **CloudConfigurationManager (CCM)** para buscar la cadena de conexión en varios orígenes externos:</span><span class="sxs-lookup"><span data-stu-id="82bc7-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="82bc7-134">de manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="82bc7-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="82bc7-135">para agregar nuevos orígenes, amplíe la clase **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="82bc7-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="82bc7-136">En los ejemplos descritos aquí, la cadena de conexión se pasará directamente.</span><span class="sxs-lookup"><span data-stu-id="82bc7-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="82bc7-137">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="82bc7-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="82bc7-138">Un objeto **BlobRestProxy** le permite crear un contenedor de blobs mediante el método **createContainer**.</span><span class="sxs-lookup"><span data-stu-id="82bc7-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="82bc7-139">Al crear un contenedor, puede establecer opciones en él, aunque no es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="82bc7-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="82bc7-140">(El ejemplo que aparece a continuación muestra cómo establecer la lista de control de acceso o ACL y los metadatos del contenedor).</span><span class="sxs-lookup"><span data-stu-id="82bc7-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
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

<span data-ttu-id="82bc7-141">Si llama a **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)**, los datos del contenedor y los blobs pasan a ser accesibles mediante solicitudes anónimas.</span><span class="sxs-lookup"><span data-stu-id="82bc7-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="82bc7-142">Si llama a **setPublicAccess(PublicAccessType::BLOBS_ONLY)**, solo los datos de los blobs pasan a ser accesibles mediante solicitudes anónimas.</span><span class="sxs-lookup"><span data-stu-id="82bc7-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="82bc7-143">Para obtener más información sobre las ACL del contenedor, consulte [Set container ACL (API de REST)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="82bc7-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="82bc7-144">Para obtener más información sobre los códigos de error del servicio BLOB, consulte [Códigos de error de Blob Service][error-codes].</span><span class="sxs-lookup"><span data-stu-id="82bc7-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="82bc7-145">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="82bc7-145">Upload a blob into a container</span></span>
<span data-ttu-id="82bc7-146">Para cargar un archivo como blob, use el método **BlobRestProxy->createBlockBlob**.</span><span class="sxs-lookup"><span data-stu-id="82bc7-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="82bc7-147">De este modo, se creará el blob si no existe, o se sobrescribirá si ya existe.</span><span class="sxs-lookup"><span data-stu-id="82bc7-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="82bc7-148">En el ejemplo de código que aparece a continuación, se asume que el contenedor ya se creó y se utiliza [fopen][fopen] para abrir el archivo como secuencia.</span><span class="sxs-lookup"><span data-stu-id="82bc7-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

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

<span data-ttu-id="82bc7-149">Observe que en el ejemplo anterior se carga un blob en forma de secuencia.</span><span class="sxs-lookup"><span data-stu-id="82bc7-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="82bc7-150">Sin embargo, también es posible cargar un blob en forma de cadena utilizando, por ejemplo, la función [file\_get\_contents][file_get_contents].</span><span class="sxs-lookup"><span data-stu-id="82bc7-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="82bc7-151">Para hacer esto en el ejemplo anterior, cambie `$content = fopen("c:\myfile.txt", "r");` a `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="82bc7-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="82bc7-152">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="82bc7-152">List the blobs in a container</span></span>
<span data-ttu-id="82bc7-153">Para enumerar los blobs de un contenedor, utilice el método **BlobRestProxy->listBlobs** aplicando un bucle **foreach** al resultado.</span><span class="sxs-lookup"><span data-stu-id="82bc7-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="82bc7-154">El código siguiente permite obtener en el explorador el nombre y el URI de cada uno de los blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="82bc7-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="82bc7-155">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="82bc7-155">Download a blob</span></span>
<span data-ttu-id="82bc7-156">Para descargar un blob, llame al método **BlobRestProxy->getBlob** y, a continuación, al método **getContentStream** en el objeto **GetBlobResult** resultante.</span><span class="sxs-lookup"><span data-stu-id="82bc7-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="82bc7-157">Observe que en el ejemplo anterior se obtiene un blob en forma de recurso de secuencia (opción predeterminada).</span><span class="sxs-lookup"><span data-stu-id="82bc7-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="82bc7-158">Sin embargo, es posible utilizar la función [stream\_get\_contents][stream-get-contents] para convertir la secuencia devuelta en una cadena.</span><span class="sxs-lookup"><span data-stu-id="82bc7-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="82bc7-159">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="82bc7-159">Delete a blob</span></span>
<span data-ttu-id="82bc7-160">Para eliminar un blob, pase el nombre del contenedor y del blob a **BlobRestProxy->deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="82bc7-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="82bc7-161">Eliminación de contenedores de blobs</span><span class="sxs-lookup"><span data-stu-id="82bc7-161">Delete a blob container</span></span>
<span data-ttu-id="82bc7-162">Finalmente, para eliminar un contenedor de blobs, pase el nombre del contenedor a **BlobRestProxy->deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="82bc7-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82bc7-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82bc7-163">Next steps</span></span>
<span data-ttu-id="82bc7-164">Ahora que está familiarizado con los aspectos básicos del servicio BLOB de Azure, use estos vínculos para obtener más información acerca de tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="82bc7-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="82bc7-165">Visite el [Blog del equipo de Almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="82bc7-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="82bc7-166">Consulte el [ejemplo de blob en bloques PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="82bc7-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="82bc7-167">Consulte el [ejemplo de blob en páginas PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="82bc7-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="82bc7-168">Transferencia de datos con la utilidad en línea de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="82bc7-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="82bc7-169">Para obtener más información, consulte también el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="82bc7-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
<span data-ttu-id="82bc7-170">[require_once]: http://php.net/require_once</span><span class="sxs-lookup"><span data-stu-id="82bc7-170">[require_once]: http://php.net/require_once</span></span>
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
