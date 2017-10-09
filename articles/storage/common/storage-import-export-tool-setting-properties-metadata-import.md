---
title: "aaaSetting propiedades y metadatos mediante la importación y exportación de Azure | Documentos de Microsoft"
description: "Ver cómo toospecify propiedades y metadatos toobe han establecido en blobs de destino de hello cuando se ejecuta tooprepare de la herramienta de importación y exportación de Azure de hello las unidades de disco."
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: c763237160f0e4b72ce88fd31e2958994bfe8e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="05b0a-103">Proceso de importación de establecer las propiedades y metadatos durante Hola</span><span class="sxs-lookup"><span data-stu-id="05b0a-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="05b0a-104">Al ejecutar tooprepare de herramienta de importación y exportación de Microsoft Azure hello las unidades de disco, puede especificar propiedades y toobe de metadatos que se establezca en blobs de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="05b0a-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="05b0a-105">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="05b0a-105">Follow these steps:</span></span>

1.  <span data-ttu-id="05b0a-106">propiedades del blob tooset, cree un archivo de texto en el equipo local que especifica los valores y nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="05b0a-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="05b0a-107">tooset metadatos del blob, crear un archivo de texto en el equipo local que especifica los valores y nombres de los metadatos.</span><span class="sxs-lookup"><span data-stu-id="05b0a-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="05b0a-108">Pasar tooone de ruta de acceso completa de Hola o ambos de estos toohello archivos herramienta de importación y exportación de Azure como parte del programa Hola `PrepImport` operación.</span><span class="sxs-lookup"><span data-stu-id="05b0a-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="05b0a-109">Cuando se especifica un archivo de propiedades o metadatos como parte de una sesión de copia, esas propiedades o metadatos se establecen para cada blob que se importa como parte de esa sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="05b0a-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="05b0a-110">Si desea toospecify un conjunto diferente de propiedades o metadatos para algunos de los blobs Hola va a importar, necesitará toocreate otro copiar sesión con diferentes propiedades o los archivos de metadatos.</span><span class="sxs-lookup"><span data-stu-id="05b0a-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="05b0a-111">Especificación de propiedades de blob en un archivo de texto</span><span class="sxs-lookup"><span data-stu-id="05b0a-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="05b0a-112">propiedades del blob toospecify, cree un archivo de texto local e incluya código XML que especifica los nombres de propiedad como elementos y valores de propiedad como valores.</span><span class="sxs-lookup"><span data-stu-id="05b0a-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="05b0a-113">Este es un ejemplo que especifica algunos valores de propiedad:</span><span class="sxs-lookup"><span data-stu-id="05b0a-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="05b0a-114">Guardar archivo de hello tooa ubicación local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="05b0a-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="05b0a-115">Especificación de metadatos de blob en un archivo de texto</span><span class="sxs-lookup"><span data-stu-id="05b0a-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="05b0a-116">De forma similar, toospecify metadatos del blob, cree un archivo de texto local que especifica los nombres de metadatos como elementos y los valores de metadatos como valores.</span><span class="sxs-lookup"><span data-stu-id="05b0a-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="05b0a-117">Este es un ejemplo que especifica algunos valores de metadatos:</span><span class="sxs-lookup"><span data-stu-id="05b0a-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="05b0a-118">Guardar archivo de hello tooa ubicación local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="05b0a-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="05b0a-119">Agregar archivos de metadatos y tooproperties de la ruta de acceso de hello en dataset.csv</span><span class="sxs-lookup"><span data-stu-id="05b0a-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="05b0a-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05b0a-120">Next steps</span></span>

* [<span data-ttu-id="05b0a-121">Formato de archivo de propiedades y metadatos del servicio Import-Export</span><span class="sxs-lookup"><span data-stu-id="05b0a-121">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
