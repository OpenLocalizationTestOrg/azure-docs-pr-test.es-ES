---
title: "trabajo de importación de aaaSample flujo de trabajo tooprep unidades de disco duro para una importación y exportación de Azure | Documentos de Microsoft"
description: "Vea un tutorial para completar el proceso de preparar las unidades para un trabajo de importación en el servicio de importación y exportación de Hola Hola."
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
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="ae4f7-103">Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="ae4f7-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="ae4f7-104">Este artículo le guiará por el proceso completo de Hola de preparar las unidades para un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="ae4f7-105">Datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ae4f7-105">Sample data</span></span>

<span data-ttu-id="ae4f7-106">Este ejemplo importan Hola después de datos en una cuenta de almacenamiento de Azure denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="ae4f7-107">Ubicación</span><span class="sxs-lookup"><span data-stu-id="ae4f7-107">Location</span></span>|<span data-ttu-id="ae4f7-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="ae4f7-108">Description</span></span>|<span data-ttu-id="ae4f7-109">Tamaño de los datos</span><span class="sxs-lookup"><span data-stu-id="ae4f7-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="ae4f7-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="ae4f7-110">H:\Video\\</span></span> |<span data-ttu-id="ae4f7-111">Una colección de vídeos</span><span class="sxs-lookup"><span data-stu-id="ae4f7-111">A collection of videos</span></span>|<span data-ttu-id="ae4f7-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="ae4f7-112">12 TB</span></span>|
|<span data-ttu-id="ae4f7-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="ae4f7-113">H:\Photo\\</span></span> |<span data-ttu-id="ae4f7-114">Una colección de fotos</span><span class="sxs-lookup"><span data-stu-id="ae4f7-114">A collection of photos</span></span>|<span data-ttu-id="ae4f7-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="ae4f7-115">30 GB</span></span>|
|<span data-ttu-id="ae4f7-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ae4f7-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ae4f7-117">Una imagen de disco Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="ae4f7-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="ae4f7-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="ae4f7-118">25 GB</span></span>|
|<span data-ttu-id="ae4f7-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="ae4f7-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="ae4f7-120">Una colección de archivos de música en un recurso compartido de red</span><span class="sxs-lookup"><span data-stu-id="ae4f7-120">A collection of music files on a network share</span></span>|<span data-ttu-id="ae4f7-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="ae4f7-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="ae4f7-122">Destinos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ae4f7-122">Storage account destinations</span></span>

<span data-ttu-id="ae4f7-123">trabajo de importación de Hello importará datos hello en hello después de destinos en la cuenta de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="ae4f7-124">Origen</span><span class="sxs-lookup"><span data-stu-id="ae4f7-124">Source</span></span>|<span data-ttu-id="ae4f7-125">Directorio virtual o blob de destino</span><span class="sxs-lookup"><span data-stu-id="ae4f7-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="ae4f7-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="ae4f7-126">H:\Video\\</span></span> |<span data-ttu-id="ae4f7-127">video/</span><span class="sxs-lookup"><span data-stu-id="ae4f7-127">video/</span></span>|
|<span data-ttu-id="ae4f7-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="ae4f7-128">H:\Photo\\</span></span> |<span data-ttu-id="ae4f7-129">photo/</span><span class="sxs-lookup"><span data-stu-id="ae4f7-129">photo/</span></span>|
|<span data-ttu-id="ae4f7-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ae4f7-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ae4f7-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ae4f7-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="ae4f7-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="ae4f7-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="ae4f7-133">music</span><span class="sxs-lookup"><span data-stu-id="ae4f7-133">music</span></span>|

<span data-ttu-id="ae4f7-134">Con esta asignación, Hola archivo `H:\Video\Drama\GreatMovie.mov` será toohello importados blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="ae4f7-135">Determinación de los requisitos de la unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="ae4f7-135">Determine hard drive requirements</span></span>

<span data-ttu-id="ae4f7-136">Después, toodetermine cuántas unidades de disco duro son necesarias, tamaño de Hola de cálculo de los datos de hello:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="ae4f7-137">En este ejemplo, dos unidades de disco duro de 8 TB deberían ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="ae4f7-138">Sin embargo, desde el directorio de origen de hello `H:\Video` tiene 12TB de datos y la capacidad de la unidad de disco duro es solo 8TB, será capaz de toospecify en Hola después de manera Hola **driveset.csv** archivo:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="ae4f7-139">herramienta de Hola encargará de distribuir datos a través de dos unidades de disco duro de forma optimizada.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="ae4f7-140">Conecte unidades y configurar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="ae4f7-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="ae4f7-141">Podrá conectar ambos máquina toohello de discos y crear volúmenes.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="ae4f7-142">Luego, cree el archivo **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="ae4f7-143">Además, puede establecer Hola después de metadatos para todos los archivos:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="ae4f7-144">**UploadMethod:** servicio Microsoft Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="ae4f7-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="ae4f7-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="ae4f7-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="ae4f7-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="ae4f7-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="ae4f7-147">tooset metadatos para los archivos de hello importado, cree un archivo de texto, `c:\WAImportExport\SampleMetadata.txt`, con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="ae4f7-148">También puede establecer algunas propiedades para hello `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="ae4f7-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="ae4f7-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="ae4f7-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="ae4f7-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="ae4f7-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="ae4f7-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="ae4f7-152">tooset estas propiedades, cree un archivo de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="ae4f7-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="ae4f7-153">Hola ejecución herramienta de importación y exportación de Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="ae4f7-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="ae4f7-154">Ahora está listo toorun Hola herramienta de importación y exportación de Azure tooprepare Hola dos unidades de disco duro.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="ae4f7-155">**Para la primera sesión de hello:**</span><span class="sxs-lookup"><span data-stu-id="ae4f7-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="ae4f7-156">Si los datos más necesitan toobe agregado, cree otro archivo de conjunto de datos (mismo formato que Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="ae4f7-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="ae4f7-157">**Para hello segunda sesión:**</span><span class="sxs-lookup"><span data-stu-id="ae4f7-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="ae4f7-158">Una vez completaron las sesiones de copia de hello, puede desconectarse dos unidades de Hola de equipo de copia de Hola y enviarlas toohello centro de datos adecuado de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="ae4f7-159">Cargue archivos de diario de hello dos, `<FirstDriveSerialNumber>.xml` y `<SecondDriveSerialNumber>.xml`, al crear trabajo de importación de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae4f7-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae4f7-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae4f7-160">Next steps</span></span>

* [<span data-ttu-id="ae4f7-161">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="ae4f7-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* <span data-ttu-id="ae4f7-162">[Quick reference for frequently used commands for import jobs](../storage-import-export-tool-quick-reference.md) (Referencia rápida para comandos usados con frecuencia)</span><span class="sxs-lookup"><span data-stu-id="ae4f7-162">[Quick reference for frequently used commands](../storage-import-export-tool-quick-reference.md)</span></span>
