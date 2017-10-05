---
title: "Referencia rápida de los comandos de trabajos de importación de la herramienta Azure Import/Export (versión 1) | Microsoft Docs"
description: "Referencia sobre los comandos de la herramienta de Azure Import/Export para comandos de trabajos de importación usados con frecuencia. Se refiere a la versión 1 de la herramienta Import/Export."
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
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="5aba1-104">Referencia rápida de comandos usados con frecuencia para trabajos de importación</span><span class="sxs-lookup"><span data-stu-id="5aba1-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="5aba1-105">En esta sección se proporcionan referencias rápidas para algunos comandos que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="5aba1-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="5aba1-106">Para obtener información detallada sobre el uso, vea [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparación de los discos duros para un trabajo de importación).</span><span class="sxs-lookup"><span data-stu-id="5aba1-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="5aba1-107">Preparación de los discos los datos ya están copiados en los discos</span><span class="sxs-lookup"><span data-stu-id="5aba1-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="5aba1-108">A continuación se indica un comando de ejemplo para preparar un disco cuando ya se han copiado datos en la unidad de disco duro que aún no se ha cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="5aba1-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="5aba1-109">Copia de un único directorio en una unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="5aba1-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="5aba1-110">A continuación se indica un comando de ejemplo para copiar un único directorio de origen en una unidad de disco duro que aún no se ha cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="5aba1-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="5aba1-111">Copia de dos directorios en una unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="5aba1-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="5aba1-112">Para copiar dos directorios de origen en una unidad, necesitará dos comandos.</span><span class="sxs-lookup"><span data-stu-id="5aba1-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="5aba1-113">El primer comando especifica el directorio de registro, la clave de cuenta de almacenamiento, la letra de la unidad de destino y los requisitos `format/encrypt`, además de los parámetros comunes:</span><span class="sxs-lookup"><span data-stu-id="5aba1-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="5aba1-114">El segundo comando especifica el archivo de diario, un nuevo identificador de sesión y las ubicaciones de origen y de destino:</span><span class="sxs-lookup"><span data-stu-id="5aba1-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="5aba1-115">Copia de un archivo grande en una unidad de disco duro en una segunda sesión de copia</span><span class="sxs-lookup"><span data-stu-id="5aba1-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="5aba1-116">A continuación se especifica un comando de ejemplo que copia un único archivo grande en una unidad que se ha preparado en una sesión de copia anterior:</span><span class="sxs-lookup"><span data-stu-id="5aba1-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="5aba1-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5aba1-117">Next steps</span></span>

* [<span data-ttu-id="5aba1-118">Flujo de trabajo de ejemplo para preparar las unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="5aba1-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
