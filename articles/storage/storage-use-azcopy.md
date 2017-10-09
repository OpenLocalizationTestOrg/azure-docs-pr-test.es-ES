---
title: aaaCopy o mover datos tooAzure almacenamiento con AzCopy en Windows | Documentos de Microsoft
description: "Usar hello AzCopy en la utilidad de Windows a toomove o copia de la tooor de datos con el de blobs, tablas y contenido del archivo. Copiar datos tooAzure almacenamiento de archivos locales, o copiar datos dentro de o entre cuentas de almacenamiento. Migrar fácilmente el almacenamiento de datos tooAzure."
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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="5262e-105">Transferencia de datos con hello AzCopy en Windows</span><span class="sxs-lookup"><span data-stu-id="5262e-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="5262e-106">AzCopy es una utilidad de línea de comandos diseñada para copiar datos tooand de almacenamiento de blobs de Microsoft Azure, el archivo y la tabla mediante comandos sencillos con un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="5262e-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="5262e-107">Puede copiar datos de una tooanother de objeto dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5262e-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="5262e-108">Hay dos versiones de AzCopy que puede descargar.</span><span class="sxs-lookup"><span data-stu-id="5262e-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="5262e-109">AzCopy en Windows está integrado en .NET Framework y ofrece opciones de línea de comandos de estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="5262e-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="5262e-110">[AzCopy en Linux](storage-use-azcopy-linux.md) está integrado en .NET Core Framework que tiene como destino plataformas Linux y ofrece opciones de línea de comandos de estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="5262e-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="5262e-111">Este artículo trata sobre AzCopy en Windows.</span><span class="sxs-lookup"><span data-stu-id="5262e-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="5262e-112">Descarga e instalación de AzCopy</span><span class="sxs-lookup"><span data-stu-id="5262e-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="5262e-113">AzCopy en Windows</span><span class="sxs-lookup"><span data-stu-id="5262e-113">AzCopy on Windows</span></span>
<span data-ttu-id="5262e-114">Descargar hello [versión más reciente de AzCopy en Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="5262e-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="5262e-115">Instalación en Windows</span><span class="sxs-lookup"><span data-stu-id="5262e-115">Installation on Windows</span></span>
<span data-ttu-id="5262e-116">Después de instalar AzCopy en Windows con el instalador de hello, abra una ventana de comandos y desplácese toohello AzCopy directorio de instalación en el equipo, donde hello `AzCopy.exe` ejecutable se encuentra.</span><span class="sxs-lookup"><span data-stu-id="5262e-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="5262e-117">Si lo desea, puede agregar hello AzCopy tooyour sistema ruta de instalación.</span><span class="sxs-lookup"><span data-stu-id="5262e-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="5262e-118">De forma predeterminada, AzCopy se instala demasiado`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` o `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="5262e-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="5262e-119">Escritura del primer comando de AzCopy</span><span class="sxs-lookup"><span data-stu-id="5262e-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="5262e-120">sintaxis básica de Hola para comandos de AzCopy es:</span><span class="sxs-lookup"><span data-stu-id="5262e-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="5262e-121">Hello en los ejemplos siguientes muestra una variedad de escenarios para copiar datos tooand de Blobs de Microsoft Azure, archivos y tablas.</span><span class="sxs-lookup"><span data-stu-id="5262e-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="5262e-122">Consulte toohello [AzCopy parámetros](#azcopy-parameters) sección para obtener una explicación detallada de los parámetros de hello utilizadas en cada ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5262e-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="5262e-123">Blob: descarga</span><span class="sxs-lookup"><span data-stu-id="5262e-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="5262e-124">Descarga de un solo blob</span><span class="sxs-lookup"><span data-stu-id="5262e-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="5262e-125">Tenga en cuenta que si carpeta hello `C:\myfolder` no existe, se cree y descargue AzCopy `abc.txt ` en la nueva carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="5262e-126">Descarga de un solo blob desde la región secundaria</span><span class="sxs-lookup"><span data-stu-id="5262e-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="5262e-127">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="5262e-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="5262e-128">Descarga de todos los blobs</span><span class="sxs-lookup"><span data-stu-id="5262e-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="5262e-129">Suponga la siguiente Hola blobs residen en el contenedor especificado de hello:</span><span class="sxs-lookup"><span data-stu-id="5262e-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="5262e-130">Después de la operación de descarga de Hola Hola directory `C:\myfolder` incluirá Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="5262e-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="5262e-131">Si no especifica la opción `/S`, no se descargará ningún blob.</span><span class="sxs-lookup"><span data-stu-id="5262e-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="5262e-132">Descarga de blobs con el prefijo especificado</span><span class="sxs-lookup"><span data-stu-id="5262e-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="5262e-133">Suponga la siguiente Hola blobs residen en el contenedor especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="5262e-134">Todos los blobs que comienzan con el prefijo de hello `a` se van a descargar:</span><span class="sxs-lookup"><span data-stu-id="5262e-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="5262e-135">Después de la operación de descarga de Hola Hola carpeta `C:\myfolder` incluirá Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="5262e-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="5262e-136">prefijo de Hello aplica toohello directorio virtual, que forma Hola primera parte del nombre de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="5262e-137">Ejemplo de Hola mostrado anteriormente, directorio virtual hello no coincide con el prefijo especificado de hello, por lo que no se descarga.</span><span class="sxs-lookup"><span data-stu-id="5262e-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="5262e-138">Además, si hello opción `\S` no se especifica, AzCopy descargará los blobs.</span><span class="sxs-lookup"><span data-stu-id="5262e-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="5262e-139">Establecer la hora de última modificación de Hola de los archivos exportados toobe igual que Hola blobs de origen</span><span class="sxs-lookup"><span data-stu-id="5262e-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="5262e-140">También puede excluir blobs de operación de descarga de hello según su hora de última modificación.</span><span class="sxs-lookup"><span data-stu-id="5262e-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="5262e-141">Por ejemplo, si desea que los blobs tooexclude cuya hora de última modificación es hello igual o más reciente que el archivo de destino de hello, agregar hello `/XN` opción:</span><span class="sxs-lookup"><span data-stu-id="5262e-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="5262e-142">O si desea que los blobs tooexclude cuya hora de última modificación es hello igual o anterior a archivo de destino de hello, agregue hello `/XO` opción:</span><span class="sxs-lookup"><span data-stu-id="5262e-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="5262e-143">Blob: carga</span><span class="sxs-lookup"><span data-stu-id="5262e-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="5262e-144">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="5262e-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="5262e-145">Si no existe el contenedor de destino especificado de hello, AzCopy se crea y cargar archivo hello en él.</span><span class="sxs-lookup"><span data-stu-id="5262e-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="5262e-146">Cargar archivo único directorio toovirtual</span><span class="sxs-lookup"><span data-stu-id="5262e-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="5262e-147">Si Hola especifica el directorio virtual no existe, AzCopy cargará Hola archivo tooinclude Hola directorio virtual en su nombre (*p. ej.*, `vd/abc.txt` en el ejemplo de Hola anterior).</span><span class="sxs-lookup"><span data-stu-id="5262e-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="5262e-148">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="5262e-149">Especificar la opción `/S` cargas Hola contenido de hello especificado directorios tooBlob almacenamiento de manera recursiva, lo que significa que todas las subcarpetas y sus archivos se cargarán así.</span><span class="sxs-lookup"><span data-stu-id="5262e-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="5262e-150">Por ejemplo, suponga el siguiente Hola archivos residen en la carpeta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="5262e-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="5262e-151">Después de la operación de carga de hello, contenedor Hola incluirá Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="5262e-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="5262e-152">Si no especifica la opción `/S`, AzCopy no realizará la carga de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="5262e-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="5262e-153">Después de la operación de carga de hello, contenedor Hola incluirá Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="5262e-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="5262e-154">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="5262e-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="5262e-155">Suponga la siguiente Hola archivos residen en la carpeta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="5262e-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="5262e-156">Después de la operación de carga de hello, contenedor Hola incluirá Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="5262e-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="5262e-157">Si no especifica la opción `/S`, AzCopy solo cargará los blobs que no residan en un directorio virtual:</span><span class="sxs-lookup"><span data-stu-id="5262e-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="5262e-158">Especifique el tipo de contenido MIME de Hola de un blob de destino</span><span class="sxs-lookup"><span data-stu-id="5262e-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="5262e-159">De forma predeterminada, AzCopy establece tipo de contenido de Hola de un blob de destino demasiado`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="5262e-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="5262e-160">A partir de la versión 3.1.0, puede especificar explícitamente Hola de tipo de contenido a través de la opción de hello `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="5262e-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="5262e-161">Esta sintaxis establece el tipo de contenido de Hola para todos los blobs en una operación de carga.</span><span class="sxs-lookup"><span data-stu-id="5262e-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="5262e-162">Si especifica `/SetContentType` sin un valor, a continuación, AzCopy establecerá cada blob o tipo de contenido del archivo según tooits extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="5262e-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="5262e-163">Blob: copia</span><span class="sxs-lookup"><span data-stu-id="5262e-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="5262e-164">Copia de un solo blob dentro de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5262e-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="5262e-165">Cuando copia un blob dentro de una cuenta de almacenamiento, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="5262e-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="5262e-166">Copia de un solo blob entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5262e-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="5262e-167">Cuando copia un blob entre cuentas de almacenamiento, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="5262e-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="5262e-168">Copiar blob único de una región secundaria tooprimary otra</span><span class="sxs-lookup"><span data-stu-id="5262e-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="5262e-169">Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.</span><span class="sxs-lookup"><span data-stu-id="5262e-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="5262e-170">Copia de un solo blob y de sus instantáneas entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5262e-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="5262e-171">Después de la operación de copia de hello, contenedor de destino de hello incluirá Hola blob y sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="5262e-172">Suponiendo que el blob de hello en el ejemplo de Hola anterior tiene dos instantáneas, el contenedor de hello incluirá siguiente Hola blobs e instantáneas:</span><span class="sxs-lookup"><span data-stu-id="5262e-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="5262e-173">Copia sincrónica de blobs entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5262e-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="5262e-174">De forma predeterminada, AzCopy copia datos entre dos extremos de almacenamiento asincrónicamente.</span><span class="sxs-lookup"><span data-stu-id="5262e-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="5262e-175">Por lo tanto, se ejecutará la operación de copia de hello en segundo plano de hello utilizando la capacidad de reserva de ancho de banda que no tenga ningún SLA en cuanto a la rapidez con que se va a copiar un blob y AzCopy comprobará periódicamente en estado de la copia de hello hasta que se copia Hola completado o no se pudo.</span><span class="sxs-lookup"><span data-stu-id="5262e-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="5262e-176">Hola `/SyncCopy` opción garantiza que la operación de copia de hello obtendrá velocidad coherente.</span><span class="sxs-lookup"><span data-stu-id="5262e-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="5262e-177">AzCopy realiza copia sincrónica hello mediante la descarga de blobs de hello toocopy de hello especificado memoria toolocal de origen y, a continuación, cargarlos toohello destino de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="5262e-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="5262e-178">`/SyncCopy`puede generar salida adicional costo tooasynchronous comparados copia, hello enfoque recomendado es toouse esta opción en una máquina virtual de Azure que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5262e-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="5262e-179">Archivo: descarga</span><span class="sxs-lookup"><span data-stu-id="5262e-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="5262e-180">Descarga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="5262e-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="5262e-181">Si no especifica Hola origen es un recurso compartido de archivos de Azure, o bien debe especificar el nombre exacto del archivo de hello, (*p. ej.* `abc.txt`) toodownload un solo archivo, o especificar la opción `/S` toodownload todos los archivos en el recurso compartido de Hola de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="5262e-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="5262e-182">Intentar toospecify un patrón de archivo y la opción `/S` juntos, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="5262e-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="5262e-183">Descarga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="5262e-184">Tenga en cuenta que ninguna carpeta vacía se descargará.</span><span class="sxs-lookup"><span data-stu-id="5262e-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="5262e-185">Archivo: carga</span><span class="sxs-lookup"><span data-stu-id="5262e-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="5262e-186">Carga de un solo archivo</span><span class="sxs-lookup"><span data-stu-id="5262e-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="5262e-187">Carga de todos los archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="5262e-188">Tenga en cuenta que ninguna carpeta vacía se cargará.</span><span class="sxs-lookup"><span data-stu-id="5262e-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="5262e-189">Carga de archivos que coincidan con el patrón especificado</span><span class="sxs-lookup"><span data-stu-id="5262e-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="5262e-190">Archivo: copia</span><span class="sxs-lookup"><span data-stu-id="5262e-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="5262e-191">Copia a través de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="5262e-192">Al copiar un archivo en distintos recursos compartidos de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="5262e-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="5262e-193">Copiar desde tooblob del recurso compartido de archivo</span><span class="sxs-lookup"><span data-stu-id="5262e-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="5262e-194">Al copiar un archivo de tooblob de recurso compartido de archivo, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.</span><span class="sxs-lookup"><span data-stu-id="5262e-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="5262e-195">Copiar desde el recurso compartido de blob toofile</span><span class="sxs-lookup"><span data-stu-id="5262e-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="5262e-196">Al copiar un archivo de recurso compartido de blob toofile, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.</span><span class="sxs-lookup"><span data-stu-id="5262e-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="5262e-197">Copia sincrónica de archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-197">Synchronously copy files</span></span>
<span data-ttu-id="5262e-198">Puede especificar hello `/SyncCopy` opción toocopy datos de almacenamiento, del almacenamiento de archivos tooFile de almacenamiento de archivos tooBlob almacenamiento y de almacenamiento de blobs tooFile almacenamiento sincrónicamente, AzCopy hace esto mediante la descarga de memoria de toolocal de datos de origen de Hola y cargarlo nuevo toodestination.</span><span class="sxs-lookup"><span data-stu-id="5262e-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="5262e-199">Se aplicará el costo de salida estándar.</span><span class="sxs-lookup"><span data-stu-id="5262e-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="5262e-200">Cuando se copia desde el almacenamiento de archivos tooBlob almacenamiento, tipo de blob de hello predeterminado es blob en bloques, usuario puede especificar la opción `/BlobType:page` tipo de blob de destino de toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="5262e-201">Tenga en cuenta que `/SyncCopy` podría generar salida adicional costo comparar copia tooasynchronous, hello enfoque recomendado es toouse esta opción en Hola VM de Azure que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5262e-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="5262e-202">Tabla: exportación</span><span class="sxs-lookup"><span data-stu-id="5262e-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="5262e-203">Tabla de exportación</span><span class="sxs-lookup"><span data-stu-id="5262e-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="5262e-204">AzCopy escribe una carpeta de destino especificado de toohello de archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="5262e-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="5262e-205">archivo de manifiesto de Hola se utiliza en los archivos de datos necesarios de hello importación proceso toolocate hello y realizar la validación de datos.</span><span class="sxs-lookup"><span data-stu-id="5262e-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="5262e-206">archivo de manifiesto de Hello usa Hola sigue la convención de nomenclatura de forma predeterminada:</span><span class="sxs-lookup"><span data-stu-id="5262e-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="5262e-207">Usuario también puede especificar la opción de hello `/Manifest:<manifest file name>` nombre de archivo de manifiesto de tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="5262e-208">Exportación dividida en varios archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="5262e-209">AzCopy utiliza un *índice de volumen* Hola dividir los datos de nombres de los archivos toodistinguish varios archivos.</span><span class="sxs-lookup"><span data-stu-id="5262e-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="5262e-210">índice de volumen de Hello consta de dos partes, un *índice de intervalo de claves de partición* y un *división archivo índice*.</span><span class="sxs-lookup"><span data-stu-id="5262e-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="5262e-211">Ambos índices se basan en 0.</span><span class="sxs-lookup"><span data-stu-id="5262e-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="5262e-212">índice de intervalo de claves de partición de Hello será 0 si el usuario no especifica la opción `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="5262e-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="5262e-213">Por ejemplo, suponga que AzCopy genera dos archivos de datos después de que el usuario de hello especifica la opción de `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="5262e-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="5262e-214">Hola resultante nombres de archivo de datos podría ser:</span><span class="sxs-lookup"><span data-stu-id="5262e-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="5262e-215">Tenga en cuenta que Hola valor mínimo posible para la opción `/SplitSize` es 32 MB.</span><span class="sxs-lookup"><span data-stu-id="5262e-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="5262e-216">Si Hola especifica el destino es el almacenamiento de blobs, AzCopy se divide el archivo de datos de hello una vez su límite de tamaño de blob de tamaños alcanza hello (200GB), con independencia de si la opción `/SplitSize` se ha especificado por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="5262e-217">Formato de archivo de datos CSV o tooJSON de la tabla de exportación</span><span class="sxs-lookup"><span data-stu-id="5262e-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="5262e-218">AzCopy predeterminada exporta los archivos de datos de tablas tooJSON.</span><span class="sxs-lookup"><span data-stu-id="5262e-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="5262e-219">También puede especificar la opción de hello `/PayloadFormat:JSON|CSV` tablas de hello tooexport como JSON o CSV.</span><span class="sxs-lookup"><span data-stu-id="5262e-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="5262e-220">Al especificar el formato de carga de hello CSV, AzCopy también generará un archivo de esquema con la extensión `.schema.csv` para cada archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="5262e-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="5262e-221">Exportación de entidades de tabla simultáneamente</span><span class="sxs-lookup"><span data-stu-id="5262e-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="5262e-222">AzCopy iniciará las entidades de las operaciones simultáneas tooexport al usuario Hola especifica la opción `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="5262e-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="5262e-223">Cada operación exporta un rango de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="5262e-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="5262e-224">Tenga en cuenta que el número de Hola de operaciones simultáneas también se controla mediante la opción `/NC`.</span><span class="sxs-lookup"><span data-stu-id="5262e-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="5262e-225">AzCopy utiliza el número de Hola de procesadores de núcleo como valor predeterminado de Hola de `/NC` cuando se copian las entidades de tabla, incluso si `/NC` no se especificó.</span><span class="sxs-lookup"><span data-stu-id="5262e-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="5262e-226">Cuando el usuario de hello especifica la opción `/PKRS`, AzCopy usa Hola menor del número de Hola de hello dos valores - intervalos clave de partición frente a las operaciones simultáneas especificados de forma implícita o explícita - toodetermine de toostart de operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="5262e-227">Para obtener más información, escriba `AzCopy /?:NC` en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="5262e-228">Tooblob de la tabla de exportación</span><span class="sxs-lookup"><span data-stu-id="5262e-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="5262e-229">AzCopy genera un archivo de datos JSON en el contenedor de blobs de hello con las siguientes convención de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="5262e-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="5262e-230">archivo de datos JSON de Hello generado sigue el formato de carga de hello para la cantidad mínima de metadatos.</span><span class="sxs-lookup"><span data-stu-id="5262e-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="5262e-231">Para obtener más información sobre el formato de carga, consulte [Formato de carga para las operaciones del servicio Tabla](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="5262e-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="5262e-232">Tenga en cuenta que cuando se exportan tablas tooblobs, AzCopy descargar archivos de datos temporales de toolocal de las entidades de tabla de hello y, a continuación, cargar los blob de toohello de entidades.</span><span class="sxs-lookup"><span data-stu-id="5262e-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="5262e-233">Estos archivos de datos temporales se colocan en la carpeta de archivos de diario de hello con ruta de acceso de hello predeterminada "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", puede especificar la opción/Z: [carpeta de archivo diario] toochange Hola ubicación de carpeta del archivo de diario y, por tanto, cambiar la ubicación de archivos de datos temporales de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="5262e-234">Hello datos temporales, tamaño del archivo se decide por tamaño y el tamaño de hello especificado con hello opción /SplitSize, las entidades de la tabla, aunque el archivo de datos temporales de hello en el disco local se eliminarán al instante una vez se ha cargan toohello blob, asegúrese de tener suficiente toostore de espacio en disco local de estos archivos de datos temporales antes de que se eliminen.</span><span class="sxs-lookup"><span data-stu-id="5262e-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="5262e-235">Tabla: importación</span><span class="sxs-lookup"><span data-stu-id="5262e-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="5262e-236">Importación de la tabla</span><span class="sxs-lookup"><span data-stu-id="5262e-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="5262e-237">Hola opción `/EntityOperation` indica cómo tooinsert entidades en Hola tabla.</span><span class="sxs-lookup"><span data-stu-id="5262e-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="5262e-238">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="5262e-238">Possible values are:</span></span>

* <span data-ttu-id="5262e-239">`InsertOrSkip`: Omite una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="5262e-240">`InsertOrMerge`: Combina una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="5262e-241">`InsertOrReplace`: Reemplaza una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="5262e-242">Tenga en cuenta que no se puede especificar la opción `/PKRS` en escenario de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="5262e-243">A diferencia del escenario de exportación de hello, en el que se debe especificar la opción `/PKRS` toostart operaciones simultáneas, AzCopy predeterminada iniciará operaciones simultáneas cuando se importa una tabla.</span><span class="sxs-lookup"><span data-stu-id="5262e-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="5262e-244">número predeterminado de Hola de operaciones simultáneas iniciado es toohello igual número de procesadores de núcleo; Sin embargo, puede especificar un número diferente de simultáneas con la opción `/NC`.</span><span class="sxs-lookup"><span data-stu-id="5262e-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="5262e-245">Para obtener más información, escriba `AzCopy /?:NC` en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="5262e-246">Tenga en cuenta que AzCopy solo admite la importación de archivos con el formato JSON, no CSV.</span><span class="sxs-lookup"><span data-stu-id="5262e-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="5262e-247">AzCopy no permite importar tablas de archivos de manifiesto y archivos JSON creados por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5262e-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="5262e-248">Estos archivos deben proceder de una exportación de tablas de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5262e-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="5262e-249">errores de tooavoid, no modifique Hola exporta JSON o archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="5262e-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="5262e-250">Importar entidades tootable mediante blobs</span><span class="sxs-lookup"><span data-stu-id="5262e-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="5262e-251">Suponga que un contenedor de Blob contiene siguiente hello: archivo A JSON que representa una tabla de Azure y su archivo de manifiesto que lo acompaña.</span><span class="sxs-lookup"><span data-stu-id="5262e-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="5262e-252">Puede ejecutar Hola siguiendo las entidades de tooimport de comando en una tabla usando el archivo de manifiesto de hello en ese contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="5262e-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="5262e-253">Otras características de AzCopy</span><span class="sxs-lookup"><span data-stu-id="5262e-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="5262e-254">Sólo copia los datos que no existen en el destino de Hola</span><span class="sxs-lookup"><span data-stu-id="5262e-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="5262e-255">Hola `/XO` y `/XN` parámetros permiten tooexclude recursos de origen anterior o posterior que copien, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="5262e-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="5262e-256">Si solo desea toocopy recursos de origen que no existen en el destino de hello, puede especificar los dos parámetros en hello AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="5262e-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="5262e-257">Tenga en cuenta que esto no se admite cuando el origen de Hola o de destino es una tabla.</span><span class="sxs-lookup"><span data-stu-id="5262e-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="5262e-258">Usar un parámetros de línea de comandos de toospecify de archivo de respuesta</span><span class="sxs-lookup"><span data-stu-id="5262e-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="5262e-259">Puede incluir cualquier parámetro de la línea de comandos de AzCopy en un archivo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="5262e-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="5262e-260">Procesos de AzCopy Hola parámetros en el archivo hello como si hubieran especificado en la línea de comandos de hello, realizar una sustitución directa con contenido de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="5262e-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="5262e-261">Se supone un archivo de respuesta denominado `copyoperation.txt`, que contiene Hola siguiendo las líneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="5262e-262">Cada parámetro de AzCopy se puede especificar en una sola línea</span><span class="sxs-lookup"><span data-stu-id="5262e-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="5262e-263">o bien, en líneas independientes:</span><span class="sxs-lookup"><span data-stu-id="5262e-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="5262e-264">AzCopy se producirá un error si se divide parámetro hello en dos líneas, como se muestra aquí para hello `/sourcekey` parámetro:</span><span class="sxs-lookup"><span data-stu-id="5262e-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="5262e-265">Utilizar varios parámetros de línea de comandos de respuesta archivos toospecify</span><span class="sxs-lookup"><span data-stu-id="5262e-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="5262e-266">Imaginemos un archivo de respuesta llamado `source.txt` que especifica un contenedor de origen:</span><span class="sxs-lookup"><span data-stu-id="5262e-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="5262e-267">Y un archivo de respuesta denominado `dest.txt` que especifica una carpeta de destino en el sistema de archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="5262e-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="5262e-268">Y un archivo de respuesta llamado `options.txt` que especifica opciones para AzCopy:</span><span class="sxs-lookup"><span data-stu-id="5262e-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="5262e-269">toocall AzCopy con estos archivos de respuesta, que residen en un directorio `C:\responsefiles`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="5262e-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="5262e-270">AzCopy procesa este comando tal como lo haría si incluye todos los parámetros individuales en la línea de comandos de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="5262e-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="5262e-271">Especificación de una firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="5262e-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="5262e-272">También puede especificar una SAS en el contenedor de hello URI:</span><span class="sxs-lookup"><span data-stu-id="5262e-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="5262e-273">Carpeta de archivo de diario</span><span class="sxs-lookup"><span data-stu-id="5262e-273">Journal file folder</span></span>
<span data-ttu-id="5262e-274">Cada vez que se emite un tooAzCopy de comando, comprueba si existe un archivo de diario en la carpeta predeterminada de hello, o si se encuentra en una carpeta que especifica mediante esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="5262e-275">Si no existe el archivo de diario de Hola en cualquier lugar, AzCopy trata operación hello como nueva y genera un nuevo archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="5262e-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="5262e-276">Si existe el archivo de diario de hello, AzCopy comprobará si línea de comandos de Hola de entrada coincida con Hola de línea de comandos en el archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="5262e-277">Si coincide con dos líneas de comandos hello, AzCopy reanuda la operación incompleta de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="5262e-278">Si no coinciden, será tooeither solicitadas sobrescribir Hola diario archivo toostart una operación de nuevo o toocancel Hola operación actual.</span><span class="sxs-lookup"><span data-stu-id="5262e-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="5262e-279">Si desea que toouse Hola esta ubicación para el archivo de diario de hello:</span><span class="sxs-lookup"><span data-stu-id="5262e-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="5262e-280">Si se omite la opción `/Z`, o especificar la opción `/Z` sin ruta de acceso de carpeta de hello, como se muestra arriba, AzCopy crea archivo diario de hello en la ubicación predeterminada de hello, que es `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="5262e-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="5262e-281">Si ya existe un archivo de diario de hello, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="5262e-282">Si desea que una ubicación personalizada para el archivo de diario de Hola toospecify:</span><span class="sxs-lookup"><span data-stu-id="5262e-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="5262e-283">Este ejemplo crea el archivo de diario de hello si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="5262e-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="5262e-284">Si existe, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="5262e-285">Si desea que una operación de AzCopy tooresume:</span><span class="sxs-lookup"><span data-stu-id="5262e-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="5262e-286">Este ejemplo reanuda la operación última hello, que podría no haber toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5262e-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="5262e-287">Generación de un archivo de registro</span><span class="sxs-lookup"><span data-stu-id="5262e-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="5262e-288">Si se especifica opción `/V` sin proporcionar un registro detallado de archivo ruta de acceso toohello, a continuación, AzCopy crea archivos de registro de hello en la ubicación predeterminada de hello, que es `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="5262e-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="5262e-289">De lo contrario, puede crear un archivo de registro en una ubicación personalizada:</span><span class="sxs-lookup"><span data-stu-id="5262e-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="5262e-290">Tenga en cuenta que si especifica una ruta de acceso relativa siguiente opción `/V`, como `/V:test/azcopy1.log`, a continuación, se crea el registro detallado de hello en el directorio de trabajo actual de hello en una subcarpeta denominada `test`.</span><span class="sxs-lookup"><span data-stu-id="5262e-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="5262e-291">Especificar número de Hola de operaciones simultáneas toostart</span><span class="sxs-lookup"><span data-stu-id="5262e-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="5262e-292">Opción `/NC` especifica Hola número de operaciones de copia simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="5262e-293">De forma predeterminada, AzCopy inicia un número determinado de rendimiento de transferencia de datos de las operaciones simultáneas tooincrease Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="5262e-294">Para las operaciones de tabla, el número de Hola de operaciones simultáneas es toohello igual número de procesadores de que disponga.</span><span class="sxs-lookup"><span data-stu-id="5262e-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="5262e-295">Para operaciones de Blob y archivo, número de Hola de operaciones simultáneas es es igual 8 veces Hola número de procesadores de que disponga.</span><span class="sxs-lookup"><span data-stu-id="5262e-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="5262e-296">Si está ejecutando AzCopy a través de una red de ancho de banda bajo, puede especificar un número menor para el parámetro/NC tooavoid error por competencia de recursos.</span><span class="sxs-lookup"><span data-stu-id="5262e-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="5262e-297">Ejecución de AzCopy en el emulador de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5262e-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="5262e-298">Puede ejecutar AzCopy contra Hola [emulador de almacenamiento de Azure](storage-use-emulator.md) para Blobs:</span><span class="sxs-lookup"><span data-stu-id="5262e-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="5262e-299">y tablas:</span><span class="sxs-lookup"><span data-stu-id="5262e-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="5262e-300">Parámetros de AzCopy</span><span class="sxs-lookup"><span data-stu-id="5262e-300">AzCopy Parameters</span></span>
<span data-ttu-id="5262e-301">A continuación se describen los parámetros para AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5262e-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="5262e-302">También puede escribir uno de los siguientes comandos de línea de comandos de Hola para Ayuda sobre el uso de AzCopy de hello:</span><span class="sxs-lookup"><span data-stu-id="5262e-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="5262e-303">Para obtener ayuda detallada sobre la línea de comandos de AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="5262e-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="5262e-304">Para obtener ayuda detallada con algún parámetro de AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="5262e-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="5262e-305">Para obtener ejemplos de línea de comandos: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="5262e-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="5262e-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="5262e-306">/Source:"source"</span></span>
<span data-ttu-id="5262e-307">Especifica los datos de origen de Hola de qué toocopy.</span><span class="sxs-lookup"><span data-stu-id="5262e-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="5262e-308">Hola origen puede ser un directorio del sistema de archivos, un contenedor de blobs, un directorio virtual de blob, un recurso compartido de archivos de almacenamiento, un directorio de archivos de almacenamiento o una tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="5262e-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="5262e-309">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="5262e-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="5262e-310">/Dest:"destination"</span></span>
<span data-ttu-id="5262e-311">Especifica Hola destino toocopy a.</span><span class="sxs-lookup"><span data-stu-id="5262e-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="5262e-312">Hola destino puede ser un directorio del sistema de archivos, un contenedor de blobs, un directorio virtual de blob, un recurso compartido de archivos de almacenamiento, un directorio de archivos de almacenamiento o una tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="5262e-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="5262e-313">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="5262e-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="5262e-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="5262e-315">Especifica un patrón de archivo que indica qué toocopy de archivos.</span><span class="sxs-lookup"><span data-stu-id="5262e-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="5262e-316">comportamiento de Hola de parámetro de hello /Pattern viene determinado por la ubicación Hola Hola de datos de origen y la presencia de Hola de opción de modo recursivo Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="5262e-317">El modo recursivo viene especificado por la opción /S.</span><span class="sxs-lookup"><span data-stu-id="5262e-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="5262e-318">Si Hola especificado es un directorio en el sistema de archivos de hello, caracteres comodín estándar está en vigor, y proporcionar el patrón del archivo Hola se compara con los archivos contenidos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="5262e-319">Si está opción que se especifica/s., AzCopy, a continuación, también coincide con patrón especificado de hello en todos los archivos de las subcarpetas por debajo del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="5262e-320">Si el origen especificado de hello es un contenedor de blob o directorio virtual, no se aplica caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="5262e-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="5262e-321">Si la opción que se especifica/s., AzCopy, a continuación, interpreta el patrón de archivo especificado de Hola como un prefijo de blob.</span><span class="sxs-lookup"><span data-stu-id="5262e-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="5262e-322">Si está opción que no se especifica/s., AzCopy, a continuación, coincide con patrón de archivo de hello con nombres de blob exacto.</span><span class="sxs-lookup"><span data-stu-id="5262e-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="5262e-323">Si no especifica Hola origen es un recurso compartido de archivos de Azure, debe especificar nombre de archivo exacto de hello, (p. ej. abc.txt) toocopy un solo archivo, o especificar opción /S toocopy todos los archivos de forma recursiva del recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="5262e-324">Intentar toospecify un patrón de archivo y la opción /S juntos se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="5262e-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="5262e-325">AzCopy usa la coincidencia distingue mayúsculas de minúsculas al Hola/Source es un contenedor de blob o el directorio virtual de blob, y entre mayúsculas y minúsculas para búsqueda de coincidencias en todos los usos Hola otros casos.</span><span class="sxs-lookup"><span data-stu-id="5262e-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="5262e-326">Hola patrón de archivo predeterminado que usa cuando no se especifica ningún patrón de archivo es *.*</span><span class="sxs-lookup"><span data-stu-id="5262e-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="5262e-327">para una ubicación del sistema de archivos, o un prefijo vacío para una ubicación de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5262e-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="5262e-328">No se admite la especificación de varios patrones de archivos.</span><span class="sxs-lookup"><span data-stu-id="5262e-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="5262e-329">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="5262e-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="5262e-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="5262e-331">Especifica la clave de cuenta de almacenamiento de hello para el recurso de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="5262e-332">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="5262e-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="5262e-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="5262e-334">Especifica una firma de acceso compartido (SAS) con permisos de lectura y escritura para el destino de hello (si procede).</span><span class="sxs-lookup"><span data-stu-id="5262e-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="5262e-335">Rodear Hola SAS con comillas dobles, ya que puede contiene caracteres especiales de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="5262e-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="5262e-336">Si el recurso de destino de hello es un contenedor de blobs, el recurso compartido de archivos o la tabla, puede especificar esta opción seguida por el token de SAS de Hola o puede especificar Hola SAS como parte del contenedor de blob de destino de hello, el recurso compartido de archivos o el URI de la tabla, sin esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="5262e-337">Si Hola origen y destino son ambos blobs, entonces blob de destino de hello debe residir dentro de hello misma cuenta de almacenamiento como blob de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="5262e-338">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="5262e-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="5262e-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="5262e-340">Especifica la clave de cuenta de almacenamiento de hello para el recurso de código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="5262e-341">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="5262e-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="5262e-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="5262e-343">Especifica una firma de acceso compartido con permisos de lectura y lista para el origen de hello (si procede).</span><span class="sxs-lookup"><span data-stu-id="5262e-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="5262e-344">Rodear Hola SAS con comillas dobles, ya que puede contiene caracteres especiales de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="5262e-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="5262e-345">Si el recurso de código fuente de hello es un contenedor de blob y se proporciona una clave ni una SAS, contenedor de blobs de Hola se leerán mediante acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="5262e-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="5262e-346">Si el origen de hello es un recurso compartido de archivos o una tabla, se debe proporcionar una clave o una SAS.</span><span class="sxs-lookup"><span data-stu-id="5262e-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="5262e-347">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="5262e-348">/S</span><span class="sxs-lookup"><span data-stu-id="5262e-348">/S</span></span>
<span data-ttu-id="5262e-349">Especifica el modo recursivo para operaciones de copia.</span><span class="sxs-lookup"><span data-stu-id="5262e-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="5262e-350">En el modo recursivo, AzCopy copiará todos los blobs o archivos que coinciden con el patrón de archivo especificado de hello, las de las subcarpetas incluidas.</span><span class="sxs-lookup"><span data-stu-id="5262e-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="5262e-351">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="5262e-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="5262e-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="5262e-353">Especifica si el blob de destino de hello es un blob en bloques, un blob de página o un blob en anexos.</span><span class="sxs-lookup"><span data-stu-id="5262e-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="5262e-354">Esta opción solo es aplicable cuando se carga un blob.</span><span class="sxs-lookup"><span data-stu-id="5262e-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="5262e-355">De lo contrario, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="5262e-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="5262e-356">Si el destino de hello es un blob y no se especifica esta opción, de forma predeterminada, AzCopy crea un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="5262e-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="5262e-357">**Aplicable a:** blobs</span><span class="sxs-lookup"><span data-stu-id="5262e-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="5262e-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="5262e-358">/CheckMD5</span></span>
<span data-ttu-id="5262e-359">Calcula un hash MD5 para datos descargados y comprueba que el hash de MD5 de hello almacenados en el blob de Hola o la propiedad Content-MD5 del archivo coincide con hello calculado hash.</span><span class="sxs-lookup"><span data-stu-id="5262e-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="5262e-360">comprobación de Hello MD5 está desactivada de forma predeterminada, por lo que debe especificar esta comprobación de opción tooperform Hola MD5 al descargar los datos.</span><span class="sxs-lookup"><span data-stu-id="5262e-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="5262e-361">Tenga en cuenta que el almacenamiento de Azure no garantiza que Hola hash MD5 almacenado para el blob de Hola o archivo está actualizado.</span><span class="sxs-lookup"><span data-stu-id="5262e-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="5262e-362">Hola tooupdate de responsabilidad del cliente MD5 es cada vez que se modifica el blob de Hola o archivo.</span><span class="sxs-lookup"><span data-stu-id="5262e-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="5262e-363">AzCopy siempre establece propiedad Content-MD5 de Hola para un blob de Azure o un archivo después de cargarlo toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="5262e-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="5262e-364">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="5262e-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="5262e-365">/Snapshot</span></span>
<span data-ttu-id="5262e-366">Indica si las instantáneas tootransfer.</span><span class="sxs-lookup"><span data-stu-id="5262e-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="5262e-367">Esta opción solo es válida si el origen de hello es un blob.</span><span class="sxs-lookup"><span data-stu-id="5262e-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="5262e-368">Hello las instantáneas de blob transferidos se cambia el nombre en este formato: .extension de nombre de blob (hora de la instantánea)</span><span class="sxs-lookup"><span data-stu-id="5262e-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="5262e-369">De forma predeterminada, las instantáneas no se copian.</span><span class="sxs-lookup"><span data-stu-id="5262e-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="5262e-370">**Aplicable a:** blobs</span><span class="sxs-lookup"><span data-stu-id="5262e-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="5262e-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="5262e-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="5262e-372">Envía mensajes con el estado detallado a un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="5262e-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="5262e-373">De forma predeterminada, el archivo de registro detallado de Hola se denomina AzCopyVerbose.log en `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="5262e-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="5262e-374">Si especifica una ubicación de archivo existente para esta opción, registro detallado de hello será archivo toothat anexado.</span><span class="sxs-lookup"><span data-stu-id="5262e-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="5262e-375">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="5262e-376">/Z:[carpeta de archivos de diario]</span><span class="sxs-lookup"><span data-stu-id="5262e-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="5262e-377">Especifica una carpeta de archivos de diario para reanudar una operación.</span><span class="sxs-lookup"><span data-stu-id="5262e-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="5262e-378">AzCopy siempre admite la reanudación si una operación se ha interrumpido.</span><span class="sxs-lookup"><span data-stu-id="5262e-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="5262e-379">Si no se especifica esta opción, o se especifica sin una ruta de acceso de carpeta, AzCopy creará el archivo de diario de hello en la ubicación predeterminada de hello, que es % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5262e-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="5262e-380">Cada vez que se emite un tooAzCopy de comando, comprueba si existe un archivo de diario en la carpeta predeterminada de hello, o si se encuentra en una carpeta que especifica mediante esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="5262e-381">Si no existe el archivo de diario de Hola en cualquier lugar, AzCopy trata operación hello como nueva y genera un nuevo archivo de diario.</span><span class="sxs-lookup"><span data-stu-id="5262e-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="5262e-382">Si existe el archivo de diario de hello, AzCopy comprobará si línea de comandos de Hola de entrada coincida con Hola de línea de comandos en el archivo de diario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="5262e-383">Si coincide con dos líneas de comandos hello, AzCopy reanuda la operación incompleta de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="5262e-384">Si no coinciden, será tooeither solicitadas sobrescribir Hola diario archivo toostart una operación de nuevo o toocancel Hola operación actual.</span><span class="sxs-lookup"><span data-stu-id="5262e-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="5262e-385">archivo de diario de Hola se elimina tras la finalización correcta de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="5262e-386">Tenga en cuenta que la reanudación de una operación a partir de un archivo de diario creado por una versión anterior de AzCopy no se admite.</span><span class="sxs-lookup"><span data-stu-id="5262e-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="5262e-387">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="5262e-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="5262e-388">/@:"parameter-file"</span></span>
<span data-ttu-id="5262e-389">Especifica un archivo que contiene parámetros.</span><span class="sxs-lookup"><span data-stu-id="5262e-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="5262e-390">Procesos de AzCopy Hola parámetros en el archivo hello como si se hubieran especificado en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="5262e-391">En un archivo de respuesta, puede especificar varios parámetros en una sola línea o especificar cada parámetro en su propia línea.</span><span class="sxs-lookup"><span data-stu-id="5262e-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="5262e-392">Tenga en cuenta que un parámetro individual no puede ocupar varias líneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="5262e-393">Archivos de respuesta pueden incluir líneas de comentarios que comienzan por el símbolo # de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="5262e-394">Puede especificar varios archivos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="5262e-394">You can specify multiple response files.</span></span> <span data-ttu-id="5262e-395">Sin embargo, tenga en cuenta que AzCopy no admite archivos de respuesta anidados.</span><span class="sxs-lookup"><span data-stu-id="5262e-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="5262e-396">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="5262e-397">/Y</span><span class="sxs-lookup"><span data-stu-id="5262e-397">/Y</span></span>
<span data-ttu-id="5262e-398">Suprime todos los mensajes de confirmación de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5262e-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="5262e-399">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="5262e-400">/L</span><span class="sxs-lookup"><span data-stu-id="5262e-400">/L</span></span>
<span data-ttu-id="5262e-401">Especifica solamente una operación de descripción; no se copian datos.</span><span class="sxs-lookup"><span data-stu-id="5262e-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="5262e-402">AzCopy interpretará Hola uso de esta opción como una simulación de línea de comandos de ejecución Hola sin esta opción /L y recuento de cuántos objetos se copiarán, puede especificar la opción /V en hello en el mismo tiempo toocheck qué objetos se copiarán en el registro detallado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="5262e-403">comportamiento de Hola de esta opción también viene determinado por la ubicación de Hola Hola de datos de origen y la presencia de Hola de hello recursiva modo /S y archivo patrón opción /Pattern.</span><span class="sxs-lookup"><span data-stu-id="5262e-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="5262e-404">AzCopy requiere el permiso LISTA y LECTURA de esta ubicación de origen cuando se usa esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="5262e-405">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="5262e-406">/MT</span><span class="sxs-lookup"><span data-stu-id="5262e-406">/MT</span></span>
<span data-ttu-id="5262e-407">Establece toobe Hola igual como blob de origen de Hola o del archivo de la hora de la última modificación del archivo descargado Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="5262e-408">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="5262e-409">/XN</span><span class="sxs-lookup"><span data-stu-id="5262e-409">/XN</span></span>
<span data-ttu-id="5262e-410">Excluye un recurso origen más nuevo.</span><span class="sxs-lookup"><span data-stu-id="5262e-410">Excludes a newer source resource.</span></span> <span data-ttu-id="5262e-411">no se copiarán recursos Hola si hora de última modificación del origen de Hola de hello es hello igual o más reciente que el destino.</span><span class="sxs-lookup"><span data-stu-id="5262e-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="5262e-412">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="5262e-413">/XO</span><span class="sxs-lookup"><span data-stu-id="5262e-413">/XO</span></span>
<span data-ttu-id="5262e-414">Excluye un recurso de origen más antiguo.</span><span class="sxs-lookup"><span data-stu-id="5262e-414">Excludes an older source resource.</span></span> <span data-ttu-id="5262e-415">no se copiarán recursos Hola si hora de última modificación del origen de Hola de hello es hello igual o anterior a destino.</span><span class="sxs-lookup"><span data-stu-id="5262e-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="5262e-416">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="5262e-417">/A</span><span class="sxs-lookup"><span data-stu-id="5262e-417">/A</span></span>
<span data-ttu-id="5262e-418">Carga sólo los archivos que tienen el atributo Archive de hello establecido.</span><span class="sxs-lookup"><span data-stu-id="5262e-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="5262e-419">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="5262e-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="5262e-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="5262e-421">Solo los archivos de carga que contenga cualquiera de Hola especifican el conjunto de atributos.</span><span class="sxs-lookup"><span data-stu-id="5262e-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="5262e-422">Los atributos disponibles son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="5262e-422">Available attributes include:</span></span>

* <span data-ttu-id="5262e-423">R = Archivos de solo lectura</span><span class="sxs-lookup"><span data-stu-id="5262e-423">R = Read-only files</span></span>
* <span data-ttu-id="5262e-424">A = Archivos listos para archivarse</span><span class="sxs-lookup"><span data-stu-id="5262e-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="5262e-425">S = Archivos del sistema</span><span class="sxs-lookup"><span data-stu-id="5262e-425">S = System files</span></span>
* <span data-ttu-id="5262e-426">H = Archivos ocultos</span><span class="sxs-lookup"><span data-stu-id="5262e-426">H = Hidden files</span></span>
* <span data-ttu-id="5262e-427">C = Archivos comprimidos</span><span class="sxs-lookup"><span data-stu-id="5262e-427">C = Compressed files</span></span>
* <span data-ttu-id="5262e-428">N = Archivos normales</span><span class="sxs-lookup"><span data-stu-id="5262e-428">N = Normal files</span></span>
* <span data-ttu-id="5262e-429">E = Archivos cifrados</span><span class="sxs-lookup"><span data-stu-id="5262e-429">E = Encrypted files</span></span>
* <span data-ttu-id="5262e-430">T = Archivos temporales</span><span class="sxs-lookup"><span data-stu-id="5262e-430">T = Temporary files</span></span>
* <span data-ttu-id="5262e-431">O = Archivos fuera de línea</span><span class="sxs-lookup"><span data-stu-id="5262e-431">O = Offline files</span></span>
* <span data-ttu-id="5262e-432">I = Archivos no indexados</span><span class="sxs-lookup"><span data-stu-id="5262e-432">I = Non-indexed files</span></span>

<span data-ttu-id="5262e-433">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="5262e-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="5262e-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="5262e-435">Excluye los archivos que contengan cualquiera de hello especificado establecido algún atributo.</span><span class="sxs-lookup"><span data-stu-id="5262e-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="5262e-436">Los atributos disponibles son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="5262e-436">Available attributes include:</span></span>

* <span data-ttu-id="5262e-437">R = Archivos de solo lectura</span><span class="sxs-lookup"><span data-stu-id="5262e-437">R = Read-only files</span></span>
* <span data-ttu-id="5262e-438">A = Archivos listos para archivarse</span><span class="sxs-lookup"><span data-stu-id="5262e-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="5262e-439">S = Archivos del sistema</span><span class="sxs-lookup"><span data-stu-id="5262e-439">S = System files</span></span>
* <span data-ttu-id="5262e-440">H = Archivos ocultos</span><span class="sxs-lookup"><span data-stu-id="5262e-440">H = Hidden files</span></span>
* <span data-ttu-id="5262e-441">C = Archivos comprimidos</span><span class="sxs-lookup"><span data-stu-id="5262e-441">C = Compressed files</span></span>
* <span data-ttu-id="5262e-442">N = Archivos normales</span><span class="sxs-lookup"><span data-stu-id="5262e-442">N = Normal files</span></span>
* <span data-ttu-id="5262e-443">E = Archivos cifrados</span><span class="sxs-lookup"><span data-stu-id="5262e-443">E = Encrypted files</span></span>
* <span data-ttu-id="5262e-444">T = Archivos temporales</span><span class="sxs-lookup"><span data-stu-id="5262e-444">T = Temporary files</span></span>
* <span data-ttu-id="5262e-445">O = Archivos fuera de línea</span><span class="sxs-lookup"><span data-stu-id="5262e-445">O = Offline files</span></span>
* <span data-ttu-id="5262e-446">I = Archivos no indexados</span><span class="sxs-lookup"><span data-stu-id="5262e-446">I = Non-indexed files</span></span>

<span data-ttu-id="5262e-447">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="5262e-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="5262e-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="5262e-449">Indica el carácter de delimitador de hello usa toodelimit los directorios virtuales en un nombre de blob.</span><span class="sxs-lookup"><span data-stu-id="5262e-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="5262e-450">De forma predeterminada, AzCopy utiliza / como carácter de delimitador de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="5262e-451">Sin embargo, AzCopy admite el uso de cualquier carácter convencional (como @, # o %) como delimitador.</span><span class="sxs-lookup"><span data-stu-id="5262e-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="5262e-452">Si necesita tooinclude uno de estos caracteres especiales en la línea de comandos de hello, ponga el nombre de archivo de hello entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="5262e-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="5262e-453">Esta opción solamente se aplica para descarga de blobs.</span><span class="sxs-lookup"><span data-stu-id="5262e-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="5262e-454">**Aplicable a:** blobs</span><span class="sxs-lookup"><span data-stu-id="5262e-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="5262e-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="5262e-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="5262e-456">Especifica el número de Hola de operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="5262e-457">AzCopy forma predeterminada, inicia un número determinado de rendimiento de transferencia de datos de las operaciones simultáneas tooincrease Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="5262e-458">Tenga en cuenta que gran número de operaciones simultáneas en un entorno de ancho de banda bajo puede saturar la conexión de red de Hola y evitar las operaciones de hello complete totalmente.</span><span class="sxs-lookup"><span data-stu-id="5262e-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="5262e-459">Reduzca el número de operaciones simultáneas basándose en el ancho de banda de red disponible real.</span><span class="sxs-lookup"><span data-stu-id="5262e-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="5262e-460">límite superior de Hola para las operaciones simultáneas es 512.</span><span class="sxs-lookup"><span data-stu-id="5262e-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="5262e-461">**Aplicable a:** blobs, archivos, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="5262e-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="5262e-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="5262e-463">Especifica que hello `source` recurso es un blob disponible en el entorno de desarrollo local hello, ejecute en un emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="5262e-464">**Aplicable a:** blobs, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="5262e-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="5262e-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="5262e-466">Especifica que hello `destination` recurso es un blob disponible en el entorno de desarrollo local hello, ejecute en un emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="5262e-467">**Aplicable a:** blobs, tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="5262e-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="5262e-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="5262e-469">Divisiones Hola tooenable de intervalo de claves de partición exportar datos de la tabla en paralelo, lo que aumenta la velocidad de Hola de operación de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="5262e-470">Si no se especifica esta opción, AzCopy utiliza un entidades de tabla de tooexport de subproceso único.</span><span class="sxs-lookup"><span data-stu-id="5262e-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="5262e-471">Por ejemplo, si hello usuario especifica /PKRS: "aa #bb" y, a continuación, AzCopy inicia tres operaciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="5262e-472">Cada operación exporta uno de los tres rangos de claves de partición, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="5262e-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="5262e-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="5262e-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="5262e-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="5262e-474">[aa, bb)</span></span>

  <span data-ttu-id="5262e-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="5262e-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="5262e-476">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="5262e-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="5262e-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="5262e-478">Especifica Hola archivo exportado dividir tamaño en MB, Hola valor mínimo permitido es de 32.</span><span class="sxs-lookup"><span data-stu-id="5262e-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="5262e-479">Si no se especifica esta opción, AzCopy exportará toosingle archivo de datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="5262e-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="5262e-480">Si datos de la tabla de hello están blob tooa exportado y tamaño del archivo exportado hello alcanza límite de 200 GB de hello para el tamaño del blob, AzCopy dividirá Hola archivo exportado, incluso si no se especifica esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="5262e-481">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="5262e-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="5262e-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="5262e-483">Especifica el comportamiento de importación de datos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="5262e-484">InsertOrSkip - omite una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="5262e-485">InsertOrMerge - combina una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="5262e-486">InsertOrReplace - reemplaza una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="5262e-487">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="5262e-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="5262e-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="5262e-489">Especifica el archivo de manifiesto de Hola para tabla Hola exportación e importación de operación.</span><span class="sxs-lookup"><span data-stu-id="5262e-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="5262e-490">Esta opción es opcional durante la operación de exportación de hello, AzCopy generará un archivo de manifiesto con nombre predefinido si no se especifica esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="5262e-491">Esta opción es necesaria durante la operación de importación de Hola para buscar archivos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="5262e-492">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="5262e-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="5262e-493">/SyncCopy</span></span>
<span data-ttu-id="5262e-494">Indica si toosynchronously copiar blobs o archivos entre dos extremos de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5262e-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="5262e-495">De forma predeterminada, AzCopy usa la copia asincrónica del servidor.</span><span class="sxs-lookup"><span data-stu-id="5262e-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="5262e-496">Especifique este tooperform opción sincrónica copy, que descarga de blobs o archivos toolocal memoria y, a continuación, carga tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5262e-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="5262e-497">Puede usar esta opción cuando se copian archivos dentro del almacenamiento de blobs, almacenamiento de archivos, o desde Blob almacenamiento tooFile almacenamiento o viceversa.</span><span class="sxs-lookup"><span data-stu-id="5262e-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="5262e-498">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="5262e-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="5262e-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="5262e-500">Especifica el tipo de contenido MIME de Hola de blobs de destino o los archivos.</span><span class="sxs-lookup"><span data-stu-id="5262e-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="5262e-501">Conjuntos de AzCopy Hola de tipo de contenido para un blob o tooapplication/octet-stream de archivos de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5262e-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="5262e-502">Puede establecer el tipo de contenido de Hola para todos los blobs o archivos especificando explícitamente un valor para esta opción.</span><span class="sxs-lookup"><span data-stu-id="5262e-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="5262e-503">Si especifica esta opción sin ningún valor, AzCopy establecerá cada blob o tipo de contenido del archivo según tooits extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="5262e-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="5262e-504">**Aplicable a:** blobs, archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="5262e-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="5262e-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="5262e-506">Especifica el formato de Hola Hola datos exportados del archivo de tabla.</span><span class="sxs-lookup"><span data-stu-id="5262e-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="5262e-507">Si no se especifica esta opción, de forma predeterminada, AzCopy exporta el archivo de datos de tabla en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="5262e-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="5262e-508">**Aplicable a:** tablas</span><span class="sxs-lookup"><span data-stu-id="5262e-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="5262e-509">Problemas conocidos y prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="5262e-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="5262e-510">Limitación de escrituras concurrentes mientras se copian datos</span><span class="sxs-lookup"><span data-stu-id="5262e-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="5262e-511">Cuando copia blobs o archivos con AzCopy, tenga en cuenta que otra aplicación puede modificar datos de hello mientras que va a copiar.</span><span class="sxs-lookup"><span data-stu-id="5262e-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="5262e-512">Si es posible, asegúrese de que los datos de hello que va a copiar no se está modificando durante la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="5262e-513">Por ejemplo, al copiar un disco duro virtual asociado a una máquina virtual de Azure, asegúrese de que ninguna otra aplicación actualmente está escribiendo toohello disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="5262e-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="5262e-514">Una buena manera toodo es mediante la concesión de hello recursos toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="5262e-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="5262e-515">Como alternativa, puede crear una instantánea de disco duro virtual de hello en primer lugar y, a continuación, copiar instantáneas Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="5262e-516">Si no se puede impedir que otras aplicaciones escribir tooblobs o archivos mientras se se copian y tenga en cuenta que al trabajo Hola Hola finaliza, hello recursos copiados pueden ya no tiene paridad completa con recursos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="5262e-517">Ejecutar una instancia de AzCopy en un solo equipo.</span><span class="sxs-lookup"><span data-stu-id="5262e-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="5262e-518">AzCopy es toomaximize diseñada Hola utilización de la transferencia de datos de máquina recursos tooaccelerate hello, le recomendamos que ejecute solo una instancia de AzCopy en un equipo y especifica la opción de hello `/NC` si necesita las operaciones más simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5262e-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="5262e-519">Para obtener más información, escriba `AzCopy /?:NC` en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5262e-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="5262e-520">Habilitar algoritmos MD5 que cumplan con FIPS para AzCopy cuando "Use algoritmos que cumplen con FIPS para el cifrado, firma y operaciones hash".</span><span class="sxs-lookup"><span data-stu-id="5262e-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="5262e-521">AzCopy predeterminada usa hello toocalculate de implementación .NET MD5 MD5 al copiar los objetos, pero hay algunos requisitos de seguridad que necesitan AzCopy tooenable FIPS MD5 comprobar si es compatible.</span><span class="sxs-lookup"><span data-stu-id="5262e-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="5262e-522">Puede crear un archivo app.config `AzCopy.exe.config` con la propiedad `AzureStorageUseV1MD5` y separarlo con AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="5262e-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="5262e-523">Para la propiedad "AzureStorageUseV1MD5" • True: valor predeterminado de hello, AzCopy utilizará implementación MD5. NET.</span><span class="sxs-lookup"><span data-stu-id="5262e-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="5262e-524">• False: AzCopy utilizará el algoritmo de MD5 compatible con FIPS.</span><span class="sxs-lookup"><span data-stu-id="5262e-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="5262e-525">Tenga en cuenta que los algoritmos compatibles con FIPS están deshabilitados de forma predeterminada en el equipo de Windows, puede escribir secpol.msc en la ventana de ejecución y comprobar este modificador en Configuración de seguridad -> Directivas locales -> Opciones de seguridad -> Criptografía de sistema: Usar algoritmos compatibles con FIPS para cifrado, firma y operaciones hash.</span><span class="sxs-lookup"><span data-stu-id="5262e-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5262e-526">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5262e-526">Next steps</span></span>
<span data-ttu-id="5262e-527">Para obtener más información sobre el almacenamiento de Azure y AzCopy, consulte toohello recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="5262e-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="5262e-528">Documentación de Almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="5262e-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="5262e-529">Introducción tooAzure almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5262e-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="5262e-530">¿Cómo toouse almacenamiento de blobs en .NET</span><span class="sxs-lookup"><span data-stu-id="5262e-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="5262e-531">¿Cómo toouse almacenamiento de archivos de .NET</span><span class="sxs-lookup"><span data-stu-id="5262e-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="5262e-532">¿Cómo toouse almacenamiento de tablas de .NET</span><span class="sxs-lookup"><span data-stu-id="5262e-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="5262e-533">Cómo administrar toocreate, o eliminar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5262e-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="5262e-534">Transferencia de datos con AzCopy en Linux</span><span class="sxs-lookup"><span data-stu-id="5262e-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="5262e-535">Publicaciones en blobs de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5262e-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="5262e-536">Introducción a la versión de vista previa de la biblioteca de movimiento de datos de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5262e-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="5262e-537">AzCopy: Introducción a la copia sincrónica y el tipo de contenido personalizado</span><span class="sxs-lookup"><span data-stu-id="5262e-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="5262e-538">AzCopy: Presentación de la disponibilidad general de AzCopy 3.0 y de la versión de vista previa de AzCopy 4.0 compatible con tablas y archivos</span><span class="sxs-lookup"><span data-stu-id="5262e-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="5262e-539">AzCopy: Optimizada para escenarios de copia a gran escala</span><span class="sxs-lookup"><span data-stu-id="5262e-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="5262e-540">AzCopy: Compatibilidad para almacenamiento con redundancia geográfica de acceso de lectura</span><span class="sxs-lookup"><span data-stu-id="5262e-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="5262e-541">AzCopy: Transferencia de datos con modo reiniciable y token SAS</span><span class="sxs-lookup"><span data-stu-id="5262e-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="5262e-542">AzCopy: Uso de copia de blobs entre cuentas</span><span class="sxs-lookup"><span data-stu-id="5262e-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="5262e-543">AzCopy: Carga y descarga de archivos para blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="5262e-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

