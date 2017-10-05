---
title: "Flujo de trabajo de ejemplo para preparar unidades de disco duro para un trabajo de importación de Azure Import/Export (versión 1) | Microsoft Docs"
description: "Vea un tutorial para conocer el proceso completo de preparación de las unidades para un trabajo de importación en el servicio Azure Import/Export."
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
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="982b8-103">Flujo de trabajo de ejemplo para preparar las unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="982b8-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="982b8-104">Este tema le guiará por el proceso completo de preparar las unidades para un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="982b8-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="982b8-105">Este ejemplo importa los datos siguientes en una cuenta de Azure Storage denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="982b8-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="982b8-106">Ubicación</span><span class="sxs-lookup"><span data-stu-id="982b8-106">Location</span></span>|<span data-ttu-id="982b8-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="982b8-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="982b8-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="982b8-108">H:\Video</span></span>|<span data-ttu-id="982b8-109">Una colección de vídeos, 5 TB en total.</span><span class="sxs-lookup"><span data-stu-id="982b8-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="982b8-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="982b8-110">H:\Photo</span></span>|<span data-ttu-id="982b8-111">Una colección de fotos, 30 GB en total.</span><span class="sxs-lookup"><span data-stu-id="982b8-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="982b8-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="982b8-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="982b8-113">Una imagen de disco Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="982b8-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="982b8-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="982b8-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="982b8-115">Una colección de archivos de música en un recurso compartido de red, 10 GB en total.</span><span class="sxs-lookup"><span data-stu-id="982b8-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="982b8-116">El trabajo de importación importará estos datos en los siguientes destinos en la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="982b8-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="982b8-117">Origen</span><span class="sxs-lookup"><span data-stu-id="982b8-117">Source</span></span>|<span data-ttu-id="982b8-118">Directorio virtual o blob de destino</span><span class="sxs-lookup"><span data-stu-id="982b8-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="982b8-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="982b8-119">H:\Video</span></span>|<span data-ttu-id="982b8-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="982b8-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="982b8-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="982b8-121">H:\Photo</span></span>|<span data-ttu-id="982b8-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="982b8-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="982b8-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="982b8-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="982b8-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="982b8-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="982b8-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="982b8-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="982b8-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="982b8-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="982b8-127">Con esta asignación, el archivo `H:\Video\Drama\GreatMovie.mov` se importará al blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="982b8-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="982b8-128">A continuación, para determinar cuántas unidades de disco duro se necesitan, calcule el tamaño de los datos:</span><span class="sxs-lookup"><span data-stu-id="982b8-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="982b8-129">En este ejemplo, dos unidades de disco duro de 3TB deberían ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="982b8-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="982b8-130">Sin embargo, dado que el directorio de origen `H:\Video` tiene 5 TB de datos y la capacidad de la unidad de disco duro es de solo 3 TB, es necesario dividir `H:\Video` en dos directorios más pequeños antes de ejecutar la herramienta Microsoft Azure Import/Export: `H:\Video1` y `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="982b8-130">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="982b8-131">Este paso genera los siguientes directorios de origen:</span><span class="sxs-lookup"><span data-stu-id="982b8-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="982b8-132">Ubicación</span><span class="sxs-lookup"><span data-stu-id="982b8-132">Location</span></span>|<span data-ttu-id="982b8-133">Tamaño</span><span class="sxs-lookup"><span data-stu-id="982b8-133">Size</span></span>|<span data-ttu-id="982b8-134">Directorio virtual o blob de destino</span><span class="sxs-lookup"><span data-stu-id="982b8-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="982b8-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="982b8-135">H:\Video1</span></span>|<span data-ttu-id="982b8-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="982b8-136">2.5TB</span></span>|<span data-ttu-id="982b8-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="982b8-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="982b8-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="982b8-138">H:\Video2</span></span>|<span data-ttu-id="982b8-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="982b8-139">2.5TB</span></span>|<span data-ttu-id="982b8-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="982b8-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="982b8-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="982b8-141">H:\Photo</span></span>|<span data-ttu-id="982b8-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="982b8-142">30GB</span></span>|<span data-ttu-id="982b8-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="982b8-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="982b8-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="982b8-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="982b8-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="982b8-145">25GB</span></span>|<span data-ttu-id="982b8-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="982b8-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="982b8-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="982b8-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="982b8-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="982b8-148">10GB</span></span>|<span data-ttu-id="982b8-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="982b8-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="982b8-150">Tenga en cuenta que aunque el directorio `H:\Video` se ha dividido en dos directorios, ambos apuntan al mismo directorio virtual de destino en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="982b8-150">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="982b8-151">De esta manera, todos los archivos de vídeo se mantienen en un único contenedor `video` en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="982b8-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="982b8-152">A continuación, los directorios de origen anteriores se distribuyen uniformemente en las dos unidades de disco duro:</span><span class="sxs-lookup"><span data-stu-id="982b8-152">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="982b8-153">Unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="982b8-153">Hard drive</span></span>|<span data-ttu-id="982b8-154">Directorios de origen</span><span class="sxs-lookup"><span data-stu-id="982b8-154">Source directories</span></span>|<span data-ttu-id="982b8-155">Tamaño total</span><span class="sxs-lookup"><span data-stu-id="982b8-155">Total size</span></span>|  
|<span data-ttu-id="982b8-156">Primera unidad</span><span class="sxs-lookup"><span data-stu-id="982b8-156">First Drive</span></span>|<span data-ttu-id="982b8-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="982b8-157">H:\Video1</span></span>|<span data-ttu-id="982b8-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="982b8-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="982b8-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="982b8-159">H:\Photo</span></span>||  
|<span data-ttu-id="982b8-160">Segunda unidad</span><span class="sxs-lookup"><span data-stu-id="982b8-160">Second Drive</span></span>|<span data-ttu-id="982b8-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="982b8-161">H:\Video2</span></span>|<span data-ttu-id="982b8-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="982b8-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="982b8-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="982b8-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="982b8-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="982b8-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="982b8-165">Además, puede establecer los metadatos siguientes para todos los archivos:</span><span class="sxs-lookup"><span data-stu-id="982b8-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="982b8-166">**UploadMethod:** servicio Microsoft Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="982b8-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="982b8-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="982b8-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="982b8-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="982b8-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="982b8-169">Para establecer los metadatos de los archivos importados, cree un archivo de texto, `c:\WAImportExport\SampleMetadata.txt`, con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="982b8-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="982b8-170">También puede establecer algunas propiedades para el blob `FavoriteMovie.ISO`:</span><span class="sxs-lookup"><span data-stu-id="982b8-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="982b8-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="982b8-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="982b8-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="982b8-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="982b8-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="982b8-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="982b8-174">Para establecer estas propiedades, cree un archivo de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="982b8-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="982b8-175">Ahora está listo para ejecutar la herramienta Azure Import/Export para preparar las dos unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="982b8-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="982b8-176">Observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="982b8-176">Note that:</span></span>  
  
-   <span data-ttu-id="982b8-177">La primera unidad se monta como unidad X.</span><span class="sxs-lookup"><span data-stu-id="982b8-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="982b8-178">La segunda unidad se monta como unidad Y.</span><span class="sxs-lookup"><span data-stu-id="982b8-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="982b8-179">La clave para la cuenta de almacenamiento `mystorageaccount` es `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="982b8-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="982b8-180">Preparación del disco para la importación cuando los datos se han cargado previamente</span><span class="sxs-lookup"><span data-stu-id="982b8-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="982b8-181">Si los datos que se van a importar ya están presentes en el disco, use la marca /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="982b8-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="982b8-182">Tanto el valor de /t como de /srcdir deben apuntar al disco que se está preparando para la importación.</span><span class="sxs-lookup"><span data-stu-id="982b8-182">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="982b8-183">Si no es necesario que todos los datos del disco vayan al mismo directorio virtual de destino o raíz de la cuenta de almacenamiento, ejecute el mismo comando para cada directorio por separado manteniendo el valor de/id igual en todas las ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="982b8-183">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="982b8-184">No especifique /format, porque borrará los datos del disco.</span><span class="sxs-lookup"><span data-stu-id="982b8-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="982b8-185">Puede especificar /encrypt o /bk dependiendo de si el disco ya está cifrado o no.</span><span class="sxs-lookup"><span data-stu-id="982b8-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="982b8-186">Copia de sesiones: primera unidad</span><span class="sxs-lookup"><span data-stu-id="982b8-186">Copy sessions - first drive</span></span>

<span data-ttu-id="982b8-187">Para la primera unidad, ejecute la herramienta Azure Import/Export dos veces para copiar los dos directorios de origen:</span><span class="sxs-lookup"><span data-stu-id="982b8-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="982b8-188">**Primera sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="982b8-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="982b8-189">**Segunda sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="982b8-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="982b8-190">Copia de sesiones: segunda unidad</span><span class="sxs-lookup"><span data-stu-id="982b8-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="982b8-191">Para la segunda unidad, ejecute la herramienta Azure Import/Export tres veces, una para cada uno de los directorios de origen y otra para el archivo de imagen independiente Blu-Ray™:</span><span class="sxs-lookup"><span data-stu-id="982b8-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="982b8-192">**Primera sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="982b8-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="982b8-193">**Segunda sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="982b8-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="982b8-194">**Tercera sesión de copia**</span><span class="sxs-lookup"><span data-stu-id="982b8-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="982b8-195">Finalización de la sesión de copia</span><span class="sxs-lookup"><span data-stu-id="982b8-195">Copy session completion</span></span>

<span data-ttu-id="982b8-196">Cuando se hayan completado las sesiones de copia, podrá desconectar las dos unidades del equipo de copia y enviarlas al centro de datos de Microsoft Azure adecuado.</span><span class="sxs-lookup"><span data-stu-id="982b8-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="982b8-197">Cargará los dos archivos de diario, `FirstDrive.jrn` y `SecondDrive.jrn`, cuando cree el trabajo de importación en el [Portal de administración de Microsoft Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="982b8-197">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="982b8-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="982b8-198">Next steps</span></span>

* [<span data-ttu-id="982b8-199">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="982b8-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* <span data-ttu-id="982b8-200">[Quick reference for frequently used commands for import jobs](storage-import-export-tool-quick-reference-v1.md) (Referencia rápida para comandos usados con frecuencia)</span><span class="sxs-lookup"><span data-stu-id="982b8-200">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md)</span></span> 
