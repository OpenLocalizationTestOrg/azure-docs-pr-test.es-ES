---
title: "Configuración de propiedades y metadatos mediante Azure Import/Export | Microsoft Docs"
description: "Obtenga información sobre cómo especificar las propiedades y los metadatos que se van a establecer en los blobs de destino cuando se ejecuta la herramienta Azure Import/Export para preparar las unidades."
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
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="fc7a6-103">Establecimiento de las propiedades y los metadatos durante el proceso de importación</span><span class="sxs-lookup"><span data-stu-id="fc7a6-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="fc7a6-104">Al ejecutar la herramienta Microsoft Azure Import/Export para preparar las unidades, puede especificar propiedades y metadatos que se establecerán en los blobs de destino.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="fc7a6-105">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fc7a6-105">Follow these steps:</span></span>

1.  <span data-ttu-id="fc7a6-106">Para establecer propiedades de blob, cree un archivo de texto en el equipo local que especifique los valores y nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="fc7a6-107">Para establecer metadatos de blob, cree un archivo de texto en el equipo local que especifique los valores y nombres de metadatos.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="fc7a6-108">Pase la ruta de acceso completa a uno de estos archivos o a ambos a la herramienta Azure Import/Export como parte de la operación `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="fc7a6-109">Cuando se especifica un archivo de propiedades o metadatos como parte de una sesión de copia, esas propiedades o metadatos se establecen para cada blob que se importa como parte de esa sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="fc7a6-110">Si desea especificar otro conjunto de propiedades o metadatos para algunos de los blobs que se importan, tendrá que crear una sesión de copia independiente con archivos de propiedades o metadatos diferentes.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="fc7a6-111">Especificación de propiedades de blob en un archivo de texto</span><span class="sxs-lookup"><span data-stu-id="fc7a6-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="fc7a6-112">Para especificar propiedades de blob, cree un archivo de texto local e incluya código XML que especifique los nombres de propiedad como elementos y los valores de propiedad como valores.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="fc7a6-113">Este es un ejemplo que especifica algunos valores de propiedad:</span><span class="sxs-lookup"><span data-stu-id="fc7a6-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="fc7a6-114">Guarde el archivo en una ubicación local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="fc7a6-115">Especificación de metadatos de blob en un archivo de texto</span><span class="sxs-lookup"><span data-stu-id="fc7a6-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="fc7a6-116">De forma similar, para especificar los metadatos de blob, cree un archivo de texto local que especifique los nombres de metadatos como elementos y los valores de metadatos como valores.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="fc7a6-117">Este es un ejemplo que especifica algunos valores de metadatos:</span><span class="sxs-lookup"><span data-stu-id="fc7a6-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="fc7a6-118">Guarde el archivo en una ubicación local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="fc7a6-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="fc7a6-119">Agregar la ruta de acceso a archivos de metadatos y propiedades en dataset.csv</span><span class="sxs-lookup"><span data-stu-id="fc7a6-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="fc7a6-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc7a6-120">Next steps</span></span>

* [<span data-ttu-id="fc7a6-121">Formato de archivo de propiedades y metadatos del servicio Import-Export</span><span class="sxs-lookup"><span data-stu-id="fc7a6-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
