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
# <a name="develop-for-azure-file-storage-with-python"></a>Desarrollo para Azure File Storage con Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial demuestra conceptos básicos de hello del uso de Python toodevelop aplicaciones o servicios que utilizan datos de archivos de toostore de almacenamiento de archivos de Azure. En este tutorial, crearemos una aplicación de consola simple y mostrar cómo tooperform acciones básicas con el almacenamiento de Python y archivos de Azure:

* Crear recursos compartidos de archivos de Azure
* Crear directorios
* Enumerar los archivos y directorios de un recurso compartido de Azure File
* Cargar, descargar y eliminar un archivo

> [!Note]  
> Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante las funciones y clases de E/S de Python estándares de Hola. En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de Python de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurar el almacenamiento de Azure archivos de aplicación toouse
Agregue los siguiente Hola cerca de la parte superior de Hola de cualquier archivo de código fuente de Python en las que quiera tooprogrammatically acceso a almacenamiento de Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Configurar una tooAzure de conexión almacenamiento de archivos 
Hola `FileService` objeto le permite trabajar con recursos compartidos, directorios y archivos. Hello código siguiente se crea un `FileService` objeto mediante la clave de cuenta y el nombre de la cuenta del almacenamiento Hola. Reemplace `<myaccount>` y `<mykey>` por el nombre y la clave de la de cuenta.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Creación de un recurso compartido de Azure File
En el siguiente ejemplo de código de hello, puede usar un `FileService` compartir de hello toocreate del objeto si no existe.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Creación de directorios
También puede organizar el almacenamiento de información colocando archivos dentro de los subdirectorios en lugar de tener todos ellos en el directorio raíz de Hola. Almacenamiento de archivos de Azure permite toocreate como permitir que varios directorios como la cuenta. código de Hello siguiente creará un subdirectorio denominado **sampledir** en el directorio raíz de Hola.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar los archivos y directorios de un recurso compartido de Azure File
archivos de hello toolist y directorios en un recurso compartido, utilice hello **lista\_directorios\_y\_archivos** método. Este método devuelve un generador. Hello código siguiente genera hello **nombre** de cada archivo y directorio en una consola de toohello de recurso compartido.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Cargar un archivo 
Archivos de Azure recurso compartido contiene en hello muy menos, un directorio raíz donde los archivos pueden encontrarse. En esta sección, aprenderá cómo tooupload un archivo de almacenamiento local en hello raíz del directorio de un recurso compartido.

toocreate un archivo y los datos de carga, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text` métodos. Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.

`create_file_from_path`cargas Hola contenido de un archivo de ruta de acceso especificada de hello, y `create_file_from_stream` cargas Hola contenido a partir de una secuencia o archivo ya abierta. `create_file_from_bytes`carga una matriz de bytes, y `create_file_from_text` Hola de cargas especifica valor de texto mediante Hola codificación (valor predeterminado es tooUTF-8).

Hello en el ejemplo siguiente se carga contenido Hola de hello **sunset.png** archivo en hello **myfile** archivo.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Descarga de un archivo
toodownload datos desde un archivo, utilice `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, o `get_file_to_text`. Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.

Hello en el ejemplo siguiente se muestra cómo utilizar `get_file_to_path` contenido de hello toodownload de hello **myfile** de archivo y almacenar toohello **sunset.png fuera** archivo.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Eliminación de un archivo
Por último, llame toodelete un archivo, `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido cómo toomanipulate almacenamiento de archivos de Azure con Python, siga estas toolearn de vínculos más.

* [Centro para desarrolladores de Python](/develop/python/)
* [API de REST de servicios de almacenamiento de Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [SDK de Almacenamiento de Microsoft Azure para Python](https://github.com/Azure/azure-storage-python)