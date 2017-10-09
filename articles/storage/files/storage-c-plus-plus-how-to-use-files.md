---
title: aaaDevelop para el almacenamiento de archivos de Azure con C++ | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodevelop C++ aplicaciones y servicios que usen toostore de almacenamiento de archivos de Azure datos de archivos."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Desarrollo para Azure File Storage con C++
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Acerca de este tutorial

En este tutorial, aprenderá cómo tooperform operaciones básicas en el almacenamiento de archivos de Azure. A través de ejemplos escritos en C++, obtendrá información sobre cómo se comparte toocreate y directorios, cargar, enumerar y eliminar archivos. Si es nuevo almacenamiento de archivo tooAzure, pasar por conceptos de hello en secciones Hola siguientes será útil para comprender los ejemplos de hello.


* Crear y eliminar recursos compartidos de Azure File
* Crear y eliminar directorios
* Enumerar los archivos y directorios de un recurso compartido de Azure File
* Cargar, descargar y eliminar un archivo
* Establecer la cuota de hello (tamaño máximo) para un recurso compartido de archivos de Azure
* Crear una firma de acceso compartido (clave SAS) para un archivo que usa una directiva de acceso compartido definida en el recurso compartido de Hola.

> [!Note]  
> Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante las funciones y clases de E/S de C++ estándares de Hola. En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de C++ de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.

## <a name="create-a-c-application"></a>Creación de una aplicación de C++
ejemplos de hello toobuild, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure 2.4.0 para C++. También deberá haber creado una cuenta de almacenamiento de Azure.

Hola tooinstall 2.4.0 del cliente de almacenamiento de Azure para C++, puede usar uno de los siguientes métodos de hello:

* **Linux:** seguir instrucciones Hola de hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.
* **Windows:**: en Visual Studio, haga clic en **Herramientas&gt;Administrador de paquetes de NuGet&gt;Consola del Administrador de paquetes**. Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurar el almacenamiento de Azure archivos de aplicación toouse
Agregue el siguiente Hola incluye la parte superior de toohello de instrucciones del archivo de código fuente de C++ Hola donde desea que el almacenamiento de archivos de Azure toomanipulate:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de Almacenamiento de Azure
toouse almacenamiento de archivos, debe tooconnect tooyour cuenta de almacenamiento Azure. Hello primer paso sería tooconfigure una cadena de conexión, lo que vamos a usar cuenta de almacenamiento de tooconnect tooyour. Vamos a definir un toodo variable estática que.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Conexión de cuenta de almacenamiento de Azure tooan
Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento. tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede utilizar hello **analizar** método.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Creación de un recurso compartido de Azure File
Todos los archivos y directorios de Azure File Storage residen en un contenedor denominado **Share**. La cuenta de almacenamiento puede tener tantos recursos compartidos como los que permita la capacidad de su cuenta. recurso compartido de tooobtain acceso tooa y su contenido, deberá toouse un cliente de almacenamiento de archivos de Azure.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Utiliza el cliente de almacenamiento de archivos de Azure de hello, a continuación, puede obtener un recurso compartido tooa de referencia.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

recurso compartido Hola de toocreate, use hello **create_if_not_exists** método de hello **cloud_file_share** objeto.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

En este momento, **compartir** contiene un recurso compartido de tooa de referencia denominado **mi recurso compartido ejemplo**.

## <a name="delete-an-azure-file-share"></a>Eliminación de un recurso compartido de Azure File
Eliminar un recurso compartido se realiza mediante llamada hello **delete_if_exists** método en un objeto cloud_file_share. A continuación se facilita código de ejemplo que lo hace.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Creación de directorios
Puede organizar el almacenamiento colocando archivos dentro de los subdirectorios en lugar de tener todos ellos en el directorio raíz de Hola. Almacenamiento de archivos de Azure permite toocreate como permitir que varios directorios como la cuenta. código de Hello siguiente creará un directorio denominado **mi directorio de ejemplo** en el directorio raíz de hello, así como un subdirectorio denominado **mi subdirectorio de ejemplo**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Eliminación de un directorio
Eliminar un directorio es una tarea sencilla, aunque se debe tener en cuenta que no se puede eliminar un directorio que contenga archivos u otros directorios.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar los archivos y directorios de un recurso compartido de Azure File
Es fácil obtener una lista de archivos y directorios dentro de un recurso compartido mediante la llamada a **list_files_and_directories** en una referencia de **cloud_file_directory**. tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **list_file_and_directory_item**, debe llamar a hello **list_file_and_directory_item.as_file** método tooget una **cloud_ archivo** objeto o hello **list_file_and_directory_item.as_directory** método tooget una **cloud_file_directory** objeto.

Hola siguiente código muestra cómo tooretrieve y salida Hola URI de cada elemento en el directorio raíz de Hola de recurso compartido de Hola.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Cargar un archivo
En muy Hola menos, un recurso compartido de archivos de Azure contiene un directorio raíz donde los archivos pueden encontrarse. En esta sección, aprenderá cómo tooupload un archivo de almacenamiento local en hello raíz del directorio de un recurso compartido.

Hola primer paso para cargar un archivo es tooobtain un directorio de toohello de referencia en el que debe reside. Para ello, que realiza la llamada hello **get_root_directory_reference** método del objeto de recurso compartido de Hola.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Ahora que tiene un directorio de raíz de referencia toohello del recurso compartido de hello, puede cargar un archivo en él. En este ejemplo se carga desde un archivo, desde texto y desde una secuencia.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Descarga de un archivo
archivos de toodownload, recuperar primero una referencia de archivo y, a continuación, llamar a hello **download_to_stream** método tootransfer Hola archivo contenido tooa objeto de secuencia, que, a continuación, puede conservar tooa de archivos local. Como alternativa, puede usar hello **download_to_file** contenido de hello toodownload de método de un archivo local tooa. Puede usar hello **download_text** contenido de hello toodownload de método de un archivo como una cadena de texto.

Hello en el ejemplo siguiente se usa hello **download_to_stream** y **download_text** toodemonstrate métodos descargar archivos de hello, que se crearon en las secciones anteriores.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Eliminación de un archivo
Otra operación común de Azure File Storage es la eliminación de archivos. Hello código siguiente elimina un archivo con el nombre mi-ejemplo-archivo-3 almacenados en el directorio raíz de Hola.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Establecer la cuota de hello (tamaño máximo) para un recurso compartido de archivos de Azure
Puede establecer la cuota de hello (o el tamaño máximo) para un recurso compartido de archivos, en gigabytes. También puede comprobar toosee la cantidad de datos está almacenada en el recurso compartido de Hola.

Establecer la cuota de Hola para un recurso compartido, puede limitar tamaño total de Hola de archivos de hello almacenados en recursos compartidos de Hola. Si supera el tamaño total de Hola de archivos en el recurso compartido de hello establece cuota de hello en el recurso compartido de hello, clientes no se puede tooincrease Hola tamaño de los archivos existentes o crear nuevos archivos, a menos que esos archivos están vacíos.

ejemplo de Hola siguiente muestra cómo toocheck Hola uso actual de un recurso compartido y cómo tooset Hola cuota para el recurso compartido de Hola.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Generar una firma de acceso compartido para un archivo o recurso compartido de archivos
Puede generar una firma de acceso compartido (SAS) para un recurso compartido de archivos o para un archivo individual. También puede crear una directiva de acceso compartido en un acceso toomanage compartido firmas. Se recomienda crear una directiva de acceso compartido, ya que proporciona un medio de revocar Hola SAS si debe estar en peligro.

Hola de ejemplo siguiente crea una directiva de acceso compartido en un recurso compartido y, a continuación, usa que comparten tooprovide hello las restricciones de directivas para una SAS en un archivo en Hola.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Pasos siguientes
toolearn más sobre el almacenamiento de Azure, explorar estos recursos:

* [Biblioteca de cliente de almacenamiento para C++](https://github.com/Azure/azure-storage-cpp)
* [Ejemplos del servicio Azure Storage File en C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Explorador de almacenamiento de Azure](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Documentación de Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/)