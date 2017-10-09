---
title: aaaHow toouse PowerShell toomanage almacenamiento de archivos de Azure | Documentos de Microsoft
description: "Obtenga información acerca de almacenamiento de archivos de Azure de toouse PowerShell toomanage."
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="c5cbb-103">¿Cómo toouse PowerShell toomanage almacenamiento de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="c5cbb-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="c5cbb-104">Puede usar toocreate de PowerShell de Azure y administrar recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="c5cbb-105">Instalar los cmdlets de PowerShell de hello para el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c5cbb-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="c5cbb-106">tooprepare toouse PowerShell, descargar e instalar los cmdlets de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c5cbb-107">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) para hello instalar punto e instrucciones de instalación.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="c5cbb-108">Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="c5cbb-109">Abra una ventana de Azure PowerShell haciendo clic en **Inicio** y escribiendo **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="c5cbb-110">ventana de PowerShell de Hello carga el módulo de Powershell de Azure de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="c5cbb-111">Creación de un contexto para la cuenta y clave de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c5cbb-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="c5cbb-112">Crear el contexto de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-112">Create hello storage account context.</span></span> <span data-ttu-id="c5cbb-113">contexto de Hello encapsula clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="c5cbb-114">Para obtener instrucciones acerca de cómo copiar la clave de cuenta de hello [portal de Azure](https://portal.azure.com), consulte [visualizar y copiar claves de acceso de almacenamiento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="c5cbb-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="c5cbb-115">Reemplace `storage-account-name` y `storage-account-key` con el nombre de la cuenta de almacenamiento y la clave en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="c5cbb-116">Creación de un nuevo recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="c5cbb-116">Create a new file share</span></span>
<span data-ttu-id="c5cbb-117">Crear recurso compartido nuevo hello, denominado `logs`.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="c5cbb-118">Ahora tiene un recurso compartido de archivos en Almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-118">You now have a file share in File storage.</span></span> <span data-ttu-id="c5cbb-119">A continuación, agregaremos un directorio y un archivo.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5cbb-120">nombre de Hello el recurso compartido de archivos debe ser en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="c5cbb-121">Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5cbb-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="c5cbb-122">Cree un directorio en el recurso compartido de archivos de Hola</span><span class="sxs-lookup"><span data-stu-id="c5cbb-122">Create a directory in hello file share</span></span>
<span data-ttu-id="c5cbb-123">Cree un directorio en el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-123">Create a directory in hello share.</span></span> <span data-ttu-id="c5cbb-124">En el siguiente ejemplo de Hola, directorio de Hola se denomina `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="c5cbb-125">Cargar un directorio de archivos local toohello</span><span class="sxs-lookup"><span data-stu-id="c5cbb-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="c5cbb-126">Ahora cargue un directorio de toohello de archivos local.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="c5cbb-127">Hello en el ejemplo siguiente se carga un archivo de `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="c5cbb-128">Edite la ruta de acceso de archivo de Hola para que apunte tooa archivo válido en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="c5cbb-129">Enumerar archivos de hello en el directorio de Hola</span><span class="sxs-lookup"><span data-stu-id="c5cbb-129">List hello files in hello directory</span></span>
<span data-ttu-id="c5cbb-130">toosee Hola archivo hello directorio, puede enumerar todos los archivos del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="c5cbb-131">Este comando devuelve subdirectorios y archivos de hello (si hay alguno) hello CustomLogs directorio.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="c5cbb-132">Get-AzureStorageFile devuelve una lista de archivos y directorios para cualquier objeto de directorio que se pase.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="c5cbb-133">"Get-AzureStorageFile-compartir $s" devuelve una lista de archivos y directorios en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="c5cbb-134">tooget una lista de archivos en un subdirectorio, deberá toopass Hola subdirectorio tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="c5cbb-135">Es lo que hace esto: Hola primera parte del comando hello la canalización de toohello devuelve una instancia del directorio del subdirectorio de hello CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="c5cbb-136">A continuación, que se pasó a Get-AzureStorageFile, que devuelve Hola archivos y directorios en CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="c5cbb-137">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="c5cbb-137">Copy files</span></span>
<span data-ttu-id="c5cbb-138">A partir de la versión 0.9.7 de PowerShell de Azure, puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="c5cbb-139">A continuación se muestran cómo tooperform estas copian operaciones mediante cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="c5cbb-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5cbb-140">Next steps</span></span>
<span data-ttu-id="c5cbb-141">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5cbb-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="c5cbb-142">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="c5cbb-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="c5cbb-143">Solución de problemas en Windows</span><span class="sxs-lookup"><span data-stu-id="c5cbb-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="c5cbb-144">Solución de problemas en Linux</span><span class="sxs-lookup"><span data-stu-id="c5cbb-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    