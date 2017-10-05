---
title: Uso de la CLI de Azure 1.0 con Azure Storage | Microsoft Docs
description: "Aprenda a usar la interfaz de la línea de comandos (CLI de Azure) 1.0 de Azure con Azure Storage para crear y administrar cuentas de almacenamiento y trabajar con archivos y blobs de Azure. La CLI de Azure es una herramienta multiplataforma"
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
ms.openlocfilehash: 837cf0f2b8db011b38de795339560574027030f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="af57f-104">Uso de la CLI de Azure 1.0 con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="af57f-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="af57f-105">Información general</span><span class="sxs-lookup"><span data-stu-id="af57f-105">Overview</span></span>

<span data-ttu-id="af57f-106">La CLI de Azure proporciona un conjunto de comandos de código abierto y multiplataforma para trabajar con la plataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="af57f-107">Proporciona muchas de las funcionalidades que se encuentran en el [Portal de Azure](https://portal.azure.com) , así como la funcionalidad de acceso a datos enriquecidos.</span><span class="sxs-lookup"><span data-stu-id="af57f-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="af57f-108">En esta guía, exploraremos cómo usar la [Interfaz de la línea de comandos de Azure (CLI de Azure)](../../cli-install-nodejs.md) para realizar diversas tareas de desarrollo y administración con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="af57f-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="af57f-109">Antes de usar esta guía es aconsejable descargar e instalar la CLI de Azure más reciente, o actualizarse a ella.</span><span class="sxs-lookup"><span data-stu-id="af57f-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="af57f-110">En esta guía se supone que conoce los conceptos básicos de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="af57f-111">La guía incluye varios scripts que muestran cómo se usa la CLI de Azure con Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="af57f-112">Antes de ejecutar cada script, asegúrese de que ha actualizado las variables del mismo según su configuración.</span><span class="sxs-lookup"><span data-stu-id="af57f-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="af57f-113">La guía proporciona ejemplos de comandos y scripts de CLI de Azure de cuentas de almacenamiento clásico.</span><span class="sxs-lookup"><span data-stu-id="af57f-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="af57f-114">Consulte [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) (Uso de la CLI de Azure para Mac, Linux y Windows mediante la administración de recursos de Azure) para ver los comandos de la CLI de Azure de las cuentas de almacenamiento de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="af57f-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="af57f-115">Introducción de 5 minutos a Almacenamiento de Azure y a la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="af57f-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="af57f-116">En esta guía se usa Ubuntu para los ejemplos, pero el funcionamiento debe ser similar en otros sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="af57f-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="af57f-117">**Nuevo en Azure:** obtenga una suscripción de Microsoft Azure y una cuenta de Microsoft asociada a dicha suscripción.</span><span class="sxs-lookup"><span data-stu-id="af57f-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="af57f-118">Para más información sobre las opciones de compra de Azure, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/) y [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) (para miembros de MSDN, Microsoft Partner Network, BizSpark y otros programas de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="af57f-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="af57f-119">Para obtener más información sobre las suscripciones a Azure, consulte [Asignación de roles de administrador en Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="af57f-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="af57f-120">**Después de crear una suscripción y una cuenta de Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="af57f-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="af57f-121">Descargue e instale la CLI de Azure siguiendo las instrucciones que encontrará en [Instalación de la CLI de Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="af57f-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="af57f-122">Una vez instalada la CLI de Azure, podrá usar el comando azure desde su interfaz de la línea de comandos (Bash, Terminal, símbolo del sistema) para tener acceso a los comandos de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="af57f-123">Escriba el comando _azure_ y debería ver la siguiente salida.</span><span class="sxs-lookup"><span data-stu-id="af57f-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Resultado del comando de Azure](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="af57f-125">En la interfaz de la línea de comandos, escriba `azure storage` para enumerar todos los comandos de Azure Storage y obtener una primera impresión de las funcionalidades que proporciona la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="af57f-126">Para ver los detalles de la sintaxis del comando, escriba el nombre del comando con el parámetro **-h** (por ejemplo, `azure storage share create -h`).</span><span class="sxs-lookup"><span data-stu-id="af57f-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="af57f-127">A continuación encontrará un sencillo script que muestra los comandos básicos de la CLI de Azure para obtener acceso a Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="af57f-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="af57f-128">En primer lugar, el script le pedirá que configure dos variables para la cuenta de almacenamiento y la clave.</span><span class="sxs-lookup"><span data-stu-id="af57f-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="af57f-129">A continuación, el script creará un nuevo contenedor en la nueva cuenta de almacenamiento y cargará un archivo de imagen existente (blob) en dicho contenedor.</span><span class="sxs-lookup"><span data-stu-id="af57f-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="af57f-130">Una vez el script haya enumerado todos los blobs del contenedor, descargará el archivo de imagen en el directorio de destino del equipo local.</span><span class="sxs-lookup"><span data-stu-id="af57f-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="af57f-131">En el equipo local, abra el editor de texto que desee (por ejemplo, vim).</span><span class="sxs-lookup"><span data-stu-id="af57f-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="af57f-132">Escriba el script anterior en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="af57f-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="af57f-133">Ahora deberá actualizar las variables del script basadas en la configuración.</span><span class="sxs-lookup"><span data-stu-id="af57f-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="af57f-134">**<storage_account_name>** Use el nombre proporcionado en el script o escriba un nuevo nombre para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af57f-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="af57f-135">**Importante:** el nombre de la cuenta de almacenamiento debe ser exclusivo en Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="af57f-136">También debe estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="af57f-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="af57f-137">**<storage_account_key>** La clave de acceso de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af57f-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="af57f-138">**<container_name>** Use el nombre proporcionado en el script o escriba un nuevo nombre para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="af57f-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="af57f-139">**<image_to_upload>** Escriba una ruta de acceso a una imagen en el equipo local, por ejemplo: "~/images/HolaMundo.png".</span><span class="sxs-lookup"><span data-stu-id="af57f-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="af57f-140">**<destination_folder>** Escriba una ruta de acceso a un directorio local para almacenar los archivos descargados desde Azure Storage, por ejemplo: "~/imágenesDescargadas".</span><span class="sxs-lookup"><span data-stu-id="af57f-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="af57f-141">Después de haber actualizado las variables necesarias en vim, presione las combinaciones de teclas `ESC`, `:`, `wq!` para guardar el script.</span><span class="sxs-lookup"><span data-stu-id="af57f-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="af57f-142">Para ejecutar este script, solo es preciso escribir el nombre del archivo de script en la consola de bash.</span><span class="sxs-lookup"><span data-stu-id="af57f-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="af57f-143">Una vez que se ejecuta el script, debería tener una carpeta de destino local que incluyera el archivo de imagen descargado.</span><span class="sxs-lookup"><span data-stu-id="af57f-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="af57f-144">La siguiente captura de pantalla le muestra un ejemplo del resultado:</span><span class="sxs-lookup"><span data-stu-id="af57f-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="af57f-145">Una vez ejecutado el script, debería tener una carpeta de destino local que incluye el archivo de imagen descargado.</span><span class="sxs-lookup"><span data-stu-id="af57f-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="af57f-146">Administración de cuentas de almacenamiento con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="af57f-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="af57f-147">Conexión a su suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="af57f-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="af57f-148">Aunque la mayoría de los comandos de almacenamiento funcionarán sin suscripción a Azure, es aconsejable que se conecte a su suscripción desde la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="af57f-149">Para configurar la CLI de Azure de modo que funcione con su suscripción, siga los pasos en [Connect to an Azure subscription from the Azure CLI](../../xplat-cli-connect.md)(Conexión a una suscripción de Azure desde la interfaz de la línea de comandos de Azure [CLI de Azure]).</span><span class="sxs-lookup"><span data-stu-id="af57f-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="af57f-150">Creación de una cuenta de almacenamiento nueva</span><span class="sxs-lookup"><span data-stu-id="af57f-150">Create a new storage account</span></span>
<span data-ttu-id="af57f-151">Para utilizar Almacenamiento de Azure, necesitará una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af57f-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="af57f-152">Puede crear una nueva cuenta de almacenamiento de Azure después de configurar el equipo para que pueda conectarse a su suscripción.</span><span class="sxs-lookup"><span data-stu-id="af57f-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="af57f-153">El nombre de la cuenta de almacenamiento debe tener entre 3 y 24 caracteres, y usar solo números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="af57f-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="af57f-154">Establecimiento de una cuenta predeterminada de Almacenamiento de Azure en las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="af57f-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="af57f-155">Puede tener varias cuentas de almacenamiento en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="af57f-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="af57f-156">Puede elegir una de ellas y establecerla en las variables de entorno de todos los comandos de almacenamiento de la misma sesión.</span><span class="sxs-lookup"><span data-stu-id="af57f-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="af57f-157">Esto le permite ejecutar los comandos de almacenamiento de la CLI de Azure sin especificar explícitamente la cuenta de almacenamiento y la clave.</span><span class="sxs-lookup"><span data-stu-id="af57f-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="af57f-158">Otra forma de establecer una cuenta de almacenamiento predeterminada es mediante una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="af57f-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="af57f-159">En primer lugar obtenga la cadena de conexión con el comando:</span><span class="sxs-lookup"><span data-stu-id="af57f-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="af57f-160">A continuación, copie la cadena de conexión de salida y establézcala como variable de entorno:</span><span class="sxs-lookup"><span data-stu-id="af57f-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="af57f-161">Creación y administración de blobs</span><span class="sxs-lookup"><span data-stu-id="af57f-161">Create and manage blobs</span></span>
<span data-ttu-id="af57f-162">El almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o datos binarios, a los que puede acceder desde cualquier lugar del mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="af57f-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="af57f-163">En esta sección se supone que ya está familiarizado con los conceptos del almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="af57f-164">Para más información, consulte [Introducción a Azure Blob Storage mediante .NET](../blobs/storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="af57f-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="af57f-165">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="af57f-165">Create a container</span></span>
<span data-ttu-id="af57f-166">Todos los blobs del almacenamiento de Azure han de estar en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="af57f-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="af57f-167">Puede crear un contenedor privado con el comando `azure storage container create` :</span><span class="sxs-lookup"><span data-stu-id="af57f-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="af57f-168">Existen tres niveles de acceso de lectura anónimo: **Desactivado**, **Blob** y **Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="af57f-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="af57f-169">Para evitar el acceso anónimo a los blobs, establezca el parámetro de permiso en **Desactivado**.</span><span class="sxs-lookup"><span data-stu-id="af57f-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="af57f-170">El nuevo contenedor es privado por defecto y solo puede acceder a él el propietario de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="af57f-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="af57f-171">Para permitir un acceso de lectura público y anónimo a los recursos de blob, pero no a los metadatos del contenedor ni a la lista de blobs del contenedor, seleccione **Blob**en el parámetro Permiso.</span><span class="sxs-lookup"><span data-stu-id="af57f-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="af57f-172">Para hacer que el acceso de lectura a los recursos de blob, a los metadatos del contenedor y a la lista de blobs del contenedor sean totalmente públicos, elija **Contenedor**en el parámetro Permiso.</span><span class="sxs-lookup"><span data-stu-id="af57f-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="af57f-173">Para obtener más información, consulte [Administración del acceso de lectura anónimo a contenedores y blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="af57f-173">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="af57f-174">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="af57f-174">Upload a blob into a container</span></span>
<span data-ttu-id="af57f-175">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="af57f-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="af57f-176">Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="af57f-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="af57f-177">Para cargar blobs en un contenedor, puede utilizar `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="af57f-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="af57f-178">Este comando carga de forma predeterminada los archivos locales a un blob en bloque.</span><span class="sxs-lookup"><span data-stu-id="af57f-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="af57f-179">Para especificar el tipo de blob, puede usar el parámetro `--blobtype` .</span><span class="sxs-lookup"><span data-stu-id="af57f-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="af57f-180">Descarga  de blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="af57f-180">Download blobs from a container</span></span>
<span data-ttu-id="af57f-181">En el siguiente ejemplo le mostraremos cómo descargar blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="af57f-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="af57f-182">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="af57f-182">Copy blobs</span></span>
<span data-ttu-id="af57f-183">Los blobs se pueden copiar dentro de las cuentas de almacenamiento y regiones, o entre ellas, de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="af57f-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="af57f-184">En el siguiente ejemplo se muestra cómo copiar blobs de una cuenta de almacenamiento a otra.</span><span class="sxs-lookup"><span data-stu-id="af57f-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="af57f-185">En este ejemplo crearemos un contenedor donde al que es posible acceder de forma pública y anónima a los blobs.</span><span class="sxs-lookup"><span data-stu-id="af57f-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="af57f-186">En este ejemplo se realiza una copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="af57f-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="af57f-187">Para supervisar el estado de cada operación de copia, ejecute la operación `azure storage blob copy show` .</span><span class="sxs-lookup"><span data-stu-id="af57f-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="af57f-188">Tenga en cuenta que debe ser posible acceder públicamente a la dirección URL de origen proporcionada para la operación de copia, o bien incluir un token SAS (firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="af57f-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="af57f-189">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="af57f-189">Delete a blob</span></span>
<span data-ttu-id="af57f-190">Para eliminar un blob, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="af57f-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="af57f-191">Creación y administración de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="af57f-191">Create and manage file shares</span></span>
<span data-ttu-id="af57f-192">El Almacenamiento de archivos de Azure ofrece almacenamiento compartido para aplicaciones que usan el protocolo SMB estándar.</span><span class="sxs-lookup"><span data-stu-id="af57f-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="af57f-193">Los servicios en la nube y las máquinas virtuales de Microsoft Azure, así como las aplicaciones locales, pueden compartir datos de archivos a través de recursos compartidos montados.</span><span class="sxs-lookup"><span data-stu-id="af57f-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="af57f-194">Los recursos compartidos de archivos y datos de archivos se pueden administrar a través de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="af57f-195">Para más información sobre Azure File Storage, consulte [Introducción a Azure File Storage en Windows](../storage-dotnet-how-to-use-files.md) o [Uso de Azure File Storage con Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="af57f-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="af57f-196">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="af57f-196">Create a file share</span></span>
<span data-ttu-id="af57f-197">Un recurso compartido de archivos de Azure es un recurso compartido de archivos de SMB en Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="af57f-198">Todos los directorios y archivos se deben crear en un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="af57f-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="af57f-199">Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, hasta los límites de capacidad de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af57f-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="af57f-200">En el siguiente ejemplo se crea un recurso compartido de archivos denominado **myshare**.</span><span class="sxs-lookup"><span data-stu-id="af57f-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="af57f-201">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="af57f-201">Create a directory</span></span>
<span data-ttu-id="af57f-202">Un directorio proporciona una estructura jerárquica opcional para los recursos compartidos de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="af57f-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="af57f-203">En el ejemplo siguiente se crea el directorio **myDir** en el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="af57f-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="af57f-204">Tenga en cuenta que la ruta de acceso al directorio puede incluir varios niveles, *p. ej.*, **a/b**.</span><span class="sxs-lookup"><span data-stu-id="af57f-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="af57f-205">Pero debe asegurarse de que existen todos los directorios principales.</span><span class="sxs-lookup"><span data-stu-id="af57f-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="af57f-206">Por ejemplo, para la ruta de acceso **a/b**, primero se debe crear el directorio **a** y luego el directorio **b**.</span><span class="sxs-lookup"><span data-stu-id="af57f-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="af57f-207">Carga de un archivo local a un directorio</span><span class="sxs-lookup"><span data-stu-id="af57f-207">Upload a local file to directory</span></span>
<span data-ttu-id="af57f-208">El siguiente ejemplo carga un archivo de **~/temp/samplefile.txt** en el directorio **myDir**.</span><span class="sxs-lookup"><span data-stu-id="af57f-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="af57f-209">Edite la ruta de acceso al archivo de forma que apunte a un archivo válido situado en la máquina local:</span><span class="sxs-lookup"><span data-stu-id="af57f-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="af57f-210">Tenga en cuenta que los archivos del recurso compartido pueden tener un tamaño máximo de 1 TB.</span><span class="sxs-lookup"><span data-stu-id="af57f-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="af57f-211">Enumeración de los archivos de la raíz o directorio compartidos</span><span class="sxs-lookup"><span data-stu-id="af57f-211">List the files in the share root or directory</span></span>
<span data-ttu-id="af57f-212">Los archivos y subdirectorios del directorio raíz del recurso compartido o de otro directorio se pueden enumerar con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="af57f-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="af57f-213">Tenga en cuenta que el nombre de directorio es opcional en la operación de enumeración.</span><span class="sxs-lookup"><span data-stu-id="af57f-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="af57f-214">Si se omite, el comando muestra el contenido del directorio raíz del recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="af57f-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="af57f-215">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="af57f-215">Copy files</span></span>
<span data-ttu-id="af57f-216">A partir de la versión 0.9.8 de la CLI de Azure, puede copiar un archivo en otro, un archivo en un blob o un blob en un archivo.</span><span class="sxs-lookup"><span data-stu-id="af57f-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="af57f-217">A continuación mostramos cómo realizar estas operaciones de copia mediante comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="af57f-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="af57f-218">Para copiar un archivo en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="af57f-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="af57f-219">Para copiar un blob en un directorio de archivos:</span><span class="sxs-lookup"><span data-stu-id="af57f-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="af57f-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af57f-220">Next Steps</span></span>

<span data-ttu-id="af57f-221">Aquí puede encontrar la referencia a los comandos de la CLI de Azure 1.0 para trabajar con recursos de Storage:</span><span class="sxs-lookup"><span data-stu-id="af57f-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="af57f-222">Comandos de la CLI de Azure en el modo de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="af57f-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="af57f-223">Comandos de la CLI de Azure en modo de Azure Service Management (asm)</span><span class="sxs-lookup"><span data-stu-id="af57f-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="af57f-224">También puede probar la [CLI de Azure 2.0 (versión preliminar)](../storage-azure-cli.md), una CLI de última generación escrita en Python que se usa con el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="af57f-224">You may also like to try the [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>
