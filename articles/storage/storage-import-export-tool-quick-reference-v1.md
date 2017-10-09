---
title: "referencia de aaaQuick para comandos de trabajo de importación de la herramienta de importación y exportación de Azure - v1 | Documentos de Microsoft"
description: "Referencia sobre los comandos de la herramienta de Azure Import/Export para comandos de trabajos de importación usados con frecuencia. Esto refiere toov1 de hello herramienta de importación/exportación."
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Referencia rápida de comandos usados con frecuencia para trabajos de importación
En esta sección se proporcionan referencias rápidas para algunos comandos que se usan con frecuencia. Para obtener información detallada sobre el uso, vea [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparación de los discos duros para un trabajo de importación).  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>Preparar los discos de hello cuando toohello discos ya copian los datos
 Es aquí un disco de un tooprepare de comando de ejemplo cuando datos copian ya toohello unidad de disco duro que todavía no se ha cifrado con BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Copiar un disco duro de tooa único directorio  
 Este es un toocopy de comando de ejemplo de origen de un único directorio tooa unidad de disco duro que todavía no se ha cifrado con BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>Copiar la unidad de disco duro tooa wwo directorios  
 toocopy dos directorios tooa unidad de origen, necesitará dos comandos.  
  
 Hello primer comando Especifica el directorio de registro de hello, la clave de la cuenta de almacenamiento, la letra de unidad de destino y `format/encrypt` requisitos, en parámetros comunes de suma toohello:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 Hola segundo comando Especifica archivo diario de hello, un nuevo identificador de sesión y las ubicaciones de origen y destino de hello:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Copiar un disco duro de tooa de archivo grande en una segunda sesión de copia  
 Este es un comando de ejemplo que se copia a una unidad de tooa de archivo grande que se ha preparado en una sesión de copia anterior:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Pasos siguientes

* [Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
