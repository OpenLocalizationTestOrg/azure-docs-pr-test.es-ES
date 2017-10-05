---
title: "Flujo de trabajo de ejemplo para preparar unidades de disco duro para un trabajo de importación de Azure Import/Export | Microsoft Docs"
description: "Vea un tutorial para conocer el proceso completo de preparación de las unidades para un trabajo de importación en el servicio Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 78d7ce3bbd3205fd995ba331af08d830097c8156
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="760de-103">Flujo de trabajo de ejemplo para preparar las unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="760de-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="760de-104">Este artículo le guiará por el proceso completo de preparar las unidades para un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="760de-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="760de-105">Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="760de-105">Sample data</span></span>

<span data-ttu-id="760de-106">Este ejemplo importa los datos siguientes en una cuenta de Azure Storage denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="760de-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="760de-107">Ubicación</span><span class="sxs-lookup"><span data-stu-id="760de-107">Location</span></span>|<span data-ttu-id="760de-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="760de-108">Description</span></span>|<span data-ttu-id="760de-109">Tamaño de los datos</span><span class="sxs-lookup"><span data-stu-id="760de-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="760de-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="760de-110">H:\Video\\</span></span> |<span data-ttu-id="760de-111">Una colección de vídeos</span><span class="sxs-lookup"><span data-stu-id="760de-111">A collection of videos</span></span>|<span data-ttu-id="760de-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="760de-112">12 TB</span></span>|
|<span data-ttu-id="760de-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="760de-113">H:\Photo\\</span></span> |<span data-ttu-id="760de-114">Una colección de fotos</span><span class="sxs-lookup"><span data-stu-id="760de-114">A collection of photos</span></span>|<span data-ttu-id="760de-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="760de-115">30 GB</span></span>|
|<span data-ttu-id="760de-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="760de-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="760de-117">Una imagen de disco Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="760de-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="760de-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="760de-118">25 GB</span></span>|
|<span data-ttu-id="760de-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="760de-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="760de-120">Una colección de archivos de música en un recurso compartido de red</span><span class="sxs-lookup"><span data-stu-id="760de-120">A collection of music files on a network share</span></span>|<span data-ttu-id="760de-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="760de-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="760de-122">Destinos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="760de-122">Storage account destinations</span></span>

<span data-ttu-id="760de-123">El trabajo de importación importará los datos en los siguientes destinos en la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="760de-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="760de-124">Origen</span><span class="sxs-lookup"><span data-stu-id="760de-124">Source</span></span>|<span data-ttu-id="760de-125">Directorio virtual o blob de destino</span><span class="sxs-lookup"><span data-stu-id="760de-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="760de-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="760de-126">H:\Video\\</span></span> |<span data-ttu-id="760de-127">video/</span><span class="sxs-lookup"><span data-stu-id="760de-127">video/</span></span>|
|<span data-ttu-id="760de-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="760de-128">H:\Photo\\</span></span> |<span data-ttu-id="760de-129">photo/</span><span class="sxs-lookup"><span data-stu-id="760de-129">photo/</span></span>|
|<span data-ttu-id="760de-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="760de-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="760de-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="760de-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="760de-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="760de-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="760de-133">music</span><span class="sxs-lookup"><span data-stu-id="760de-133">music</span></span>|

<span data-ttu-id="760de-134">Con esta asignación, el archivo `H:\Video\Drama\GreatMovie.mov` se importará al blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="760de-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="760de-135">Determinación de los requisitos de la unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="760de-135">Determine hard drive requirements</span></span>

<span data-ttu-id="760de-136">A continuación, para determinar cuántas unidades de disco duro se necesitan, calcule el tamaño de los datos:</span><span class="sxs-lookup"><span data-stu-id="760de-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="760de-137">En este ejemplo, dos unidades de disco duro de 8 TB deberían ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="760de-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="760de-138">Sin embargo, dado que el directorio de origen `H:\Video` tiene 12 TB de datos y la capacidad de la unidad de disco duro es de solo 8 TB, podrá especificarlo de la siguiente manera en el archivo **driveset.csv**:</span><span class="sxs-lookup"><span data-stu-id="760de-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="760de-139">La herramienta distribuirá datos en las dos unidades de disco duro de forma optimizada.</span><span class="sxs-lookup"><span data-stu-id="760de-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="760de-140">Conexión de unidades y configuración del trabajo</span><span class="sxs-lookup"><span data-stu-id="760de-140">Attach drives and configure the job</span></span>
<span data-ttu-id="760de-141">Conectará ambos discos a la máquina y creará volúmenes.</span><span class="sxs-lookup"><span data-stu-id="760de-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="760de-142">Luego, cree el archivo **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="760de-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="760de-143">Además, puede establecer los metadatos siguientes para todos los archivos:</span><span class="sxs-lookup"><span data-stu-id="760de-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="760de-144">**UploadMethod:** servicio Microsoft Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="760de-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="760de-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="760de-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="760de-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="760de-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="760de-147">Para establecer los metadatos de los archivos importados, cree un archivo de texto, `c:\WAImportExport\SampleMetadata.txt`, con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="760de-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="760de-148">También puede establecer algunas propiedades para el blob `FavoriteMovie.ISO`:</span><span class="sxs-lookup"><span data-stu-id="760de-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="760de-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="760de-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="760de-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="760de-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="760de-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="760de-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="760de-152">Para establecer estas propiedades, cree un archivo de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="760de-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="760de-153">Ejecución de la herramienta Azure Import/Export (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="760de-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="760de-154">Ahora está listo para ejecutar la herramienta Azure Import/Export para preparar las dos unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="760de-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="760de-155">**Para la primera sesión:**</span><span class="sxs-lookup"><span data-stu-id="760de-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="760de-156">Si es necesario agregar más datos, cree otro archivo de conjunto de datos (con el mismo formato que Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="760de-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="760de-157">**Para la segunda sesión:**</span><span class="sxs-lookup"><span data-stu-id="760de-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="760de-158">Cuando se hayan completado las sesiones de copia, podrá desconectar las dos unidades del equipo de copia y enviarlas al centro de datos de Azure adecuado.</span><span class="sxs-lookup"><span data-stu-id="760de-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="760de-159">Cargará los dos archivos de diario, `<FirstDriveSerialNumber>.xml` y `<SecondDriveSerialNumber>.xml`, cuando cree el trabajo de importación en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="760de-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="760de-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="760de-160">Next steps</span></span>

* [<span data-ttu-id="760de-161">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="760de-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* <span data-ttu-id="760de-162">[Quick reference for frequently used commands for import jobs](storage-import-export-tool-quick-reference.md) (Referencia rápida para comandos usados con frecuencia)</span><span class="sxs-lookup"><span data-stu-id="760de-162">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference.md)</span></span>
