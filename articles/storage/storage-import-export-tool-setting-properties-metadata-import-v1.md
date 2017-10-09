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
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Proceso de importación de establecer las propiedades y metadatos durante Hola
Al ejecutar tooprepare de herramienta de importación y exportación de Microsoft Azure hello las unidades de disco, puede especificar propiedades y toobe de metadatos que se establezca en blobs de destino de Hola. Siga estos pasos:  
  
1.  propiedades del blob tooset, cree un archivo de texto en el equipo local que especifica los valores y nombres de propiedad.  
  
2.  tooset metadatos del blob, crear un archivo de texto en el equipo local que especifica los valores y nombres de los metadatos.  
  
3.  Pasar tooone de ruta de acceso completa de Hola o ambos de estos toohello archivos herramienta de importación y exportación de Azure como parte del programa Hola `PrepImport` operación.  
  
> [!NOTE]
>  Cuando se especifica un archivo de propiedades o metadatos como parte de una sesión de copia, esas propiedades o metadatos se establecen para cada blob que se importa como parte de esa sesión de copia. Si desea toospecify un conjunto diferente de propiedades o metadatos para algunos de los blobs Hola va a importar, necesitará toocreate otro copiar sesión con diferentes propiedades o los archivos de metadatos.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Especificación de propiedades de blob en un archivo de texto  
propiedades del blob toospecify, cree un archivo de texto local e incluya código XML que especifica los nombres de propiedad como elementos y valores de propiedad como valores. Este es un ejemplo que especifica algunos valores de propiedad:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Guardar archivo de hello tooa ubicación local como `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Especificación de metadatos de blob en un archivo de texto  
De forma similar, toospecify metadatos del blob, cree un archivo de texto local que especifica los nombres de metadatos como elementos y los valores de metadatos como valores. Este es un ejemplo que especifica algunos valores de metadatos:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Guardar archivo de hello tooa ubicación local como `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Crear un hello incluidos de sesión de copia archivos de propiedades o metadatos  
Cuando se ejecuta el trabajo de importación de hello herramienta de importación y exportación de Azure tooprepare hello, especificar el archivo de propiedades de hello en línea de comandos de hello mediante hello `PropertyFile` parámetro. Especificar archivo de metadatos de hello en línea de comandos de hello mediante hello `/MetadataFile` parámetro. Este es un ejemplo que especifica ambos archivos:  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Pasos siguientes

* [Formato de archivo de propiedades y metadatos del servicio Import-Export](storage-import-export-file-format-metadata-and-properties.md)