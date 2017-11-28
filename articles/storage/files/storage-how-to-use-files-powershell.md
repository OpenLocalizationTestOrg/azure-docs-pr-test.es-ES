---
title: "Uso de PowerShell para la administración de Azure File Storage | Microsoft Docs"
description: Aprenda a usar PowerShell para administrar Azure File Storage.
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
ms.openlocfilehash: ce62d4423ce711a6902aed7b8174ff4e827f6083
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="138b7-103">Uso de PowerShell para la administración de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="138b7-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="138b7-104">Puede usar Azure PowerShell para crear y administrar recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="138b7-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="138b7-105">Instalación de cmdlets de PowerShell para Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="138b7-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="138b7-106">Para prepararse para usar PowerShell, descargue e instale los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="138b7-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="138b7-107">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azureps-cmdlets-docs) para obtener instrucciones sobre el punto de instalación y la instalación.</span><span class="sxs-lookup"><span data-stu-id="138b7-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="138b7-108">Es recomendable descargar e instalar el módulo más reciente de Azure PowerShell o actualizar a dicho módulo.</span><span class="sxs-lookup"><span data-stu-id="138b7-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="138b7-109">Abra una ventana de Azure PowerShell haciendo clic en **Inicio** y escribiendo **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="138b7-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="138b7-110">La ventana de PowerShell cargará el módulo de Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="138b7-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="138b7-111">Creación de un contexto para la cuenta y clave de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="138b7-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="138b7-112">Creación del contexto de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="138b7-112">Create the storage account context.</span></span> <span data-ttu-id="138b7-113">El contexto encapsula el nombre y la clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="138b7-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="138b7-114">Para obtener instrucciones acerca de cómo copiar la clave de una cuenta desde [Azure Portal](https://portal.azure.com), consulte [Visualización y copia de las claves de acceso de almacenamiento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="138b7-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="138b7-115">Sustituya `storage-account-name` y `storage-account-key` por el nombre y clave de su cuenta de almacenamiento  en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="138b7-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="138b7-116">Creación de un nuevo recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="138b7-116">Create a new file share</span></span>
<span data-ttu-id="138b7-117">Cree el nuevo recurso compartido, denominado `logs`.</span><span class="sxs-lookup"><span data-stu-id="138b7-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="138b7-118">Ahora tiene un recurso compartido de archivos en Almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="138b7-118">You now have a file share in File storage.</span></span> <span data-ttu-id="138b7-119">A continuación, agregaremos un directorio y un archivo.</span><span class="sxs-lookup"><span data-stu-id="138b7-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="138b7-120">El nombre del recurso compartido de archivos debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="138b7-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="138b7-121">Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="138b7-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="138b7-122">Creación de un directorio en el recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="138b7-122">Create a directory in the file share</span></span>
<span data-ttu-id="138b7-123">Creación de un directorio en el recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="138b7-123">Create a directory in the share.</span></span> <span data-ttu-id="138b7-124">En el siguiente ejemplo, el directorio se llama `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="138b7-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="138b7-125">Carga de un archivo local al directorio</span><span class="sxs-lookup"><span data-stu-id="138b7-125">Upload a local file to the directory</span></span>
<span data-ttu-id="138b7-126">Ahora cargará un archivo local al directorio.</span><span class="sxs-lookup"><span data-stu-id="138b7-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="138b7-127">El siguiente ejemplo carga un archivo desde `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="138b7-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="138b7-128">Edite la ruta de acceso al archivo de forma que apunte a un archivo válido situado en su equipo local.</span><span class="sxs-lookup"><span data-stu-id="138b7-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="138b7-129">Visualización de los archivos del directorio en una lista</span><span class="sxs-lookup"><span data-stu-id="138b7-129">List the files in the directory</span></span>
<span data-ttu-id="138b7-130">Para ver el archivo en el directorio, puede mostrar todos los archivos de este en una lista.</span><span class="sxs-lookup"><span data-stu-id="138b7-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="138b7-131">Este comando devuelve los archivos y subdirectorios (si hay alguno) del directorio CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="138b7-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="138b7-132">Get-AzureStorageFile devuelve una lista de archivos y directorios para cualquier objeto de directorio que se pase.</span><span class="sxs-lookup"><span data-stu-id="138b7-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="138b7-133">"Get-AzureStorageFile -Share $s" devuelve una lista de archivos y directorios en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="138b7-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="138b7-134">Para obtener una lista de los archivos de un subdirectorio, tiene que pasar el subdirectorio a Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="138b7-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="138b7-135">Esto es lo que hace: la primera parte del comando hasta la barra vertical devuelve una instancia de directorio del subdirectorio CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="138b7-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="138b7-136">A continuación, esto se pasa a Get-AzureStorageFile, que devuelve los archivos y directorios en CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="138b7-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="138b7-137">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="138b7-137">Copy files</span></span>
<span data-ttu-id="138b7-138">A partir de la versión 0.9.7 de Azure PowerShell, puede copiar un archivo en otro, un archivo en un blob o un blob en un archivo.</span><span class="sxs-lookup"><span data-stu-id="138b7-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="138b7-139">A continuación se muestra cómo realizar estas operaciones de copia mediante cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="138b7-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="138b7-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="138b7-140">Next steps</span></span>
<span data-ttu-id="138b7-141">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="138b7-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="138b7-142">P+F</span><span class="sxs-lookup"><span data-stu-id="138b7-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="138b7-143">Solución de problemas en Windows</span><span class="sxs-lookup"><span data-stu-id="138b7-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="138b7-144">Solución de problemas en Linux</span><span class="sxs-lookup"><span data-stu-id="138b7-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    