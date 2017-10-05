---
title: Uso de Blob Storage (almacenamiento de objetos) en Ruby | Microsoft Docs
description: Almacene datos no estructurados en la nube con Almacenamiento de blobs (objetos) de Azure.
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
ms.openlocfilehash: d27cf1594d6a31a746ca85b5c3184f8a5dbbaa54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="c1d22-103">Uso del almacenamiento de blobs de Ruby</span><span class="sxs-lookup"><span data-stu-id="c1d22-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c1d22-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c1d22-104">Overview</span></span>
<span data-ttu-id="c1d22-105">Almacenamiento de blobs de Azure es un servicio que almacena datos no estructurados en la nube como objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d22-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="c1d22-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1d22-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c1d22-107">El Almacenamiento de blobs a veces se conoce como "almacenamiento de objetos".</span><span class="sxs-lookup"><span data-stu-id="c1d22-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="c1d22-108">En esta guía se muestra cómo realizar algunas tareas comunes con Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d22-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="c1d22-109">Los ejemplos están escritos usando la API Ruby.</span><span class="sxs-lookup"><span data-stu-id="c1d22-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="c1d22-110">En los escenarios, se explica la **carga, enumeración, descarga** y **eliminación** de blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d22-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="c1d22-111">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="c1d22-111">Create a Ruby application</span></span>
<span data-ttu-id="c1d22-112">Cree una aplicación de Ruby.</span><span class="sxs-lookup"><span data-stu-id="c1d22-112">Create a Ruby application.</span></span> <span data-ttu-id="c1d22-113">Para obtener instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="c1d22-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="c1d22-114">Configuración de la aplicación para obtener acceso al almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c1d22-114">Configure your application to access Storage</span></span>
<span data-ttu-id="c1d22-115">Para usar el almacenamiento de Azure tendrá que descargar y usar el paquete Ruby azure, que incluye un conjunto de útiles bibliotecas que se comunican con los servicios REST de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c1d22-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="c1d22-116">Uso de RubyGems para obtener el paquete</span><span class="sxs-lookup"><span data-stu-id="c1d22-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="c1d22-117">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="c1d22-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="c1d22-118">Escriba "gem install azure" en la ventana de comandos para instalar la gema y las dependencias.</span><span class="sxs-lookup"><span data-stu-id="c1d22-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="c1d22-119">Importación del paquete</span><span class="sxs-lookup"><span data-stu-id="c1d22-119">Import the package</span></span>
<span data-ttu-id="c1d22-120">Con el editor de texto que prefiera, agregue lo siguiente al principio del archivo de Ruby en el que pretenda utilizar el almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="c1d22-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c1d22-121">Configuración de una conexión de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c1d22-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="c1d22-122">El módulo azure leerá las variables de entorno **AZURE\_STORAGE\_ACCOUNT** y **AZURE\_STORAGE\_ACCESS_KEY** para obtener información necesaria para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c1d22-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="c1d22-123">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta antes de usar **Azure::Blob::BlobService** con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="c1d22-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="c1d22-124">Para obtener estos valores desde una cuenta de almacenamiento de Azure Resource Manager o clásica en el Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="c1d22-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="c1d22-125">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1d22-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1d22-126">Vaya a la cuenta de almacenamiento que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="c1d22-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="c1d22-127">En la hoja Configuración que se encuentra a la derecha, haga clic en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="c1d22-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="c1d22-128">En la hoja Claves de acceso que aparece, verá la clave de acceso 1 y 2.</span><span class="sxs-lookup"><span data-stu-id="c1d22-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="c1d22-129">Puede usar cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="c1d22-129">You can use either of these.</span></span>
5. <span data-ttu-id="c1d22-130">Haga clic en el icono de copia para copiar la clave en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="c1d22-130">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="c1d22-131">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="c1d22-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c1d22-132">El objeto **Azure::Blob::BlobService** permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d22-132">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="c1d22-133">Para crear un contenedor, use el método **create\_container()**.</span><span class="sxs-lookup"><span data-stu-id="c1d22-133">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="c1d22-134">En el siguiente ejemplo de código se crea un contenedor o se imprime el error, si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="c1d22-134">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="c1d22-135">Si desea hacer públicos los archivos del contenedor, debe configurar los permisos del contenedor.</span><span class="sxs-lookup"><span data-stu-id="c1d22-135">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="c1d22-136">Puede modificar solo la llamada <strong>create\_\_container()</strong> para pasar la opción **:public\__access\__level**:</span><span class="sxs-lookup"><span data-stu-id="c1d22-136">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="c1d22-137">Los valores válidos para la opción **:public\_access\_level** son:</span><span class="sxs-lookup"><span data-stu-id="c1d22-137">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="c1d22-138">**blob:** habilita el acceso de lectura público a los blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d22-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="c1d22-139">Los datos de blob dentro de este contenedor pueden leerse a través de una solicitud anónima, pero los datos del contenedor no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="c1d22-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="c1d22-140">Los clientes no pueden enumerar los blobs incluidos en el contenedor mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="c1d22-140">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="c1d22-141">**container:** habilita el acceso de lectura público completo a los datos del contenedor y los blobs.</span><span class="sxs-lookup"><span data-stu-id="c1d22-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="c1d22-142">Los clientes pueden enumerar los blobs del contenedor a través de una solicitud anónima, pero no pueden enumerar los contenedores que están en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c1d22-142">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="c1d22-143">Si lo desea, también puede modificar el nivel de acceso público de un contenedor usando el método **set\_container\_acl()** para especificarlo.</span><span class="sxs-lookup"><span data-stu-id="c1d22-143">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="c1d22-144">El ejemplo de código siguiente cambia el nivel de acceso público a **container**:</span><span class="sxs-lookup"><span data-stu-id="c1d22-144">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="c1d22-145">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="c1d22-145">Upload a blob into a container</span></span>
<span data-ttu-id="c1d22-146">Para cargar contenido en un blob, use el método **create\_block\_blob()** para crear el blob y utilice un archivo o una cadena como contenido del blob.</span><span class="sxs-lookup"><span data-stu-id="c1d22-146">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="c1d22-147">El siguiente código carga el archivo **test.png** como un blob nuevo llamado "image-blob" en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="c1d22-147">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="c1d22-148">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="c1d22-148">List the blobs in a container</span></span>
<span data-ttu-id="c1d22-149">Para enumerar los contenedores, use el método **list_containers()**.</span><span class="sxs-lookup"><span data-stu-id="c1d22-149">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="c1d22-150">Para enumerar los blobs de un contenedor, utilice el método **list\_blobs()**.</span><span class="sxs-lookup"><span data-stu-id="c1d22-150">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="c1d22-151">Esta acción obtiene como resultado las URL de todos los blobs en todos los contenedores para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="c1d22-151">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="c1d22-152">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="c1d22-152">Download blobs</span></span>
<span data-ttu-id="c1d22-153">Si desea descargar blobs, use el método **get\_blob()** para recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="c1d22-153">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="c1d22-154">En el ejemplo de código siguiente se muestra cómo se utiliza **get\_blob()** para descargar el contenido de "image-blob" y escribirlo en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="c1d22-154">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="c1d22-155">un blob</span><span class="sxs-lookup"><span data-stu-id="c1d22-155">Delete a Blob</span></span>
<span data-ttu-id="c1d22-156">Finalmente, para eliminar un blob, use el método **delete\_blob**.</span><span class="sxs-lookup"><span data-stu-id="c1d22-156">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="c1d22-157">En el siguiente ejemplo de código se muestra cómo eliminar un blob.</span><span class="sxs-lookup"><span data-stu-id="c1d22-157">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="c1d22-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1d22-158">Next steps</span></span>
<span data-ttu-id="c1d22-159">Para obtener información acerca de tareas de almacenamiento más complejas, siga estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="c1d22-159">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="c1d22-160">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c1d22-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="c1d22-161">[SDK de Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) en GitHub</span><span class="sxs-lookup"><span data-stu-id="c1d22-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="c1d22-162">Transferencia de datos con la utilidad en línea de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="c1d22-162">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

