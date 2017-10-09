---
title: "aaaSetting propiedades y metadatos mediante la importación y exportación de Azure - v1 | Documentos de Microsoft"
description: "Ver cómo toospecify propiedades y metadatos toobe han establecido en blobs de destino de hello cuando se ejecuta tooprepare de la herramienta de importación y exportación de Azure de hello las unidades de disco. Esto refiere toov1 de hello herramienta de importación/exportación."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="13626-104">Proceso de importación de establecer las propiedades y metadatos durante Hola</span><span class="sxs-lookup"><span data-stu-id="13626-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="13626-105">Al ejecutar tooprepare de herramienta de importación y exportación de Microsoft Azure hello las unidades de disco, puede especificar propiedades y toobe de metadatos que se establezca en blobs de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="13626-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="13626-106">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="13626-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="13626-107">propiedades del blob tooset, cree un archivo de texto en el equipo local que especifica los valores y nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="13626-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="13626-108">tooset metadatos del blob, crear un archivo de texto en el equipo local que especifica los valores y nombres de los metadatos.</span><span class="sxs-lookup"><span data-stu-id="13626-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="13626-109">Pasar tooone de ruta de acceso completa de Hola o ambos de estos toohello archivos herramienta de importación y exportación de Azure como parte del programa Hola `PrepImport` operación.</span><span class="sxs-lookup"><span data-stu-id="13626-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="13626-110">Cuando se especifica un archivo de propiedades o metadatos como parte de una sesión de copia, esas propiedades o metadatos se establecen para cada blob que se importa como parte de esa sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="13626-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="13626-111">Si desea toospecify un conjunto diferente de propiedades o metadatos para algunos de los blobs Hola va a importar, necesitará toocreate otro copiar sesión con diferentes propiedades o los archivos de metadatos.</span><span class="sxs-lookup"><span data-stu-id="13626-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="13626-112">Especificación de propiedades de blob en un archivo de texto</span><span class="sxs-lookup"><span data-stu-id="13626-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="13626-113">propiedades del blob toospecify, cree un archivo de texto local e incluya código XML que especifica los nombres de propiedad como elementos y valores de propiedad como valores.</span><span class="sxs-lookup"><span data-stu-id="13626-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="13626-114">Este es un ejemplo que especifica algunos valores de propiedad:</span><span class="sxs-lookup"><span data-stu-id="13626-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="13626-115">Guardar archivo de hello tooa ubicación local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="13626-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="13626-116">Especificación de metadatos de blob en un archivo de texto</span><span class="sxs-lookup"><span data-stu-id="13626-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="13626-117">De forma similar, toospecify metadatos del blob, cree un archivo de texto local que especifica los nombres de metadatos como elementos y los valores de metadatos como valores.</span><span class="sxs-lookup"><span data-stu-id="13626-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="13626-118">Este es un ejemplo que especifica algunos valores de metadatos:</span><span class="sxs-lookup"><span data-stu-id="13626-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="13626-119">Guardar archivo de hello tooa ubicación local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="13626-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="13626-120">Crear un hello incluidos de sesión de copia archivos de propiedades o metadatos</span><span class="sxs-lookup"><span data-stu-id="13626-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="13626-121">Cuando se ejecuta el trabajo de importación de hello herramienta de importación y exportación de Azure tooprepare hello, especificar el archivo de propiedades de hello en línea de comandos de hello mediante hello `PropertyFile` parámetro.</span><span class="sxs-lookup"><span data-stu-id="13626-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="13626-122">Especificar archivo de metadatos de hello en línea de comandos de hello mediante hello `/MetadataFile` parámetro.</span><span class="sxs-lookup"><span data-stu-id="13626-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="13626-123">Este es un ejemplo que especifica ambos archivos:</span><span class="sxs-lookup"><span data-stu-id="13626-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="13626-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13626-124">Next steps</span></span>

* [<span data-ttu-id="13626-125">Formato de archivo de propiedades y metadatos del servicio Import-Export</span><span class="sxs-lookup"><span data-stu-id="13626-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
