---
title: "uso de la unidad de aaaPreviewing para un trabajo de exportación de importación y exportación de Azure - v1 | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopreview Hola lista de blobs ha seleccionado para un trabajo de exportación en el servicio de importación y exportación de Azure de Hola."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="1834f-103">Vista previa de uso de disco para un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="1834f-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="1834f-104">Antes de crear un trabajo de exportación, debe exportar un conjunto de blobs toobe de toochoose.</span><span class="sxs-lookup"><span data-stu-id="1834f-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="1834f-105">Hola servicio de importación y exportación de Microsoft Azure permite toouse una lista de rutas de acceso de blob o prefijos de blob blobs de hello toorepresent que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1834f-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="1834f-106">A continuación, debe toodetermine cuántas unidades necesita toosend.</span><span class="sxs-lookup"><span data-stu-id="1834f-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="1834f-107">Herramienta de importación y exportación de Hello proporciona hello `PreviewExport` uso del comando toopreview unidad para los blobs de hello ha seleccionado, en función hello tamaño de unidades de hello va toouse.</span><span class="sxs-lookup"><span data-stu-id="1834f-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="1834f-108">Parámetros de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="1834f-108">Command-line parameters</span></span>

<span data-ttu-id="1834f-109">Puede usar Hola parámetros siguientes al usar hello `PreviewExport` comando de hello herramienta de importación/exportación.</span><span class="sxs-lookup"><span data-stu-id="1834f-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="1834f-110">Parámetro de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="1834f-110">Command-line parameter</span></span>|<span data-ttu-id="1834f-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="1834f-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="1834f-112">**/logdir:**&lt;DirectorioRegistro\></span><span class="sxs-lookup"><span data-stu-id="1834f-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="1834f-113">Opcional.</span><span class="sxs-lookup"><span data-stu-id="1834f-113">Optional.</span></span> <span data-ttu-id="1834f-114">directorio de registro de Hello.</span><span class="sxs-lookup"><span data-stu-id="1834f-114">hello log directory.</span></span> <span data-ttu-id="1834f-115">Archivos de registro detallado se escribirán toothis directory.</span><span class="sxs-lookup"><span data-stu-id="1834f-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="1834f-116">Si no se especifica ningún directorio de registro, se utilizará el directorio actual de hello como directorio de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="1834f-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="1834f-117">**/sn:**&lt;NombreCuentaAlmacenamiento\></span><span class="sxs-lookup"><span data-stu-id="1834f-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="1834f-118">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1834f-118">Required.</span></span> <span data-ttu-id="1834f-119">nombre de Hola de cuenta de almacenamiento de Hola para hello el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="1834f-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1834f-120">**/sk:**&lt;ClaveCuentaAlmacenamiento\></span><span class="sxs-lookup"><span data-stu-id="1834f-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="1834f-121">Necesario únicamente si no se especifica un contenedor SAS.</span><span class="sxs-lookup"><span data-stu-id="1834f-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="1834f-122">trabajo de exportación de la clave de cuenta de almacenamiento de Hola para Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="1834f-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1834f-123">**/csas:**&lt;SasContenedor\></span><span class="sxs-lookup"><span data-stu-id="1834f-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="1834f-124">Requerido únicamente si no se especifica una clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1834f-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="1834f-125">contenedor de Hello SAS para toobe de blobs de anuncio Hola se exporta en el trabajo de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1834f-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="1834f-126">**/ExportBlobListFile:**&lt;ArchivoListaBlobExportación\></span><span class="sxs-lookup"><span data-stu-id="1834f-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="1834f-127">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1834f-127">Required.</span></span> <span data-ttu-id="1834f-128">Ruta de acceso toohello XML archivo que contiene una lista de rutas de acceso de blob o prefijos de ruta de acceso para hello blobs toobe exportado de blob.</span><span class="sxs-lookup"><span data-stu-id="1834f-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="1834f-129">formato de archivo de Hello usado en hello `BlobListBlobPath` elemento Hola [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación de servicio de importación y exportación de API de REST de hello.</span><span class="sxs-lookup"><span data-stu-id="1834f-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="1834f-130">**/DriveSize:**&lt;TamañoUnidad\></span><span class="sxs-lookup"><span data-stu-id="1834f-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="1834f-131">Necesario.</span><span class="sxs-lookup"><span data-stu-id="1834f-131">Required.</span></span> <span data-ttu-id="1834f-132">Hola tamaño de unidades toouse para un trabajo de exportación, *p. ej.*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="1834f-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="1834f-133">Ejemplo de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="1834f-133">Command-line example</span></span>

<span data-ttu-id="1834f-134">Hello en el ejemplo siguiente se muestra hello `PreviewExport` comando:</span><span class="sxs-lookup"><span data-stu-id="1834f-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="1834f-135">Hello archivo de lista de blobs de exportación puede contener nombres de blob y prefijos de blob, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="1834f-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="1834f-136">Hola herramienta de importación y exportación de Azure enumera todos los toobe blobs exportado y calcula cómo toopack en unidades de hello especifica tamaño, teniendo en cuenta cualquier sobrecarga necesaria, a continuación, calcula el número de Hola de unidades necesario toohold blobs de Hola y uso de la unidad información.</span><span class="sxs-lookup"><span data-stu-id="1834f-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="1834f-137">Este es un ejemplo de salida de hello, con registros informativos omitidos:</span><span class="sxs-lookup"><span data-stu-id="1834f-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="1834f-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1834f-138">Next steps</span></span>

* [<span data-ttu-id="1834f-139">Referencia de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="1834f-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
