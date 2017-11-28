---
title: aaaCopy o mover datos tooAzure almacenamiento con AzCopy en Linux | Documentos de Microsoft
description: "Usar hello AzCopy en la utilidad de Linux a toomove o copia de la tooor de datos con el del contenido de blob y archivo. Copiar datos tooAzure almacenamiento de archivos locales, o copiar datos dentro de o entre cuentas de almacenamiento. Migrar fácilmente el almacenamiento de datos tooAzure."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="a4798-105">Transferencia de datos con AzCopy en Linux</span><span class="sxs-lookup"><span data-stu-id="a4798-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="a4798-106">AzCopy en Linux es una utilidad de línea de comandos diseñada para copiar datos tooand de almacenamiento de blobs de Microsoft Azure y el archivo mediante comandos sencillos con un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="a4798-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="a4798-107">Puede copiar datos de una tooanother de objeto dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a4798-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="a4798-108">Hay dos versiones de AzCopy que puede descargar.</span><span class="sxs-lookup"><span data-stu-id="a4798-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="a4798-109">AzCopy en Linux se compila con .NET Core Framework, que tiene como destino plataformas Linux que ofrecen opciones de línea de comandos con estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="a4798-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="a4798-110">[AzCopy en Windows](storage-use-azcopy.md) se compila con .NET Framework y ofrece opciones de línea de comandos con estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="a4798-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="a4798-111">En este artículo se describe AzCopy en Linux.</span><span class="sxs-lookup"><span data-stu-id="a4798-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="a4798-112">Descarga e instalación de AzCopy</span><span class="sxs-lookup"><span data-stu-id="a4798-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="a4798-113">Instalación en Linux</span><span class="sxs-lookup"><span data-stu-id="a4798-113">Installation on Linux</span></span>

<span data-ttu-id="a4798-114">AzCopy en Linux requiere el marco de trabajo de .NET Core en la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="a4798-115">Consulte las instrucciones de instalación de hello en hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) página.</span><span class="sxs-lookup"><span data-stu-id="a4798-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="a4798-116">Como ejemplo, instalemos .NET Core en Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="a4798-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="a4798-117">Para la Guía de instalación más reciente de hello, visite [.NET Core en Linux](https://www.microsoft.com/net/core#linuxubuntu) página de instalación.</span><span class="sxs-lookup"><span data-stu-id="a4798-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="a4798-118">Una vez que instale .NET Core, descargue e instale AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a4798-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="a4798-119">Puede quitar archivos de hello extraída una vez instalado AzCopy en Linux.</span><span class="sxs-lookup"><span data-stu-id="a4798-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="a4798-120">O bien si no tiene privilegios de superusuario, también puede ejecutar AzCopy mediante script de shell de hello 'azcopy' en la carpeta extraída de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="a4798-121">Instalación alternativa en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a4798-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="a4798-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="a4798-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="a4798-123">Agregue apt source para .NET Core:</span><span class="sxs-lookup"><span data-stu-id="a4798-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="a4798-124">Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:</span><span class="sxs-lookup"><span data-stu-id="a4798-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="a4798-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="a4798-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="a4798-126">Agregue apt source para .NET Core:</span><span class="sxs-lookup"><span data-stu-id="a4798-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="a4798-127">Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:</span><span class="sxs-lookup"><span data-stu-id="a4798-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="a4798-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="a4798-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="a4798-129">Agregue apt source para .NET Core:</span><span class="sxs-lookup"><span data-stu-id="a4798-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="a4798-130">Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:</span><span class="sxs-lookup"><span data-stu-id="a4798-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="a4798-131">Escritura del primer comando de AzCopy</span><span class="sxs-lookup"><span data-stu-id="a4798-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="a4798-132">sintaxis básica de Hola para comandos de AzCopy es:</span><span class="sxs-lookup"><span data-stu-id="a4798-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="a4798-133">Hello en los ejemplos siguientes muestra varios escenarios para copiar datos tooand de Blobs de Microsoft Azure y los archivos.</span><span class="sxs-lookup"><span data-stu-id="a4798-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="a4798-134">Consulte toohello `azcopy --help` menú para obtener una explicación detallada de los parámetros de hello utilizadas en cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a4798-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="a4798-135">Blob: descarga</span><span class="sxs-lookup"><span data-stu-id="a4798-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="a4798-136">Descarga de un solo blob</span><span class="sxs-lookup"><span data-stu-id="a4798-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-137">Si carpeta hello `/mnt/myfiles` no existe, AzCopy lo crea y descarga `abc.txt ` en la nueva carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="a4798-138">Descarga de un solo blob desde la región secundaria</span><span class="sxs-lookup"><span data-stu-id="a4798-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-139">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="a4798-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="a4798-140">Descarga de todos los blobs</span><span class="sxs-lookup"><span data-stu-id="a4798-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="a4798-141">Suponga la siguiente Hola blobs residen en el contenedor especificado de hello:</span><span class="sxs-lookup"><span data-stu-id="a4798-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="a4798-142">Después de la operación de descarga de Hola Hola directory `/mnt/myfiles` incluye Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="a4798-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="a4798-143">Si no especifica la opción `--recursive`, no se descargará ningún blob.</span><span class="sxs-lookup"><span data-stu-id="a4798-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="a4798-144">Descarga de blobs con el prefijo especificado</span><span class="sxs-lookup"><span data-stu-id="a4798-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="a4798-145">Suponga la siguiente Hola blobs residen en el contenedor especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="a4798-146">Todos los blobs que comienzan con el prefijo de hello `a` se descargan.</span><span class="sxs-lookup"><span data-stu-id="a4798-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="a4798-147">Después de la operación de descarga de Hola Hola carpeta `/mnt/myfiles` incluye Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="a4798-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="a4798-148">prefijo de Hello aplica toohello directorio virtual, que forma Hola primera parte del nombre de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="a4798-149">Ejemplo de Hola mostrado anteriormente, directorio virtual hello no coincide con el prefijo especificado de hello, por lo que no se descarga ningún blob.</span><span class="sxs-lookup"><span data-stu-id="a4798-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="a4798-150">Además, si hello opción `--recursive` no se especifica, AzCopy descargar los blobs.</span><span class="sxs-lookup"><span data-stu-id="a4798-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="a4798-151">Establecer la hora de última modificación de Hola de los archivos exportados toobe igual que Hola blobs de origen</span><span class="sxs-lookup"><span data-stu-id="a4798-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="a4798-152">También puede excluir blobs de operación de descarga de hello según su hora de última modificación.</span><span class="sxs-lookup"><span data-stu-id="a4798-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="a4798-153">Por ejemplo, si desea que los blobs tooexclude cuya hora de última modificación es hello igual o más reciente que el archivo de destino de hello, agregar hello `--exclude-newer` opción:</span><span class="sxs-lookup"><span data-stu-id="a4798-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="a4798-154">O si desea que los blobs tooexclude cuya hora de última modificación es hello igual o anterior a archivo de destino de hello, agregue hello `--exclude-older` opción:</span><span class="sxs-lookup"><span data-stu-id="a4798-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="a4798-155">Blob: carga</span><span class="sxs-lookup"><span data-stu-id="a4798-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="a4798-156">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="a4798-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-157">Si no existe el contenedor de destino especificado de hello, AzCopy lo crea y cargas Hola archivos en él.</span><span class="sxs-lookup"><span data-stu-id="a4798-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="a4798-158">Cargar archivo único directorio toovirtual</span><span class="sxs-lookup"><span data-stu-id="a4798-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-159">Si Hola especifica el directorio virtual no existe, se AzCopy carga Hola archivo tooinclude Hola directorio virtual en el nombre del blob de hello (*p. ej.*, `vd/abc.txt` en el ejemplo de Hola anterior).</span><span class="sxs-lookup"><span data-stu-id="a4798-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="a4798-160">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="a4798-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="a4798-161">Especificar la opción `--recursive` cargas Hola contenido de hello especificado directorios tooBlob almacenamiento de manera recursiva, lo que significa que todas las subcarpetas y sus archivos se cargan también.</span><span class="sxs-lookup"><span data-stu-id="a4798-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="a4798-162">Por ejemplo, suponga el siguiente Hola archivos residen en la carpeta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="a4798-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="a4798-163">Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="a4798-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="a4798-164">Hola cuando la opción `--recursive` no se especifica, solo hello siguientes tres archivos se cargan:</span><span class="sxs-lookup"><span data-stu-id="a4798-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="a4798-165">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="a4798-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="a4798-166">Suponga la siguiente Hola archivos residen en la carpeta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="a4798-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="a4798-167">Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="a4798-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="a4798-168">Hola cuando la opción `--recursive` no se especifica, AzCopy omite los archivos que están en subdirectorios:</span><span class="sxs-lookup"><span data-stu-id="a4798-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="a4798-169">Especifique el tipo de contenido MIME de Hola de un blob de destino</span><span class="sxs-lookup"><span data-stu-id="a4798-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="a4798-170">De forma predeterminada, AzCopy establece tipo de contenido de Hola de un blob de destino demasiado`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="a4798-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="a4798-171">Sin embargo, puede especificar explícitamente los tipo de contenido de Hola a través de la opción de hello `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="a4798-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="a4798-172">Esta sintaxis establece el tipo de contenido de Hola para todos los blobs en una operación de carga.</span><span class="sxs-lookup"><span data-stu-id="a4798-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="a4798-173">Si hello opción `--set-content-type` se especifica sin un valor, AzCopy establece cada blob o el archivo del tipo de contenido según tooits extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="a4798-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="a4798-174">Blob: copia</span><span class="sxs-lookup"><span data-stu-id="a4798-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="a4798-175">Copia de un solo blob dentro de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a4798-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-176">Cuando copia un blob sin la opción --syn-copy, se realiza una operación de [copia de lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4798-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="a4798-177">Copia de un solo blob entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a4798-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-178">Cuando copia un blob sin la opción --syn-copy, se realiza una operación de [copia de lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4798-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="a4798-179">Copiar blob único de una región secundaria tooprimary otra</span><span class="sxs-lookup"><span data-stu-id="a4798-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-180">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="a4798-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="a4798-181">Copia de un solo blob y de sus instantáneas entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a4798-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="a4798-182">Después de la operación de copia de hello, contenedor de destino de hello incluye blob hello y sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="a4798-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="a4798-183">Hello contenedor incluye siguiente Hola blob y sus instantáneas:</span><span class="sxs-lookup"><span data-stu-id="a4798-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="a4798-184">Copia sincrónica de blobs entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a4798-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="a4798-185">De forma predeterminada, AzCopy copia datos entre dos extremos de almacenamiento asincrónicamente.</span><span class="sxs-lookup"><span data-stu-id="a4798-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="a4798-186">Por lo tanto, se copia la copia de hello operación se ejecuta en segundo plano de hello utilizando la capacidad de reserva de ancho de banda que no tenga ningún SLA en cuanto a la rapidez con que un blob.</span><span class="sxs-lookup"><span data-stu-id="a4798-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="a4798-187">Hola `--sync-copy` opción garantiza que la operación de copia de Hola obtiene velocidad coherente.</span><span class="sxs-lookup"><span data-stu-id="a4798-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="a4798-188">AzCopy realiza copia sincrónica hello mediante la descarga de blobs de hello toocopy de hello especificado memoria toolocal de origen y, a continuación, cargarlos toohello destino de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="a4798-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="a4798-189">`--sync-copy`puede generar una salida adicional en comparación con el costo tooasynchronous copia.</span><span class="sxs-lookup"><span data-stu-id="a4798-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="a4798-190">Hola enfoque recomendado es toouse esta opción en una máquina virtual de Azure, que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a4798-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="a4798-191">Archivo: descarga</span><span class="sxs-lookup"><span data-stu-id="a4798-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="a4798-192">Descarga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="a4798-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a4798-193">Si no especifica Hola origen es un recurso compartido de archivos de Azure, o bien debe especificar el nombre exacto del archivo de hello, (*p. ej.* `abc.txt`) toodownload un solo archivo, o especificar la opción `--recursive` toodownload todos los archivos en el recurso compartido de Hola de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="a4798-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="a4798-194">Intentar toospecify un patrón de archivo y la opción `--recursive` junto produce un error.</span><span class="sxs-lookup"><span data-stu-id="a4798-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="a4798-195">Descarga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="a4798-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="a4798-196">Tenga en cuenta que no se descarga ninguna carpeta vacía.</span><span class="sxs-lookup"><span data-stu-id="a4798-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="a4798-197">Archivo: carga</span><span class="sxs-lookup"><span data-stu-id="a4798-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="a4798-198">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="a4798-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="a4798-199">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="a4798-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="a4798-200">Tenga en cuenta que no se carga ninguna carpeta vacía.</span><span class="sxs-lookup"><span data-stu-id="a4798-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="a4798-201">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="a4798-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="a4798-202">Archivo: copia</span><span class="sxs-lookup"><span data-stu-id="a4798-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="a4798-203">Copia a través de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="a4798-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="a4798-204">Al copiar un archivo en distintos recursos compartidos de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4798-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="a4798-205">Copiar desde tooblob del recurso compartido de archivo</span><span class="sxs-lookup"><span data-stu-id="a4798-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="a4798-206">Al copiar un archivo de tooblob de recurso compartido de archivo, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.</span><span class="sxs-lookup"><span data-stu-id="a4798-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="a4798-207">Copiar desde el recurso compartido de blob toofile</span><span class="sxs-lookup"><span data-stu-id="a4798-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="a4798-208">Al copiar un archivo de recurso compartido de blob toofile, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.</span><span class="sxs-lookup"><span data-stu-id="a4798-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="a4798-209">Copia sincrónica de archivos</span><span class="sxs-lookup"><span data-stu-id="a4798-209">Synchronously copy files</span></span>
<span data-ttu-id="a4798-210">Puede especificar hello `--sync-copy` opción toocopy datos de almacenamiento de archivos tooFile almacenamiento, de almacenamiento de archivos tooBlob almacenamiento y de almacenamiento de blobs tooFile almacenamiento de forma sincrónica.</span><span class="sxs-lookup"><span data-stu-id="a4798-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="a4798-211">AzCopy ejecuta esta operación, se descargan de memoria de toolocal de datos de origen de hello y, a continuación, cargarlo toodestination.</span><span class="sxs-lookup"><span data-stu-id="a4798-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="a4798-212">En este caso, se aplica el costo de salida estándar.</span><span class="sxs-lookup"><span data-stu-id="a4798-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="a4798-213">Cuando se copia desde el almacenamiento de archivos tooBlob almacenamiento, tipo de blob de hello predeterminado es blob en bloques, usuario puede especificar la opción `/BlobType:page` tipo de blob de destino de toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="a4798-214">Tenga en cuenta que `--sync-copy` podría generar salida adicional costo comparar copia tooasynchronous.</span><span class="sxs-lookup"><span data-stu-id="a4798-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="a4798-215">Hola enfoque recomendado es toouse esta opción en una máquina virtual de Azure, que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a4798-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="a4798-216">Otras características de AzCopy</span><span class="sxs-lookup"><span data-stu-id="a4798-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="a4798-217">Sólo copia los datos que no existen en el destino de Hola</span><span class="sxs-lookup"><span data-stu-id="a4798-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="a4798-218">Hola `--exclude-older` y `--exclude-newer` parámetros permiten tooexclude recursos de origen anterior o posterior que copien, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a4798-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="a4798-219">Si solo desea toocopy recursos de origen que no existen en el destino de hello, puede especificar los dos parámetros en hello AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="a4798-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="a4798-220">Usar un parámetros de línea de comandos de toospecify de archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="a4798-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="a4798-221">Puede incluir cualquier parámetro de la línea de comandos de AzCopy en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="a4798-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="a4798-222">Procesos de AzCopy Hola parámetros en el archivo hello como si hubieran especificado en la línea de comandos de hello, realizar una sustitución directa con contenido de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="a4798-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="a4798-223">Se supone un archivo de configuración denominado `copyoperation`, que contiene Hola siguiendo las líneas.</span><span class="sxs-lookup"><span data-stu-id="a4798-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="a4798-224">Cada parámetro de AzCopy se puede especificar en una sola línea.</span><span class="sxs-lookup"><span data-stu-id="a4798-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="a4798-225">o bien, en líneas independientes:</span><span class="sxs-lookup"><span data-stu-id="a4798-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="a4798-226">AzCopy se produce un error si parámetro hello se divide en dos líneas, como se muestra aquí para hello `--source-key` parámetro:</span><span class="sxs-lookup"><span data-stu-id="a4798-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="a4798-227">Especificación de una firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="a4798-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="a4798-228">También puede especificar una SAS en el contenedor de hello URI:</span><span class="sxs-lookup"><span data-stu-id="a4798-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="a4798-229">Tenga en cuenta que AzCopy actualmente sólo admite hello [cuenta SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="a4798-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="a4798-230">Carpeta de archivo de diario</span><span class="sxs-lookup"><span data-stu-id="a4798-230">Journal file folder</span></span>
<span data-ttu-id="a4798-231">Cada vez que se emite un tooAzCopy de comando, comprueba si existe un archivo de diario en la carpeta predeterminada de hello, o si se encuentra en una carpeta que especifica mediante esta opción.</span><span class="sxs-lookup"><span data-stu-id="a4798-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="a4798-232">Si no existe el archivo de diario de Hola en cualquier lugar, AzCopy trata operación hello como nueva y genera un nuevo archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="a4798-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="a4798-233">Si existe el archivo de diario de hello, AzCopy comprueba si línea de comandos de hello especificado coincide con hello de línea de comandos en el archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="a4798-234">Si coincide con dos líneas de comandos hello, AzCopy reanuda la operación incompleta de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="a4798-235">Si no coinciden, AzCopy solicita diario archivo toostart una nueva operación de usuario tooeither sobrescribir Hola o toocancel operación en curso Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="a4798-236">Si desea que toouse Hola esta ubicación para el archivo de diario de hello:</span><span class="sxs-lookup"><span data-stu-id="a4798-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="a4798-237">Si se omite la opción `--resume`, o especificar la opción `--resume` sin ruta de acceso de carpeta de hello, como se muestra arriba, AzCopy crea archivo diario de hello en la ubicación predeterminada de hello, que es `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="a4798-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="a4798-238">Si ya existe un archivo de diario de hello, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="a4798-239">Si desea que una ubicación personalizada para el archivo de diario de Hola toospecify:</span><span class="sxs-lookup"><span data-stu-id="a4798-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="a4798-240">Este ejemplo crea el archivo de diario de hello si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="a4798-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="a4798-241">Si existe, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="a4798-242">Si desea que una operación de AzCopy tooresume, repita Hola mismo comando.</span><span class="sxs-lookup"><span data-stu-id="a4798-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="a4798-243">AzCopy en Linux le pedirá confirmación:</span><span class="sxs-lookup"><span data-stu-id="a4798-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="a4798-244">Registros detallados de salida</span><span class="sxs-lookup"><span data-stu-id="a4798-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="a4798-245">Especificar número de Hola de operaciones simultáneas toostart</span><span class="sxs-lookup"><span data-stu-id="a4798-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="a4798-246">Opción `--parallel-level` especifica Hola número de operaciones de copia simultáneas.</span><span class="sxs-lookup"><span data-stu-id="a4798-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="a4798-247">De forma predeterminada, AzCopy inicia un número determinado de rendimiento de transferencia de datos de las operaciones simultáneas tooincrease Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="a4798-248">Hola número de operaciones simultáneas es igual ocho veces Hola número de procesadores de que disponga.</span><span class="sxs-lookup"><span data-stu-id="a4798-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="a4798-249">Si está ejecutando AzCopy a través de una red de ancho de banda bajo, puede especificar un número menor para: error de tooavoid de nivel de paralelo causado por la competencia de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4798-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="a4798-250">lista completa de hello tooview de parámetros de AzCopy, desproteger 'azcopy--ayuda' menú.</span><span class="sxs-lookup"><span data-stu-id="a4798-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="a4798-251">Problemas conocidos y procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="a4798-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="a4798-252">Error: No se encuentra .NET Core en sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="a4798-253">Si se produce un error que indica que no está instalado .NET Core en sistema de hello, Hola binario de .NET Core de ruta de acceso toohello `dotnet` posible que falte.</span><span class="sxs-lookup"><span data-stu-id="a4798-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="a4798-254">En Ordenar tooaddress este problema, busque binario de .NET Core hello en el sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="a4798-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="a4798-255">Esto devuelve Hola ruta de acceso toohello dotnet binario.</span><span class="sxs-lookup"><span data-stu-id="a4798-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="a4798-256">Ahora agregue esta variable de ruta de acceso de toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="a4798-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="a4798-257">Para sudo, edite secure_path toocontain Hola ruta de acceso toohello dotnet binario:</span><span class="sxs-lookup"><span data-stu-id="a4798-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="a4798-258">En este ejemplo, la variable secure_path se lee de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="a4798-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="a4798-259">Para el usuario actual de hello, editar.bash_profile/.profile tooinclude Hola ruta de acceso toohello dotnet binario en la variable de ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="a4798-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="a4798-260">Compruebe que .NET Core ahora esté en PATH:</span><span class="sxs-lookup"><span data-stu-id="a4798-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="a4798-261">Error al instalar AzCopy</span><span class="sxs-lookup"><span data-stu-id="a4798-261">Error Installing AzCopy</span></span>
<span data-ttu-id="a4798-262">Si encuentra problemas con la instalación de AzCopy, puede intentar toorun AzCopy mediante scripts de bash Hola Hola extraído `azcopy` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a4798-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="a4798-263">Limitación de escrituras concurrentes mientras se copian datos</span><span class="sxs-lookup"><span data-stu-id="a4798-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="a4798-264">Cuando copia blobs o archivos con AzCopy, tenga en cuenta que otra aplicación puede modificar datos de hello mientras que va a copiar.</span><span class="sxs-lookup"><span data-stu-id="a4798-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="a4798-265">Si es posible, asegúrese de que los datos de hello que va a copiar no se está modificando durante la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="a4798-266">Por ejemplo, al copiar un disco duro virtual asociado a una máquina virtual de Azure, asegúrese de que ninguna otra aplicación actualmente está escribiendo toohello disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="a4798-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="a4798-267">Una buena manera toodo es mediante la concesión de hello recursos toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="a4798-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="a4798-268">Como alternativa, puede crear una instantánea de disco duro virtual de hello en primer lugar y, a continuación, copiar instantáneas Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="a4798-269">Si no se puede impedir que otras aplicaciones escribir tooblobs o archivos mientras se se copian y tenga en cuenta que al trabajo Hola Hola finaliza, hello recursos copiados pueden ya no tiene paridad completa con recursos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="a4798-270">Ejecutar una instancia de AzCopy en un solo equipo.</span><span class="sxs-lookup"><span data-stu-id="a4798-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="a4798-271">AzCopy es toomaximize diseñada Hola utilización de la transferencia de datos de máquina recursos tooaccelerate hello, le recomendamos que ejecute solo una instancia de AzCopy en un equipo y especifica la opción de hello `--parallel-level` si necesita las operaciones más simultáneas.</span><span class="sxs-lookup"><span data-stu-id="a4798-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="a4798-272">Para obtener más información, escriba `AzCopy --help parallel-level` en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4798-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4798-273">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4798-273">Next steps</span></span>
<span data-ttu-id="a4798-274">Para obtener más información sobre el almacenamiento de Azure y AzCopy, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4798-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="a4798-275">Documentación de Almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="a4798-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="a4798-276">Introducción tooAzure almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a4798-276">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="a4798-277">crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a4798-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="a4798-278">Administración de blobs con el Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="a4798-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="a4798-279">Uso de hello Azure CLI 2.0 con el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a4798-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="a4798-280">¿Cómo toouse almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="a4798-280">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="a4798-281">¿Cómo toouse almacenamiento de blobs desde Java</span><span class="sxs-lookup"><span data-stu-id="a4798-281">How toouse Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="a4798-282">¿Cómo toouse almacenamiento de blobs de Node.js</span><span class="sxs-lookup"><span data-stu-id="a4798-282">How toouse Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="a4798-283">¿Cómo toouse almacenamiento de blobs de Python</span><span class="sxs-lookup"><span data-stu-id="a4798-283">How toouse Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="a4798-284">Publicaciones en blobs de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a4798-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="a4798-285">Anuncio de AzCopy en Linux (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a4798-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="a4798-286">Introducción a la versión de vista previa de la biblioteca de movimiento de datos de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a4798-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="a4798-287">AzCopy: Introducción a la copia sincrónica y el tipo de contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="a4798-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="a4798-288">AzCopy: Presentación de la disponibilidad general de AzCopy 3.0 y de la versión de vista previa de AzCopy 4.0 compatible con tablas y archivos</span><span class="sxs-lookup"><span data-stu-id="a4798-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="a4798-289">AzCopy: Optimizada para escenarios de copia a gran escala</span><span class="sxs-lookup"><span data-stu-id="a4798-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="a4798-290">AzCopy: Compatibilidad para almacenamiento con redundancia geográfica de acceso de lectura</span><span class="sxs-lookup"><span data-stu-id="a4798-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="a4798-291">AzCopy: Transferencia de datos con modo reiniciable y token SAS</span><span class="sxs-lookup"><span data-stu-id="a4798-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="a4798-292">AzCopy: Uso de copia de blobs entre cuentas</span><span class="sxs-lookup"><span data-stu-id="a4798-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="a4798-293">AzCopy: Carga y descarga de archivos para blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="a4798-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

