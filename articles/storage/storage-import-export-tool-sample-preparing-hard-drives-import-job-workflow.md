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
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación

Este artículo le guiará por el proceso completo de Hola de preparar las unidades para un trabajo de importación.

## <a name="sample-data"></a>Datos de ejemplo

Este ejemplo importan Hola después de datos en una cuenta de almacenamiento de Azure denominada `mystorageaccount`:

|Ubicación|Descripción|Tamaño de los datos|
|--------------|-----------------|-----|
|H:\Video\ |Una colección de vídeos|12 TB|
|H:\Photo\ |Una colección de fotos|30 GB|
|K:\Temp\FavoriteMovie.ISO|Una imagen de disco Blu-ray™|25 GB|
|\\\bigshare\john\music\|Una colección de archivos de música en un recurso compartido de red|10 GB|

## <a name="storage-account-destinations"></a>Destinos de la cuenta de almacenamiento

trabajo de importación de Hello importará datos hello en hello después de destinos en la cuenta de almacenamiento de hello:

|Origen|Directorio virtual o blob de destino|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

Con esta asignación, Hola archivo `H:\Video\Drama\GreatMovie.mov` será toohello importados blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Determinación de los requisitos de la unidad de disco duro

Después, toodetermine cuántas unidades de disco duro son necesarias, tamaño de Hola de cálculo de los datos de hello:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

En este ejemplo, dos unidades de disco duro de 8 TB deberían ser suficientes. Sin embargo, desde el directorio de origen de hello `H:\Video` tiene 12TB de datos y la capacidad de la unidad de disco duro es solo 8TB, será capaz de toospecify en Hola después de manera Hola **driveset.csv** archivo:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
herramienta de Hola encargará de distribuir datos a través de dos unidades de disco duro de forma optimizada.

## <a name="attach-drives-and-configure-hello-job"></a>Conecte unidades y configurar el trabajo de Hola
Podrá conectar ambos máquina toohello de discos y crear volúmenes. Luego, cree el archivo **dataset.csv**:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Además, puede establecer Hola después de metadatos para todos los archivos:

* **UploadMethod:** servicio Microsoft Azure Import/Export
* **DataSetName:** SampleData
* **CreationDate:** 10/1/2013

tooset metadatos para los archivos de hello importado, cree un archivo de texto, `c:\WAImportExport\SampleMetadata.txt`, con hello siguen contenido:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

También puede establecer algunas propiedades para hello `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control:** no-cache

tooset estas propiedades, cree un archivo de texto, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Hola ejecución herramienta de importación y exportación de Azure (WAImportExport.exe)

Ahora está listo toorun Hola herramienta de importación y exportación de Azure tooprepare Hola dos unidades de disco duro.

**Para la primera sesión de hello:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Si los datos más necesitan toobe agregado, cree otro archivo de conjunto de datos (mismo formato que Initialdataset).

**Para hello segunda sesión:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Una vez completaron las sesiones de copia de hello, puede desconectarse dos unidades de Hola de equipo de copia de Hola y enviarlas toohello centro de datos adecuado de Azure. Cargue archivos de diario de hello dos, `<FirstDriveSerialNumber>.xml` y `<SecondDriveSerialNumber>.xml`, al crear trabajo de importación de Hola Hola portal de Azure.

## <a name="next-steps"></a>Pasos siguientes

* [Preparación de unidades de disco duro para un trabajo de importación](storage-import-export-tool-preparing-hard-drives-import.md)
* [Referencia rápida de comandos usados con frecuencia para trabajos de importación](storage-import-export-tool-quick-reference.md)
