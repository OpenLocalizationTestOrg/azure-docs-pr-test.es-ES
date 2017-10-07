---
title: aaaHow toouse el almacenamiento de blobs de Azure (almacenamiento de objetos) de Python | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>¿Cómo toouse almacenamiento de blobs de Azure de Python
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

En este artículo le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs. ejemplos de Hello están escritos en Python y usar hello [SDK de almacenamiento de Microsoft Azure para Python]. escenarios de Hello descritos incluyen cargar, enumerar, descargar y eliminación de blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Crear un contenedor
En función de tipo hello de blob que desearía toouse, cree un **BlockBlobService**, **AppendBlobService**, o **PageBlobService** objeto. Hola siguiente de código utiliza un **BlockBlobService** objeto. Agregue los siguiente Hola cerca de parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically almacenamiento de blobs de bloque de Azure.

```python
from azure.storage.blob import BlockBlobService
```

Hello código siguiente se crea un **BlockBlobService** objeto mediante la clave de cuenta y el nombre de la cuenta del almacenamiento Hola.  Reemplace 'myaccount' y 'mykey' por la clave y el nombre de cuenta.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

En el siguiente ejemplo de código de hello, puede usar un **BlockBlobService** contenedor Hola de objetos de toocreate si no existe.

```python
block_blob_service.create_container('mycontainer')
```

De forma predeterminada, nuevo contenedor de hello es privado, por lo que debe especificar la clave de acceso de almacenamiento (como hizo anteriormente) blobs toodownload de este contenedor. Si desea toomake blobs Hola Hola contenedor disponibles tooeveryone, puede crear contenedor de Hola y pasar el nivel de acceso público de hello mediante el siguiente código de hello.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

Como alternativa, puede modificar un contenedor después de haber creado mediante el siguiente código de hello.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Después de este cambio, todos los usuarios de hello Internet pueden ver los blobs en un contenedor público, pero solo puede modificar o eliminarlos.

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
toocreate un blob en bloques y los datos de carga, use hello **crear\_blob\_de\_ruta de acceso**, **crear\_blob\_de\_flujo**, **crear\_blob\_de\_bytes** o **crear\_blob\_de\_texto** métodos. Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.

**crear\_blob\_de\_ruta de acceso** cargas Hola contenido de un archivo de ruta de acceso especificada de hello, y **crear\_blob\_de\_flujo** cargas Hola contenido a partir de una secuencia o archivo ya abierta. **crear\_blob\_de\_bytes** carga una matriz de bytes, y **crear\_blob\_de\_texto** carga Hola especificado valor de texto mediante Hola especifica codificación (valor predeterminado es tooUTF-8).

Hello en el ejemplo siguiente se carga contenido Hola de hello **sunset.png** archivo en hello **myblob** blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, use hello **lista\_blobs** método. Este método devuelve un generador. Hello código siguiente genera hello **nombre** de cada blob en una consola de toohello de contenedor.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Descargar blobs
toodownload datos de un blob, utilice **obtener\_blob\_a\_ruta de acceso**, **obtener\_blob\_a\_flujo**, **obtener\_blob\_a\_bytes**, o **obtener\_blob\_a\_texto**. Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.

Hello en el ejemplo siguiente se muestra cómo utilizar **obtener\_blob\_a\_ruta de acceso** contenido de hello toodownload de hello **myblob** blob y almacenar toohello **fuera sunset.png** archivo.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Eliminar un blob
Por último, llame un blob, toodelete **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Escritura tooan anexar blob
Un blob en anexos se optimiza para las operaciones de anexado, como el registro. Como un blob en bloques, un blob en anexos está formado por bloques, pero cuando se agrega un nuevo blob en bloques tooan anexado, siempre es toohello anexado final del blob de Hola. No se puede actualizar o eliminar un bloque existente en un blob en anexos. Identificadores de bloque de Hola para un blob en anexos no se exponen como sirven como un blob en bloques.

Cada bloque de un blob en anexos puede tener un tamaño diferente, la tooa máximo de 4 MB, y un blob en anexos puede incluir un máximo de 50.000 bloques. tamaño máximo de Hola de un blob en anexos, por tanto, es un poco más de 195 GB (4 MB X 50.000 bloques).

ejemplo de Hola siguiente crea un nuevo blob en anexos y anexa algunos tooit de datos, simular una operación de registro simple.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn de vínculos más.

* [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/)
* [API de REST de servicios de almacenamiento de Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog del equipo de almacenamiento de Azure]
* [SDK de almacenamiento de Microsoft Azure para Python]

[Blog del equipo de almacenamiento de Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[SDK de almacenamiento de Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python
