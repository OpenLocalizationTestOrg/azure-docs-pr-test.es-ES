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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>¿Cómo toouse blob almacenamiento de PHP
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

Esta guía le mostrará cómo tooperform escenarios comunes con hello Azure el servicio de blob. ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP][download]. Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs. Para obtener más información sobre los blobs, vea hello [pasos siguientes](#next-steps) sección.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Creación de una aplicación PHP
Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de blobs de Azure de hello es hello las referencias de las clases de hello Azure SDK para PHP desde dentro del código. Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación, incluso el Bloc de notas.

En esta guía, usará funciones del servicio a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtener Hola bibliotecas de cliente de Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Configurar el servicio de blob de aplicación tooaccess Hola
toouse hello Azure API del servicio blob, debe:

1. Archivo de referencia hello cargador automático con hello [require_once] (instrucción), y
2. Hacer referencia a todas las clases que utilice.

Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServicesBuilder** clase.

> [!NOTE]
> ejemplos de Hello en este artículo se supone que ha instalado Hola bibliotecas de cliente de PHP para Azure mediante el compositor. Si ha instalado manualmente las bibliotecas de hello, necesita hello tooreference `WindowsAzure.php` archivo cargador automático.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

En los siguientes ejemplos de hello, Hola `require_once` instrucción se muestran siempre, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de Almacenamiento de Azure
tooinstantiate un cliente de servicios de blobs de Azure, primero debe tener una cadena de conexión válida. Hola formato de cadena de conexión de servicio de blob de hello es:

Para obtener acceso a un servicio en directo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para tener acceso a emulador de almacenamiento de hello:

```php
UseDevelopmentStorage=true
```

toocreate cualquier cliente de servicio de Azure, necesita hello toouse **ServicesBuilder** clase. Puede:

* Pasar Hola conexión cadena directamente tooit o
* Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:
  * de manera predeterminada, admite un origen externo: variables de entorno.
  * Puede agregar nuevos orígenes de extendiendo hello **ConnectionStringSource** clase.

Para obtener ejemplos de hello descritos a continuación, cadena de conexión de Hola se pasará directamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Crear un contenedor
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy** objeto le permite crear un contenedor de blobs con hello **createContainer** método. Al crear un contenedor, puede establecer opciones en el contenedor de hello, pero al hacerlo, por lo tanto, no es necesario. (ejemplo de Hola siguiente muestra cómo contenedor de hello tooset tener acceso a la lista de control (ACL) y metadatos del contenedor).

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

Al llamar a **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOBS)** hace Hola datos del contenedor y blob accesibles a través de las solicitudes anónimas. Si llama a **setPublicAccess(PublicAccessType::BLOBS_ONLY)**, solo los datos de los blobs pasan a ser accesibles mediante solicitudes anónimas. Para obtener más información sobre las ACL del contenedor, consulte [Set container ACL (API de REST)][container-acl].

Para obtener más información sobre los códigos de error del servicio BLOB, consulte [Códigos de error de Blob Service][error-codes].

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
un archivo como un blob, use hello tooupload **BlobRestProxy -> createBlockBlob** método. Esta operación crea blob Hola si no existe, o lo sobrescribe si lo hace. Hello ejemplo de código siguiente supone que el contenedor de hello ya se ha creado y utiliza [fopen] [ fopen] tooopen archivo de hello como una secuencia.

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

Tenga en cuenta que Hola anterior ejemplo carga un blob como una secuencia. Sin embargo, un blob también se puede cargar como una cadena que se usa, por ejemplo, hello [archivo\_obtener\_contenido] [ file_get_contents] (función). toodo este ejemplo de Hola a anterior, cambie `$content = fopen("c:\myfile.txt", "r");` demasiado`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, use hello **BlobRestProxy -> listBlobs** método con un **foreach** tooloop a través del resultado de hello en bucle. Hello código siguiente muestra el nombre de Hola de cada blob como salida en un contenedor y muestra su explorador toohello URI.

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

## <a name="download-a-blob"></a>Descarga de un blob
toodownload un blob, llamada hello **BlobRestProxy -> getBlob** método y, a continuación, llamada hello **getContentStream** método en hello resultante **GetBlobResult** objeto.

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

Tenga en cuenta que ese ejemplo Hola anterior obtiene un objeto binario como un recurso de secuencia (comportamiento predeterminado de hello). Sin embargo, puede usar hello [flujo\_obtener\_contenido] [ stream-get-contents] Hola de función tooconvert devolvió la cadena de tooa de secuencia.

## <a name="delete-a-blob"></a>Eliminar un blob
toodelete un blob, pase el nombre del contenedor de Hola y el nombre de blob demasiado**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>un contenedor de blobs
Por último, toodelete un contenedor de blobs, pase el nombre del contenedor de hello demasiado**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de hello servicio blob de Azure, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* Visite hello [blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Vea hello [ejemplo de blob de bloque PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Vea hello [ejemplo de blob de página PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)

Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
