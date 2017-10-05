---
title: Copia o movimiento de datos a Azure Storage con AzCopy en Linux | Microsoft Docs
description: "Use la utilidad AzCopy en Linux para mover o copiar datos hacia contenido de blobs y archivos o desde ellos. Copie datos a Almacenamiento de Azure desde archivos locales o copie datos en o entre cuentas de almacenamiento. Migre fácilmente sus datos a Almacenamiento de Azure."
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
ms.openlocfilehash: d17f63dcee590529756d48d699f78b3fb30f973c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="8c571-105">Transferencia de datos con AzCopy en Linux</span><span class="sxs-lookup"><span data-stu-id="8c571-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="8c571-106">AzCopy en Linux es una utilidad de la línea de comandos diseñada para copiar datos hacia almacenamiento de archivos y blobs de Microsoft Azure o desde estos mediante comandos sencillos con un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="8c571-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="8c571-107">También puede copiar datos de un objeto a otro dentro de la cuenta de almacenamiento o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c571-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="8c571-108">Hay dos versiones de AzCopy que puede descargar.</span><span class="sxs-lookup"><span data-stu-id="8c571-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="8c571-109">AzCopy en Linux se compila con .NET Core Framework, que tiene como destino plataformas Linux que ofrecen opciones de línea de comandos con estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="8c571-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="8c571-110">[AzCopy en Windows](storage-use-azcopy.md) se compila con .NET Framework y ofrece opciones de línea de comandos con estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="8c571-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="8c571-111">En este artículo se describe AzCopy en Linux.</span><span class="sxs-lookup"><span data-stu-id="8c571-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="8c571-112">Descarga e instalación de AzCopy</span><span class="sxs-lookup"><span data-stu-id="8c571-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="8c571-113">Instalación en Linux</span><span class="sxs-lookup"><span data-stu-id="8c571-113">Installation on Linux</span></span>

<span data-ttu-id="8c571-114">AzCopy en Linux requiere .NET Core Framework en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="8c571-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="8c571-115">Consulte las instrucciones de instalación en la página [.NET Core](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="8c571-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="8c571-116">Como ejemplo, instalemos .NET Core en Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="8c571-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="8c571-117">Para la guía de instalación más reciente, visite la página de instalación de [.NET Core en Linux](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="8c571-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="8c571-118">Una vez que instale .NET Core, descargue e instale AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8c571-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="8c571-119">Puede quitar los archivos extraídos una vez que se instale AzCopy en Linux.</span><span class="sxs-lookup"><span data-stu-id="8c571-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="8c571-120">También, si no tiene privilegios de superusuario, también puede ejecutar AzCopy con el script de shell "azcopy" en la carpeta extraída.</span><span class="sxs-lookup"><span data-stu-id="8c571-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="8c571-121">Instalación alternativa en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8c571-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="8c571-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="8c571-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="8c571-123">Agregue apt source para .NET Core:</span><span class="sxs-lookup"><span data-stu-id="8c571-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="8c571-124">Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8c571-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="8c571-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="8c571-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="8c571-126">Agregue apt source para .NET Core:</span><span class="sxs-lookup"><span data-stu-id="8c571-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="8c571-127">Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8c571-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="8c571-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="8c571-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="8c571-129">Agregue apt source para .NET Core:</span><span class="sxs-lookup"><span data-stu-id="8c571-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="8c571-130">Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8c571-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="8c571-131">Escritura del primer comando de AzCopy</span><span class="sxs-lookup"><span data-stu-id="8c571-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="8c571-132">La sintaxis básica del comando AzCopy es:</span><span class="sxs-lookup"><span data-stu-id="8c571-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="8c571-133">Los ejemplos siguientes demuestran diversos escenarios para copiar datos a los blobs y archivos de Microsoft Azure y desde estos.</span><span class="sxs-lookup"><span data-stu-id="8c571-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="8c571-134">Consulte el menú `azcopy --help` para una explicación detallada de los parámetros que se usan en cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8c571-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="8c571-135">Blob: descarga</span><span class="sxs-lookup"><span data-stu-id="8c571-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="8c571-136">Descarga de un solo blob</span><span class="sxs-lookup"><span data-stu-id="8c571-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-137">Si la carpeta `/mnt/myfiles` no existe, AzCopy la crea y descarga `abc.txt ` a la carpeta nueva.</span><span class="sxs-lookup"><span data-stu-id="8c571-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="8c571-138">Descarga de un solo blob desde la región secundaria</span><span class="sxs-lookup"><span data-stu-id="8c571-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-139">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="8c571-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="8c571-140">Descarga de todos los blobs</span><span class="sxs-lookup"><span data-stu-id="8c571-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="8c571-141">Supongamos que los siguientes blobs residen en el contenedor especificado:</span><span class="sxs-lookup"><span data-stu-id="8c571-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="8c571-142">Después de la operación de descarga, el directorio `/mnt/myfiles` incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="8c571-143">Si no especifica la opción `--recursive`, no se descargará ningún blob.</span><span class="sxs-lookup"><span data-stu-id="8c571-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="8c571-144">Descarga de blobs con el prefijo especificado</span><span class="sxs-lookup"><span data-stu-id="8c571-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="8c571-145">Supongamos que los siguientes blobs residen en el contenedor especificado.</span><span class="sxs-lookup"><span data-stu-id="8c571-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="8c571-146">Se descargarán todos los blobs que comiencen con el prefijo `a`.</span><span class="sxs-lookup"><span data-stu-id="8c571-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="8c571-147">Después de la operación de descarga, la carpeta `/mnt/myfiles` incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="8c571-148">El prefijo se aplica al directorio virtual, que forma la primera parte del nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="8c571-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="8c571-149">En el ejemplo mostrado anteriormente, el directorio virtual no coincide con el prefijo especificado, por lo que no se descarga ningún blob.</span><span class="sxs-lookup"><span data-stu-id="8c571-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="8c571-150">Además, si no se especifica la opción `--recursive`, AzCopy no descarga ningún blob.</span><span class="sxs-lookup"><span data-stu-id="8c571-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="8c571-151">Establecimiento de la hora de la última modificación de los archivos exportados para que coincida con la de los blobs de origen</span><span class="sxs-lookup"><span data-stu-id="8c571-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="8c571-152">También puede excluir los blobs de la operación de descarga basándose en la hora de su última modificación.</span><span class="sxs-lookup"><span data-stu-id="8c571-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="8c571-153">Por ejemplo, si desea excluir los blobs cuya hora de la última modificación es igual o más reciente que la del archivo de destino, agregue la opción `--exclude-newer` :</span><span class="sxs-lookup"><span data-stu-id="8c571-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="8c571-154">O, si desea excluir los blobs cuya hora de la última modificación es igual o anterior a la del archivo de destino, agregue la opción `--exclude-older` :</span><span class="sxs-lookup"><span data-stu-id="8c571-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="8c571-155">Blob: carga</span><span class="sxs-lookup"><span data-stu-id="8c571-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="8c571-156">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="8c571-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-157">Si el contenedor de destino especificado no existe, AzCopy lo crea y carga el archivo en él.</span><span class="sxs-lookup"><span data-stu-id="8c571-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="8c571-158">Carga de un solo archivo en el directorio virtual</span><span class="sxs-lookup"><span data-stu-id="8c571-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-159">Si el directorio virtual especificado no existe, AzCopy carga el archivo para incluir el directorio virtual en el nombre del blob (*por ejemplo*, `vd/abc.txt` en el ejemplo anterior).</span><span class="sxs-lookup"><span data-stu-id="8c571-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="8c571-160">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="8c571-161">Al especificar la opción `--recursive` se carga el contenido del directorio especificado en Blob Storage de forma recursiva, lo que significa que todas las subcarpetas y sus archivos también se cargan.</span><span class="sxs-lookup"><span data-stu-id="8c571-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="8c571-162">Por ejemplo, supongamos que los siguientes archivos residen en la carpeta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="8c571-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="8c571-163">Después de la operación de carga, el contenedor incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="8c571-164">Cuando la opción `--recursive` no se especifica, solo se cargan los tres archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="8c571-165">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="8c571-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="8c571-166">Supongamos que los siguientes archivos residen en la carpeta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="8c571-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="8c571-167">Después de la operación de carga, el contenedor incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="8c571-168">Cuando no se especifica la opción `--recursive`, AzCopy omite los archivos que se encuentran en subdirectorios:</span><span class="sxs-lookup"><span data-stu-id="8c571-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="8c571-169">Especificación del tipo de contenido MIME de un blob de destino</span><span class="sxs-lookup"><span data-stu-id="8c571-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="8c571-170">De forma predeterminada, AzCopy define el tipo de contenido de un blob de destino como `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="8c571-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="8c571-171">Sin embargo, puede especificar explícitamente el tipo de contenido a través de la opción `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="8c571-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="8c571-172">Esta sintaxis establece el tipo de contenido para todos los blobs de una operación de carga.</span><span class="sxs-lookup"><span data-stu-id="8c571-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="8c571-173">Si la opción `--set-content-type` se especifica sin un valor, AzCopy establece el tipo de contenido de cada blob o archivo según su extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="8c571-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="8c571-174">Blob: copia</span><span class="sxs-lookup"><span data-stu-id="8c571-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="8c571-175">Copia de un solo blob dentro de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c571-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-176">Cuando copia un blob sin la opción --syn-copy, se realiza una operación de [copia de lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c571-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="8c571-177">Copia de un solo blob entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c571-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-178">Cuando copia un blob sin la opción --syn-copy, se realiza una operación de [copia de lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c571-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="8c571-179">Copia de un solo blob desde la región secundaria a la región primaria</span><span class="sxs-lookup"><span data-stu-id="8c571-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-180">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="8c571-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="8c571-181">Copia de un solo blob y de sus instantáneas entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c571-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="8c571-182">Después de la operación de copia, el contenedor de destino incluye el blob y sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="8c571-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="8c571-183">El contenedor incluye el siguiente blob y sus instantáneas:</span><span class="sxs-lookup"><span data-stu-id="8c571-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="8c571-184">Copia sincrónica de blobs entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c571-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="8c571-185">De forma predeterminada, AzCopy copia datos entre dos extremos de almacenamiento asincrónicamente.</span><span class="sxs-lookup"><span data-stu-id="8c571-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="8c571-186">Por lo tanto, la operación de copia se ejecuta en segundo plano con una capacidad de ancho de banda de reserva que no tiene contrato de nivel de servicio en términos de la rapidez con que se copia un blob.</span><span class="sxs-lookup"><span data-stu-id="8c571-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="8c571-187">La opción `--sync-copy` garantiza que la operación de copia tiene una velocidad uniforme.</span><span class="sxs-lookup"><span data-stu-id="8c571-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="8c571-188">Para hacer la copia sincrónica, AzCopy descarga los blobs que se deben copiar desde el origen especificado a la memoria local y, a continuación, los carga en el destino de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c571-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="8c571-189">`--sync-copy` podría generar un costo de salida adicional en comparación con la copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="8c571-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="8c571-190">El enfoque recomendado es usar esta opción en una máquina virtual de Azure que se encuentre en la misma región que la cuenta de almacenamiento de origen, para evitar el costo de salida.</span><span class="sxs-lookup"><span data-stu-id="8c571-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="8c571-191">Archivo: descarga</span><span class="sxs-lookup"><span data-stu-id="8c571-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="8c571-192">Descarga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="8c571-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8c571-193">Si el origen especificado es un recurso compartido de archivos de Azure, entonces tiene que especificar el nombre de archivo exacto (*p. ej.* `abc.txt`) para descargar un solo archivo, o especificar la opción `--recursive` para descargar todos los archivos en el recurso compartido de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="8c571-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="8c571-194">Si intenta especificar tanto un patrón de archivos como la opción `--recursive` en conjunto, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8c571-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="8c571-195">Descarga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="8c571-196">Tenga en cuenta que no se descarga ninguna carpeta vacía.</span><span class="sxs-lookup"><span data-stu-id="8c571-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="8c571-197">Archivo: carga</span><span class="sxs-lookup"><span data-stu-id="8c571-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="8c571-198">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="8c571-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="8c571-199">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="8c571-200">Tenga en cuenta que no se carga ninguna carpeta vacía.</span><span class="sxs-lookup"><span data-stu-id="8c571-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="8c571-201">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="8c571-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="8c571-202">Archivo: copia</span><span class="sxs-lookup"><span data-stu-id="8c571-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="8c571-203">Copia a través de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="8c571-204">Al copiar un archivo en distintos recursos compartidos de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c571-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="8c571-205">Copia desde el recurso compartido de archivos al blob</span><span class="sxs-lookup"><span data-stu-id="8c571-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="8c571-206">Al copiar un archivo desde un recurso compartido de archivos en un blob, se realiza una [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c571-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="8c571-207">Copia desde el blob al recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="8c571-208">Al copiar un archivo desde un blob en un recurso compartido de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c571-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="8c571-209">Copia sincrónica de archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-209">Synchronously copy files</span></span>
<span data-ttu-id="8c571-210">Puede especificar la opción `--sync-copy` para copiar datos de File Storage a File Storage, de File Storage a Blob Storage y de Blob Storage a File Storage de manera sincrónica.</span><span class="sxs-lookup"><span data-stu-id="8c571-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="8c571-211">AzCopy ejecuta esta operación mediante la descarga de los datos de origen a la memoria local y, luego, su carga en el destino.</span><span class="sxs-lookup"><span data-stu-id="8c571-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="8c571-212">En este caso, se aplica el costo de salida estándar.</span><span class="sxs-lookup"><span data-stu-id="8c571-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="8c571-213">Al realizar la copia del Almacenamiento de archivos al Almacenamiento de blobs, el tipo de blob predeterminado es el blob en bloques, por lo tanto, el usuario puede especificar la opción `/BlobType:page` para cambiar el tipo de blob de destino.</span><span class="sxs-lookup"><span data-stu-id="8c571-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="8c571-214">Tenga en cuenta que `--sync-copy` podría generar un costo de salida adicional en comparación con la copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="8c571-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="8c571-215">El enfoque recomendado es usar esta opción en una máquina virtual de Azure que se encuentre en la misma región que la cuenta de almacenamiento de origen, para evitar el costo de salida.</span><span class="sxs-lookup"><span data-stu-id="8c571-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="8c571-216">Otras características de AzCopy</span><span class="sxs-lookup"><span data-stu-id="8c571-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="8c571-217">Solo copie los datos que no existan en el destino</span><span class="sxs-lookup"><span data-stu-id="8c571-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="8c571-218">Los parámetros `--exclude-older` y `--exclude-newer` le permiten excluir los recursos de origen anteriores o posteriores a la copia, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8c571-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="8c571-219">Si solo desea copiar los recursos de origen que no existen en el destino, puede especificar ambos parámetros en el comando de AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8c571-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="8c571-220">Uso de un archivo de configuración para especificar parámetros de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="8c571-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="8c571-221">Puede incluir cualquier parámetro de la línea de comandos de AzCopy en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8c571-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="8c571-222">AzCopy procesa los parámetros del archivo como si hubieran sido especificados en la línea de comandos, realizando una sustitución directa con el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="8c571-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="8c571-223">Imaginemos un archivo de configuración denominado `copyoperation`, que contiene las siguientes líneas.</span><span class="sxs-lookup"><span data-stu-id="8c571-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="8c571-224">Cada parámetro de AzCopy se puede especificar en una sola línea.</span><span class="sxs-lookup"><span data-stu-id="8c571-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="8c571-225">o bien, en líneas independientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="8c571-226">AzCopy genera un error si divide el parámetro en dos líneas, tal como se muestra aquí para el parámetro `--source-key`:</span><span class="sxs-lookup"><span data-stu-id="8c571-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="8c571-227">Especificación de una firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="8c571-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="8c571-228">También puede especificar una SAS en el identificador URI del contenedor:</span><span class="sxs-lookup"><span data-stu-id="8c571-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="8c571-229">Tenga en cuenta que AzCopy actualmente admite solo [SAS de cuenta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="8c571-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="8c571-230">Carpeta de archivo de diario</span><span class="sxs-lookup"><span data-stu-id="8c571-230">Journal file folder</span></span>
<span data-ttu-id="8c571-231">Cada vez que emite un comando a AzCopy, comprueba si existe un archivo de diario en la carpeta predeterminada o si existe una carpeta que especificó a través de esta opción.</span><span class="sxs-lookup"><span data-stu-id="8c571-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="8c571-232">Si el archivo de diario no existe en ningún lugar, AzCopy trata la operación como una nueva y genera un nuevo archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="8c571-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="8c571-233">Si el archivo de diario existe, AzCopy comprueba si la línea de comandos escrita coincide con la línea de comandos de dicho archivo.</span><span class="sxs-lookup"><span data-stu-id="8c571-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="8c571-234">Si las dos líneas de comandos coinciden, AzCopy reanudará la operación incompleta.</span><span class="sxs-lookup"><span data-stu-id="8c571-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="8c571-235">Si no coinciden, AzCopy le pide al usuario que sobrescriba el archivo de diario para iniciar una operación nueva o que cancele la operación actual.</span><span class="sxs-lookup"><span data-stu-id="8c571-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="8c571-236">Si desea usar la ubicación predeterminada para el archivo de diario:</span><span class="sxs-lookup"><span data-stu-id="8c571-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="8c571-237">Si omite la opción `--resume` o especifica la opción `--resume` sin la ruta de acceso a la carpeta, tal y como se muestra anteriormente, AzCopy crea el archivo de diario en la ubicación predeterminada, que es `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="8c571-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="8c571-238">Si el archivo de diario ya existe, AzCopy reanuda la operación basándose en dicho archivo.</span><span class="sxs-lookup"><span data-stu-id="8c571-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="8c571-239">Si desea especificar una ubicación personalizada para el archivo de diario:</span><span class="sxs-lookup"><span data-stu-id="8c571-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="8c571-240">Este ejemplo crea el archivo de diario si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="8c571-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="8c571-241">Si no existe, AzCopy reanuda la operación basándose en el archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="8c571-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="8c571-242">Si desea reanudar una operación de AzCopy, repita el mismo comando.</span><span class="sxs-lookup"><span data-stu-id="8c571-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="8c571-243">AzCopy en Linux le pedirá confirmación:</span><span class="sxs-lookup"><span data-stu-id="8c571-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="8c571-244">Registros detallados de salida</span><span class="sxs-lookup"><span data-stu-id="8c571-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="8c571-245">Especificación del número de operaciones simultáneas para iniciar</span><span class="sxs-lookup"><span data-stu-id="8c571-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="8c571-246">La opción `--parallel-level` especifica el número de operaciones de copia simultáneas.</span><span class="sxs-lookup"><span data-stu-id="8c571-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="8c571-247">De manera predeterminada, AzCopy inicia un número determinado de operaciones simultáneas para aumentar el rendimiento de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="8c571-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="8c571-248">El número de operaciones simultáneas equivale a ocho veces el número de procesadores que posee.</span><span class="sxs-lookup"><span data-stu-id="8c571-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="8c571-249">Si ejecuta AzCopy en una red de ancho de banda bajo, puede especificar un número inferior para --parallel-level con el fin de evitar errores provocados por la competencia de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c571-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="8c571-250">Para ver la lista completa de parámetros de AzCopy, compruebe el menú "azcopy --help".</span><span class="sxs-lookup"><span data-stu-id="8c571-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="8c571-251">Problemas conocidos y procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="8c571-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="8c571-252">Error: .NET Core no se encuentra en el sistema.</span><span class="sxs-lookup"><span data-stu-id="8c571-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="8c571-253">Si encuentra un error que indica que .NET Core no está instalado en el sistema, es probable que falte la variable PATH al archivo binario `dotnet` de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8c571-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="8c571-254">Para solucionar este problema, busque el archivo binario de .NET Core en el sistema:</span><span class="sxs-lookup"><span data-stu-id="8c571-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="8c571-255">Con esto se devuelve la ruta de acceso al archivo binario dotnet.</span><span class="sxs-lookup"><span data-stu-id="8c571-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="8c571-256">Ahora agregue esta ruta de acceso a la variable PATH.</span><span class="sxs-lookup"><span data-stu-id="8c571-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="8c571-257">Para sudo, edite secure_path para que contenga el archivo binario dotnet:</span><span class="sxs-lookup"><span data-stu-id="8c571-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="8c571-258">En este ejemplo, la variable secure_path se lee de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="8c571-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="8c571-259">En el caso del usuario actual, edite .bash_profile/.profile para incluir la ruta de acceso al archivo binario dotnet en la variable PATH</span><span class="sxs-lookup"><span data-stu-id="8c571-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="8c571-260">Compruebe que .NET Core ahora esté en PATH:</span><span class="sxs-lookup"><span data-stu-id="8c571-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="8c571-261">Error al instalar AzCopy</span><span class="sxs-lookup"><span data-stu-id="8c571-261">Error Installing AzCopy</span></span>
<span data-ttu-id="8c571-262">Si encuentra problemas para instalar AzCopy, puede intentar ejecutar AzCopy con el script de Bash en la carpeta `azcopy` extraída.</span><span class="sxs-lookup"><span data-stu-id="8c571-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="8c571-263">Limitación de escrituras concurrentes mientras se copian datos</span><span class="sxs-lookup"><span data-stu-id="8c571-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="8c571-264">Cuando copie blobs o archivos con AzCopy, recuerde que otra aplicación puede estar modificando los datos mientras se copian.</span><span class="sxs-lookup"><span data-stu-id="8c571-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="8c571-265">Si es posible, asegúrese de que los datos no se modifican durante la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="8c571-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="8c571-266">Por ejemplo, cuando copie un VHD asociado con una máquina virtual de Azure, asegúrese de que ninguna otra aplicación está escribiendo actualmente en el VHD.</span><span class="sxs-lookup"><span data-stu-id="8c571-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="8c571-267">Una buena manera de hacerlo es mediante la concesión de los recursos que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="8c571-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="8c571-268">Alternativamente, puede crear una instantánea del VHD primero y, después, copiar la instantánea.</span><span class="sxs-lookup"><span data-stu-id="8c571-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="8c571-269">Si no puede impedir que otras aplicaciones escriban en blobs o archivos mientras se copian, recuerde que para cuando el trabajo finalice, los recursos copiados puede que ya no tengan una paridad total con los recursos de origen.</span><span class="sxs-lookup"><span data-stu-id="8c571-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="8c571-270">Ejecutar una instancia de AzCopy en un solo equipo.</span><span class="sxs-lookup"><span data-stu-id="8c571-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="8c571-271">AzCopy está diseñado para maximizar el uso de los recursos del equipo para acelerar la transferencia de datos. Se recomienda ejecutar solo una instancia de AzCopy en un equipo y especificar la opción `--parallel-level` si necesita más operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="8c571-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="8c571-272">Para obtener más detalles, escriba `AzCopy --help parallel-level` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="8c571-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c571-273">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c571-273">Next steps</span></span>
<span data-ttu-id="8c571-274">Para más información sobre Azure Storage y AzCopy, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c571-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="8c571-275">Documentación de Almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="8c571-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="8c571-276">Introducción a Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8c571-276">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="8c571-277">Cree una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c571-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="8c571-278">Administración de blobs con el Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="8c571-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="8c571-279">Uso de la CLI de Azure 2.0 con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8c571-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="8c571-280">Uso del almacenamiento de blobs en C++</span><span class="sxs-lookup"><span data-stu-id="8c571-280">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8c571-281">Uso del almacenamiento de blobs de Java</span><span class="sxs-lookup"><span data-stu-id="8c571-281">How to use Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="8c571-282">Uso de almacenamiento de blobs en Node.js</span><span class="sxs-lookup"><span data-stu-id="8c571-282">How to use Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="8c571-283">Uso del almacenamiento de blobs de Python</span><span class="sxs-lookup"><span data-stu-id="8c571-283">How to use Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="8c571-284">Publicaciones en blobs de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8c571-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="8c571-285">Anuncio de AzCopy en Linux (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8c571-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="8c571-286">Introducción a la versión de vista previa de la biblioteca de movimiento de datos de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8c571-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="8c571-287">AzCopy: Introducción a la copia sincrónica y el tipo de contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="8c571-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="8c571-288">AzCopy: Presentación de la disponibilidad general de AzCopy 3.0 y de la versión de vista previa de AzCopy 4.0 compatible con tablas y archivos</span><span class="sxs-lookup"><span data-stu-id="8c571-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="8c571-289">AzCopy: Optimizada para escenarios de copia a gran escala</span><span class="sxs-lookup"><span data-stu-id="8c571-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="8c571-290">AzCopy: Compatibilidad para almacenamiento con redundancia geográfica de acceso de lectura</span><span class="sxs-lookup"><span data-stu-id="8c571-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="8c571-291">AzCopy: Transferencia de datos con modo reiniciable y token SAS</span><span class="sxs-lookup"><span data-stu-id="8c571-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="8c571-292">AzCopy: Uso de copia de blobs entre cuentas</span><span class="sxs-lookup"><span data-stu-id="8c571-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="8c571-293">AzCopy: Carga y descarga de archivos para blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="8c571-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

