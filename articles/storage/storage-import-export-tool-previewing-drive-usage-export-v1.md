---
title: "Vista previa de uso de disco para un trabajo de exportación de Azure Import/Export (versión 1) | Microsoft Docs"
description: "Obtenga información sobre cómo conseguir una vista previa de la lista de blobs que ha seleccionado para un trabajo de exportación en el servicio Azure Import/Export."
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
ms.openlocfilehash: 7bf74247090f91e17f81a9bc98ebfa78334c8c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="3fa4c-103">Vista previa de uso de disco para un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="3fa4c-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="3fa4c-104">Antes de crear un trabajo de exportación, debe elegir un conjunto de blobs que se van a exportar.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="3fa4c-105">El servicio Microsoft Azure Import/Export permite usar una lista de rutas de acceso de blob o prefijos de blob para representar los blobs que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="3fa4c-106">A continuación, debe determinar cuántas unidades necesita enviar.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="3fa4c-107">La herramienta Import/Export proporciona el comando `PreviewExport` para obtener una vista previa del uso de la unidad para los blobs que ha seleccionado, en función del tamaño de las unidades que se van a usar.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="3fa4c-108">Parámetros de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="3fa4c-108">Command-line parameters</span></span>

<span data-ttu-id="3fa4c-109">Puede usar los parámetros siguientes al usar el comando `PreviewExport` de la herramienta Import/Export.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="3fa4c-110">Parámetro de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="3fa4c-110">Command-line parameter</span></span>|<span data-ttu-id="3fa4c-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="3fa4c-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="3fa4c-112">**/logdir:**<DirectorioRegistro\></span><span class="sxs-lookup"><span data-stu-id="3fa4c-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="3fa4c-113">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-113">Optional.</span></span> <span data-ttu-id="3fa4c-114">El directorio de registro.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-114">The log directory.</span></span> <span data-ttu-id="3fa4c-115">Los archivos de registro detallados se escribirán en este directorio.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="3fa4c-116">Si no se especifica un directorio de registro, se usará el directorio actual como directorio de registro.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="3fa4c-117">**/sn:**<NombreCuentaAlmacenamiento\></span><span class="sxs-lookup"><span data-stu-id="3fa4c-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="3fa4c-118">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-118">Required.</span></span> <span data-ttu-id="3fa4c-119">El nombre de la cuenta de almacenamiento para el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="3fa4c-120">**/sk:**<ClaveCuentaAlmacenamiento\></span><span class="sxs-lookup"><span data-stu-id="3fa4c-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="3fa4c-121">Necesario únicamente si no se especifica un contenedor SAS.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="3fa4c-122">La clave de cuenta para la cuenta de almacenamiento correspondiente al trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="3fa4c-123">**/csas:**<SasContenedor\></span><span class="sxs-lookup"><span data-stu-id="3fa4c-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="3fa4c-124">Requerido únicamente si no se especifica una clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="3fa4c-125">El contenedor SAS para enumerar los blobs que se van a exportar en el trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="3fa4c-126">**/ExportBlobListFile:**<ArchivoListaBlobExportación\></span><span class="sxs-lookup"><span data-stu-id="3fa4c-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="3fa4c-127">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-127">Required.</span></span> <span data-ttu-id="3fa4c-128">Ruta de acceso al archivo XML que contiene una lista de rutas de acceso de blob o prefijos de ruta de acceso para los blobs que se van a exportar.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="3fa4c-129">El formato de archivo usado en el elemento `BlobListBlobPath` de la operación [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) de la API de REST del servicio Import/Export.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="3fa4c-130">**/DriveSize:**<TamañoUnidad\></span><span class="sxs-lookup"><span data-stu-id="3fa4c-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="3fa4c-131">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-131">Required.</span></span> <span data-ttu-id="3fa4c-132">El tamaño de las unidades que se van a usar para un trabajo de exportación, *por ejemplo*, 500 GB o 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="3fa4c-133">Ejemplo de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="3fa4c-133">Command-line example</span></span>

<span data-ttu-id="3fa4c-134">En el siguiente ejemplo se muestra el comando `PreviewExport`:</span><span class="sxs-lookup"><span data-stu-id="3fa4c-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="3fa4c-135">El archivo de lista de blobs de exportación puede contener nombres de blob y prefijos de blob, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="3fa4c-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="3fa4c-136">La herramienta Azure Import/Export enumera todos los blobs que se van a exportar y calcula cómo empaquetarlos en unidades del tamaño especificado, teniendo en cuenta cualquier sobrecarga necesaria; después calcula el número de unidades necesarias para albergar los blobs y la información de uso de la unidad.</span><span class="sxs-lookup"><span data-stu-id="3fa4c-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="3fa4c-137">Este es un ejemplo de la salida, con los registros informativos omitidos:</span><span class="sxs-lookup"><span data-stu-id="3fa4c-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="3fa4c-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3fa4c-138">Next steps</span></span>

* [<span data-ttu-id="3fa4c-139">Referencia de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="3fa4c-139">Azure Import/Export Tool reference</span></span>](storage-import-export-tool-how-to-v1.md)
