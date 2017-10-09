---
title: almacenamiento de blobs de toouse aaaHow (almacenamiento de objetos) de C++ | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>¿Cómo toouse almacenamiento de blobs de C++
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

Esta guía demuestra cómo tooperform escenarios comunes con Hola servicio de almacenamiento de blobs de Azure. ejemplos de Hello están escritos en C++ y usar hello [biblioteca de cliente de almacenamiento de Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.  

> [!NOTE]
> Destinos de esta guía Hola biblioteca de cliente de almacenamiento de Azure para C++ versión 1.0.0 y versiones posteriores. Hola recomienda versión es la biblioteca de cliente de almacenamiento 2.2.0, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Creación de una aplicación de C++
En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.  

toodo por lo tanto, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.   

Hola tooinstall biblioteca de cliente de almacenamiento de Azure para C++, puede usar Hola siguientes métodos:

* **Linux:** seguir instrucciones Hola de hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.  
* **Windows:** en Visual Studio, haga clic en **Herramientas &gt; Administrador de paquetes de NuGet &gt; Consola del Administrador de paquetes**. Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurar el almacenamiento de blobs de aplicación tooaccess
Agregue el siguiente Hola incluye la parte superior de toohello de las instrucciones del archivo de C++ de hello en el que desea toouse Hola almacenamiento de Azure API tooaccess blobs:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de almacenamiento de Azure
Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos. Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, utilizando el nombre de Hola de su clave de acceso almacenamiento hello y cuenta de almacenamiento para cuenta de almacenamiento Hola Hola [Portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores. Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md). Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest la aplicación en el equipo local de Windows, puede usar Microsoft Azure hello [emulador de almacenamiento](storage-use-emulator.md) que se instala con hello [Azure SDK](https://azure.microsoft.com/downloads/). emulador de almacenamiento de Hello es una utilidad que simula los servicios de Blob, cola y tabla de hello disponibles en Azure en su equipo de desarrollo local. Hello en el ejemplo siguiente se muestra cómo se puede declarar un emulador de almacenamiento local de campo estático toohold Hola conexión cadena tooyour:

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulador de almacenamiento de Azure de hello toostart, seleccione hello **iniciar** Hola o presionen **Windows** clave. Comience a escribir **emulador de almacenamiento de Azure**y seleccione **emulador de almacenamiento de Microsoft Azure** de lista de Hola de aplicaciones.  

Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.  

## <a name="retrieve-your-connection-string"></a>Recuperación de la cadena de conexión
Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento. tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede utilizar hello **analizar** método.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

A continuación, obtener una referencia tooa **cloud_blob_client** clase puesto que permite tooretrieve objetos que representan contenedores y blobs almacenados en el servicio de almacenamiento Blob de Hola. Hello código siguiente se crea un **cloud_blob_client** objeto mediante el objeto de cuenta de almacenamiento Hola recuperamos anteriormente:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Cómo crear un contenedor
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Este ejemplo se muestra cómo toocreate un contenedor si aún no existe:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

De forma predeterminada, Hola nuevo contenedor es privado y debe especificar los blobs de toodownload clave de acceso de almacenamiento de este contenedor. Si desea que toomake Hola archivos (BLOB) en hello contenedor disponibles tooeveryone, puede establecer Hola contenedor toobe público mediante el siguiente código de hello:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Todos los usuarios de hello Internet pueden ver los blobs en un contenedor público, pero puede modificar o eliminarlos únicamente si tiene la clave de acceso adecuado de Hola.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Cómo cargar un blob en un contenedor
El almacenamiento de blobs de Azure admite blobs en bloques y en páginas. En la mayoría de los casos Hola blob en bloques es hello recomendada toouse de tipo.  

tooupload un blob en bloques archivo tooa, obtener una referencia de contenedor y usarlo tooget una referencia de blob de bloque. Una vez que tenga una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **upload_from_stream** método. Esta operación creará blob Hola si no existe previamente o sobrescribir si existe. Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

Como alternativa, puede usar hello **upload_from_file** tooupload método un blob en bloques archivo tooa.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Cómo: enumerar los blobs de hello en un contenedor
blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor. A continuación, puede usar del contenedor de hello **list_blobs** blobs de método tooretrieve Hola y/o directorios dentro de él. tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **list_blob_item**, debe llamar a hello **list_blob_item.as_blob** método tooget una **cloud_blob** objeto, o hello **list_blob.as_directory** tooget método un objeto cloud_blob_directory. Hello código siguiente muestra cómo tooretrieve y salida Hola URI de cada elemento de hello **mi contenedor de ejemplo** contenedor:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Para obtener más información sobre cómo enumerar las operaciones, consulte [Enumeración de recursos de almacenamiento de Azure en C++](storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Cómo descargar blobs
blobs toodownload, recuperar primero una referencia de blob y, a continuación, llamar a hello **download_to_stream** método. Hello en el ejemplo siguiente se usa hello **download_to_stream** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede conservar tooa de archivos local.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

Como alternativa, puede usar hello **download_to_file** contenido de hello toodownload de método de un archivo de tooa de blob.
Además, también puede utilizar hello **download_text** contenido de hello toodownload de método de un blob como una cadena de texto.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Cómo eliminar blobs
toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llamar a hello **delete_blob** método en él.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn de vínculos más sobre el almacenamiento de Azure.  

* [¿Cómo toouse almacenamiento de cola desde C++](storage-c-plus-plus-how-to-use-queues.md)
* [¿Cómo toouse almacenamiento de tablas de C++](storage-c-plus-plus-how-to-use-tables.md)
* [Enumeración de los recursos de almacenamiento de Azure en C++](storage-c-plus-plus-enumeration.md)
* [Referencia de la biblioteca de clientes de almacenamiento para C++](http://azure.github.io/azure-storage-cpp)
* [Documentación de Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)

