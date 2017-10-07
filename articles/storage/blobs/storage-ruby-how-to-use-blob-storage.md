---
title: aaaHow toouse (almacenamiento de objetos) de almacenamiento de blobs de Ruby | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>¿Cómo toouse almacenamiento de blobs de Ruby
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

Esta guía le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs. ejemplos de Hola se escriben con hello API Ruby. Hello escenarios descritos se incluyen **cargar, enumerar, descargar,** y **eliminar** blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Creación de una aplicación de Ruby
Cree una aplicación de Ruby. Para obtener instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar el almacenamiento de aplicación tooaccess
toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquete de azure, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use el paquete de RubyGems tooobtain Hola
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.

### <a name="import-hello-package"></a>Importar paquete de Hola
Con el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de Azure Storage
módulo de Hello azure leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_ACCESS_KEY** para cuenta de almacenamiento de Azure de tooconnect tooyour la información necesaria. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::Blob::BlobService** con hello siguiente código:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Navegar por cuenta de almacenamiento toohello que desea toouse.
3. En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.
4. En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso. Puede usar cualquiera de estas.
5. Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.

## <a name="create-a-container"></a>Crear un contenedor
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Hola **Azure::Blob::BlobService** objeto le permite trabajar con contenedores y blobs. toocreate un contenedor, use hello **crear\_container()** método.

Hello ejemplo de código siguiente crea un contenedor o imprime error Hola si hay alguno.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Si desea toomake Hola archivos de hello contenedor público, puede establecer permisos del contenedor de Hola.

Solo puede modificar hello <strong>crear\_container()</strong> llamada toopass hello **: pública\_acceso\_nivel** opción:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Los valores válidos de hello **: pública\_acceso\_nivel** opción son:

* **blob:** habilita el acceso de lectura público a los blobs. Los datos de blob dentro de este contenedor pueden leerse a través de una solicitud anónima, pero los datos del contenedor no están disponibles. Los clientes no pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima.
* **container:** habilita el acceso de lectura público completo a los datos del contenedor y los blobs. Los clientes pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.

Como alternativa, puede modificar el nivel de acceso público de Hola de un contenedor mediante el uso de **establecer\_contenedor\_acl()** nivel de acceso público de método toospecify Hola.

Hola el siguiente código de ejemplo Hola a cambios de nivel de acceso público demasiado**contenedor**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
blob de tooupload tooa contenido, use hello **crear\_bloque\_blob()** blob de método toocreate hello, utilice un archivo o una cadena como contenido de Hola de blob de Hola.

Hello código siguiente carga el archivo de hello **test.png** como un blob nuevo denominado "-el blob de imágenes" en el contenedor de Hola.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
utilizar contenedores de hello toolist, **list_containers()** método.
los blobs de hello toolist dentro de un contenedor, usar **lista\_blobs()** método.

Esto da como resultado hello las direcciones URL de todos los blobs de hello en todos los contenedores de hello para la cuenta de hello.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Descargar blobs
los blobs de toodownload, usar hello **obtener\_blob()** contenido del método tooretrieve Hola.

Hello ejemplo de código siguiente muestra cómo utilizar **obtener\_blob()** toodownload Hola contenido de "imagen"blob y escribir tooa de archivos local.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>un blob
Por último, toodelete un blob, utilice hello **eliminar\_blob()** método. Hello ejemplo de código siguiente se muestra cómo toodelete un blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Pasos siguientes
toolearn acerca de las tareas más complejas de almacenamiento, siga estos vínculos:

* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [SDK de Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

