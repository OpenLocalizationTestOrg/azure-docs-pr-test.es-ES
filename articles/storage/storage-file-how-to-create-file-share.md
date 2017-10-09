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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="0ea81-103">Creación de un recurso compartido de archivos en Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="0ea81-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="0ea81-104">Puede crear recursos compartidos de archivos de Azure mediante [portal de Azure](https://portal.azure.com/)Hola cmdlets de PowerShell de almacenamiento de Azure, Hola bibliotecas de cliente de almacenamiento de Azure u Hola API de REST de almacenamiento de Azure. En este tutorial, obtendrá información sobre:</span><span class="sxs-lookup"><span data-stu-id="0ea81-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="0ea81-105">¿Cómo toocreate un archivo de Azure compartir el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0ea81-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="0ea81-106">¿Cómo toocreate un archivo de Azure compartir con Powershell</span><span class="sxs-lookup"><span data-stu-id="0ea81-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="0ea81-107">¿Cómo toocreate un archivo de Azure compartir con CLI</span><span class="sxs-lookup"><span data-stu-id="0ea81-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="0ea81-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ea81-108">Prerequisites</span></span>
<span data-ttu-id="0ea81-109">toocreate un recurso compartido de archivos de Azure, puede usar una cuenta de almacenamiento que ya existe, o [crear una nueva cuenta de almacenamiento de Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0ea81-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="0ea81-110">toocreate un recurso compartido de archivos de Azure con PowerShell, necesitará la clave de cuenta de hello y nombre de la cuenta de almacenamiento...</span><span class="sxs-lookup"><span data-stu-id="0ea81-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="0ea81-111">Necesitará la clave de la cuenta de almacenamiento si tiene previsto toouse Powershell o CLI.</span><span class="sxs-lookup"><span data-stu-id="0ea81-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="0ea81-112">Crear recurso compartido de archivos a través de hello Portal</span><span class="sxs-lookup"><span data-stu-id="0ea81-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="0ea81-113">**Vaya tooStorage hoja de cuenta en el Portal de Azure**:</span><span class="sxs-lookup"><span data-stu-id="0ea81-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="0ea81-114">![Hoja de la cuenta de almacenamiento](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="0ea81-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="0ea81-115">**Haga clic en el botón Agregar recurso compartido de archivos**:</span><span class="sxs-lookup"><span data-stu-id="0ea81-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="0ea81-116">![Haga clic en hello Agregar botón de recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="0ea81-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="0ea81-117">**Proporcione el nombre y la cuota. Actualmente, la cuota puede llegar a un máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="0ea81-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="0ea81-118">![Proporcione un nombre y una cuota deseada Hola nuevo recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="0ea81-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="0ea81-119">**Ver el nuevo recurso compartido de archivos**: ![ver el nuevo recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="0ea81-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="0ea81-120">**Cargar un archivo**: ![Cargar un archivo](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="0ea81-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="0ea81-121">**Explorar el recurso compartido de archivos y administrar los directorios y archivos**: ![Explorar el recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="0ea81-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="0ea81-122">Creación de un recurso compartido de archivos mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ea81-122">Create file share through PowerShell</span></span>
<span data-ttu-id="0ea81-123">tooprepare toouse PowerShell, descargar e instalar los cmdlets de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea81-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0ea81-124">Vea [cómo tooinstall y configurar Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para hello instalar punto e instrucciones de instalación.</span><span class="sxs-lookup"><span data-stu-id="0ea81-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="0ea81-125">Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ea81-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="0ea81-126">**Crear un contexto para la cuenta de almacenamiento y clave** contexto Hola encapsula clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea81-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="0ea81-127">Para obtener instrucciones acerca de cómo copiar la clave de una cuenta desde [Azure Portal](https://portal.azure.com/), consulte [Visualización y copia de las claves de acceso de almacenamiento](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="0ea81-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="0ea81-128">**Creación de un nuevo recurso compartido de archivos**:</span><span class="sxs-lookup"><span data-stu-id="0ea81-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="0ea81-129">nombre de Hello el recurso compartido de archivos debe ser en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0ea81-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="0ea81-130">Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ea81-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="0ea81-131">Creación de un recurso compartido de archivos mediante la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="0ea81-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="0ea81-132">**tooprepare toouse una interfaz de línea de comandos (CLI), descargue e instale Hola CLI de Azure.**</span><span class="sxs-lookup"><span data-stu-id="0ea81-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="0ea81-133">Consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-az-cli2.md) e [Introducción a la CLI de Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0ea81-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="0ea81-134">**Crear una cuenta de almacenamiento toohello de cadena de conexión en la que desea compartir de hello toocreate.**</span><span class="sxs-lookup"><span data-stu-id="0ea81-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="0ea81-135">Reemplace ```<storage-account>``` y ```<resource_group>``` con su grupo de recursos y el nombre de la cuenta de almacenamiento en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea81-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="0ea81-136">**Creación de un recurso compartido de archivos**</span><span class="sxs-lookup"><span data-stu-id="0ea81-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="0ea81-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ea81-137">Next steps</span></span>
* [<span data-ttu-id="0ea81-138">Conectar y montar un recurso compartido de archivos - Windows</span><span class="sxs-lookup"><span data-stu-id="0ea81-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="0ea81-139">Conectar y montar un recurso compartido de archivos - Linux</span><span class="sxs-lookup"><span data-stu-id="0ea81-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="0ea81-140">Conectar y montar un recurso compartido de archivos - macOS</span><span class="sxs-lookup"><span data-stu-id="0ea81-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="0ea81-141">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ea81-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="0ea81-142">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="0ea81-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="0ea81-143">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="0ea81-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)