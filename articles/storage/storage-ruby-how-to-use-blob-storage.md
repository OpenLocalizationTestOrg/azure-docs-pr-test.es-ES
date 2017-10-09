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
ms.openlocfilehash: 638826777f5a7ae8330fd67cdbb51d5eee1736a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="939d1-103">¿Cómo toouse almacenamiento de blobs de Ruby</span><span class="sxs-lookup"><span data-stu-id="939d1-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="939d1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="939d1-104">Overview</span></span>
<span data-ttu-id="939d1-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="939d1-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="939d1-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="939d1-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="939d1-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="939d1-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="939d1-108">Esta guía le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="939d1-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="939d1-109">ejemplos de Hola se escriben con hello API Ruby.</span><span class="sxs-lookup"><span data-stu-id="939d1-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="939d1-110">Hello escenarios descritos se incluyen **cargar, enumerar, descargar,** y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="939d1-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="939d1-111">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="939d1-111">Create a Ruby application</span></span>
<span data-ttu-id="939d1-112">Cree una aplicación de Ruby.</span><span class="sxs-lookup"><span data-stu-id="939d1-112">Create a Ruby application.</span></span> <span data-ttu-id="939d1-113">Para obtener instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="939d1-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="939d1-114">Configurar el almacenamiento de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="939d1-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="939d1-115">toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquete de azure, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="939d1-116">Use el paquete de RubyGems tooobtain Hola</span><span class="sxs-lookup"><span data-stu-id="939d1-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="939d1-117">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="939d1-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="939d1-118">Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.</span><span class="sxs-lookup"><span data-stu-id="939d1-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="939d1-119">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="939d1-119">Import hello package</span></span>
<span data-ttu-id="939d1-120">Con el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="939d1-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="939d1-121">Configuración de una conexión de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="939d1-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="939d1-122">módulo de Hello azure leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_ACCESS_KEY** para cuenta de almacenamiento de Azure de tooconnect tooyour la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="939d1-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="939d1-123">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::Blob::BlobService** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="939d1-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="939d1-124">tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="939d1-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="939d1-125">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="939d1-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="939d1-126">Navegar por cuenta de almacenamiento toohello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="939d1-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="939d1-127">En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="939d1-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="939d1-128">En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="939d1-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="939d1-129">Puede usar cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="939d1-129">You can use either of these.</span></span>
5. <span data-ttu-id="939d1-130">Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="939d1-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="939d1-131">Estos valores desde un almacenamiento clásico tooobtain tenga en cuenta en el portal de Azure clásico hello:</span><span class="sxs-lookup"><span data-stu-id="939d1-131">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="939d1-132">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="939d1-132">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="939d1-133">Navegar por cuenta de almacenamiento toohello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="939d1-133">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="939d1-134">Haga clic en **administrar claves de acceso** final Hola Hola del panel de exploración.</span><span class="sxs-lookup"><span data-stu-id="939d1-134">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="939d1-135">En el cuadro de diálogo emergente de hello, verá el nombre de cuenta de almacenamiento de hello, clave de acceso principal y clave de acceso secundaria.</span><span class="sxs-lookup"><span data-stu-id="939d1-135">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="939d1-136">Para las claves de acceso, puede usar Hola principal o secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-136">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="939d1-137">Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="939d1-137">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="939d1-138">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="939d1-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="939d1-139">Hola **Azure::Blob::BlobService** objeto le permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="939d1-139">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="939d1-140">toocreate un contenedor, use hello **crear\_container()** método.</span><span class="sxs-lookup"><span data-stu-id="939d1-140">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="939d1-141">Hello ejemplo de código siguiente crea un contenedor o imprime error Hola si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="939d1-141">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="939d1-142">Si desea toomake Hola archivos de hello contenedor público, puede establecer permisos del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-142">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="939d1-143">Solo puede modificar hello <strong>crear\_container()</strong> llamada toopass hello **: pública\_acceso\_nivel** opción:</span><span class="sxs-lookup"><span data-stu-id="939d1-143">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="939d1-144">Los valores válidos de hello **: pública\_acceso\_nivel** opción son:</span><span class="sxs-lookup"><span data-stu-id="939d1-144">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="939d1-145">**blob:** habilita el acceso de lectura público a los blobs.</span><span class="sxs-lookup"><span data-stu-id="939d1-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="939d1-146">Los datos de blob dentro de este contenedor pueden leerse a través de una solicitud anónima, pero los datos del contenedor no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="939d1-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="939d1-147">Los clientes no pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="939d1-147">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="939d1-148">**container:** habilita el acceso de lectura público completo a los datos del contenedor y los blobs.</span><span class="sxs-lookup"><span data-stu-id="939d1-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="939d1-149">Los clientes pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-149">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="939d1-150">Como alternativa, puede modificar el nivel de acceso público de Hola de un contenedor mediante el uso de **establecer\_contenedor\_acl()** nivel de acceso público de método toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-150">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="939d1-151">Hola el siguiente código de ejemplo Hola a cambios de nivel de acceso público demasiado**contenedor**:</span><span class="sxs-lookup"><span data-stu-id="939d1-151">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="939d1-152">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="939d1-152">Upload a blob into a container</span></span>
<span data-ttu-id="939d1-153">blob de tooupload tooa contenido, use hello **crear\_bloque\_blob()** blob de método toocreate hello, utilice un archivo o una cadena como contenido de Hola de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-153">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="939d1-154">Hello código siguiente carga el archivo de hello **test.png** como un blob nuevo denominado "-el blob de imágenes" en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-154">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="939d1-155">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="939d1-155">List hello blobs in a container</span></span>
<span data-ttu-id="939d1-156">utilizar contenedores de hello toolist, **list_containers()** método.</span><span class="sxs-lookup"><span data-stu-id="939d1-156">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="939d1-157">los blobs de hello toolist dentro de un contenedor, usar **lista\_blobs()** método.</span><span class="sxs-lookup"><span data-stu-id="939d1-157">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="939d1-158">Esto da como resultado hello las direcciones URL de todos los blobs de hello en todos los contenedores de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="939d1-158">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="939d1-159">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="939d1-159">Download blobs</span></span>
<span data-ttu-id="939d1-160">los blobs de toodownload, usar hello **obtener\_blob()** contenido del método tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="939d1-160">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="939d1-161">Hello ejemplo de código siguiente muestra cómo utilizar **obtener\_blob()** toodownload Hola contenido de "imagen"blob y escribir tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="939d1-161">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="939d1-162">un blob</span><span class="sxs-lookup"><span data-stu-id="939d1-162">Delete a Blob</span></span>
<span data-ttu-id="939d1-163">Por último, toodelete un blob, utilice hello **eliminar\_blob()** método.</span><span class="sxs-lookup"><span data-stu-id="939d1-163">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="939d1-164">Hello ejemplo de código siguiente se muestra cómo toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="939d1-164">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="939d1-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="939d1-165">Next steps</span></span>
<span data-ttu-id="939d1-166">toolearn acerca de las tareas más complejas de almacenamiento, siga estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="939d1-166">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="939d1-167">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="939d1-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="939d1-168">[SDK de Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub</span><span class="sxs-lookup"><span data-stu-id="939d1-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="939d1-169">Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola</span><span class="sxs-lookup"><span data-stu-id="939d1-169">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

