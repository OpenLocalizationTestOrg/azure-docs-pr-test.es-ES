---
title: aaaMove tooand de datos del almacenamiento de Blob de Azure con AzCopy | Documentos de Microsoft
description: Mover datos tooand de almacenamiento de blobs de Azure con AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="406b9-103">Mover datos tooand de almacenamiento de blobs de Azure con AzCopy</span><span class="sxs-lookup"><span data-stu-id="406b9-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="406b9-104">AzCopy es una utilidad de línea de comandos diseñada para cargar, descargar y copia tooand de datos de blob de Microsoft Azure, archivos y almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="406b9-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="406b9-105">Para obtener instrucciones acerca de cómo instalar AzCopy e información adicional sobre el uso con hello plataforma Windows Azure, consulte [Introducción a la utilidad de línea de comandos de AzCopy hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="406b9-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="406b9-106">Si está usando la máquina virtual que se configuró con secuencias de comandos de hello proporcionadas por [máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), a continuación, AzCopy ya está instalado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="406b9-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="406b9-107">Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="406b9-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="406b9-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="406b9-108">Prerequisites</span></span>
<span data-ttu-id="406b9-109">Este documento se supone que tiene una suscripción de Azure, una cuenta de almacenamiento y Hola correspondiente clave de almacenamiento para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="406b9-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="406b9-110">Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="406b9-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="406b9-111">tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="406b9-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="406b9-112">Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="406b9-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="406b9-113">Ejecución de comandos de AzCopy</span><span class="sxs-lookup"><span data-stu-id="406b9-113">Run AzCopy commands</span></span>
<span data-ttu-id="406b9-114">comandos de AzCopy toorun, abra una ventana de comandos y navegar por el directorio de instalación de AzCopy toohello en el equipo, donde se encuentra la aplicación ejecutable de hello AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="406b9-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="406b9-115">sintaxis básica de Hola para comandos de AzCopy es:</span><span class="sxs-lookup"><span data-stu-id="406b9-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="406b9-116">Puede agregar hello AzCopy tooyour sistema ruta de instalación y, a continuación, ejecute comandos de Hola desde cualquier directorio.</span><span class="sxs-lookup"><span data-stu-id="406b9-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="406b9-117">De forma predeterminada, AzCopy se instala demasiado*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* o *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="406b9-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="406b9-118">Cargar archivos tooan blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="406b9-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="406b9-119">tooupload un archivo, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="406b9-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="406b9-120">Descarga de archivos de un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="406b9-120">Download files from an Azure blob</span></span>
<span data-ttu-id="406b9-121">toodownload un archivo de un blob de Azure, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="406b9-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="406b9-122">Transferir blobs de un contenedor de Azure a otro</span><span class="sxs-lookup"><span data-stu-id="406b9-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="406b9-123">blobs de tootransfer entre contenedores de Azure, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="406b9-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="406b9-124">Sugerencias de uso de AzCopy</span><span class="sxs-lookup"><span data-stu-id="406b9-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="406b9-125">Al **cargar** archivos, */S* lo hace de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="406b9-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="406b9-126">Sin este parámetro, no se cargan los archivos de los subdirectorios.</span><span class="sxs-lookup"><span data-stu-id="406b9-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="406b9-127">Cuando **descargar** archivo */S* búsquedas Hola contenedor de forma recursiva hasta que todos los archivos en el directorio especificado hello y sus subdirectorios u Hola a todos los archivos que coinciden con un patrón especificado en hello dado directorio y sus subdirectorios, se descargan.</span><span class="sxs-lookup"><span data-stu-id="406b9-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="406b9-128">No se puede especificar un **archivos blob en cuestión** toodownload con hello */Source* parámetro.</span><span class="sxs-lookup"><span data-stu-id="406b9-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="406b9-129">toodownload un archivo específico, especifique toodownload de nombre de archivo hello blob mediante hello */patrón* parámetro.</span><span class="sxs-lookup"><span data-stu-id="406b9-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="406b9-130">**/S** parámetro puede ser usado toohave AzCopy, busque un patrón de nombre de archivo recursivamente.</span><span class="sxs-lookup"><span data-stu-id="406b9-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="406b9-131">Sin el parámetro de patrón de hello, AzCopy descarga todos los archivos de ese directorio.</span><span class="sxs-lookup"><span data-stu-id="406b9-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

