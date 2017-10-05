---
title: Copia o traslado de datos a Azure Storage con AzCopy en Windows| Microsoft Docs
description: "Use la utilidad AzCopy en Windows para mover o copiar datos hacia o desde contenido de archivos, blobs y tablas. Copie datos a Almacenamiento de Azure desde archivos locales o copie datos en o entre cuentas de almacenamiento. Migre fácilmente sus datos a Almacenamiento de Azure."
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
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: 9806697747b2409d4bd0ae19dc0b9fe01f500dc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="e0707-105">Transferencia de datos con AzCopy en Windows</span><span class="sxs-lookup"><span data-stu-id="e0707-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="e0707-106">AzCopy es una utilidad de línea de comandos diseñada para copiar datos a y desde los servicios de Almacenamiento de blobs, Archivos y Almacenamiento de tablas de Microsoft Azure, mediante sencillos comandos con un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="e0707-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="e0707-107">También puede copiar datos de un objeto a otro dentro de la cuenta de almacenamiento o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0707-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="e0707-108">Hay dos versiones de AzCopy que puede descargar.</span><span class="sxs-lookup"><span data-stu-id="e0707-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="e0707-109">AzCopy en Windows está integrado en .NET Framework y ofrece opciones de línea de comandos de estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="e0707-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="e0707-110">[AzCopy en Linux](storage-use-azcopy-linux.md) está integrado en .NET Core Framework que tiene como destino plataformas Linux y ofrece opciones de línea de comandos de estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="e0707-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="e0707-111">Este artículo trata sobre AzCopy en Windows.</span><span class="sxs-lookup"><span data-stu-id="e0707-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="e0707-112">Descarga e instalación de AzCopy</span><span class="sxs-lookup"><span data-stu-id="e0707-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="e0707-113">AzCopy en Windows</span><span class="sxs-lookup"><span data-stu-id="e0707-113">AzCopy on Windows</span></span>
<span data-ttu-id="e0707-114">Descargue la [versión más reciente de AzCopy en Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="e0707-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="e0707-115">Instalación en Windows</span><span class="sxs-lookup"><span data-stu-id="e0707-115">Installation on Windows</span></span>
<span data-ttu-id="e0707-116">Después de instalar AzCopy en Windows con el programa de instalación, abra una ventana de comandos y desplácese hasta el directorio de instalación de AzCopy en el equipo, donde se encuentra el ejecutable `AzCopy.exe`.</span><span class="sxs-lookup"><span data-stu-id="e0707-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="e0707-117">Si lo desea, puede agregar la ubicación de instalación de AzCopy a la ruta de acceso del sistema.</span><span class="sxs-lookup"><span data-stu-id="e0707-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="e0707-118">De forma predeterminada, AzCopy se instala en `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` o `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e0707-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="e0707-119">Escritura del primer comando de AzCopy</span><span class="sxs-lookup"><span data-stu-id="e0707-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="e0707-120">La sintaxis básica del comando AzCopy es:</span><span class="sxs-lookup"><span data-stu-id="e0707-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="e0707-121">Los ejemplos siguientes muestran diversos escenarios para copiar datos a y desde los blobs, archivos y tablas de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e0707-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="e0707-122">Consulte la sección [Parámetros de AzCopy](#azcopy-parameters) para obtener una explicación detallada de los parámetros utilizados en cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e0707-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="e0707-123">Blob: descarga</span><span class="sxs-lookup"><span data-stu-id="e0707-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="e0707-124">Descarga de un solo blob</span><span class="sxs-lookup"><span data-stu-id="e0707-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="e0707-125">Tenga en cuenta que si la carpeta `C:\myfolder` no existe, AzCopy la crea y descarga `abc.txt ` en la nueva carpeta.</span><span class="sxs-lookup"><span data-stu-id="e0707-125">Note that if the folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="e0707-126">Descarga de un solo blob desde la región secundaria</span><span class="sxs-lookup"><span data-stu-id="e0707-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="e0707-127">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="e0707-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="e0707-128">Descarga de todos los blobs</span><span class="sxs-lookup"><span data-stu-id="e0707-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="e0707-129">Supongamos que los siguientes blobs residen en el contenedor especificado:</span><span class="sxs-lookup"><span data-stu-id="e0707-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="e0707-130">Después de la operación de descarga, el directorio `C:\myfolder` incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-130">After the download operation, the directory `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="e0707-131">Si no especifica la opción `/S`, no se descarga ningún blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="e0707-132">Descarga de blobs con el prefijo especificado</span><span class="sxs-lookup"><span data-stu-id="e0707-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="e0707-133">Supongamos que los siguientes blobs residen en el contenedor especificado.</span><span class="sxs-lookup"><span data-stu-id="e0707-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="e0707-134">Se descargan todos los blobs que comiencen con el prefijo `a`:</span><span class="sxs-lookup"><span data-stu-id="e0707-134">All blobs beginning with the prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="e0707-135">Después de la operación de descarga, la carpeta `C:\myfolder` incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-135">After the download operation, the folder `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="e0707-136">El prefijo se aplica al directorio virtual, que forma la primera parte del nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="e0707-137">En el ejemplo mostrado anteriormente, el directorio virtual no coincide con el prefijo especificado, por lo que no se descarga.</span><span class="sxs-lookup"><span data-stu-id="e0707-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="e0707-138">Además, si no se especifica la opción `\S`, AzCopy no descarga ningún blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-138">In addition, if the option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="e0707-139">Establecimiento de la hora de la última modificación de los archivos exportados para que coincida con la de los blobs de origen</span><span class="sxs-lookup"><span data-stu-id="e0707-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="e0707-140">También puede excluir los blobs de la operación de descarga basándose en la hora de su última modificación.</span><span class="sxs-lookup"><span data-stu-id="e0707-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="e0707-141">Por ejemplo, si desea excluir los blobs cuya hora de la última modificación es igual o más reciente que la del archivo de destino, agregue la opción `/XN` :</span><span class="sxs-lookup"><span data-stu-id="e0707-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="e0707-142">O, si desea excluir los blobs cuya hora de la última modificación es igual o anterior a la del archivo de destino, agregue la opción `/XO` :</span><span class="sxs-lookup"><span data-stu-id="e0707-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="e0707-143">Blob: carga</span><span class="sxs-lookup"><span data-stu-id="e0707-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="e0707-144">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="e0707-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="e0707-145">Si el contenedor de destino especificado no existe, AzCopy lo crea y carga el archivo en él.</span><span class="sxs-lookup"><span data-stu-id="e0707-145">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="e0707-146">Carga de un solo archivo en el directorio virtual</span><span class="sxs-lookup"><span data-stu-id="e0707-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="e0707-147">Si el directorio virtual especificado no existe, AzCopy carga el archivo para incluir el directorio virtual en su nombre (*por ejemplo*, `vd/abc.txt` en el ejemplo anterior).</span><span class="sxs-lookup"><span data-stu-id="e0707-147">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="e0707-148">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="e0707-149">Al especificar la opción `/S` se carga el contenido del directorio especificado en Blob Storage de forma recursiva, lo que significa que todas las subcarpetas y sus archivos también se cargan.</span><span class="sxs-lookup"><span data-stu-id="e0707-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="e0707-150">Por ejemplo, supongamos que los siguientes archivos residen en la carpeta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="e0707-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="e0707-151">Después de la operación de carga, el contenedor incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-151">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="e0707-152">Si no especifica la opción `/S`, AzCopy no realiza la carga de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="e0707-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="e0707-153">Después de la operación de carga, el contenedor incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-153">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="e0707-154">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="e0707-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="e0707-155">Supongamos que los siguientes archivos residen en la carpeta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="e0707-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="e0707-156">Después de la operación de carga, el contenedor incluye los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-156">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="e0707-157">Si no especifica la opción `/S`, AzCopy solo carga los blobs que no residan en un directorio virtual:</span><span class="sxs-lookup"><span data-stu-id="e0707-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="e0707-158">Especificación del tipo de contenido MIME de un blob de destino</span><span class="sxs-lookup"><span data-stu-id="e0707-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="e0707-159">De forma predeterminada, AzCopy define el tipo de contenido de un blob de destino como `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="e0707-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="e0707-160">A partir de la versión 3.1.0, puede especificar explícitamente el tipo de contenido a través de la opción `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="e0707-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="e0707-161">Esta sintaxis establece el tipo de contenido para todos los blobs de una operación de carga.</span><span class="sxs-lookup"><span data-stu-id="e0707-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="e0707-162">Si especifica `/SetContentType` sin un valor, AzCopy establece cada blob o tipo de contenido del archivo según su extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="e0707-163">Blob: copia</span><span class="sxs-lookup"><span data-stu-id="e0707-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="e0707-164">Copia de un solo blob dentro de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e0707-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="e0707-165">Cuando copia un blob dentro de una cuenta de almacenamiento, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e0707-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="e0707-166">Copia de un solo blob entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e0707-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="e0707-167">Cuando copia un blob entre cuentas de almacenamiento, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e0707-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="e0707-168">Copia de un solo blob desde la región secundaria a la región primaria</span><span class="sxs-lookup"><span data-stu-id="e0707-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="e0707-169">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="e0707-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="e0707-170">Copia de un solo blob y de sus instantáneas entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e0707-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="e0707-171">Después de la operación de copia, el contenedor de destino incluye el blob y sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-171">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="e0707-172">Suponiendo que el blob del ejemplo anterior tiene dos instantáneas, el contenedor incluye el siguiente blob e instantáneas:</span><span class="sxs-lookup"><span data-stu-id="e0707-172">Assuming the blob in the example above has two snapshots, the container includes the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="e0707-173">Copia sincrónica de blobs entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0707-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="e0707-174">De forma predeterminada, AzCopy copia datos entre dos extremos de almacenamiento asincrónicamente.</span><span class="sxs-lookup"><span data-stu-id="e0707-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="e0707-175">Por lo tanto, la operación de copia se ejecuta en segundo plano con la capacidad de ancho de banda de reserva sin SLA en relación con la velocidad con que se copia un blob y AzCopy comprueba periódicamente el estado de la copia hasta que se complete o se devuelva un error.</span><span class="sxs-lookup"><span data-stu-id="e0707-175">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="e0707-176">La opción `/SyncCopy` garantiza que la operación de copia tiene una velocidad uniforme.</span><span class="sxs-lookup"><span data-stu-id="e0707-176">The `/SyncCopy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="e0707-177">Para hacer la copia sincrónica, AzCopy descarga los blobs que se deben copiar desde el origen especificado a la memoria local y, a continuación, los carga en el destino de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="e0707-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="e0707-178">`/SyncCopy` podría generar un costo de salida adicional en comparación con la copia asincrónica. Es recomendable usar esta opción en la máquina virtual de Azure que se encuentra en la misma región que la cuenta de almacenamiento de origen, para evitar el costo de salida.</span><span class="sxs-lookup"><span data-stu-id="e0707-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="e0707-179">Archivo: descarga</span><span class="sxs-lookup"><span data-stu-id="e0707-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="e0707-180">Descarga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="e0707-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="e0707-181">Si el origen especificado es un recurso compartido de archivos de Azure, entonces tiene que especificar el nombre de archivo exacto (*p. ej.* `abc.txt`) para descargar un solo archivo, o especificar la opción `/S` para descargar todos los archivos en el recurso compartido de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="e0707-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="e0707-182">Si intenta especificar tanto un patrón de archivos como la opción `/S` en conjunto, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="e0707-182">Attempting to specify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="e0707-183">Descarga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="e0707-184">Tenga en cuenta que no se descarga ninguna carpeta vacía.</span><span class="sxs-lookup"><span data-stu-id="e0707-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="e0707-185">Archivo: carga</span><span class="sxs-lookup"><span data-stu-id="e0707-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="e0707-186">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="e0707-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="e0707-187">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="e0707-188">Tenga en cuenta que no se carga ninguna carpeta vacía.</span><span class="sxs-lookup"><span data-stu-id="e0707-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="e0707-189">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="e0707-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="e0707-190">Archivo: copia</span><span class="sxs-lookup"><span data-stu-id="e0707-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="e0707-191">Copia a través de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e0707-192">Al copiar un archivo en distintos recursos compartidos de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0707-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="e0707-193">Copia desde el recurso compartido de archivos al blob</span><span class="sxs-lookup"><span data-stu-id="e0707-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e0707-194">Al copiar un archivo desde un recurso compartido de archivos en un blob, se realiza una [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0707-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="e0707-195">Copia desde el blob al recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e0707-196">Al copiar un archivo desde un blob en un recurso compartido de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0707-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="e0707-197">Copia sincrónica de archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-197">Synchronously copy files</span></span>
<span data-ttu-id="e0707-198">Puede especificar la opción `/SyncCopy` para copiar datos de forma sincrónica del Almacenamiento de archivos al Almacenamiento de archivos, del Almacenamiento de archivos al Almacenamiento de blobs y del Almacenamiento de blobs al Almacenamiento de archivos; para ello, AzCopy descarga los datos de origen en la memoria local y los carga de nuevo al destino.</span><span class="sxs-lookup"><span data-stu-id="e0707-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="e0707-199">Se aplica el costo de salida estándar.</span><span class="sxs-lookup"><span data-stu-id="e0707-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="e0707-200">Al realizar la copia del Almacenamiento de archivos al Almacenamiento de blobs, el tipo de blob predeterminado es el blob en bloques, por lo tanto, el usuario puede especificar la opción `/BlobType:page` para cambiar el tipo de blob de destino.</span><span class="sxs-lookup"><span data-stu-id="e0707-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="e0707-201">Tenga en cuenta que `/SyncCopy` podría generar un coste de salida adicional en comparación con la copia asincrónica. Es recomendable usar esta opción en la máquina virtual de Azure que se encuentra en la misma región que la cuenta de almacenamiento de origen, para evitar el coste de salida.</span><span class="sxs-lookup"><span data-stu-id="e0707-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="e0707-202">Tabla: exportación</span><span class="sxs-lookup"><span data-stu-id="e0707-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="e0707-203">Tabla de exportación</span><span class="sxs-lookup"><span data-stu-id="e0707-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="e0707-204">AzCopy escribe un archivo de manifiesto en la carpeta de destino especificada.</span><span class="sxs-lookup"><span data-stu-id="e0707-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="e0707-205">El archivo de manifiesto se utiliza por parte del proceso de importación para ubicar los archivos de datos necesarios y realizar la validación de datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="e0707-206">El archivo de manifiesto utiliza la siguiente convención de nombres de forma predeterminada:</span><span class="sxs-lookup"><span data-stu-id="e0707-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="e0707-207">El usuario también puede especificar la opción `/Manifest:<manifest file name>` para establecer el nombre del archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="e0707-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="e0707-208">Exportación dividida en varios archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="e0707-209">AzCopy usa un *índice de volumen* en los nombres de los archivos de datos divididos para distinguir los diversos archivos.</span><span class="sxs-lookup"><span data-stu-id="e0707-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="e0707-210">El índice de volumen consta de dos partes, un *índice de rango de clave de partición* y un *índice de archivo dividido*.</span><span class="sxs-lookup"><span data-stu-id="e0707-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="e0707-211">Ambos índices se basan en 0.</span><span class="sxs-lookup"><span data-stu-id="e0707-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="e0707-212">El rango de clave de partición es 0, si un usuario no especifica la opción `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="e0707-212">The partition key range index is 0 if the user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="e0707-213">Por ejemplo, imagine que AzCopy genera dos archivos de datos después de que el usuario especifique la opción `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="e0707-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="e0707-214">Los nombres de archivos de datos resultantes serían:</span><span class="sxs-lookup"><span data-stu-id="e0707-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="e0707-215">Tenga en cuenta que el mínimo valor posible para la opción `/SplitSize` es 32 MB.</span><span class="sxs-lookup"><span data-stu-id="e0707-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="e0707-216">Si el destino especificado es Blob Storage, AzCopy divide el archivo de datos una vez que su tamaño alcanza el límite especificado (200 GB), independientemente de si el usuario ha especificado o no la opción `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="e0707-216">If the specified destination is Blob storage, AzCopy splits the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="e0707-217">Exportación de tablas en formato de archivo de datos JSON o CSV</span><span class="sxs-lookup"><span data-stu-id="e0707-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="e0707-218">De forma predeterminada, AzCopy exporta tablas a archivos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="e0707-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="e0707-219">Puede especificar la opción `/PayloadFormat:JSON|CSV` para exportar las tablas como JSON o CSV.</span><span class="sxs-lookup"><span data-stu-id="e0707-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="e0707-220">Al especificar el formato de carga CSV, AzCopy también genera un archivo de esquema con la extensión `.schema.csv` para cada archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-220">When specifying the CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="e0707-221">Exportación de entidades de tabla simultáneamente</span><span class="sxs-lookup"><span data-stu-id="e0707-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="e0707-222">AzCopy inicia operaciones simultáneas para exportar entidades cuando el usuario especifica la opción `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="e0707-222">AzCopy starts concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="e0707-223">Cada operación exporta un rango de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="e0707-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="e0707-224">Tenga en cuenta que el número de operaciones simultáneas está controlado también por la opción `/NC`.</span><span class="sxs-lookup"><span data-stu-id="e0707-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="e0707-225">AzCopy usa el número de procesadores de núcleo como valor predeterminado de `/NC` al copiar entidades de tabla, incluso si no se especificó `/NC`.</span><span class="sxs-lookup"><span data-stu-id="e0707-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="e0707-226">Si el usuario especifica la opción `/PKRS`, AzCopy usa el valor más pequeño de los dos (rangos de claves de partición u operaciones simultáneas especificadas de manera implícita o explícita) para determinar el número de operaciones simultáneas que van a dar inicio.</span><span class="sxs-lookup"><span data-stu-id="e0707-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="e0707-227">Para obtener más detalles, escriba `AzCopy /?:NC` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e0707-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="e0707-228">Exportación de tablas a blobs</span><span class="sxs-lookup"><span data-stu-id="e0707-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="e0707-229">AzCopy genera un archivo de datos JSON en el contenedor de blobs local con la siguiente convención de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="e0707-229">AzCopy generates a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="e0707-230">El archivo de datos JSON generado sigue el formato de carga para metadatos mínimos.</span><span class="sxs-lookup"><span data-stu-id="e0707-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="e0707-231">Para obtener más información sobre el formato de carga, consulte [Formato de carga para las operaciones del servicio Tabla](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0707-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="e0707-232">Tenga en cuenta que, al exportar tablas a blobs, AzCopy descarga las entidades de tabla en archivos de datos temporales locales y, a continuación, carga tales entidades en el blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-232">Note that when exporting tables to blobs, AzCopy downloads the Table entities to local temporary data files and then uploads those entities to the blob.</span></span> <span data-ttu-id="e0707-233">Estos archivos de datos temporales se colocan en la carpeta de archivos de diario con la ruta de acceso predeterminada "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>". Puede especificar la opción /Z:[carpeta-de-archivos-de-diario] para cambiar la ubicación de esta carpeta y, así, modificar también la de los archivos de datos temporales.</span><span class="sxs-lookup"><span data-stu-id="e0707-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="e0707-234">El tamaño de los archivos de datos temporales se decide según el de las entidades de tabla y el especificado con la opción /SplitSize, aunque el archivo de datos temporales en el disco local se elimina inmediatamente después de cargarse en el blob. Asegúrese de que tiene suficiente espacio en el disco local para almacenar estos archivos de datos temporales antes de que se eliminen.</span><span class="sxs-lookup"><span data-stu-id="e0707-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk is deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="e0707-235">Tabla: importación</span><span class="sxs-lookup"><span data-stu-id="e0707-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="e0707-236">Importación de la tabla</span><span class="sxs-lookup"><span data-stu-id="e0707-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="e0707-237">La opción `/EntityOperation` indica cómo insertar entidades en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="e0707-238">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="e0707-238">Possible values are:</span></span>

* <span data-ttu-id="e0707-239">`InsertOrSkip`omite una entidad existente o inserta una nueva entidad si esta no existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e0707-240">`InsertOrMerge`combina una entidad existente o inserta una nueva entidad si esta no existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e0707-241">`InsertOrReplace`reemplaza una entidad existente o inserta una nueva entidad si esta no existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="e0707-242">Tenga en cuenta que no puede especificar la opción `/PKRS` en el escenario de importación.</span><span class="sxs-lookup"><span data-stu-id="e0707-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="e0707-243">A diferencia del escenario de exportación, en el que debe especificar la opción `/PKRS` para iniciar las operaciones simultáneas, AzCopy inicia de manera predeterminada operaciones simultáneas cuando se importa una tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="e0707-244">El número predeterminado de operaciones simultáneas que se inician equivale al número de procesadores de núcleo; sin embargo, puede especificar un número diferente para la simultaneidad con la opción `/NC`.</span><span class="sxs-lookup"><span data-stu-id="e0707-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="e0707-245">Para obtener más detalles, escriba `AzCopy /?:NC` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e0707-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="e0707-246">Tenga en cuenta que AzCopy solo admite la importación de archivos con el formato JSON, no CSV.</span><span class="sxs-lookup"><span data-stu-id="e0707-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="e0707-247">AzCopy no permite importar tablas de archivos de manifiesto y archivos JSON creados por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e0707-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="e0707-248">Estos archivos deben proceder de una exportación de tablas de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e0707-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="e0707-249">Para evitar errores, no modifique el archivo JSON exportado ni el archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="e0707-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="e0707-250">Importación de entidades a tabla mediante blobs</span><span class="sxs-lookup"><span data-stu-id="e0707-250">Import entities to table using blobs</span></span>
<span data-ttu-id="e0707-251">Suponga que un contenedor de blobs contiene lo siguiente: un archivo JSON que representa una tabla de Azure y el archivo de manifiesto que lo acompaña.</span><span class="sxs-lookup"><span data-stu-id="e0707-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="e0707-252">Puede ejecutar el comando siguiente para importar las entidades en una tabla mediante el archivo de manifiesto de ese contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="e0707-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="e0707-253">Otras características de AzCopy</span><span class="sxs-lookup"><span data-stu-id="e0707-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="e0707-254">Solo copie los datos que no existan en el destino</span><span class="sxs-lookup"><span data-stu-id="e0707-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="e0707-255">Los parámetros `/XO` y `/XN` le permiten excluir los recursos de origen anteriores o posteriores a la copia, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e0707-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="e0707-256">Si solo desea copiar los recursos de origen que no existen en el destino, puede especificar ambos parámetros en el comando de AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e0707-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="e0707-257">Tenga en cuenta que esto no se admite cuando el origen o el destino es una tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="e0707-258">Uso de un archivo de respuesta para especificar parámetros de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="e0707-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="e0707-259">Puede incluir cualquier parámetro de la línea de comandos de AzCopy en un archivo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e0707-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="e0707-260">AzCopy procesa los parámetros del archivo como si hubieran sido especificados en la línea de comandos, realizando una sustitución directa con el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="e0707-261">Imaginemos un archivo de respuesta llamado `copyoperation.txt`, que contiene las siguientes líneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="e0707-262">Cada parámetro de AzCopy se puede especificar en una sola línea</span><span class="sxs-lookup"><span data-stu-id="e0707-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="e0707-263">o bien, en líneas independientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="e0707-264">AzCopy genera un error si divide el parámetro en dos líneas, tal como se muestra aquí para el parámetro `/sourcekey`:</span><span class="sxs-lookup"><span data-stu-id="e0707-264">AzCopy fails if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="e0707-265">Uso de varios archivos de respuesta para especificar parámetros de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="e0707-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="e0707-266">Imaginemos un archivo de respuesta llamado `source.txt` que especifica un contenedor de origen:</span><span class="sxs-lookup"><span data-stu-id="e0707-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="e0707-267">Y un archivo de respuesta llamado `dest.txt` que especifica una carpeta de destino en el sistema de archivos:</span><span class="sxs-lookup"><span data-stu-id="e0707-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="e0707-268">Y un archivo de respuesta llamado `options.txt` que especifica opciones para AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e0707-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="e0707-269">Para llamar a AzCopy con estos archivos de respuesta, todos los cuales residen en un directorio `C:\responsefiles`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="e0707-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="e0707-270">AzCopy procesa este comando como si se incluyeran todos los parámetros individuales en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="e0707-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="e0707-271">Especificación de una firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="e0707-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="e0707-272">También puede especificar una SAS en el identificador URI del contenedor:</span><span class="sxs-lookup"><span data-stu-id="e0707-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="e0707-273">Carpeta de archivo de diario</span><span class="sxs-lookup"><span data-stu-id="e0707-273">Journal file folder</span></span>
<span data-ttu-id="e0707-274">Cada vez que emite un comando a AzCopy, comprueba si existe un archivo de diario en la carpeta predeterminada o si existe una carpeta que especificó a través de esta opción.</span><span class="sxs-lookup"><span data-stu-id="e0707-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="e0707-275">Si el archivo de diario no existe en ningún lugar, AzCopy trata la operación como una nueva y genera un nuevo archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="e0707-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="e0707-276">Si el archivo de diario existe, AzCopy comprueba si la línea de comandos escrita coincide con la línea de comandos de dicho archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-276">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="e0707-277">Si las dos líneas de comandos coinciden, AzCopy reanudará la operación incompleta.</span><span class="sxs-lookup"><span data-stu-id="e0707-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="e0707-278">Si no coinciden, se le pregunta si desea sobrescribir el archivo de diario, iniciar una nueva operación o cancelar la operación actual.</span><span class="sxs-lookup"><span data-stu-id="e0707-278">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="e0707-279">Si desea usar la ubicación predeterminada para el archivo de diario:</span><span class="sxs-lookup"><span data-stu-id="e0707-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="e0707-280">Si omite la opción `/Z` o especifica la opción `/Z` sin la ruta de acceso a la carpeta, tal y como se muestra anteriormente, AzCopy crea el archivo de diario en la ubicación predeterminada, que es `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e0707-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="e0707-281">Si el archivo de diario ya existe, AzCopy reanuda la operación basándose en dicho archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="e0707-282">Si desea especificar una ubicación personalizada para el archivo de diario:</span><span class="sxs-lookup"><span data-stu-id="e0707-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="e0707-283">Este ejemplo crea el archivo de diario si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="e0707-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="e0707-284">Si no existe, AzCopy reanuda la operación basándose en el archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="e0707-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="e0707-285">Si desea reanudar una operación de AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e0707-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="e0707-286">Este ejemplo reanuda la última operación que es posible que no terminara.</span><span class="sxs-lookup"><span data-stu-id="e0707-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="e0707-287">Generación de un archivo de registro</span><span class="sxs-lookup"><span data-stu-id="e0707-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="e0707-288">Si especifica la opción `/V` sin proporcionar una ruta de acceso de archivo al registro detallado, AzCopy crea el archivo de registro en la ubicación predeterminada, que es `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e0707-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="e0707-289">De lo contrario, puede crear un archivo de registro en una ubicación personalizada:</span><span class="sxs-lookup"><span data-stu-id="e0707-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="e0707-290">Tenga en cuenta que si especifica una ruta de acceso relativa después de la opción `/V`, como por ejemplo `/V:test/azcopy1.log`, el registro detallado se creará en el directorio de trabajo actual dentro de una subcarpeta llamada `test`.</span><span class="sxs-lookup"><span data-stu-id="e0707-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="e0707-291">Especificación del número de operaciones simultáneas para iniciar</span><span class="sxs-lookup"><span data-stu-id="e0707-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="e0707-292">La opción `/NC` especifica el número de operaciones de copia simultáneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="e0707-293">De manera predeterminada, AzCopy inicia un número determinado de operaciones simultáneas para aumentar el rendimiento de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="e0707-294">Para las operaciones de tablas, el número de operaciones simultáneas es igual al número de procesadores que se tiene.</span><span class="sxs-lookup"><span data-stu-id="e0707-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="e0707-295">Para las operaciones de blobs y archivos, el número de operaciones simultáneas es igual a ocho veces el número de procesadores que se tiene.</span><span class="sxs-lookup"><span data-stu-id="e0707-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="e0707-296">Si ejecuta AzCopy en una red con un ancho de banda bajo, puede especificar un número bajo para /NC con el fin de evitar errores provocados por la competencia de recursos.</span><span class="sxs-lookup"><span data-stu-id="e0707-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="e0707-297">Ejecución de AzCopy en el emulador de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e0707-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="e0707-298">Puede ejecutar AzCopy en el [emulador de Almacenamiento de Azure](storage-use-emulator.md) para blobs:</span><span class="sxs-lookup"><span data-stu-id="e0707-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="e0707-299">y tablas:</span><span class="sxs-lookup"><span data-stu-id="e0707-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="e0707-300">Parámetros de AzCopy</span><span class="sxs-lookup"><span data-stu-id="e0707-300">AzCopy Parameters</span></span>
<span data-ttu-id="e0707-301">A continuación se describen los parámetros para AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e0707-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="e0707-302">También puede escribir uno de los siguientes comandos desde la línea de comandos para obtener ayuda en el uso de AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e0707-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="e0707-303">Para obtener ayuda detallada sobre la línea de comandos de AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="e0707-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="e0707-304">Para obtener ayuda detallada con algún parámetro de AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="e0707-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="e0707-305">Para obtener ejemplos de línea de comandos: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="e0707-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="e0707-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="e0707-306">/Source:"source"</span></span>
<span data-ttu-id="e0707-307">Especifica los datos de origen desde los que copiar.</span><span class="sxs-lookup"><span data-stu-id="e0707-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="e0707-308">El origen puede ser un directorio del sistema de archivos, un contenedor de blobs, un directorio virtual de blobs, un recurso compartido de archivos de almacenamiento, un directorio de archivos de almacenamiento o una tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0707-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="e0707-309">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="e0707-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="e0707-310">/Dest:"destination"</span></span>
<span data-ttu-id="e0707-311">Especifica el destino de la copia.</span><span class="sxs-lookup"><span data-stu-id="e0707-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="e0707-312">El destino puede ser un directorio del sistema de archivos, un contenedor de blobs, un directorio virtual de blobs, un recurso compartido de archivos de almacenamiento, un directorio de archivos de almacenamiento o una tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0707-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="e0707-313">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="e0707-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="e0707-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="e0707-315">Especifica un patrón de archivos que indica qué archivos se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="e0707-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="e0707-316">El comportamiento del parámetro /Pattern viene determinado por la ubicación de los datos de origen y la presencia de la opción del modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="e0707-317">El modo recursivo viene especificado por la opción /S.</span><span class="sxs-lookup"><span data-stu-id="e0707-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="e0707-318">Si el origen especificado es un directorio del sistema de archivos, se aplican los caracteres comodín estándar y el patrón de archivos proporcionado coincidirá con los archivos del directorio.</span><span class="sxs-lookup"><span data-stu-id="e0707-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="e0707-319">Si se especifica la opción /S, AzCopy también hará coincidir el patrón especificado con todos los archivos de cualquier subcarpeta que se encuentre bajo el directorio.</span><span class="sxs-lookup"><span data-stu-id="e0707-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="e0707-320">Si el origen especificado es un contenedor de blobs o un directorio virtual, entonces los caracteres comodín no se aplican.</span><span class="sxs-lookup"><span data-stu-id="e0707-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="e0707-321">Si se especifica la opción /S, AzCopy interpreta el patrón de archivos especificado como un prefijo de blobs.</span><span class="sxs-lookup"><span data-stu-id="e0707-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="e0707-322">Si la opción /S no se especifica, AzCopy hará coincidir el patrón de archivos con los nombres de blob exactos.</span><span class="sxs-lookup"><span data-stu-id="e0707-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="e0707-323">Si el origen especificado es un recurso compartido de archivos de Azure, debe especificar el nombre de archivo exacto (p. ej. abc.txt) para copiar un solo archivo, o especificar la opción /S para copiar todos los archivos en el recurso compartido de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="e0707-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="e0707-324">Si intenta especificar tanto un patrón de archivos como la opción /S en conjunto, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="e0707-324">Attempting to specify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="e0707-325">AzCopy utiliza la coincidencia entre mayúsculas y minúsculas cuando /Soure es un contenedor de blob o el directorio virtual de blob y utiliza la falta de coincidencia entre mayúsculas y minúsculas en todos los demás casos.</span><span class="sxs-lookup"><span data-stu-id="e0707-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="e0707-326">El patrón de archivo predeterminado que se usa cuando no se especifica ninguno es *.*</span><span class="sxs-lookup"><span data-stu-id="e0707-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="e0707-327">para una ubicación del sistema de archivos, o un prefijo vacío para una ubicación de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0707-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="e0707-328">No se admite la especificación de varios patrones de archivos.</span><span class="sxs-lookup"><span data-stu-id="e0707-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="e0707-329">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="e0707-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="e0707-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="e0707-331">Especifica la clave de cuenta de almacenamiento para el recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="e0707-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="e0707-332">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="e0707-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="e0707-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="e0707-334">Especifica una firma de acceso compartido (SAS) para los permisos de LECTURA y ESCRITURA del destino (si corresponde).</span><span class="sxs-lookup"><span data-stu-id="e0707-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="e0707-335">Encierre la SAS con comillas dobles, ya que puede contener caracteres de línea de comandos especiales.</span><span class="sxs-lookup"><span data-stu-id="e0707-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="e0707-336">Si el recurso de destino es un contenedor de blobs, un recurso compartido de archivos o tabla, puede especificar esta opción seguida por el token SAS, o bien puede especificar la SAS como parte del URI del contenedor de blob, recurso compartido de archivos o tabla, sin esta opción.</span><span class="sxs-lookup"><span data-stu-id="e0707-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="e0707-337">Si el origen y el destino son blobs en ambos casos, el blob de destino debe residir dentro de la misma cuenta de almacenamiento que el blob de origen.</span><span class="sxs-lookup"><span data-stu-id="e0707-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="e0707-338">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="e0707-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="e0707-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="e0707-340">Especifica la clave de cuenta de almacenamiento para el recurso de origen.</span><span class="sxs-lookup"><span data-stu-id="e0707-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="e0707-341">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="e0707-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="e0707-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="e0707-343">Especifica una firma de acceso compartido (SAS) para los permisos de LECTURA y LISTA del origen (si corresponde).</span><span class="sxs-lookup"><span data-stu-id="e0707-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="e0707-344">Encierre la SAS con comillas dobles, ya que puede contener caracteres de línea de comandos especiales.</span><span class="sxs-lookup"><span data-stu-id="e0707-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="e0707-345">Si el recurso de origen es un contenedor de blobs y no se proporciona una clave ni una SAS, el contenedor de blobs se lee con acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="e0707-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container is read via anonymous access.</span></span>

<span data-ttu-id="e0707-346">Si el origen es un recurso compartido de archivos o una tabla, es necesario proporcionar una clave o una SAS.</span><span class="sxs-lookup"><span data-stu-id="e0707-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="e0707-347">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="e0707-348">/S</span><span class="sxs-lookup"><span data-stu-id="e0707-348">/S</span></span>
<span data-ttu-id="e0707-349">Especifica el modo recursivo para operaciones de copia.</span><span class="sxs-lookup"><span data-stu-id="e0707-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="e0707-350">En el modo recursivo, AzCopy copia todos los blobs o archivos que coinciden con el patrón de archivos especificado, incluidos los que se encuentran en las subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="e0707-350">In recursive mode, AzCopy copies all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="e0707-351">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="e0707-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="e0707-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="e0707-353">Especifica si el blob de destino es un blob en bloques, un blob en páginas o un blob de anexo.</span><span class="sxs-lookup"><span data-stu-id="e0707-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="e0707-354">Esta opción solo es aplicable cuando se carga un blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="e0707-355">De lo contrario, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="e0707-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="e0707-356">Si el destino es un blob y esta opción no se especifica, AzCopy, de forma predeterminada, creará un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="e0707-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="e0707-357">**Aplicable a:** blobs</span><span class="sxs-lookup"><span data-stu-id="e0707-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="e0707-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="e0707-358">/CheckMD5</span></span>
<span data-ttu-id="e0707-359">Calcula un hash MD5 para datos descargados y comprueba que el hash MD5 almacenado en la propiedad Content-MD5 del blob o archivo coincide con el hash calculado.</span><span class="sxs-lookup"><span data-stu-id="e0707-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="e0707-360">La comprobación MD5 se desactiva de forma predeterminada, por lo que debe especificar esta opción para realizar dicha comprobación cuando se descargan datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="e0707-361">Tenga en cuenta que Almacenamiento de Azure no garantiza que el hash MD5 almacenado para el blob o archivo esté actualizado.</span><span class="sxs-lookup"><span data-stu-id="e0707-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="e0707-362">El cliente será el responsable de actualizar el MD5 siempre que el blob o el archivo se modifique.</span><span class="sxs-lookup"><span data-stu-id="e0707-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="e0707-363">AzCopy siempre establece la propiedad Content-MD5 para un blob o archivo de Azure después de cargarlo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="e0707-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="e0707-364">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="e0707-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="e0707-365">/Snapshot</span></span>
<span data-ttu-id="e0707-366">Indica si se desean transferir instantáneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="e0707-367">Esta opción solo es válida cuando el origen es un blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="e0707-368">El nombre de las instantáneas del blob transferidas se cambia según este formato: nombre-blog (hora de la instantánea).extensión.</span><span class="sxs-lookup"><span data-stu-id="e0707-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="e0707-369">De forma predeterminada, las instantáneas no se copian.</span><span class="sxs-lookup"><span data-stu-id="e0707-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="e0707-370">**Aplicable a:** blobs</span><span class="sxs-lookup"><span data-stu-id="e0707-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="e0707-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="e0707-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="e0707-372">Envía mensajes con el estado detallado a un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="e0707-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="e0707-373">De forma predeterminada, el nombre del archivo de registro detallado es AzCopyVerbose.log en `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="e0707-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="e0707-374">Si especifica una ubicación existente para el archivo en esta opción, el registro detallado se anexa a dicho archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-374">If you specify an existing file location for this option, the verbose log is appended to that file.</span></span>  

<span data-ttu-id="e0707-375">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="e0707-376">/Z:[carpeta de archivos de diario]</span><span class="sxs-lookup"><span data-stu-id="e0707-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="e0707-377">Especifica una carpeta de archivos de diario para reanudar una operación.</span><span class="sxs-lookup"><span data-stu-id="e0707-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="e0707-378">AzCopy siempre admite la reanudación si una operación se ha interrumpido.</span><span class="sxs-lookup"><span data-stu-id="e0707-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="e0707-379">Si esta opción no se especifica o si se especifica sin una ruta de acceso a la carpeta, AzCopy crea el archivo de diario en la ubicación predeterminada, que es %LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e0707-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="e0707-380">Cada vez que emite un comando a AzCopy, comprueba si existe un archivo de diario en la carpeta predeterminada o si existe una carpeta que especificó a través de esta opción.</span><span class="sxs-lookup"><span data-stu-id="e0707-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="e0707-381">Si el archivo de diario no existe en ningún lugar, AzCopy trata la operación como una nueva y genera un nuevo archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="e0707-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="e0707-382">Si el archivo de diario existe, AzCopy comprueba si la línea de comandos escrita coincide con la línea de comandos de dicho archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-382">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="e0707-383">Si las dos líneas de comandos coinciden, AzCopy reanudará la operación incompleta.</span><span class="sxs-lookup"><span data-stu-id="e0707-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="e0707-384">Si no coinciden, se le pregunta si desea sobrescribir el archivo de diario, iniciar una nueva operación o cancelar la operación actual.</span><span class="sxs-lookup"><span data-stu-id="e0707-384">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="e0707-385">El archivo de diario se elimina cuando la operación se completa correctamente.</span><span class="sxs-lookup"><span data-stu-id="e0707-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="e0707-386">Tenga en cuenta que la reanudación de una operación a partir de un archivo de diario creado por una versión anterior de AzCopy no se admite.</span><span class="sxs-lookup"><span data-stu-id="e0707-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="e0707-387">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="e0707-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="e0707-388">/@:"parameter-file"</span></span>
<span data-ttu-id="e0707-389">Especifica un archivo que contiene parámetros.</span><span class="sxs-lookup"><span data-stu-id="e0707-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="e0707-390">AzCopy procesa los parámetros del archivo como si hubieran sido especificados en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e0707-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="e0707-391">En un archivo de respuesta, puede especificar varios parámetros en una sola línea o especificar cada parámetro en su propia línea.</span><span class="sxs-lookup"><span data-stu-id="e0707-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="e0707-392">Tenga en cuenta que un parámetro individual no puede ocupar varias líneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="e0707-393">Los archivos de respuesta pueden incluir líneas de comentario que comiencen con el símbolo #.</span><span class="sxs-lookup"><span data-stu-id="e0707-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="e0707-394">Puede especificar varios archivos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e0707-394">You can specify multiple response files.</span></span> <span data-ttu-id="e0707-395">Sin embargo, tenga en cuenta que AzCopy no admite archivos de respuesta anidados.</span><span class="sxs-lookup"><span data-stu-id="e0707-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="e0707-396">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="e0707-397">/Y</span><span class="sxs-lookup"><span data-stu-id="e0707-397">/Y</span></span>
<span data-ttu-id="e0707-398">Suprime todos los mensajes de confirmación de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e0707-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="e0707-399">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="e0707-400">/L</span><span class="sxs-lookup"><span data-stu-id="e0707-400">/L</span></span>
<span data-ttu-id="e0707-401">Especifica solamente una operación de descripción; no se copian datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="e0707-402">AzCopy interpreta el uso de esta opción como una simulación para ejecutar la línea de comandos sin esta opción /L y cuenta el número de objetos que se va a copiar; puede especificar la opción /V al mismo tiempo para comprobar qué objetos se copian en el registro detallado.</span><span class="sxs-lookup"><span data-stu-id="e0707-402">AzCopy interprets the using of this option as a simulation for running the command line without this option /L and counts how many objects are copied, you can specify option /V at the same time to check which objects are copied in the verbose log.</span></span>

<span data-ttu-id="e0707-403">El comportamiento de esta opción también está determinado por la ubicación de los datos de origen y la presencia de la opción /S del modo recursivo y la opción /Pattern del patrón de archivos.</span><span class="sxs-lookup"><span data-stu-id="e0707-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="e0707-404">AzCopy requiere el permiso LISTA y LECTURA de esta ubicación de origen cuando se usa esta opción.</span><span class="sxs-lookup"><span data-stu-id="e0707-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="e0707-405">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="e0707-406">/MT</span><span class="sxs-lookup"><span data-stu-id="e0707-406">/MT</span></span>
<span data-ttu-id="e0707-407">Establece la hora de la última modificación del archivo descargado para que coincida con la del blob o archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="e0707-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="e0707-408">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="e0707-409">/XN</span><span class="sxs-lookup"><span data-stu-id="e0707-409">/XN</span></span>
<span data-ttu-id="e0707-410">Excluye un recurso origen más nuevo.</span><span class="sxs-lookup"><span data-stu-id="e0707-410">Excludes a newer source resource.</span></span> <span data-ttu-id="e0707-411">El recurso no se copia si la hora de la última modificación del origen es la misma o más reciente que el destino.</span><span class="sxs-lookup"><span data-stu-id="e0707-411">The resource is not copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="e0707-412">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="e0707-413">/XO</span><span class="sxs-lookup"><span data-stu-id="e0707-413">/XO</span></span>
<span data-ttu-id="e0707-414">Excluye un recurso de origen más antiguo.</span><span class="sxs-lookup"><span data-stu-id="e0707-414">Excludes an older source resource.</span></span> <span data-ttu-id="e0707-415">El recurso no se copia si la hora de la última modificación del origen es la misma o anterior que el destino.</span><span class="sxs-lookup"><span data-stu-id="e0707-415">The resource is not copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="e0707-416">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="e0707-417">/A</span><span class="sxs-lookup"><span data-stu-id="e0707-417">/A</span></span>
<span data-ttu-id="e0707-418">Carga solamente archivos que tienen el atributo de archivado establecido.</span><span class="sxs-lookup"><span data-stu-id="e0707-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="e0707-419">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="e0707-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="e0707-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="e0707-421">Carga solamente archivos que tienen cualquiera de los atributos especificados establecido.</span><span class="sxs-lookup"><span data-stu-id="e0707-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="e0707-422">Los atributos disponibles son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-422">Available attributes include:</span></span>

* <span data-ttu-id="e0707-423">R = Archivos de solo lectura</span><span class="sxs-lookup"><span data-stu-id="e0707-423">R = Read-only files</span></span>
* <span data-ttu-id="e0707-424">A = Archivos listos para archivarse</span><span class="sxs-lookup"><span data-stu-id="e0707-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="e0707-425">S = Archivos del sistema</span><span class="sxs-lookup"><span data-stu-id="e0707-425">S = System files</span></span>
* <span data-ttu-id="e0707-426">H = Archivos ocultos</span><span class="sxs-lookup"><span data-stu-id="e0707-426">H = Hidden files</span></span>
* <span data-ttu-id="e0707-427">C = Archivos comprimidos</span><span class="sxs-lookup"><span data-stu-id="e0707-427">C = Compressed files</span></span>
* <span data-ttu-id="e0707-428">N = Archivos normales</span><span class="sxs-lookup"><span data-stu-id="e0707-428">N = Normal files</span></span>
* <span data-ttu-id="e0707-429">E = Archivos cifrados</span><span class="sxs-lookup"><span data-stu-id="e0707-429">E = Encrypted files</span></span>
* <span data-ttu-id="e0707-430">T = Archivos temporales</span><span class="sxs-lookup"><span data-stu-id="e0707-430">T = Temporary files</span></span>
* <span data-ttu-id="e0707-431">O = Archivos fuera de línea</span><span class="sxs-lookup"><span data-stu-id="e0707-431">O = Offline files</span></span>
* <span data-ttu-id="e0707-432">I = Archivos no indexados</span><span class="sxs-lookup"><span data-stu-id="e0707-432">I = Non-indexed files</span></span>

<span data-ttu-id="e0707-433">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="e0707-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="e0707-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="e0707-435">Excluye archivos que tienen cualquiera de los atributos especificados establecido.</span><span class="sxs-lookup"><span data-stu-id="e0707-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="e0707-436">Los atributos disponibles son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-436">Available attributes include:</span></span>

* <span data-ttu-id="e0707-437">R = Archivos de solo lectura</span><span class="sxs-lookup"><span data-stu-id="e0707-437">R = Read-only files</span></span>
* <span data-ttu-id="e0707-438">A = Archivos listos para archivarse</span><span class="sxs-lookup"><span data-stu-id="e0707-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="e0707-439">S = Archivos del sistema</span><span class="sxs-lookup"><span data-stu-id="e0707-439">S = System files</span></span>
* <span data-ttu-id="e0707-440">H = Archivos ocultos</span><span class="sxs-lookup"><span data-stu-id="e0707-440">H = Hidden files</span></span>
* <span data-ttu-id="e0707-441">C = Archivos comprimidos</span><span class="sxs-lookup"><span data-stu-id="e0707-441">C = Compressed files</span></span>
* <span data-ttu-id="e0707-442">N = Archivos normales</span><span class="sxs-lookup"><span data-stu-id="e0707-442">N = Normal files</span></span>
* <span data-ttu-id="e0707-443">E = Archivos cifrados</span><span class="sxs-lookup"><span data-stu-id="e0707-443">E = Encrypted files</span></span>
* <span data-ttu-id="e0707-444">T = Archivos temporales</span><span class="sxs-lookup"><span data-stu-id="e0707-444">T = Temporary files</span></span>
* <span data-ttu-id="e0707-445">O = Archivos fuera de línea</span><span class="sxs-lookup"><span data-stu-id="e0707-445">O = Offline files</span></span>
* <span data-ttu-id="e0707-446">I = Archivos no indexados</span><span class="sxs-lookup"><span data-stu-id="e0707-446">I = Non-indexed files</span></span>

<span data-ttu-id="e0707-447">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="e0707-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="e0707-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="e0707-449">Indica el carácter delimitador usado para delimitar directorios virtuales en un nombre de blob.</span><span class="sxs-lookup"><span data-stu-id="e0707-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="e0707-450">De forma predeterminada, AzCopy usa / como carácter delimitador.</span><span class="sxs-lookup"><span data-stu-id="e0707-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="e0707-451">Sin embargo, AzCopy admite el uso de cualquier carácter convencional (como @, # o %) como delimitador.</span><span class="sxs-lookup"><span data-stu-id="e0707-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="e0707-452">Si necesita incluir uno de estos caracteres especiales en la línea de comandos, encierre el nombre de archivo entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="e0707-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="e0707-453">Esta opción solamente se aplica para descarga de blobs.</span><span class="sxs-lookup"><span data-stu-id="e0707-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="e0707-454">**Aplicable a:** blobs</span><span class="sxs-lookup"><span data-stu-id="e0707-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="e0707-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="e0707-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="e0707-456">Especifica el número de operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="e0707-457">AzCopy inicia de manera predeterminada un número determinado de operaciones simultáneas para aumentar el rendimiento de la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="e0707-458">Tenga en cuenta que un número elevado de operaciones simultáneas en un entorno con poco ancho de banda puede saturar la conexión de red e impedir que las operaciones se completen.</span><span class="sxs-lookup"><span data-stu-id="e0707-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="e0707-459">Reduzca el número de operaciones simultáneas basándose en el ancho de banda de red disponible real.</span><span class="sxs-lookup"><span data-stu-id="e0707-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="e0707-460">El límite máximo de operaciones simultáneas es de 512.</span><span class="sxs-lookup"><span data-stu-id="e0707-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="e0707-461">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="e0707-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="e0707-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="e0707-463">Especifica que el recurso `source` es un blob disponible en el entorno de desarrollo local, que se ejecuta en el emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0707-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="e0707-464">**Aplicable a:** blobs, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="e0707-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="e0707-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="e0707-466">Especifica que el recurso `destination` es un blob disponible en el entorno de desarrollo local, que se ejecuta en el emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0707-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="e0707-467">**Aplicable a:** blobs, tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="e0707-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="e0707-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="e0707-469">Divide el rango de claves de partición para habilitar la exportación de datos de tablas en paralelo, lo que aumenta la velocidad de la operación de exportación.</span><span class="sxs-lookup"><span data-stu-id="e0707-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="e0707-470">Si esta opción no se especifica, AzCopy utiliza un solo subproceso para exportar las entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="e0707-471">Por ejemplo, si el usuario especifica /PKRS:"aa#bb", AzCopy inicia tres operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="e0707-472">Cada operación exporta uno de los tres rangos de claves de partición, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="e0707-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="e0707-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="e0707-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="e0707-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="e0707-474">[aa, bb)</span></span>

  <span data-ttu-id="e0707-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="e0707-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="e0707-476">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="e0707-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="e0707-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="e0707-478">Especifica el tamaño dividido del archivo exportado en MB; el valor mínimo permitido es 32.</span><span class="sxs-lookup"><span data-stu-id="e0707-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="e0707-479">Si esta opción no se especifica, AzCopy exporta los datos de la tabla a un único archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-479">If this option is not specified, AzCopy exports table data to a single file.</span></span>

<span data-ttu-id="e0707-480">Si los datos de la tabla se exportan a un blob y el tamaño del archivo exportado alcanza el límite de 200 GB establecido para el tamaño de un blob, AzCopy divide el archivo exportado, incluso si no se ha especificado esta opción.</span><span class="sxs-lookup"><span data-stu-id="e0707-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy splits the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="e0707-481">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="e0707-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="e0707-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="e0707-483">Especifica el comportamiento de la importación de los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="e0707-484">InsertOrSkip: omite una entidad existente o inserta una nueva entidad si esta no existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e0707-485">InsertOrMerge: combina una entidad existente o inserta una nueva entidad si esta no existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e0707-486">InsertOrReplace: reemplaza una entidad existente o inserta una nueva entidad si esta no existe en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="e0707-487">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="e0707-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="e0707-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="e0707-489">Especifica el archivo de manifiesto para la operación de exportación e importación de tablas.</span><span class="sxs-lookup"><span data-stu-id="e0707-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="e0707-490">Esta opción es opcional durante la operación de exportación, AzCopy genera un archivo de manifiesto con nombre predefinido si esta opción no se especifica.</span><span class="sxs-lookup"><span data-stu-id="e0707-490">This option is optional during the export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="e0707-491">Esta opción es necesaria durante la operación de importación para localizar los archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="e0707-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="e0707-492">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="e0707-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="e0707-493">/SyncCopy</span></span>
<span data-ttu-id="e0707-494">Indica si se van a copiar archivos o blobs entre dos extremos de Almacenamiento de Azure de forma sincrónica.</span><span class="sxs-lookup"><span data-stu-id="e0707-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="e0707-495">De forma predeterminada, AzCopy usa la copia asincrónica del servidor.</span><span class="sxs-lookup"><span data-stu-id="e0707-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="e0707-496">Especifique esta opción para hacer una copia sincrónica, que se descarga blobs o archivos en la memoria local y, a continuación, los carga en el Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0707-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="e0707-497">Puede usar esta opción al copiar archivos dentro del almacenamiento de blobs o el almacenamiento de archivos o del almacenamiento de blobs al almacenamiento de archivos o viceversa.</span><span class="sxs-lookup"><span data-stu-id="e0707-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="e0707-498">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="e0707-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="e0707-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="e0707-500">Especifica el tipo de contenido MIME de los blobs o archivos de destino.</span><span class="sxs-lookup"><span data-stu-id="e0707-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="e0707-501">AzCopy establece el tipo de contenido de un blob o archivo en application/octet-stream de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e0707-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="e0707-502">Puede establecer el tipo de contenido para todos los blobs o archivos especificando explícitamente un valor para esta opción.</span><span class="sxs-lookup"><span data-stu-id="e0707-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="e0707-503">Si especifica sin un valor, AzCopy establece cada tipo de contenido de blob o archivo según su extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="e0707-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="e0707-504">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="e0707-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="e0707-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="e0707-506">Especifica el formato del archivo de datos exportados de tabla.</span><span class="sxs-lookup"><span data-stu-id="e0707-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="e0707-507">Si no se especifica esta opción, de forma predeterminada, AzCopy exporta el archivo de datos de tabla en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e0707-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="e0707-508">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="e0707-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="e0707-509">Problemas conocidos y prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="e0707-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="e0707-510">Limitación de escrituras concurrentes mientras se copian datos</span><span class="sxs-lookup"><span data-stu-id="e0707-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="e0707-511">Cuando copie blobs o archivos con AzCopy, recuerde que otra aplicación puede estar modificando los datos mientras se copian.</span><span class="sxs-lookup"><span data-stu-id="e0707-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="e0707-512">Si es posible, asegúrese de que los datos no se modifican durante la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="e0707-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="e0707-513">Por ejemplo, cuando copie un VHD asociado con una máquina virtual de Azure, asegúrese de que ninguna otra aplicación está escribiendo actualmente en el VHD.</span><span class="sxs-lookup"><span data-stu-id="e0707-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="e0707-514">Una buena manera de hacerlo es mediante la concesión de los recursos que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="e0707-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="e0707-515">Alternativamente, puede crear una instantánea del VHD primero y, después, copiar la instantánea.</span><span class="sxs-lookup"><span data-stu-id="e0707-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="e0707-516">Si no puede impedir que otras aplicaciones escriban en blobs o archivos mientras se copian, recuerde que para cuando el trabajo finalice, los recursos copiados puede que ya no tengan una paridad total con los recursos de origen.</span><span class="sxs-lookup"><span data-stu-id="e0707-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="e0707-517">Ejecutar una instancia de AzCopy en un solo equipo.</span><span class="sxs-lookup"><span data-stu-id="e0707-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="e0707-518">AzCopy está diseñado para maximizar el uso de los recursos del equipo para acelerar la transferencia de datos. Se recomienda ejecutar solo una instancia de AzCopy en un equipo y especificar la opción `/NC` si necesita más operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="e0707-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="e0707-519">Para obtener más detalles, escriba `AzCopy /?:NC` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e0707-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="e0707-520">Habilitar algoritmos MD5 que cumplan con FIPS para AzCopy cuando "Use algoritmos que cumplen con FIPS para el cifrado, firma y operaciones hash".</span><span class="sxs-lookup"><span data-stu-id="e0707-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="e0707-521">AzCopy usa de forma predeterminada la implementación de .NET MD5 para calcular el MD5 al copiar los objetos, pero hay algunos requisitos de seguridad que necesitan AzCopy para habilitar la configuración de MD5 compatible con FIPS.</span><span class="sxs-lookup"><span data-stu-id="e0707-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="e0707-522">Puede crear un archivo app.config `AzCopy.exe.config` con la propiedad `AzureStorageUseV1MD5` y separarlo con AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="e0707-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="e0707-523">Respecto a la propiedad "AzureStorageUseV1MD5" • True (valor predeterminado): AzCopy utiliza la implementación de MD5 .NET.</span><span class="sxs-lookup"><span data-stu-id="e0707-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="e0707-524">• False: AzCopy utiliza el algoritmo MD5 compatible con FIPS.</span><span class="sxs-lookup"><span data-stu-id="e0707-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="e0707-525">Tenga en cuenta que los algoritmos compatibles con FIPS están deshabilitados de forma predeterminada en el equipo de Windows, puede escribir secpol.msc en la ventana de ejecución y comprobar este modificador en Configuración de seguridad -> Directivas locales -> Opciones de seguridad -> Criptografía de sistema: Usar algoritmos compatibles con FIPS para cifrado, firma y operaciones hash.</span><span class="sxs-lookup"><span data-stu-id="e0707-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0707-526">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0707-526">Next steps</span></span>
<span data-ttu-id="e0707-527">Para más información sobre Azure Storage y AzCopy, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0707-527">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="e0707-528">Documentación de Almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="e0707-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="e0707-529">Introducción a Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e0707-529">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="e0707-530">Uso del almacenamiento de blobs de .NET</span><span class="sxs-lookup"><span data-stu-id="e0707-530">How to use Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e0707-531">Uso del almacenamiento de archivos de .NET</span><span class="sxs-lookup"><span data-stu-id="e0707-531">How to use File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="e0707-532">Uso del almacenamiento de tablas de .NET</span><span class="sxs-lookup"><span data-stu-id="e0707-532">How to use Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="e0707-533">Creación, administración o eliminación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e0707-533">How to create, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="e0707-534">Transferencia de datos con AzCopy en Linux</span><span class="sxs-lookup"><span data-stu-id="e0707-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="e0707-535">Publicaciones en blobs de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e0707-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="e0707-536">Introducción a la versión de vista previa de la biblioteca de movimiento de datos de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e0707-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="e0707-537">AzCopy: Introducción a la copia sincrónica y el tipo de contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="e0707-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="e0707-538">AzCopy: Presentación de la disponibilidad general de AzCopy 3.0 y de la versión de vista previa de AzCopy 4.0 compatible con tablas y archivos</span><span class="sxs-lookup"><span data-stu-id="e0707-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="e0707-539">AzCopy: Optimizada para escenarios de copia a gran escala</span><span class="sxs-lookup"><span data-stu-id="e0707-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="e0707-540">AzCopy: Compatibilidad para almacenamiento con redundancia geográfica de acceso de lectura</span><span class="sxs-lookup"><span data-stu-id="e0707-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="e0707-541">AzCopy: Transferencia de datos con modo reiniciable y token SAS</span><span class="sxs-lookup"><span data-stu-id="e0707-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="e0707-542">AzCopy: Uso de copia de blobs entre cuentas</span><span class="sxs-lookup"><span data-stu-id="e0707-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="e0707-543">AzCopy: Carga y descarga de archivos para blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="e0707-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

