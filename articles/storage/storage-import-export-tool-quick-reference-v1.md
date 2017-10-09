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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="9b44e-104">Referencia rápida de comandos usados con frecuencia para trabajos de importación</span><span class="sxs-lookup"><span data-stu-id="9b44e-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="9b44e-105">En esta sección se proporcionan referencias rápidas para algunos comandos que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="9b44e-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="9b44e-106">Para obtener información detallada sobre el uso, vea [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparación de los discos duros para un trabajo de importación).</span><span class="sxs-lookup"><span data-stu-id="9b44e-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="9b44e-107">Preparar los discos de hello cuando toohello discos ya copian los datos</span><span class="sxs-lookup"><span data-stu-id="9b44e-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="9b44e-108">Es aquí un disco de un tooprepare de comando de ejemplo cuando datos copian ya toohello unidad de disco duro que todavía no se ha cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="9b44e-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="9b44e-109">Copiar un disco duro de tooa único directorio</span><span class="sxs-lookup"><span data-stu-id="9b44e-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="9b44e-110">Este es un toocopy de comando de ejemplo de origen de un único directorio tooa unidad de disco duro que todavía no se ha cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="9b44e-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="9b44e-111">Copiar la unidad de disco duro tooa wwo directorios</span><span class="sxs-lookup"><span data-stu-id="9b44e-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="9b44e-112">toocopy dos directorios tooa unidad de origen, necesitará dos comandos.</span><span class="sxs-lookup"><span data-stu-id="9b44e-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="9b44e-113">Hello primer comando Especifica el directorio de registro de hello, la clave de la cuenta de almacenamiento, la letra de unidad de destino y `format/encrypt` requisitos, en parámetros comunes de suma toohello:</span><span class="sxs-lookup"><span data-stu-id="9b44e-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="9b44e-114">Hola segundo comando Especifica archivo diario de hello, un nuevo identificador de sesión y las ubicaciones de origen y destino de hello:</span><span class="sxs-lookup"><span data-stu-id="9b44e-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="9b44e-115">Copiar un disco duro de tooa de archivo grande en una segunda sesión de copia</span><span class="sxs-lookup"><span data-stu-id="9b44e-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="9b44e-116">Este es un comando de ejemplo que se copia a una unidad de tooa de archivo grande que se ha preparado en una sesión de copia anterior:</span><span class="sxs-lookup"><span data-stu-id="9b44e-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="9b44e-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b44e-117">Next steps</span></span>

* [<span data-ttu-id="9b44e-118">Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="9b44e-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
