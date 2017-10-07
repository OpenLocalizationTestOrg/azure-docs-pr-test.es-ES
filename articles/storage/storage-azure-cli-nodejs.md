---
title: Hola aaaUsing 1.0 de CLI de Azure con el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola interfaz de línea de comandos de Azure (CLI de Azure) 1.0 con toocreate de almacenamiento de Azure y administrar cuentas de almacenamiento y trabajar con blobs de Azure y archivos. Hola CLI de Azure es una herramienta multiplataforma"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="dc083-104">Uso de hello Azure CLI 1.0 con el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="dc083-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="dc083-105">Información general</span><span class="sxs-lookup"><span data-stu-id="dc083-105">Overview</span></span>

<span data-ttu-id="dc083-106">Hola CLI de Azure proporciona un conjunto de código abierto, multiplataforma comandos para trabajar con hello plataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="dc083-107">Proporciona gran parte de la misma funcionalidad que se encuentra en Hola de Hola [portal de Azure](https://portal.azure.com) datos enriquecidos, así como tener acceso a funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="dc083-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="dc083-108">En esta guía, exploraremos cómo toouse [interfaz de línea de comandos de Azure (Azure CLI)](../cli-install-nodejs.md) tooperform una serie de tareas de desarrollo y la administración con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="dc083-109">Se recomienda descargar e instalar o actualizar toohello CLI de Azure más recientes antes de utilizar esta guía.</span><span class="sxs-lookup"><span data-stu-id="dc083-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="dc083-110">Esta guía se da por supuesto que comprende los conceptos básicos de hello del almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="dc083-111">Guía de Hello proporciona a una serie de secuencias de comandos toodemonstrate uso de Hola de hello CLI de Azure con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="dc083-112">Ser tooupdate seguro de las variables de script de Hola según la configuración antes de ejecutar cada script.</span><span class="sxs-lookup"><span data-stu-id="dc083-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="dc083-113">Guía de Hello proporciona ejemplos de comandos y secuencias de comandos de CLI de Azure de Hola para cuentas de almacenamiento clásicas.</span><span class="sxs-lookup"><span data-stu-id="dc083-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="dc083-114">Vea [Using Hola CLI de Azure para Mac, Linux y Windows con administración de recursos de Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) para comandos de CLI de Azure para las cuentas de almacenamiento de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc083-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="dc083-115">Introducción a almacenamiento de Azure y Azure CLI hello en 5 minutos</span><span class="sxs-lookup"><span data-stu-id="dc083-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="dc083-116">En esta guía se usa Ubuntu para los ejemplos, pero el funcionamiento debe ser similar en otros sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="dc083-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="dc083-117">**Nueva tooAzure:** obtener una suscripción de Microsoft Azure y una cuenta de Microsoft asociadas a esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="dc083-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="dc083-118">Para más información sobre las opciones de compra de Azure, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/) y [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) (para miembros de MSDN, Microsoft Partner Network, BizSpark y otros programas de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="dc083-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="dc083-119">Para obtener más información sobre las suscripciones a Azure, consulte [Asignación de roles de administrador en Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="dc083-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="dc083-120">**Después de crear una suscripción y una cuenta de Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="dc083-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="dc083-121">Descargue e instale Hola CLI de Azure siguiendo las instrucciones de Hola que se describen en [Install hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dc083-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="dc083-122">Una vez hello CLI de Azure se ha instalado, podrá toouse capaz de hello azure comando desde los comandos de CLI de Azure de interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema) tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="dc083-123">Hola de tipo _azure_ command y debería ver Hola después de salida.</span><span class="sxs-lookup"><span data-stu-id="dc083-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Resultado del comando de Azure][Image1]
3. <span data-ttu-id="dc083-125">En la interfaz de línea de comandos de hello, escriba `azure storage` toolist todas Hola comandos de almacenamiento de azure y obtener una primera impresión de Hola Hola de funcionalidades CLI de Azure proporciona.</span><span class="sxs-lookup"><span data-stu-id="dc083-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="dc083-126">Puede escribir el nombre de comando con **-h** parámetro (por ejemplo, `azure storage share create -h`) toosee detalles de la sintaxis del comando.</span><span class="sxs-lookup"><span data-stu-id="dc083-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="dc083-127">Ahora, le ofreceremos una secuencia de comandos simple que muestra tooaccess de comandos de CLI de Azure básico almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="dc083-128">script de Hola le primero preguntará si tooset dos variables para la cuenta de almacenamiento y la clave.</span><span class="sxs-lookup"><span data-stu-id="dc083-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="dc083-129">A continuación, Hola script creará un nuevo contenedor en esta nueva cuenta de almacenamiento y cargar un contenedor de toothat de archivo (blob) de imagen existente.</span><span class="sxs-lookup"><span data-stu-id="dc083-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="dc083-130">Después de que el script de Hola enumera todos los blobs en ese contenedor, descargará Hola imagen archivo toohello directorio de destino que se encuentra en el equipo local de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="dc083-131">En el equipo local, abra el editor de texto que desee (por ejemplo, vim).</span><span class="sxs-lookup"><span data-stu-id="dc083-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="dc083-132">Escriba Hola por encima de la secuencia de comandos en el editor de texto.</span><span class="sxs-lookup"><span data-stu-id="dc083-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="dc083-133">Ahora, necesita las variables de script de Hola tooupdate basadas en las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="dc083-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="dc083-134">**< Storage_account_name >** usar hello según el nombre de script de Hola o escriba un nombre nuevo para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc083-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="dc083-135">**Importante:** Hola nombre de cuenta de almacenamiento de hello debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="dc083-136">También debe estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="dc083-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="dc083-137">**< storage_account_key >** clave de acceso de saludo de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc083-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="dc083-138">**< Container_name >** usar hello según el nombre de script de Hola o escriba un nombre nuevo para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="dc083-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="dc083-139">**< Image_to_upload >** escriba una imagen de tooa de ruta de acceso en el equipo local, como por ejemplo: "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="dc083-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="dc083-140">**< Destination_folder >** ENTRAR archivos toostore en el directorio local de tooa de una ruta de acceso se descargan desde el almacenamiento de Azure, como: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="dc083-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="dc083-141">Después de actualizar las variables necesarias de hello en vim, presionar combinaciones de teclas `ESC`, `:`, `wq!` script de Hola toosave.</span><span class="sxs-lookup"><span data-stu-id="dc083-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="dc083-142">toorun esta secuencia de comandos, simplemente tipo hello script nombre de archivo en la consola de hello intensiva de errores.</span><span class="sxs-lookup"><span data-stu-id="dc083-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="dc083-143">Después de ejecutar este script, debe tener una carpeta de destino local que incluye el archivo de imagen de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="dc083-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="dc083-144">Hola siguiente captura de pantalla muestra una salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dc083-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="dc083-145">Después de ejecutar el script de Hola, debe tener una carpeta de destino local que incluye el archivo de imagen de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="dc083-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="dc083-146">Administrar cuentas de almacenamiento con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dc083-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="dc083-147">Conectar tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="dc083-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="dc083-148">Mientras que la mayoría de los comandos de almacenamiento de hello funcionará sin una suscripción de Azure, le recomendamos que tooconnect tooyour suscripción de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="dc083-149">tooconfigure hello Azure CLI toowork con su suscripción, siga los pasos de hello en [conectarse tooan suscripción de Azure desde hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="dc083-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="dc083-150">Creación de una cuenta de almacenamiento nueva</span><span class="sxs-lookup"><span data-stu-id="dc083-150">Create a new storage account</span></span>
<span data-ttu-id="dc083-151">toouse almacenamiento de Azure, necesitará una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc083-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="dc083-152">Puede crear una nueva cuenta de almacenamiento de Azure después de haber configurado la suscripción de tooyour tooconnect de equipo.</span><span class="sxs-lookup"><span data-stu-id="dc083-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="dc083-153">nombre de Hello de la cuenta de almacenamiento debe tener entre 3 y 24 caracteres de longitud y usar números y letras en minúsculas solo.</span><span class="sxs-lookup"><span data-stu-id="dc083-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="dc083-154">Establecimiento de una cuenta predeterminada de Almacenamiento de Azure en las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="dc083-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="dc083-155">Puede tener varias cuentas de almacenamiento en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="dc083-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="dc083-156">Puede elegir uno de ellos y establecerla en hello las variables de entorno de comandos de todo el almacenamiento de Hola Hola misma sesión.</span><span class="sxs-lookup"><span data-stu-id="dc083-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="dc083-157">Esto le permite toorun almacenamiento de Azure CLI Hola comandos sin especificar almacenamiento de hello cuenta y clave de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="dc083-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="dc083-158">Otra manera tooset una cuenta de almacenamiento predeterminada está usando la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc083-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="dc083-159">En primer lugar obtener cadena de conexión de hello, comando:</span><span class="sxs-lookup"><span data-stu-id="dc083-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="dc083-160">A continuación, copie la cadena de conexión de salida de hello y establézcalo tooenvironment variable:</span><span class="sxs-lookup"><span data-stu-id="dc083-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="dc083-161">Creación y administración de blobs</span><span class="sxs-lookup"><span data-stu-id="dc083-161">Create and manage blobs</span></span>
<span data-ttu-id="dc083-162">Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dc083-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="dc083-163">En esta sección se da por supuesto que ya está familiarizado con conceptos de almacenamiento de blobs de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="dc083-164">Para más información, consulte [Introducción a Azure Blob Storage mediante .NET](storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc083-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="dc083-165">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="dc083-165">Create a container</span></span>
<span data-ttu-id="dc083-166">Todos los blobs del almacenamiento de Azure han de estar en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="dc083-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="dc083-167">Puede crear un contenedor privado con hello `azure storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="dc083-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="dc083-168">Existen tres niveles de acceso de lectura anónimo: **Desactivado**, **Blob** y **Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="dc083-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="dc083-169">tooprevent anónimo tener acceso a tooblobs, parámetro del conjunto de permisos Hola demasiado**desactivar**.</span><span class="sxs-lookup"><span data-stu-id="dc083-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="dc083-170">De forma predeterminada, el nuevo contenedor de hello es privado y son accesibles solo por el propietario de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="dc083-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="dc083-171">público anónimo tooallow lee tooblob acceder a los recursos, pero no toocontainer metadatos o toohello lista de blobs en el contenedor de hello, establezca el parámetro de permiso de hello demasiado**Blob**.</span><span class="sxs-lookup"><span data-stu-id="dc083-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="dc083-172">tooallow completa público de lectura tooblob acceder a los recursos, metadatos del contenedor y lista de Hola de blobs en el contenedor de Hola, establezca el parámetro de permiso de hello demasiado**contenedor**.</span><span class="sxs-lookup"><span data-stu-id="dc083-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="dc083-173">Para obtener más información, consulte [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="dc083-173">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="dc083-174">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="dc083-174">Upload a blob into a container</span></span>
<span data-ttu-id="dc083-175">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="dc083-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="dc083-176">Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc083-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="dc083-177">blobs tooupload tooa contenedor, puede usar hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="dc083-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="dc083-178">De forma predeterminada, este comando carga blob en bloques tooa Hola archivos locales.</span><span class="sxs-lookup"><span data-stu-id="dc083-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="dc083-179">tipo de hello toospecify para blob hello, puede usar hello `--blobtype` parámetro.</span><span class="sxs-lookup"><span data-stu-id="dc083-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="dc083-180">Descarga  de blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="dc083-180">Download blobs from a container</span></span>
<span data-ttu-id="dc083-181">Hola siguiente ejemplo muestra cómo toodownload blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="dc083-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="dc083-182">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="dc083-182">Copy blobs</span></span>
<span data-ttu-id="dc083-183">Los blobs se pueden copiar dentro de las cuentas de almacenamiento y regiones, o entre ellas, de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="dc083-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="dc083-184">Hello en el ejemplo siguiente se muestra cómo toocopy blobs desde el almacenamiento de una cuenta tooanother.</span><span class="sxs-lookup"><span data-stu-id="dc083-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="dc083-185">En este ejemplo crearemos un contenedor donde al que es posible acceder de forma pública y anónima a los blobs.</span><span class="sxs-lookup"><span data-stu-id="dc083-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="dc083-186">En este ejemplo se realiza una copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="dc083-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="dc083-187">Puede supervisar el estado Hola de cada operación de copia ejecutando Hola `azure storage blob copy show` operación.</span><span class="sxs-lookup"><span data-stu-id="dc083-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="dc083-188">Tenga en cuenta que Hola dirección URL de origen proporcionado para la operación de copia de hello debe ser accesibles públicamente, o incluir un token SAS (firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="dc083-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="dc083-189">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="dc083-189">Delete a blob</span></span>
<span data-ttu-id="dc083-190">toodelete un blob, use Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc083-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="dc083-191">Creación y administración de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="dc083-191">Create and manage file shares</span></span>
<span data-ttu-id="dc083-192">Almacenamiento de archivos de Azure ofrece almacenamiento compartido para las aplicaciones que usan el protocolo SMB estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="dc083-193">Los servicios en la nube y las máquinas virtuales de Microsoft Azure, así como las aplicaciones locales, pueden compartir datos de archivos a través de recursos compartidos montados.</span><span class="sxs-lookup"><span data-stu-id="dc083-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="dc083-194">Puede administrar recursos compartidos de archivos y datos de archivos a través de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="dc083-195">Para obtener más información sobre el almacenamiento de archivos de Azure, consulte [Introducción al almacenamiento de archivos de Azure en Windows](storage-dotnet-how-to-use-files.md) o [cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dc083-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="dc083-196">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="dc083-196">Create a file share</span></span>
<span data-ttu-id="dc083-197">Un recurso compartido de archivos de Azure es un recurso compartido de archivos de SMB en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="dc083-198">Todos los directorios y archivos se deben crear en un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="dc083-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="dc083-199">Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, los límites de capacidad de toohello de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="dc083-200">Hello en el ejemplo siguiente se crea un recurso compartido de archivos denominado **MiRecursoCompartido**.</span><span class="sxs-lookup"><span data-stu-id="dc083-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="dc083-201">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="dc083-201">Create a directory</span></span>
<span data-ttu-id="dc083-202">Un directorio proporciona una estructura jerárquica opcional para los recursos compartidos de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc083-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="dc083-203">Hello en el ejemplo siguiente se crea un directorio denominado **myDir** en el recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="dc083-204">Tenga en cuenta que la ruta de acceso al directorio puede incluir varios niveles, *p. ej.*, **a/b**.</span><span class="sxs-lookup"><span data-stu-id="dc083-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="dc083-205">Pero debe asegurarse de que existen todos los directorios principales.</span><span class="sxs-lookup"><span data-stu-id="dc083-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="dc083-206">Por ejemplo, para la ruta de acceso **a/b**, primero se debe crear el directorio **a** y luego el directorio **b**.</span><span class="sxs-lookup"><span data-stu-id="dc083-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="dc083-207">Cargar un archivo local toodirectory</span><span class="sxs-lookup"><span data-stu-id="dc083-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="dc083-208">Hello en el ejemplo siguiente se carga un archivo de **~/temp/samplefile.txt** toohello **myDir** directory.</span><span class="sxs-lookup"><span data-stu-id="dc083-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="dc083-209">Edite la ruta de acceso de archivo de Hola para que apunte tooa archivo válido en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="dc083-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="dc083-210">Tenga en cuenta que puede ser un archivo en el recurso compartido de hello hasta too1 TB de tamaño.</span><span class="sxs-lookup"><span data-stu-id="dc083-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="dc083-211">Enumerar archivos de hello en la raíz del recurso compartido de Hola o directorio</span><span class="sxs-lookup"><span data-stu-id="dc083-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="dc083-212">Puede enumerar Hola archivos y subdirectorios en una raíz de recurso compartido o un directorio mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="dc083-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="dc083-213">Tenga en cuenta que nombre del directorio hello es opcional para la operación de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="dc083-214">Si se omite, comando hello muestra contenido de hello del directorio raíz de Hola de recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="dc083-215">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="dc083-215">Copy files</span></span>
<span data-ttu-id="dc083-216">A partir de la versión 0.9.8 de CLI de Azure, puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="dc083-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="dc083-217">A continuación se muestran cómo tooperform estas copian operaciones mediante comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="dc083-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="dc083-218">toocopy un archivo toohello directorio:</span><span class="sxs-lookup"><span data-stu-id="dc083-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="dc083-219">toocopy un directorio de archivos de blob tooa:</span><span class="sxs-lookup"><span data-stu-id="dc083-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="dc083-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc083-220">Next Steps</span></span>

<span data-ttu-id="dc083-221">Aquí puede encontrar la referencia a los comandos de la CLI de Azure 1.0 para trabajar con recursos de Storage:</span><span class="sxs-lookup"><span data-stu-id="dc083-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="dc083-222">Comandos de la CLI de Azure en el modo de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc083-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="dc083-223">Comandos de la CLI de Azure en modo de Azure Service Management (asm)</span><span class="sxs-lookup"><span data-stu-id="dc083-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="dc083-224">También les gusta hello tootry [CLI de Azure 2.0](storage-azure-cli.md), nuestro CLI de próxima generación escrito en Python, para su uso con el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc083-224">You may also like tootry hello [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
