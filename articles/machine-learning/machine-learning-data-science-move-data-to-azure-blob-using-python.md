---
title: Mover datos hacia y desde Azure Blob Storage con Python | Microsoft Docs
description: Mover datos hacia y desde el almacenamiento de blobs de Azure con Python
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="b9de6-103">Movimiento de datos hacia y desde Azure Blob Storage de Azure con Python</span><span class="sxs-lookup"><span data-stu-id="b9de6-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="b9de6-104">En este tema se describe cómo enumerar, cargar y descargar blobs usando la API de Python.</span><span class="sxs-lookup"><span data-stu-id="b9de6-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="b9de6-105">Con la API de Python proporcionada en el SDK de Azure, puede:</span><span class="sxs-lookup"><span data-stu-id="b9de6-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="b9de6-106">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="b9de6-106">Create a container</span></span>
* <span data-ttu-id="b9de6-107">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="b9de6-107">Upload a blob into a container</span></span>
* <span data-ttu-id="b9de6-108">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="b9de6-108">Download blobs</span></span>
* <span data-ttu-id="b9de6-109">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="b9de6-109">List the blobs in a container</span></span>
* <span data-ttu-id="b9de6-110">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="b9de6-110">Delete a blob</span></span>

<span data-ttu-id="b9de6-111">Para obtener más información sobre el uso de la API de Python, consulte [Uso del servicio de almacenamiento de blobs desde Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b9de6-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="b9de6-112">Si está usando la máquina virtual que se configuró con los scripts ofrecidos por [Máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), AzCopy ya está instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b9de6-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b9de6-113">Para ver una introducción completa a Azure Blob Storage, consulte [Aspectos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9de6-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b9de6-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b9de6-114">Prerequisites</span></span>
<span data-ttu-id="b9de6-115">En este documento se supone que tiene una suscripción de Azure y una cuenta de almacenamiento y la clave de almacenamiento correspondiente para dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="b9de6-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="b9de6-116">Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="b9de6-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="b9de6-117">Para configurar una suscripción a Azure, consulte [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9de6-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b9de6-118">Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b9de6-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="b9de6-119">Cargar datos en blob</span><span class="sxs-lookup"><span data-stu-id="b9de6-119">Upload Data to Blob</span></span>
<span data-ttu-id="b9de6-120">Agregue el siguiente fragmento de código cerca de la parte superior de cualquier código de Python en el que desee obtener acceso mediante programación al almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="b9de6-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="b9de6-121">El objeto **BlobService** permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="b9de6-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="b9de6-122">El código siguiente crea un objeto BlobService utilizando el nombre de la cuenta de almacenamiento y la clave de la cuenta:</span><span class="sxs-lookup"><span data-stu-id="b9de6-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="b9de6-123">Reemplace el nombre de la cuenta y la clave de cuenta por la cuenta real y la clave.</span><span class="sxs-lookup"><span data-stu-id="b9de6-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="b9de6-124">Use los siguientes métodos para cargar datos en un blob:</span><span class="sxs-lookup"><span data-stu-id="b9de6-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="b9de6-125">put\_block\_blob\_from\_path (carga el contenido de un archivo desde la ruta especificada)</span><span class="sxs-lookup"><span data-stu-id="b9de6-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="b9de6-126">put\_block_blob\_from\_file (carga el contenido de una secuencia o archivo ya abierto)</span><span class="sxs-lookup"><span data-stu-id="b9de6-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="b9de6-127">put\_block\_blob\_from\_bytes (carga una matriz de bytes)</span><span class="sxs-lookup"><span data-stu-id="b9de6-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="b9de6-128">put\_block\_blob\_from\_text (carga el valor de texto especificado con la codificación especificada)</span><span class="sxs-lookup"><span data-stu-id="b9de6-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="b9de6-129">El siguiente código de ejemplo carga un archivo local en un contenedor:</span><span class="sxs-lookup"><span data-stu-id="b9de6-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="b9de6-130">El siguiente código de ejemplo carga todos los archivos (excepto los directorios) en un directorio local para el almacenamiento de blobs:</span><span class="sxs-lookup"><span data-stu-id="b9de6-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="b9de6-131">Descargar datos del blob</span><span class="sxs-lookup"><span data-stu-id="b9de6-131">Download Data from Blob</span></span>
<span data-ttu-id="b9de6-132">Utilice los siguientes métodos para descargar datos de un blob:</span><span class="sxs-lookup"><span data-stu-id="b9de6-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="b9de6-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="b9de6-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="b9de6-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="b9de6-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="b9de6-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="b9de6-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="b9de6-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="b9de6-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="b9de6-137">Estos métodos que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="b9de6-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="b9de6-138">El código de ejemplo siguiente descarga el contenido de un blob de un contenedor en un archivo local:</span><span class="sxs-lookup"><span data-stu-id="b9de6-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="b9de6-139">El siguiente código de ejemplo descarga todos los blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="b9de6-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="b9de6-140">Usa list\_blobs para obtener la lista de blobs disponibles del contenedor y los descarga en un directorio local.</span><span class="sxs-lookup"><span data-stu-id="b9de6-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading the data %s"%blob.name
