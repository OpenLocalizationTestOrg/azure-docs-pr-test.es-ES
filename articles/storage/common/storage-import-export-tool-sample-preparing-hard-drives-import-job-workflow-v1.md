---
title: "trabajo - v1 de importación de aaaSample flujo de trabajo tooprep unidades de disco duro para una importación y exportación de Azure | Documentos de Microsoft"
description: "Vea un tutorial para completar el proceso de preparar las unidades para un trabajo de importación en el servicio de importación y exportación de Hola Hola."
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
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación
Este tema explica cómo completar el proceso de Hola de preparar las unidades para un trabajo de importación.  
  
Este ejemplo importan Hola después de datos en una cuenta de almacenamiento de Windows Azure denominada `mystorageaccount`:  
  
|Ubicación|Descripción|  
|--------------|-----------------|  
|H:\Video|Una colección de vídeos, 5 TB en total.|  
|H:\Photo|Una colección de fotos, 30 GB en total.|  
|K:\Temp\FavoriteMovie.ISO|Una imagen de disco Blu-ray™, 25 GB.|  
|\\\bigshare\john\music|Una colección de archivos de música en un recurso compartido de red, 10 GB en total.|  
  
trabajo de importación de Hello importa estos datos en hello después de destinos en la cuenta de almacenamiento de hello:  
  
|Origen|Directorio virtual o blob de destino|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
Con esta asignación, Hola archivo `H:\Video\Drama\GreatMovie.mov` es toohello importados blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Después, toodetermine cuántas unidades de disco duro son necesarias, tamaño de Hola de cálculo de los datos de hello:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
En este ejemplo, dos unidades de disco duro de 3 TB deberían ser suficientes. Sin embargo, desde el directorio de origen de hello `H:\Video` tiene 5 TB de datos y la capacidad de la unidad de disco duro es solo 3 TB, es necesario toobreak `H:\Video` en dos directorios más pequeños: `H:\Video1` y `H:\Video2`, antes de ejecutar Hola Microsoft Herramienta de importación y exportación de Azure. Este paso produce Hola siguiendo los directorios de origen:  
  
|Ubicación|Tamaño|Directorio virtual o blob de destino|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2,5 TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2,5 TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30 GB|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25 GB|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10 GB|https://mystorageaccount.blob.core.windows.net/music|  
  
 Aunque Hola `H:\Video`directory se ha dividido tootwo directorios, señalan toohello mismo directorio virtual de destino en la cuenta de almacenamiento de Hola. De esta manera, todos los archivos de vídeo se mantienen en un único `video` contenedor en la cuenta de almacenamiento de Hola.  
  
 A continuación, directorios de origen anterior Hola son toohello distribuido uniformemente dos unidades de disco duro:  
  
||||  
|-|-|-|  
|Unidad de disco duro|Directorios de origen|Tamaño total|  
|Primera unidad|H:\Video1|2,5 TB + 30 GB|  
||H:\Photo||  
|Segunda unidad|H:\Video2|2,5 TB + 35 GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
Además, puede establecer Hola después de metadatos para todos los archivos:  
  
-   **UploadMethod:** servicio Microsoft Azure Import/Export  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 10/1/2013  
  
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
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control:** no-cache  
  
tooset estas propiedades, cree un archivo de texto, `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Ahora está listo toorun Hola herramienta de importación y exportación de Azure tooprepare Hola dos unidades de disco duro. Observe lo siguiente:  
  
-   Hola primera unidad se monta como unidad X.  
  
-   Hola segunda unidad se monta como unidad Y.  
  
-   Hola clave Hola cuenta de almacenamiento `mystorageaccount` es `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Preparación del disco para la importación cuando los datos se han cargado previamente
 
 Si ya está presente en el disco de Hola Hola toobe de datos importado, utilice Hola marca /skipwrite. valor de Hola de /t y /srcdir debe ambos disco toohello de punto que se está preparando para la importación. Si no todos hello toobe de datos importado se va toohello mismo directorio virtual de destino o raíz de cuenta de almacenamiento Hola Hola ejecución mismo comando para cada directorio de destino por separado, mantener el valor de Hola de/Id. Hola igual en todas las ejecuciones.

>[!NOTE] 
>No especifique/Format, dado que borrar datos de hello en el disco de Hola. Puede especificar / cifrar o /bk dependiendo de si el disco de hello ya está cifrado o no. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Copia de sesiones: primera unidad

Para la primera unidad de hello, ejecute hello herramienta de importación y exportación de Azure de origen dos veces hello toocopy dos directorios:  

**Primera sesión de copia**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Segunda sesión de copia**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Copia de sesiones: segunda unidad
 
Para hello segunda unidad, ejecute Hola herramienta de importación y exportación de Azure tres veces, una vez cada uno de ellos para hello directorios de origen y una vez para independiente de hello Blu-Ray™ archivo de imagen):  
  
**Primera sesión de copia** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Segunda sesión de copia**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Tercera sesión de copia**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Finalización de la sesión de copia

Una vez completaron las sesiones de copia de hello, puede desconectarse dos unidades de Hola de equipo de copia de Hola y enviarlas toohello centro de datos de Windows Azure adecuado. Cargar archivos de diario de hello dos, `FirstDrive.jrn` y `SecondDrive.jrn`, cuando se crea el trabajo de importación de hello en hello [portal de Windows Azure](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Pasos siguientes

* [Preparación de unidades de disco duro para un trabajo de importación](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Quick reference for frequently used commands for import jobs](../storage-import-export-tool-quick-reference-v1.md) (Referencia rápida para comandos usados con frecuencia) 
