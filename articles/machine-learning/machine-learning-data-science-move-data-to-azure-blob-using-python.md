---
title: aaaMove tooand de datos de almacenamiento de blobs de Azure con Python | Documentos de Microsoft
description: Mover datos tooand de almacenamiento de blobs de Azure usa Python
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
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="ede48-103">Mover datos tooand de almacenamiento de blobs de Azure usa Python</span><span class="sxs-lookup"><span data-stu-id="ede48-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="ede48-104">Este tema describe cómo toolist, cargar y descargar blobs mediante Hola API de Python.</span><span class="sxs-lookup"><span data-stu-id="ede48-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="ede48-105">Con hello API de Python proporcionado en Azure SDK, puede:</span><span class="sxs-lookup"><span data-stu-id="ede48-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="ede48-106">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="ede48-106">Create a container</span></span>
* <span data-ttu-id="ede48-107">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ede48-107">Upload a blob into a container</span></span>
* <span data-ttu-id="ede48-108">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="ede48-108">Download blobs</span></span>
* <span data-ttu-id="ede48-109">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ede48-109">List hello blobs in a container</span></span>
* <span data-ttu-id="ede48-110">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="ede48-110">Delete a blob</span></span>

<span data-ttu-id="ede48-111">Para obtener más información acerca del uso de hello Python API, consulte [cómo tooUse Hola servicio de almacenamiento de blobs de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ede48-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="ede48-112">Si está usando la máquina virtual que se configuró con secuencias de comandos de hello proporcionadas por [máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), a continuación, AzCopy ya está instalado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ede48-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ede48-113">Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="ede48-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ede48-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ede48-114">Prerequisites</span></span>
<span data-ttu-id="ede48-115">Este documento se da por supuesto que tiene una suscripción de Azure, una cuenta de almacenamiento y la clave de almacenamiento correspondiente de Hola para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="ede48-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="ede48-116">Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="ede48-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="ede48-117">tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ede48-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ede48-118">Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ede48-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="ede48-119">Cargar datos tooBlob</span><span class="sxs-lookup"><span data-stu-id="ede48-119">Upload Data tooBlob</span></span>
<span data-ttu-id="ede48-120">Agregue Hola siguiente fragmento de código cerca de la parte superior de Hola de cualquier código de Python en las que quiera tooprogrammatically acceso a almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="ede48-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="ede48-121">Hola **BlobService** objeto le permite trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="ede48-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ede48-122">Hola siguiente código crea un objeto de BlobService con clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="ede48-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="ede48-123">Reemplace el nombre de la cuenta y la clave de cuenta por la cuenta real y la clave.</span><span class="sxs-lookup"><span data-stu-id="ede48-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="ede48-124">Usar hello después de blob de métodos tooupload datos tooa:</span><span class="sxs-lookup"><span data-stu-id="ede48-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="ede48-125">colocar\_bloque\_blob\_de\_(carga el contenido de Hola de un archivo de ruta de acceso especificada de hello) de la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="ede48-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="ede48-126">colocar\_block_blob\_de\_archivo (carga contenido Hola desde un archivo ya abierto/stream)</span><span class="sxs-lookup"><span data-stu-id="ede48-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="ede48-127">put\_block\_blob\_from\_bytes (carga una matriz de bytes)</span><span class="sxs-lookup"><span data-stu-id="ede48-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="ede48-128">colocar\_bloque\_blob\_de\_texto (carga Hola especificada valor de texto mediante Hola una codificación especificada)</span><span class="sxs-lookup"><span data-stu-id="ede48-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="ede48-129">Hola siguiente código de ejemplo carga un contenedor de tooa de archivo local:</span><span class="sxs-lookup"><span data-stu-id="ede48-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ede48-130">Hello código de ejemplo siguiente carga todos los archivos de hello (excluyendo los directorios) en un almacenamiento de tooblob de directorio local:</span><span class="sxs-lookup"><span data-stu-id="ede48-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="ede48-131">Descargar datos del blob</span><span class="sxs-lookup"><span data-stu-id="ede48-131">Download Data from Blob</span></span>
<span data-ttu-id="ede48-132">Usar hello siguientes datos toodownload de métodos de un blob:</span><span class="sxs-lookup"><span data-stu-id="ede48-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="ede48-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="ede48-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="ede48-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="ede48-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="ede48-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="ede48-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="ede48-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="ede48-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="ede48-137">Estos métodos que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="ede48-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="ede48-138">Hello código de ejemplo siguiente descarga contenido de Hola de un blob en un archivo local de tooa de contenedor:</span><span class="sxs-lookup"><span data-stu-id="ede48-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ede48-139">Hello código de ejemplo siguiente descarga todos los blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="ede48-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="ede48-140">Utiliza lista\_blobs tooget lista de Hola de blobs disponibles en el contenedor de Hola y descargarlos tooa de directorio local.</span><span class="sxs-lookup"><span data-stu-id="ede48-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
            print "something wrong happened when downloading hello data %s"%blob.name
