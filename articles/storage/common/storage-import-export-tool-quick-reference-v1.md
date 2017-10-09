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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="c9f3c-104">Referencia rápida de comandos usados con frecuencia para trabajos de importación</span><span class="sxs-lookup"><span data-stu-id="c9f3c-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="c9f3c-105">En esta sección se proporciona una referencia rápida para algunos comandos que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="c9f3c-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="c9f3c-106">Para obtener información detallada sobre el uso, vea [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparación de los discos duros para un trabajo de importación).</span><span class="sxs-lookup"><span data-stu-id="c9f3c-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="c9f3c-107">Preparar un disco duro cuando datos ya se ha copiado toohello unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="c9f3c-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="c9f3c-108">Hola siguiente comando prepara una unidad de disco duro cuando los datos ya se ha sido tooit copiado, pero aún no se ha cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="c9f3c-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="c9f3c-109">Copiar un disco duro de tooa único directorio</span><span class="sxs-lookup"><span data-stu-id="c9f3c-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="c9f3c-110">Hola siguiente comando copia una unidad de disco duro de tooa directorio de origen único que aún no se han cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="c9f3c-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="c9f3c-111">Copiar dos directorios de unidad de disco duro tooa</span><span class="sxs-lookup"><span data-stu-id="c9f3c-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="c9f3c-112">unidad de tooa de directorios de toocopy dos origen, Hola de uso siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c9f3c-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="c9f3c-113">Hello primer comando Especifica el directorio de registro de hello, la clave de la cuenta de almacenamiento, la letra de unidad de destino, `format/encrypt` requisitos y parámetros comunes:</span><span class="sxs-lookup"><span data-stu-id="c9f3c-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="c9f3c-114">Hola segundo comando Especifica archivo diario de hello, un nuevo identificador de sesión y las ubicaciones de origen y destino de hello:</span><span class="sxs-lookup"><span data-stu-id="c9f3c-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="c9f3c-115">Copiar un disco duro de tooa de archivo grande en una segunda sesión de copia</span><span class="sxs-lookup"><span data-stu-id="c9f3c-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="c9f3c-116">Hola siguiente comando copia una unidad de disco duro de tooa archivo grande que se preparó en una sesión de copia anterior:</span><span class="sxs-lookup"><span data-stu-id="c9f3c-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="c9f3c-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9f3c-117">Next steps</span></span>

* [<span data-ttu-id="c9f3c-118">Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="c9f3c-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
