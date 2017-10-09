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
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="d457d-103">Desarrollo para Azure File Storage con C++</span><span class="sxs-lookup"><span data-stu-id="d457d-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="d457d-104">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="d457d-104">About this tutorial</span></span>

<span data-ttu-id="d457d-105">En este tutorial, aprenderá cómo tooperform operaciones básicas en el almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d457d-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="d457d-106">A través de ejemplos escritos en C++, obtendrá información sobre cómo se comparte toocreate y directorios, cargar, enumerar y eliminar archivos.</span><span class="sxs-lookup"><span data-stu-id="d457d-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="d457d-107">Si es nuevo almacenamiento de archivo tooAzure, pasar por conceptos de hello en secciones Hola siguientes será útil para comprender los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="d457d-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="d457d-108">Crear y eliminar recursos compartidos de Azure File</span><span class="sxs-lookup"><span data-stu-id="d457d-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="d457d-109">Crear y eliminar directorios</span><span class="sxs-lookup"><span data-stu-id="d457d-109">Create and delete directories</span></span>
* <span data-ttu-id="d457d-110">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="d457d-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="d457d-111">Cargar, descargar y eliminar un archivo</span><span class="sxs-lookup"><span data-stu-id="d457d-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="d457d-112">Establecer la cuota de hello (tamaño máximo) para un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="d457d-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="d457d-113">Crear una firma de acceso compartido (clave SAS) para un archivo que usa una directiva de acceso compartido definida en el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="d457d-114">Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante las funciones y clases de E/S de C++ estándares de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="d457d-115">En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de C++ de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="d457d-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="d457d-116">Creación de una aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="d457d-116">Create a C++ application</span></span>
<span data-ttu-id="d457d-117">ejemplos de hello toobuild, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure 2.4.0 para C++.</span><span class="sxs-lookup"><span data-stu-id="d457d-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="d457d-118">También deberá haber creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d457d-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="d457d-119">Hola tooinstall 2.4.0 del cliente de almacenamiento de Azure para C++, puede usar uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="d457d-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="d457d-120">**Linux:** seguir instrucciones Hola de hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="d457d-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="d457d-121">**Windows:**: en Visual Studio, haga clic en **Herramientas&gt;Administrador de paquetes de NuGet&gt;Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="d457d-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="d457d-122">Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="d457d-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="d457d-123">Configurar el almacenamiento de Azure archivos de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="d457d-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="d457d-124">Agregue el siguiente Hola incluye la parte superior de toohello de instrucciones del archivo de código fuente de C++ Hola donde desea que el almacenamiento de archivos de Azure toomanipulate:</span><span class="sxs-lookup"><span data-stu-id="d457d-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d457d-125">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d457d-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="d457d-126">toouse almacenamiento de archivos, debe tooconnect tooyour cuenta de almacenamiento Azure.</span><span class="sxs-lookup"><span data-stu-id="d457d-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="d457d-127">Hello primer paso sería tooconfigure una cadena de conexión, lo que vamos a usar cuenta de almacenamiento de tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="d457d-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="d457d-128">Vamos a definir un toodo variable estática que.</span><span class="sxs-lookup"><span data-stu-id="d457d-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="d457d-129">Conexión de cuenta de almacenamiento de Azure tooan</span><span class="sxs-lookup"><span data-stu-id="d457d-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="d457d-130">Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d457d-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="d457d-131">tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede utilizar hello **analizar** método.</span><span class="sxs-lookup"><span data-stu-id="d457d-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="d457d-132">Creación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="d457d-132">Create an Azure File share</span></span>
<span data-ttu-id="d457d-133">Todos los archivos y directorios de Azure File Storage residen en un contenedor denominado **Share**.</span><span class="sxs-lookup"><span data-stu-id="d457d-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="d457d-134">La cuenta de almacenamiento puede tener tantos recursos compartidos como los que permita la capacidad de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="d457d-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="d457d-135">recurso compartido de tooobtain acceso tooa y su contenido, deberá toouse un cliente de almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d457d-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="d457d-136">Utiliza el cliente de almacenamiento de archivos de Azure de hello, a continuación, puede obtener un recurso compartido tooa de referencia.</span><span class="sxs-lookup"><span data-stu-id="d457d-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="d457d-137">recurso compartido Hola de toocreate, use hello **create_if_not_exists** método de hello **cloud_file_share** objeto.</span><span class="sxs-lookup"><span data-stu-id="d457d-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="d457d-138">En este momento, **compartir** contiene un recurso compartido de tooa de referencia denominado **mi recurso compartido ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="d457d-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="d457d-139">Eliminación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="d457d-139">Delete an Azure File share</span></span>
<span data-ttu-id="d457d-140">Eliminar un recurso compartido se realiza mediante llamada hello **delete_if_exists** método en un objeto cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="d457d-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="d457d-141">A continuación se facilita código de ejemplo que lo hace.</span><span class="sxs-lookup"><span data-stu-id="d457d-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="d457d-142">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="d457d-142">Create a directory</span></span>
<span data-ttu-id="d457d-143">Puede organizar el almacenamiento colocando archivos dentro de los subdirectorios en lugar de tener todos ellos en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="d457d-144">Almacenamiento de archivos de Azure permite toocreate como permitir que varios directorios como la cuenta.</span><span class="sxs-lookup"><span data-stu-id="d457d-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="d457d-145">código de Hello siguiente creará un directorio denominado **mi directorio de ejemplo** en el directorio raíz de hello, así como un subdirectorio denominado **mi subdirectorio de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="d457d-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="d457d-146">Eliminación de un directorio</span><span class="sxs-lookup"><span data-stu-id="d457d-146">Delete a directory</span></span>
<span data-ttu-id="d457d-147">Eliminar un directorio es una tarea sencilla, aunque se debe tener en cuenta que no se puede eliminar un directorio que contenga archivos u otros directorios.</span><span class="sxs-lookup"><span data-stu-id="d457d-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="d457d-148">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="d457d-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="d457d-149">Es fácil obtener una lista de archivos y directorios dentro de un recurso compartido mediante la llamada a **list_files_and_directories** en una referencia de **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="d457d-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="d457d-150">tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **list_file_and_directory_item**, debe llamar a hello **list_file_and_directory_item.as_file** método tooget una **cloud_ archivo** objeto o hello **list_file_and_directory_item.as_directory** método tooget una **cloud_file_directory** objeto.</span><span class="sxs-lookup"><span data-stu-id="d457d-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="d457d-151">Hola siguiente código muestra cómo tooretrieve y salida Hola URI de cada elemento en el directorio raíz de Hola de recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

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

## <a name="upload-a-file"></a><span data-ttu-id="d457d-152">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="d457d-152">Upload a file</span></span>
<span data-ttu-id="d457d-153">En muy Hola menos, un recurso compartido de archivos de Azure contiene un directorio raíz donde los archivos pueden encontrarse.</span><span class="sxs-lookup"><span data-stu-id="d457d-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="d457d-154">En esta sección, aprenderá cómo tooupload un archivo de almacenamiento local en hello raíz del directorio de un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="d457d-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="d457d-155">Hola primer paso para cargar un archivo es tooobtain un directorio de toohello de referencia en el que debe reside.</span><span class="sxs-lookup"><span data-stu-id="d457d-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="d457d-156">Para ello, que realiza la llamada hello **get_root_directory_reference** método del objeto de recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="d457d-157">Ahora que tiene un directorio de raíz de referencia toohello del recurso compartido de hello, puede cargar un archivo en él.</span><span class="sxs-lookup"><span data-stu-id="d457d-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="d457d-158">En este ejemplo se carga desde un archivo, desde texto y desde una secuencia.</span><span class="sxs-lookup"><span data-stu-id="d457d-158">This example uploads from a file, from text, and from a stream.</span></span>

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

## <a name="download-a-file"></a><span data-ttu-id="d457d-159">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="d457d-159">Download a file</span></span>
<span data-ttu-id="d457d-160">archivos de toodownload, recuperar primero una referencia de archivo y, a continuación, llamar a hello **download_to_stream** método tootransfer Hola archivo contenido tooa objeto de secuencia, que, a continuación, puede conservar tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="d457d-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="d457d-161">Como alternativa, puede usar hello **download_to_file** contenido de hello toodownload de método de un archivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="d457d-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="d457d-162">Puede usar hello **download_text** contenido de hello toodownload de método de un archivo como una cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="d457d-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="d457d-163">Hello en el ejemplo siguiente se usa hello **download_to_stream** y **download_text** toodemonstrate métodos descargar archivos de hello, que se crearon en las secciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="d457d-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="d457d-164">Eliminación de un archivo</span><span class="sxs-lookup"><span data-stu-id="d457d-164">Delete a file</span></span>
<span data-ttu-id="d457d-165">Otra operación común de Azure File Storage es la eliminación de archivos.</span><span class="sxs-lookup"><span data-stu-id="d457d-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="d457d-166">Hello código siguiente elimina un archivo con el nombre mi-ejemplo-archivo-3 almacenados en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

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

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="d457d-167">Establecer la cuota de hello (tamaño máximo) para un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="d457d-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="d457d-168">Puede establecer la cuota de hello (o el tamaño máximo) para un recurso compartido de archivos, en gigabytes.</span><span class="sxs-lookup"><span data-stu-id="d457d-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="d457d-169">También puede comprobar toosee la cantidad de datos está almacenada en el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="d457d-170">Establecer la cuota de Hola para un recurso compartido, puede limitar tamaño total de Hola de archivos de hello almacenados en recursos compartidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="d457d-171">Si supera el tamaño total de Hola de archivos en el recurso compartido de hello establece cuota de hello en el recurso compartido de hello, clientes no se puede tooincrease Hola tamaño de los archivos existentes o crear nuevos archivos, a menos que esos archivos están vacíos.</span><span class="sxs-lookup"><span data-stu-id="d457d-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="d457d-172">ejemplo de Hola siguiente muestra cómo toocheck Hola uso actual de un recurso compartido y cómo tooset Hola cuota para el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

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

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="d457d-173">Generar una firma de acceso compartido para un archivo o recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="d457d-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="d457d-174">Puede generar una firma de acceso compartido (SAS) para un recurso compartido de archivos o para un archivo individual.</span><span class="sxs-lookup"><span data-stu-id="d457d-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="d457d-175">También puede crear una directiva de acceso compartido en un acceso toomanage compartido firmas.</span><span class="sxs-lookup"><span data-stu-id="d457d-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="d457d-176">Se recomienda crear una directiva de acceso compartido, ya que proporciona un medio de revocar Hola SAS si debe estar en peligro.</span><span class="sxs-lookup"><span data-stu-id="d457d-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="d457d-177">Hola de ejemplo siguiente crea una directiva de acceso compartido en un recurso compartido y, a continuación, usa que comparten tooprovide hello las restricciones de directivas para una SAS en un archivo en Hola.</span><span class="sxs-lookup"><span data-stu-id="d457d-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="d457d-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d457d-178">Next steps</span></span>
<span data-ttu-id="d457d-179">toolearn más sobre el almacenamiento de Azure, explorar estos recursos:</span><span class="sxs-lookup"><span data-stu-id="d457d-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="d457d-180">Biblioteca de cliente de almacenamiento para C++</span><span class="sxs-lookup"><span data-stu-id="d457d-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="d457d-181">[Ejemplos del servicio Azure Storage File en C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="d457d-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="d457d-182">Explorador de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d457d-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="d457d-183">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d457d-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)