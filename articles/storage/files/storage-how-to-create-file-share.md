---
title: aaaHow toocreate un recurso compartido de archivos de Azure | Documentos de Microsoft
description: "Cómo toocreate compartir un archivo de Azure en almacenamiento de archivos de Azure con hello portal de Azure, PowerShell y Hola CLI de Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="cd136-103">Creación de un recurso compartido de archivos en Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="cd136-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="cd136-104">Puede crear recursos compartidos de archivos de Azure mediante [portal de Azure](https://portal.azure.com/)Hola cmdlets de PowerShell de almacenamiento de Azure, Hola bibliotecas de cliente de almacenamiento de Azure u Hola API de REST de almacenamiento de Azure. En este tutorial, obtendrá información sobre:</span><span class="sxs-lookup"><span data-stu-id="cd136-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="cd136-105">¿Cómo toocreate un archivo de Azure compartir el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cd136-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="cd136-106">¿Cómo toocreate un archivo de Azure compartir con Powershell</span><span class="sxs-lookup"><span data-stu-id="cd136-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="cd136-107">¿Cómo toocreate un archivo de Azure compartir con CLI</span><span class="sxs-lookup"><span data-stu-id="cd136-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="cd136-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd136-108">Prerequisites</span></span>
<span data-ttu-id="cd136-109">toocreate un recurso compartido de archivos de Azure, puede usar una cuenta de almacenamiento que ya existe, o [crear una nueva cuenta de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd136-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="cd136-110">toocreate un recurso compartido de archivos de Azure con PowerShell, necesitará la clave de cuenta de hello y nombre de la cuenta de almacenamiento...</span><span class="sxs-lookup"><span data-stu-id="cd136-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="cd136-111">Necesitará la clave de la cuenta de almacenamiento si tiene previsto toouse Powershell o CLI.</span><span class="sxs-lookup"><span data-stu-id="cd136-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="cd136-112">Crear recurso compartido de archivos a través de hello Portal</span><span class="sxs-lookup"><span data-stu-id="cd136-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="cd136-113">**Vaya tooStorage hoja de cuenta en el Portal de Azure**:</span><span class="sxs-lookup"><span data-stu-id="cd136-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="cd136-114">![Hoja de la cuenta de almacenamiento](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="cd136-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="cd136-115">**Haga clic en el botón Agregar recurso compartido de archivos**:</span><span class="sxs-lookup"><span data-stu-id="cd136-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="cd136-116">![Haga clic en hello Agregar botón de recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="cd136-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="cd136-117">**Proporcione el nombre y la cuota. Actualmente, la cuota puede llegar a un máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="cd136-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="cd136-118">![Proporcione un nombre y una cuota deseada Hola nuevo recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="cd136-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="cd136-119">**Ver el nuevo recurso compartido de archivos**: ![ver el nuevo recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="cd136-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="cd136-120">**Cargar un archivo**: ![Cargar un archivo](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="cd136-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="cd136-121">**Explorar el recurso compartido de archivos y administrar los directorios y archivos**: ![Explorar el recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="cd136-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="cd136-122">Creación de un recurso compartido de archivos mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd136-122">Create file share through PowerShell</span></span>
<span data-ttu-id="cd136-123">tooprepare toouse PowerShell, descargar e instalar los cmdlets de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd136-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="cd136-124">Vea [cómo tooinstall y configurar Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para hello instalar punto e instrucciones de instalación.</span><span class="sxs-lookup"><span data-stu-id="cd136-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="cd136-125">Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd136-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="cd136-126">**Crear un contexto para la cuenta de almacenamiento y clave** contexto Hola encapsula clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="cd136-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="cd136-127">Para obtener instrucciones acerca de cómo copiar la clave de una cuenta desde [Azure Portal](https://portal.azure.com/), consulte [Visualización y copia de las claves de acceso de almacenamiento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cd136-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="cd136-128">**Creación de un nuevo recurso compartido de archivos**:</span><span class="sxs-lookup"><span data-stu-id="cd136-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="cd136-129">nombre de Hello el recurso compartido de archivos debe ser en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cd136-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="cd136-130">Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd136-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="cd136-131">Creación de un recurso compartido de archivos mediante la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="cd136-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="cd136-132">**tooprepare toouse una interfaz de línea de comandos (CLI), descargue e instale Hola CLI de Azure.**</span><span class="sxs-lookup"><span data-stu-id="cd136-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="cd136-133">Consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-az-cli2.md) e [Introducción a la CLI de Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cd136-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="cd136-134">**Crear una cuenta de almacenamiento toohello de cadena de conexión en la que desea compartir de hello toocreate.**</span><span class="sxs-lookup"><span data-stu-id="cd136-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="cd136-135">Reemplace ```<storage-account>``` y ```<resource_group>``` con su grupo de recursos y el nombre de la cuenta de almacenamiento en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd136-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="cd136-136">**Creación de un recurso compartido de archivos**</span><span class="sxs-lookup"><span data-stu-id="cd136-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="cd136-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd136-137">Next steps</span></span>
* [<span data-ttu-id="cd136-138">Conectar y montar un recurso compartido de archivos - Windows</span><span class="sxs-lookup"><span data-stu-id="cd136-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="cd136-139">Conectar y montar un recurso compartido de archivos - Linux</span><span class="sxs-lookup"><span data-stu-id="cd136-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="cd136-140">Conectar y montar un recurso compartido de archivos - macOS</span><span class="sxs-lookup"><span data-stu-id="cd136-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="cd136-141">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd136-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="cd136-142">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="cd136-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="cd136-143">Solución de problemas en Windows</span><span class="sxs-lookup"><span data-stu-id="cd136-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="cd136-144">Solución de problemas en Linux</span><span class="sxs-lookup"><span data-stu-id="cd136-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   