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
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="78d95-103">¿Cómo toouse almacenamiento de blobs de Ruby</span><span class="sxs-lookup"><span data-stu-id="78d95-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="78d95-104">Información general</span><span class="sxs-lookup"><span data-stu-id="78d95-104">Overview</span></span>
<span data-ttu-id="78d95-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="78d95-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="78d95-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="78d95-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="78d95-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="78d95-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="78d95-108">Esta guía le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="78d95-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="78d95-109">ejemplos de Hola se escriben con hello API Ruby.</span><span class="sxs-lookup"><span data-stu-id="78d95-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="78d95-110">Hello escenarios descritos se incluyen **cargar, enumerar, descargar,** y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="78d95-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="78d95-111">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="78d95-111">Create a Ruby application</span></span>
<span data-ttu-id="78d95-112">Cree una aplicación de Ruby.</span><span class="sxs-lookup"><span data-stu-id="78d95-112">Create a Ruby application.</span></span> <span data-ttu-id="78d95-113">Para obtener instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="78d95-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="78d95-114">Configurar el almacenamiento de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="78d95-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="78d95-115">toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquete de azure, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="78d95-116">Use el paquete de RubyGems tooobtain Hola</span><span class="sxs-lookup"><span data-stu-id="78d95-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="78d95-117">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="78d95-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="78d95-118">Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.</span><span class="sxs-lookup"><span data-stu-id="78d95-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="78d95-119">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="78d95-119">Import hello package</span></span>
<span data-ttu-id="78d95-120">Con el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="78d95-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="78d95-121">Configuración de una conexión de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="78d95-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="78d95-122">módulo de Hello azure leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_ACCESS_KEY** para cuenta de almacenamiento de Azure de tooconnect tooyour la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="78d95-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="78d95-123">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::Blob::BlobService** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="78d95-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="78d95-124">tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="78d95-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="78d95-125">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78d95-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78d95-126">Navegar por cuenta de almacenamiento toohello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="78d95-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="78d95-127">En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="78d95-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="78d95-128">En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="78d95-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="78d95-129">Puede usar cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="78d95-129">You can use either of these.</span></span>
5. <span data-ttu-id="78d95-130">Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="78d95-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="78d95-131">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="78d95-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="78d95-132">Hola **Azure::Blob::BlobService** objeto le permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="78d95-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="78d95-133">toocreate un contenedor, use hello **crear\_container()** método.</span><span class="sxs-lookup"><span data-stu-id="78d95-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="78d95-134">Hello ejemplo de código siguiente crea un contenedor o imprime error Hola si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="78d95-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="78d95-135">Si desea toomake Hola archivos de hello contenedor público, puede establecer permisos del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="78d95-136">Solo puede modificar hello <strong>crear\_container()</strong> llamada toopass hello **: pública\_acceso\_nivel** opción:</span><span class="sxs-lookup"><span data-stu-id="78d95-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="78d95-137">Los valores válidos de hello **: pública\_acceso\_nivel** opción son:</span><span class="sxs-lookup"><span data-stu-id="78d95-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="78d95-138">**blob:** habilita el acceso de lectura público a los blobs.</span><span class="sxs-lookup"><span data-stu-id="78d95-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="78d95-139">Los datos de blob dentro de este contenedor pueden leerse a través de una solicitud anónima, pero los datos del contenedor no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="78d95-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="78d95-140">Los clientes no pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="78d95-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="78d95-141">**container:** habilita el acceso de lectura público completo a los datos del contenedor y los blobs.</span><span class="sxs-lookup"><span data-stu-id="78d95-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="78d95-142">Los clientes pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="78d95-143">Como alternativa, puede modificar el nivel de acceso público de Hola de un contenedor mediante el uso de **establecer\_contenedor\_acl()** nivel de acceso público de método toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="78d95-144">Hola el siguiente código de ejemplo Hola a cambios de nivel de acceso público demasiado**contenedor**:</span><span class="sxs-lookup"><span data-stu-id="78d95-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="78d95-145">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="78d95-145">Upload a blob into a container</span></span>
<span data-ttu-id="78d95-146">blob de tooupload tooa contenido, use hello **crear\_bloque\_blob()** blob de método toocreate hello, utilice un archivo o una cadena como contenido de Hola de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="78d95-147">Hello código siguiente carga el archivo de hello **test.png** como un blob nuevo denominado "-el blob de imágenes" en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="78d95-148">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="78d95-148">List hello blobs in a container</span></span>
<span data-ttu-id="78d95-149">utilizar contenedores de hello toolist, **list_containers()** método.</span><span class="sxs-lookup"><span data-stu-id="78d95-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="78d95-150">los blobs de hello toolist dentro de un contenedor, usar **lista\_blobs()** método.</span><span class="sxs-lookup"><span data-stu-id="78d95-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="78d95-151">Esto da como resultado hello las direcciones URL de todos los blobs de hello en todos los contenedores de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="78d95-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="78d95-152">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="78d95-152">Download blobs</span></span>
<span data-ttu-id="78d95-153">los blobs de toodownload, usar hello **obtener\_blob()** contenido del método tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="78d95-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="78d95-154">Hello ejemplo de código siguiente muestra cómo utilizar **obtener\_blob()** toodownload Hola contenido de "imagen"blob y escribir tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="78d95-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="78d95-155">un blob</span><span class="sxs-lookup"><span data-stu-id="78d95-155">Delete a Blob</span></span>
<span data-ttu-id="78d95-156">Por último, toodelete un blob, utilice hello **eliminar\_blob()** método.</span><span class="sxs-lookup"><span data-stu-id="78d95-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="78d95-157">Hello ejemplo de código siguiente se muestra cómo toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="78d95-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="78d95-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78d95-158">Next steps</span></span>
<span data-ttu-id="78d95-159">toolearn acerca de las tareas más complejas de almacenamiento, siga estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="78d95-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="78d95-160">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="78d95-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="78d95-161">[SDK de Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub</span><span class="sxs-lookup"><span data-stu-id="78d95-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="78d95-162">Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola</span><span class="sxs-lookup"><span data-stu-id="78d95-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

