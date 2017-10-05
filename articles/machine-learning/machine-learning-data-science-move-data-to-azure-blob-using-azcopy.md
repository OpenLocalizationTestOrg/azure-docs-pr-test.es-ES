---
title: Mover datos hacia y desde Azure Blob Storage con AzCopy | Microsoft Docs
description: Mover datos hacia y desde el almacenamiento de blobs de Azure con AzCopy
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
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="fef94-103">Mover datos hacia y desde Azure Blob Storage de Azure con AzCopy</span><span class="sxs-lookup"><span data-stu-id="fef94-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="fef94-104">AzCopy es una utilidad de línea de comandos diseñada para realizar operaciones de carga, descarga y copia de datos a y desde los servicios Table Storage, File Storage y Blob Storage de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fef94-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="fef94-105">Para obtener instrucciones sobre la instalación de AzCopy y de información adicional sobre su uso con la plataforma de Azure, consulte [Introducción a la utilidad de línea de comandos AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="fef94-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="fef94-106">Si está usando la máquina virtual que se configuró con los scripts ofrecidos por [Máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), AzCopy ya está instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fef94-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="fef94-107">Para ver una introducción completa a Azure Blob Storage, consulte [Aspectos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="fef94-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fef94-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fef94-108">Prerequisites</span></span>
<span data-ttu-id="fef94-109">En este documento se supone que tiene una suscripción de Azure y una cuenta de almacenamiento y la clave de almacenamiento correspondiente para dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="fef94-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="fef94-110">Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="fef94-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="fef94-111">Para configurar una suscripción a Azure, consulte [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fef94-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fef94-112">Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="fef94-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="fef94-113">Ejecución de comandos de AzCopy</span><span class="sxs-lookup"><span data-stu-id="fef94-113">Run AzCopy commands</span></span>
<span data-ttu-id="fef94-114">Para ejecutar comandos de AzCopy, abra una ventana de comandos y navegue al directorio de instalación de AzCopy en el equipo, donde se encuentra el ejecutable AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="fef94-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="fef94-115">La sintaxis básica del comando AzCopy es:</span><span class="sxs-lookup"><span data-stu-id="fef94-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="fef94-116">Puede agregar la ubicación de instalación de AzCopy a la ruta del sistema y, a continuación, ejecutar los comandos desde cualquier directorio.</span><span class="sxs-lookup"><span data-stu-id="fef94-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="fef94-117">De forma predeterminada, AzCopy se instala en *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* o *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="fef94-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="fef94-118">Carga de archivos en un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="fef94-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="fef94-119">Para descargar un archivo, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fef94-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="fef94-120">Descarga de archivos de un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="fef94-120">Download files from an Azure blob</span></span>
<span data-ttu-id="fef94-121">Para descargar un archivo desde un blob de Azure, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fef94-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="fef94-122">Transferir blobs de un contenedor de Azure a otro</span><span class="sxs-lookup"><span data-stu-id="fef94-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="fef94-123">Para transferir blobs de un contenedor de Azure a otro, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fef94-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="fef94-124">Sugerencias de uso de AzCopy</span><span class="sxs-lookup"><span data-stu-id="fef94-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="fef94-125">Al **cargar** archivos, */S* lo hace de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="fef94-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="fef94-126">Sin este parámetro, no se cargan los archivos de los subdirectorios.</span><span class="sxs-lookup"><span data-stu-id="fef94-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="fef94-127">Al **descargar** el archivo, */S* busca el contenedor de manera recursiva hasta que se descarguen todos los archivos del directorio especificado y sus subdirectorios, o todos los archivos que coincidan con el patrón especificado en el directorio especificado y sus subdirectorios.</span><span class="sxs-lookup"><span data-stu-id="fef94-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="fef94-128">No se puede especificar un **archivo de blob específico** para descargar mediante el parámetro */Source* .</span><span class="sxs-lookup"><span data-stu-id="fef94-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="fef94-129">Para descargar un archivo específico, especifique el nombre del archivo blob que se va a descargar mediante el parámetro */Pattern* .</span><span class="sxs-lookup"><span data-stu-id="fef94-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="fef94-130">**/S** se puede usar para que AzCopy busque de forma recursiva un patrón de nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="fef94-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="fef94-131">Sin el parámetro de patrón, AzCopy descargará todos los archivos en ese directorio.</span><span class="sxs-lookup"><span data-stu-id="fef94-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

