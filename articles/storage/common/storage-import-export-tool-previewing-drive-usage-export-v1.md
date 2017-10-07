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
# <a name="previewing-drive-usage-for-an-export-job"></a>Vista previa de uso de disco para un trabajo de exportación
Antes de crear un trabajo de exportación, debe exportar un conjunto de blobs toobe de toochoose. Hola servicio de importación y exportación de Microsoft Azure permite toouse una lista de rutas de acceso de blob o prefijos de blob blobs de hello toorepresent que ha seleccionado.  
  
A continuación, debe toodetermine cuántas unidades necesita toosend. Herramienta de importación y exportación de Hello proporciona hello `PreviewExport` uso del comando toopreview unidad para los blobs de hello ha seleccionado, en función hello tamaño de unidades de hello va toouse.

## <a name="command-line-parameters"></a>Parámetros de línea de comandos

Puede usar Hola parámetros siguientes al usar hello `PreviewExport` comando de hello herramienta de importación/exportación.

|Parámetro de línea de comandos|Descripción|  
|--------------------------|-----------------|  
|**/logdir:**&lt;DirectorioRegistro\>|Opcional. directorio de registro de Hello. Archivos de registro detallado se escribirán toothis directory. Si no se especifica ningún directorio de registro, se utilizará el directorio actual de hello como directorio de registro de hello.|  
|**/sn:**&lt;NombreCuentaAlmacenamiento\>|Necesario. nombre de Hola de cuenta de almacenamiento de Hola para hello el trabajo de exportación.|  
|**/sk:**&lt;ClaveCuentaAlmacenamiento\>|Necesario únicamente si no se especifica un contenedor SAS. trabajo de exportación de la clave de cuenta de almacenamiento de Hola para Hola Hola.|  
|**/csas:**&lt;SasContenedor\>|Requerido únicamente si no se especifica una clave de cuenta de almacenamiento. contenedor de Hello SAS para toobe de blobs de anuncio Hola se exporta en el trabajo de exportación de Hola.|  
|**/ExportBlobListFile:**&lt;ArchivoListaBlobExportación\>|Necesario. Ruta de acceso toohello XML archivo que contiene una lista de rutas de acceso de blob o prefijos de ruta de acceso para hello blobs toobe exportado de blob. formato de archivo de Hello usado en hello `BlobListBlobPath` elemento Hola [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación de servicio de importación y exportación de API de REST de hello.|  
|**/DriveSize:**&lt;TamañoUnidad\>|Necesario. Hola tamaño de unidades toouse para un trabajo de exportación, *p. ej.*, 500 GB, 1,5 TB.|  

## <a name="command-line-example"></a>Ejemplo de línea de comandos

Hello en el ejemplo siguiente se muestra hello `PreviewExport` comando:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Hello archivo de lista de blobs de exportación puede contener nombres de blob y prefijos de blob, como se muestra aquí:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Hola herramienta de importación y exportación de Azure enumera todos los toobe blobs exportado y calcula cómo toopack en unidades de hello especifica tamaño, teniendo en cuenta cualquier sobrecarga necesaria, a continuación, calcula el número de Hola de unidades necesario toohold blobs de Hola y uso de la unidad información.  
  
Este es un ejemplo de salida de hello, con registros informativos omitidos:  
  
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
  
## <a name="next-steps"></a>Pasos siguientes

* [Referencia de la herramienta Azure Import/Export](../storage-import-export-tool-how-to-v1.md)
