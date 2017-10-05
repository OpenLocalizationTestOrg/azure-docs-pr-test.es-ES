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
# <a name="develop-for-azure-file-storage-with-python"></a>Desarrollo para Azure File Storage con Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial mostrará los aspectos básicos del uso de Python para desarrollar aplicaciones o servicios que utilizan Azure File Storage para almacenar datos de archivos. En este tutorial, se creará una aplicación de consola simple y se mostrará cómo realizar las acciones básicas con Python y Azure File Storage:

* Crear recursos compartidos de archivos de Azure
* Crear directorios
* Enumerar los archivos y directorios de un recurso compartido de Azure File
* Cargar, descargar y eliminar un archivo

> [!Note]  
> Dado que se puede acceder a Azure File Storage a través de SMB, es posible escribir aplicaciones simples que accedan al recurso compartido de archivos de Azure mediante las clases y funciones estándar de E/S de Python. En este artículo se describe cómo escribir aplicaciones que utilizan el SDK de Python de Azure Storage, que usa la [API de REST de Azure File Storage](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) para comunicarse con Azure File Storage.

### <a name="set-up-your-application-to-use-azure-file-storage"></a>Configuración de la aplicación para usar Azure File Storage
Agregue lo siguiente cerca de la parte superior de todo archivo de origen de Python en el que desee acceder a Azure Storage mediante programación.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a>Configuración de una conexión a Azure File Storage 
El objeto `FileService` le permite trabajar con recursos compartidos, directorios y archivos. El código siguiente crea un objeto `FileService` mediante el nombre de la cuenta de almacenamiento y la clave de la cuenta. Reemplace `<myaccount>` y `<mykey>` por el nombre y la clave de la de cuenta.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Creación de un recurso compartido de Azure File
En el siguiente código de ejemplo, puede usar un objeto `FileService` para crear el recurso compartido, en caso de que no exista.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Creación de directorios
También puede organizar el almacenamiento colocando archivos dentro de los subdirectorios en lugar de mantenerlos a todos en el directorio raíz. Azure File Storage permite crear tantos directorios como permita su cuenta. El código siguiente creará un subdirectorio denominado **sampledir** bajo el directorio raíz.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar los archivos y directorios de un recurso compartido de Azure File
Para mostrar los archivos y los directorios de un recurso compartido, use el método **list\_directories\_and\_files**. Este método devuelve un generador. El código siguiente ofrece el **nombre** de todos los archivos y el directorio de un recurso compartido de la consola.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Cargar un archivo 
Un recurso compartido de Azure File contiene como mínimo un directorio raíz donde pueden residir los archivos. En esta sección, aprenderá cómo cargar un archivo del almacenamiento local en el directorio raíz de un recurso compartido.

Para crear un archivo y actualizar los datos, use los métodos `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text`. Se trata de métodos de alto nivel que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.

`create_file_from_path` carga el contenido de un archivo de la ruta de acceso especificada y `create_file_from_stream` carga el contenido de un archivo o secuencia ya abiertos. `create_file_from_bytes` carga una matriz de bytes y `create_file_from_text`carga el valor de texto especificado con la codificación especificada (el valor predeterminado es UTF-8).

En el siguiente ejemplo se carga el contenido del archivo **sunset.png** en el archivo **myfile**.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Descarga de un archivo
Para descargar los datos de un archivo, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` o `get_file_to_text`. Se trata de métodos de alto nivel que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.

En el ejemplo siguiente se muestra cómo usar `get_file_to_path` para descargar el contenido en el archivo **myfile** y almacenarlo en el archivo **out-sunset.png**.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Eliminación de un archivo
Finalmente, para eliminar un archivo, llame a `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido a manipular Azure File Storage con Python, siga estos vínculos para obtener más información.

* [Centro para desarrolladores de Python](/develop/python/)
* [API de REST de servicios de almacenamiento de Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [SDK de Almacenamiento de Microsoft Azure para Python](https://github.com/Azure/azure-storage-python)