---
title: "formato de archivo de importación y exportación de metadatos y propiedades de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toospecify metadatos y propiedades de uno o más blobs que forman parte de una importación o exportación de trabajo."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Formato del archivo de propiedades y metadatos de Azure Import/Export
Puede especificar metadatos y propiedades para uno o más blobs como parte de un trabajo de importación o exportación. tooset metadatos o propiedades de blobs que se crean como parte de un trabajo de importación, proporcione un archivo de metadatos o propiedades en unidad de disco duro de Hola que contiene Hola datos toobe importado. Para un trabajo de exportación, metadatos y propiedades se escriben tooa archivo de metadatos o las propiedades que se incluye en la unidad de disco duro de hello devuelve tooyou.  
  
## <a name="metadata-file-format"></a>Formato del archivo de metadatos  
formato de Hola de un archivo de metadatos es el siguiente:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|Elemento XML|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|`Metadata`|Elemento raíz|elemento raíz de Hello del archivo de metadatos de Hola.|  
|`metadata-name`|String|Opcional. elemento XML de Hello especifica el nombre de Hola de metadatos de hello para el blob de Hola y su valor especifica el valor de Hola de configuración de metadatos de Hola.|  
  
## <a name="properties-file-format"></a>Formato de archivo de propiedades  
formato de Hola de un archivo de propiedades es el siguiente:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|Elemento XML|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|`Properties`|Elemento raíz|elemento raíz de Hola de archivo de propiedades de hello.|  
|`Last-Modified`|String|Opcional. hora de última modificación de Hello para el blob de Hola. Solo para trabajos de exportación.|  
|`Etag`|string|Opcional. Hola valor ETag del blob. Solo para trabajos de exportación.|  
|`Content-Length`|string|Opcional. tamaño de Hello del blob de hello en bytes. Solo para trabajos de exportación.|  
|`Content-Type`|string|Opcional. tipo de contenido de Hola de blob de Hola.|  
|`Content-MD5`|String|Opcional. Hola hash MD5 del blob.|  
|`Content-Encoding`|String|Opcional. Hola contenido del blob de codificación.|  
|`Content-Language`|String|Opcional. Hola idioma del contenido del blob.|  
|`Cache-Control`|String|Opcional. cadena de control de caché de Hello para el blob de Hola.|  

## <a name="next-steps"></a>Pasos siguientes

Vea [Set Blob Properties](/rest/api/storageservices/set-blob-properties) (Establecer propiedades del blob), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Establecer metadatos del blob) y [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Configuración y recuperación de propiedades y metadatos para los recursos del blob) para consultar reglas detalladas sobre cómo establecer propiedades y metadatos del blob.
