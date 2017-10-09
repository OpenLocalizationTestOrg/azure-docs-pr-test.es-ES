---
title: "trabajo - v1 de importación de aaaSample flujo de trabajo tooprep unidades de disco duro para una importación y exportación de Azure | Documentos de Microsoft"
description: "Vea un tutorial para completar el proceso de preparar las unidades para un trabajo de importación en el servicio de importación y exportación de Hola Hola."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="ee5a5-103">Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="ee5a5-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="ee5a5-104">Este tema explica cómo completar el proceso de Hola de preparar las unidades para un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="ee5a5-105">Este ejemplo importan Hola después de datos en una cuenta de almacenamiento de Windows Azure denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="ee5a5-106">Ubicación</span><span class="sxs-lookup"><span data-stu-id="ee5a5-106">Location</span></span>|<span data-ttu-id="ee5a5-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee5a5-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="ee5a5-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="ee5a5-108">H:\Video</span></span>|<span data-ttu-id="ee5a5-109">Una colección de vídeos, 5 TB en total.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="ee5a5-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ee5a5-110">H:\Photo</span></span>|<span data-ttu-id="ee5a5-111">Una colección de fotos, 30 GB en total.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="ee5a5-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ee5a5-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ee5a5-113">Una imagen de disco Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="ee5a5-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ee5a5-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="ee5a5-115">Una colección de archivos de música en un recurso compartido de red, 10 GB en total.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="ee5a5-116">trabajo de importación de Hello importará estos datos en hello después de destinos en la cuenta de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="ee5a5-117">Origen</span><span class="sxs-lookup"><span data-stu-id="ee5a5-117">Source</span></span>|<span data-ttu-id="ee5a5-118">Directorio virtual o blob de destino</span><span class="sxs-lookup"><span data-stu-id="ee5a5-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="ee5a5-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="ee5a5-119">H:\Video</span></span>|<span data-ttu-id="ee5a5-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ee5a5-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="ee5a5-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ee5a5-121">H:\Photo</span></span>|<span data-ttu-id="ee5a5-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="ee5a5-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="ee5a5-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ee5a5-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ee5a5-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ee5a5-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="ee5a5-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ee5a5-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="ee5a5-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="ee5a5-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="ee5a5-127">Con esta asignación, Hola archivo `H:\Video\Drama\GreatMovie.mov` será toohello importados blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="ee5a5-128">Después, toodetermine cuántas unidades de disco duro son necesarias, tamaño de Hola de cálculo de los datos de hello:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="ee5a5-129">En este ejemplo, dos unidades de disco duro de 3TB deberían ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="ee5a5-130">Sin embargo, desde el directorio de origen de hello `H:\Video` tiene 5TB de datos y la capacidad de la unidad de disco duro es solo 3TB, es necesario toobreak `H:\Video` en dos directorios más pequeños antes de ejecutar Hola herramienta de importación y exportación de Microsoft Azure: `H:\Video1` y `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="ee5a5-131">Este paso produce Hola siguiendo los directorios de origen:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="ee5a5-132">Ubicación</span><span class="sxs-lookup"><span data-stu-id="ee5a5-132">Location</span></span>|<span data-ttu-id="ee5a5-133">Tamaño</span><span class="sxs-lookup"><span data-stu-id="ee5a5-133">Size</span></span>|<span data-ttu-id="ee5a5-134">Directorio virtual o blob de destino</span><span class="sxs-lookup"><span data-stu-id="ee5a5-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="ee5a5-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="ee5a5-135">H:\Video1</span></span>|<span data-ttu-id="ee5a5-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-136">2.5TB</span></span>|<span data-ttu-id="ee5a5-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ee5a5-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="ee5a5-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="ee5a5-138">H:\Video2</span></span>|<span data-ttu-id="ee5a5-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-139">2.5TB</span></span>|<span data-ttu-id="ee5a5-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ee5a5-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="ee5a5-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ee5a5-141">H:\Photo</span></span>|<span data-ttu-id="ee5a5-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-142">30GB</span></span>|<span data-ttu-id="ee5a5-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="ee5a5-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="ee5a5-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ee5a5-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="ee5a5-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-145">25GB</span></span>|<span data-ttu-id="ee5a5-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ee5a5-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="ee5a5-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ee5a5-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="ee5a5-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-148">10GB</span></span>|<span data-ttu-id="ee5a5-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="ee5a5-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="ee5a5-150">Tenga en cuenta que aunque Hola `H:\Video`directory se ha dividido tootwo directorios, señalan toohello mismo directorio virtual de destino en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="ee5a5-151">De esta manera, todos los archivos de vídeo se mantienen en un único `video` contenedor en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="ee5a5-152">A continuación, Hola por encima del origen de directorios se uniformemente distribuidas toohello dos unidades de disco duro:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="ee5a5-153">Unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="ee5a5-153">Hard drive</span></span>|<span data-ttu-id="ee5a5-154">Directorios de origen</span><span class="sxs-lookup"><span data-stu-id="ee5a5-154">Source directories</span></span>|<span data-ttu-id="ee5a5-155">Tamaño total</span><span class="sxs-lookup"><span data-stu-id="ee5a5-155">Total size</span></span>|  
|<span data-ttu-id="ee5a5-156">Primera unidad</span><span class="sxs-lookup"><span data-stu-id="ee5a5-156">First Drive</span></span>|<span data-ttu-id="ee5a5-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="ee5a5-157">H:\Video1</span></span>|<span data-ttu-id="ee5a5-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="ee5a5-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ee5a5-159">H:\Photo</span></span>||  
|<span data-ttu-id="ee5a5-160">Segunda unidad</span><span class="sxs-lookup"><span data-stu-id="ee5a5-160">Second Drive</span></span>|<span data-ttu-id="ee5a5-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="ee5a5-161">H:\Video2</span></span>|<span data-ttu-id="ee5a5-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="ee5a5-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="ee5a5-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="ee5a5-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="ee5a5-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ee5a5-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="ee5a5-165">Además, puede establecer Hola después de metadatos para todos los archivos:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="ee5a5-166">**UploadMethod:** servicio Microsoft Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="ee5a5-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="ee5a5-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="ee5a5-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="ee5a5-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="ee5a5-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="ee5a5-169">tooset metadatos para los archivos de hello importado, cree un archivo de texto, `c:\WAImportExport\SampleMetadata.txt`, con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="ee5a5-170">También puede establecer algunas propiedades para hello `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="ee5a5-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="ee5a5-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="ee5a5-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="ee5a5-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="ee5a5-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="ee5a5-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="ee5a5-174">tooset estas propiedades, cree un archivo de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="ee5a5-175">Ahora está listo toorun Hola herramienta de importación y exportación de Azure tooprepare Hola dos unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="ee5a5-176">Observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-176">Note that:</span></span>  
  
-   <span data-ttu-id="ee5a5-177">Hola primera unidad se monta como unidad X.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="ee5a5-178">Hola segunda unidad se monta como unidad Y.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="ee5a5-179">Hola clave Hola cuenta de almacenamiento `mystorageaccount` es `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="ee5a5-180">Preparación del disco para la importación cuando los datos se han cargado previamente</span><span class="sxs-lookup"><span data-stu-id="ee5a5-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="ee5a5-181">Si ya está presente en el disco de Hola Hola toobe de datos importado, utilice Hola marca /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="ee5a5-182">Valor de /t y /srcdir debe apuntar disco toohello que se está preparando para la importación.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="ee5a5-183">Si no todos Hola datos en disco de hello necesita toogo toohello mismo directorio virtual de destino o raíz de cuenta de almacenamiento Hola Hola ejecución mismo comando para cada directorio mantener por separado de valor de Hola de /id mismo a través de todas las ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="ee5a5-184">No especifique/Format, dado que borrar datos de hello en el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="ee5a5-185">Puede especificar / cifrar o /bk dependiendo de si el disco de hello ya está cifrado o no.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="ee5a5-186">Copia de sesiones: primera unidad</span><span class="sxs-lookup"><span data-stu-id="ee5a5-186">Copy sessions - first drive</span></span>

<span data-ttu-id="ee5a5-187">Para la primera unidad de hello, ejecute hello herramienta de importación y exportación de Azure de origen dos veces hello toocopy dos directorios:</span><span class="sxs-lookup"><span data-stu-id="ee5a5-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="ee5a5-188">**Primera sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="ee5a5-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="ee5a5-189">**Segunda sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="ee5a5-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="ee5a5-190">Copia de sesiones: segunda unidad</span><span class="sxs-lookup"><span data-stu-id="ee5a5-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="ee5a5-191">Para hello segunda unidad, ejecute Hola herramienta de importación y exportación de Azure tres veces, una vez cada uno de ellos para hello directorios de origen y una vez para independiente de hello Blu-Ray™ archivo de imagen):</span><span class="sxs-lookup"><span data-stu-id="ee5a5-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="ee5a5-192">**Primera sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="ee5a5-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="ee5a5-193">**Segunda sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="ee5a5-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="ee5a5-194">**Tercera sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="ee5a5-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="ee5a5-195">Finalización de la sesión de copia</span><span class="sxs-lookup"><span data-stu-id="ee5a5-195">Copy session completion</span></span>

<span data-ttu-id="ee5a5-196">Una vez completaron las sesiones de copia de hello, puede desconectarse dos unidades de Hola de equipo de copia de Hola y enviarlas toohello centro de datos de Windows Azure adecuado.</span><span class="sxs-lookup"><span data-stu-id="ee5a5-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="ee5a5-197">Cargue archivos de diario de hello dos, `FirstDrive.jrn` y `SecondDrive.jrn`, cuando se crea el trabajo de importación de hello en hello [Portal de administración de Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="ee5a5-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ee5a5-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee5a5-198">Next steps</span></span>

* [<span data-ttu-id="ee5a5-199">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="ee5a5-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* <span data-ttu-id="ee5a5-200">[Quick reference for frequently used commands for import jobs](storage-import-export-tool-quick-reference-v1.md) (Referencia rápida para comandos usados con frecuencia)</span><span class="sxs-lookup"><span data-stu-id="ee5a5-200">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md)</span></span> 
