---
title: Desarrollo para Azure File Storage con Python | Microsoft Docs
description: Aprenda a desarrollar aplicaciones y servicios de Python que utilizan Azure File Storage para almacenar datos de archivos.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="e1d34-103">Desarrollo para Azure File Storage con Python</span><span class="sxs-lookup"><span data-stu-id="e1d34-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="e1d34-104">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="e1d34-104">About this tutorial</span></span>
<span data-ttu-id="e1d34-105">Este tutorial mostrará los aspectos básicos del uso de Python para desarrollar aplicaciones o servicios que utilizan Azure File Storage para almacenar datos de archivos.</span><span class="sxs-lookup"><span data-stu-id="e1d34-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="e1d34-106">En este tutorial, se creará una aplicación de consola simple y se mostrará cómo realizar las acciones básicas con Python y Azure File Storage:</span><span class="sxs-lookup"><span data-stu-id="e1d34-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="e1d34-107">Crear recursos compartidos de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="e1d34-107">Create Azure File shares</span></span>
* <span data-ttu-id="e1d34-108">Crear directorios</span><span class="sxs-lookup"><span data-stu-id="e1d34-108">Create directories</span></span>
* <span data-ttu-id="e1d34-109">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="e1d34-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="e1d34-110">Cargar, descargar y eliminar un archivo</span><span class="sxs-lookup"><span data-stu-id="e1d34-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="e1d34-111">Dado que se puede acceder a Azure File Storage a través de SMB, es posible escribir aplicaciones simples que accedan al recurso compartido de archivos de Azure mediante las clases y funciones estándar de E/S de Python.</span><span class="sxs-lookup"><span data-stu-id="e1d34-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="e1d34-112">En este artículo se describe cómo escribir aplicaciones que utilizan el SDK de Python de Azure Storage, que usa la [API de REST de Azure File Storage](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) para comunicarse con Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="e1d34-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="e1d34-113">Configuración de la aplicación para usar Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e1d34-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="e1d34-114">Agregue lo siguiente cerca de la parte superior de todo archivo de origen de Python en el que desee acceder a Azure Storage mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e1d34-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="e1d34-115">Configuración de una conexión a Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e1d34-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="e1d34-116">El objeto `FileService` le permite trabajar con recursos compartidos, directorios y archivos.</span><span class="sxs-lookup"><span data-stu-id="e1d34-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="e1d34-117">El código siguiente crea un objeto `FileService` mediante el nombre de la cuenta de almacenamiento y la clave de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="e1d34-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="e1d34-118">Reemplace `<myaccount>` y `<mykey>` por el nombre y la clave de la de cuenta.</span><span class="sxs-lookup"><span data-stu-id="e1d34-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="e1d34-119">Creación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="e1d34-119">Create an Azure File share</span></span>
<span data-ttu-id="e1d34-120">En el siguiente código de ejemplo, puede usar un objeto `FileService` para crear el recurso compartido, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="e1d34-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="e1d34-121">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="e1d34-121">Create a directory</span></span>
<span data-ttu-id="e1d34-122">También puede organizar el almacenamiento colocando archivos dentro de los subdirectorios en lugar de mantenerlos a todos en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="e1d34-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="e1d34-123">Azure File Storage permite crear tantos directorios como permita su cuenta.</span><span class="sxs-lookup"><span data-stu-id="e1d34-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="e1d34-124">El código siguiente creará un subdirectorio denominado **sampledir** bajo el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="e1d34-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="e1d34-125">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="e1d34-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="e1d34-126">Para mostrar los archivos y los directorios de un recurso compartido, use el método **list\_directories\_and\_files**.</span><span class="sxs-lookup"><span data-stu-id="e1d34-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="e1d34-127">Este método devuelve un generador.</span><span class="sxs-lookup"><span data-stu-id="e1d34-127">This method returns a generator.</span></span> <span data-ttu-id="e1d34-128">El código siguiente ofrece el **nombre** de todos los archivos y el directorio de un recurso compartido de la consola.</span><span class="sxs-lookup"><span data-stu-id="e1d34-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="e1d34-129">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="e1d34-129">Upload a file</span></span> 
<span data-ttu-id="e1d34-130">Un recurso compartido de Azure File contiene como mínimo un directorio raíz donde pueden residir los archivos.</span><span class="sxs-lookup"><span data-stu-id="e1d34-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="e1d34-131">En esta sección, aprenderá cómo cargar un archivo del almacenamiento local en el directorio raíz de un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="e1d34-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="e1d34-132">Para crear un archivo y actualizar los datos, use los métodos `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text`.</span><span class="sxs-lookup"><span data-stu-id="e1d34-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="e1d34-133">Se trata de métodos de alto nivel que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="e1d34-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="e1d34-134">`create_file_from_path` carga el contenido de un archivo de la ruta de acceso especificada y `create_file_from_stream` carga el contenido de un archivo o secuencia ya abiertos.</span><span class="sxs-lookup"><span data-stu-id="e1d34-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="e1d34-135">`create_file_from_bytes` carga una matriz de bytes y `create_file_from_text`carga el valor de texto especificado con la codificación especificada (el valor predeterminado es UTF-8).</span><span class="sxs-lookup"><span data-stu-id="e1d34-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="e1d34-136">En el siguiente ejemplo se carga el contenido del archivo **sunset.png** en el archivo **myfile**.</span><span class="sxs-lookup"><span data-stu-id="e1d34-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="e1d34-137">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="e1d34-137">Download a file</span></span>
<span data-ttu-id="e1d34-138">Para descargar los datos de un archivo, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` o `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="e1d34-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="e1d34-139">Se trata de métodos de alto nivel que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="e1d34-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="e1d34-140">En el ejemplo siguiente se muestra cómo usar `get_file_to_path` para descargar el contenido en el archivo **myfile** y almacenarlo en el archivo **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="e1d34-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="e1d34-141">Eliminación de un archivo</span><span class="sxs-lookup"><span data-stu-id="e1d34-141">Delete a file</span></span>
<span data-ttu-id="e1d34-142">Finalmente, para eliminar un archivo, llame a `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="e1d34-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="e1d34-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1d34-143">Next steps</span></span>
<span data-ttu-id="e1d34-144">Ahora que ha aprendido a manipular Azure File Storage con Python, siga estos vínculos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e1d34-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="e1d34-145">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="e1d34-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="e1d34-146">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e1d34-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="e1d34-147">SDK de Almacenamiento de Microsoft Azure para Python</span><span class="sxs-lookup"><span data-stu-id="e1d34-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)