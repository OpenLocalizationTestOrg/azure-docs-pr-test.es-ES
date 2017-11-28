---
title: "Creación de un recurso compartido de archivos de Azure | Microsoft Docs"
description: "Cómo crear un recurso compartido de archivos de Azure en Azure File Storage mediante Azure Portal, PowerShell y la CLI de Azure."
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
ms.openlocfilehash: b81701e2544ace092f007e5d98b3141e1f7da724
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="6dbf6-103">Creación de un recurso compartido de archivos en Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="6dbf6-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="6dbf6-104">Puede crear recursos compartidos de archivos de Azure mediante [Azure Portal](https://portal.azure.com/), los cmdlets de PowerShell de Azure Storage, las bibliotecas de cliente de Azure Storage o la API de REST de Azure Storage. En este tutorial, aprenderá a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dbf6-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="6dbf6-105">Crear un recurso compartido de archivos de Azure mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6dbf6-105">How to create an Azure File share using the Azure portal</span></span>](#Create file share through the Portal)
* [<span data-ttu-id="6dbf6-106">Crear un recurso compartido de archivos de Azure mediante Powershell</span><span class="sxs-lookup"><span data-stu-id="6dbf6-106">How to create an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="6dbf6-107">Crear un recurso compartido de archivos de Azure mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="6dbf6-107">How to create an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="6dbf6-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6dbf6-108">Prerequisites</span></span>
<span data-ttu-id="6dbf6-109">Para crear un recurso compartido de archivos de Azure, puede usar una cuenta de almacenamiento que ya exista o [crear una nueva cuenta de Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6dbf6-109">To create an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="6dbf6-110">Para crear un recurso compartido de archivos de Azure con PowerShell, necesitará la clave de la cuenta y el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-110">To create an Azure File share with PowerShell, you will need the account key and name of your storage account..</span></span> <span data-ttu-id="6dbf6-111">Necesitará la clave de la cuenta de almacenamiento si tiene previsto usar Powershell o la CLI.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-111">You will need Storage account key if you plan to use Powershell or CLI.</span></span>

## <a name="create-file-share-through-the-portal"></a><span data-ttu-id="6dbf6-112">Creación de un recurso compartido de archivos mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6dbf6-112">Create file share through the Portal</span></span>
1. <span data-ttu-id="6dbf6-113">**Vaya a la hoja de la cuenta de almacenamiento en Azure Portal**:</span><span class="sxs-lookup"><span data-stu-id="6dbf6-113">**Go to Storage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="6dbf6-114">![Hoja de la cuenta de almacenamiento](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="6dbf6-115">**Haga clic en el botón Agregar recurso compartido de archivos**:</span><span class="sxs-lookup"><span data-stu-id="6dbf6-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="6dbf6-116">![Haga clic en el botón Agregar recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-116">![Click the add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="6dbf6-117">**Proporcione el nombre y la cuota. Actualmente, la cuota puede llegar a un máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="6dbf6-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="6dbf6-118">![Proporcione el nombre y cuota deseada para el nuevo recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-118">![Provide a name and a desired quota for the new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="6dbf6-119">**Ver el nuevo recurso compartido de archivos**: ![ver el nuevo recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="6dbf6-120">**Cargar un archivo**: ![Cargar un archivo](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="6dbf6-121">**Explorar el recurso compartido de archivos y administrar los directorios y archivos**: ![Explorar el recurso compartido de archivos](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="6dbf6-122">Creación de un recurso compartido de archivos mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dbf6-122">Create file share through PowerShell</span></span>
<span data-ttu-id="6dbf6-123">Para prepararse para usar PowerShell, descargue e instale los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-123">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="6dbf6-124">Consulte [Instalación y configuración de Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para obtener instrucciones sobre el punto de instalación y la instalación.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-124">See [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for the install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="6dbf6-125">Es recomendable descargar e instalar el módulo más reciente de Azure PowerShell o actualizar a dicho módulo.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-125">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="6dbf6-126">**Creación de un contexto para la cuenta de almacenamiento y la clave** El contexto encapsula la clave de cuenta y el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-126">**Create a context for your storage account and key** The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="6dbf6-127">Para obtener instrucciones acerca de cómo copiar la clave de una cuenta desde [Azure Portal](https://portal.azure.com/), consulte [Visualización y copia de las claves de acceso de almacenamiento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="6dbf6-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="6dbf6-128">**Creación de un nuevo recurso compartido de archivos**:</span><span class="sxs-lookup"><span data-stu-id="6dbf6-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="6dbf6-129">El nombre del recurso compartido de archivos debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-129">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="6dbf6-130">Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="6dbf6-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="6dbf6-131">Creación de un recurso compartido de archivos mediante la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="6dbf6-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="6dbf6-132">**Para prepararse para usar la interfaz de línea de comandos (CLI), descargue e instale la CLI de Azure.**</span><span class="sxs-lookup"><span data-stu-id="6dbf6-132">**To prepare to use a Command Line Interface (CLI), download and install the Azure CLI.**</span></span>  
    <span data-ttu-id="6dbf6-133">Consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-az-cli2.md) e [Introducción a la CLI de Azure 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6dbf6-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="6dbf6-134">**Creación de una cadena de conexión a la cuenta de almacenamiento donde desea crear el recurso compartido.**</span><span class="sxs-lookup"><span data-stu-id="6dbf6-134">**Create a connection string to the storage account where you want to create the share.**</span></span>  
    <span data-ttu-id="6dbf6-135">Sustituya ```<storage-account>``` y ```<resource_group>``` por el nombre de la cuenta de almacenamiento y el grupo de recursos en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in the following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. <span data-ttu-id="6dbf6-136">**Creación de un recurso compartido de archivos**</span><span class="sxs-lookup"><span data-stu-id="6dbf6-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="6dbf6-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6dbf6-137">Next steps</span></span>
* [<span data-ttu-id="6dbf6-138">Conectar y montar un recurso compartido de archivos - Windows</span><span class="sxs-lookup"><span data-stu-id="6dbf6-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="6dbf6-139">Conectar y montar un recurso compartido de archivos - Linux</span><span class="sxs-lookup"><span data-stu-id="6dbf6-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="6dbf6-140">Conectar y montar un recurso compartido de archivos - macOS</span><span class="sxs-lookup"><span data-stu-id="6dbf6-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="6dbf6-141">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dbf6-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="6dbf6-142">P+F</span><span class="sxs-lookup"><span data-stu-id="6dbf6-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="6dbf6-143">Solución de problemas en Windows</span><span class="sxs-lookup"><span data-stu-id="6dbf6-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="6dbf6-144">Solución de problemas en Linux</span><span class="sxs-lookup"><span data-stu-id="6dbf6-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   