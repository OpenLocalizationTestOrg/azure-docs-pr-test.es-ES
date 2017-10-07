---
title: aaaDevelop para el almacenamiento de archivos de Azure con Python | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodevelop Python aplicaciones y servicios que use toostore de almacenamiento de archivos de Azure datos de archivos."
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="db39b-103">Desarrollo para Azure File Storage con Python</span><span class="sxs-lookup"><span data-stu-id="db39b-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="db39b-104">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="db39b-104">About this tutorial</span></span>
<span data-ttu-id="db39b-105">Este tutorial demuestra conceptos básicos de hello del uso de Python toodevelop aplicaciones o servicios que utilizan datos de archivos de toostore de almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="db39b-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="db39b-106">En este tutorial, crearemos una aplicación de consola simple y mostrar cómo tooperform acciones básicas con el almacenamiento de Python y archivos de Azure:</span><span class="sxs-lookup"><span data-stu-id="db39b-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="db39b-107">Crear recursos compartidos de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="db39b-107">Create Azure File shares</span></span>
* <span data-ttu-id="db39b-108">Crear directorios</span><span class="sxs-lookup"><span data-stu-id="db39b-108">Create directories</span></span>
* <span data-ttu-id="db39b-109">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="db39b-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="db39b-110">Cargar, descargar y eliminar un archivo</span><span class="sxs-lookup"><span data-stu-id="db39b-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="db39b-111">Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante las funciones y clases de E/S de Python estándares de Hola.</span><span class="sxs-lookup"><span data-stu-id="db39b-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="db39b-112">En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de Python de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="db39b-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="db39b-113">Configurar el almacenamiento de Azure archivos de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="db39b-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="db39b-114">Agregue los siguiente Hola cerca de la parte superior de Hola de cualquier archivo de código fuente de Python en las que quiera tooprogrammatically acceso a almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="db39b-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="db39b-115">Configurar una tooAzure de conexión almacenamiento de archivos</span><span class="sxs-lookup"><span data-stu-id="db39b-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="db39b-116">Hola `FileService` objeto le permite trabajar con recursos compartidos, directorios y archivos.</span><span class="sxs-lookup"><span data-stu-id="db39b-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="db39b-117">Hello código siguiente se crea un `FileService` objeto mediante la clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="db39b-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="db39b-118">Reemplace `<myaccount>` y `<mykey>` por el nombre y la clave de la de cuenta.</span><span class="sxs-lookup"><span data-stu-id="db39b-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="db39b-119">Creación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="db39b-119">Create an Azure File share</span></span>
<span data-ttu-id="db39b-120">En el siguiente ejemplo de código de hello, puede usar un `FileService` compartir de hello toocreate del objeto si no existe.</span><span class="sxs-lookup"><span data-stu-id="db39b-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="db39b-121">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="db39b-121">Create a directory</span></span>
<span data-ttu-id="db39b-122">También puede organizar el almacenamiento de información colocando archivos dentro de los subdirectorios en lugar de tener todos ellos en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="db39b-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="db39b-123">Almacenamiento de archivos de Azure permite toocreate como permitir que varios directorios como la cuenta.</span><span class="sxs-lookup"><span data-stu-id="db39b-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="db39b-124">código de Hello siguiente creará un subdirectorio denominado **sampledir** en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="db39b-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="db39b-125">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="db39b-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="db39b-126">archivos de hello toolist y directorios en un recurso compartido, utilice hello **lista\_directorios\_y\_archivos** método.</span><span class="sxs-lookup"><span data-stu-id="db39b-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="db39b-127">Este método devuelve un generador.</span><span class="sxs-lookup"><span data-stu-id="db39b-127">This method returns a generator.</span></span> <span data-ttu-id="db39b-128">Hello código siguiente genera hello **nombre** de cada archivo y directorio en una consola de toohello de recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="db39b-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="db39b-129">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="db39b-129">Upload a file</span></span> 
<span data-ttu-id="db39b-130">Archivos de Azure recurso compartido contiene en hello muy menos, un directorio raíz donde los archivos pueden encontrarse.</span><span class="sxs-lookup"><span data-stu-id="db39b-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="db39b-131">En esta sección, aprenderá cómo tooupload un archivo de almacenamiento local en hello raíz del directorio de un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="db39b-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="db39b-132">toocreate un archivo y los datos de carga, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text` métodos.</span><span class="sxs-lookup"><span data-stu-id="db39b-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="db39b-133">Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="db39b-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="db39b-134">`create_file_from_path`cargas Hola contenido de un archivo de ruta de acceso especificada de hello, y `create_file_from_stream` cargas Hola contenido a partir de una secuencia o archivo ya abierta.</span><span class="sxs-lookup"><span data-stu-id="db39b-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="db39b-135">`create_file_from_bytes`carga una matriz de bytes, y `create_file_from_text` Hola de cargas especifica valor de texto mediante Hola codificación (valor predeterminado es tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="db39b-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="db39b-136">Hello en el ejemplo siguiente se carga contenido Hola de hello **sunset.png** archivo en hello **myfile** archivo.</span><span class="sxs-lookup"><span data-stu-id="db39b-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="db39b-137">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="db39b-137">Download a file</span></span>
<span data-ttu-id="db39b-138">toodownload datos desde un archivo, utilice `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, o `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="db39b-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="db39b-139">Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="db39b-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="db39b-140">Hello en el ejemplo siguiente se muestra cómo utilizar `get_file_to_path` contenido de hello toodownload de hello **myfile** de archivo y almacenar toohello **sunset.png fuera** archivo.</span><span class="sxs-lookup"><span data-stu-id="db39b-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="db39b-141">Eliminación de un archivo</span><span class="sxs-lookup"><span data-stu-id="db39b-141">Delete a file</span></span>
<span data-ttu-id="db39b-142">Por último, llame toodelete un archivo, `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="db39b-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="db39b-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db39b-143">Next steps</span></span>
<span data-ttu-id="db39b-144">Ahora que ha aprendido cómo toomanipulate almacenamiento de archivos de Azure con Python, siga estas toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="db39b-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="db39b-145">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="db39b-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="db39b-146">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="db39b-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="db39b-147">SDK de Almacenamiento de Microsoft Azure para Python</span><span class="sxs-lookup"><span data-stu-id="db39b-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)