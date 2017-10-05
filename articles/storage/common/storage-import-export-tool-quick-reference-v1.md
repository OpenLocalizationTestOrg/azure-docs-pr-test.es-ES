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
ms.openlocfilehash: 370cf6fae7ae106e8341f65086c8b8187d335746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="ac32e-104">Referencia rápida de comandos usados con frecuencia para trabajos de importación</span><span class="sxs-lookup"><span data-stu-id="ac32e-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="ac32e-105">En esta sección se proporciona una referencia rápida para algunos comandos que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="ac32e-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="ac32e-106">Para obtener información detallada sobre el uso, vea [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparación de los discos duros para un trabajo de importación).</span><span class="sxs-lookup"><span data-stu-id="ac32e-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-to-the-hard-drive"></a><span data-ttu-id="ac32e-107">Preparación de un disco duro cuando los datos ya se han copiado en el disco duro</span><span class="sxs-lookup"><span data-stu-id="ac32e-107">Prepare a hard drive when data has already been copied to the hard drive</span></span>
 <span data-ttu-id="ac32e-108">El siguiente comando prepara una unidad de disco duro cuando los datos ya se han copiado en ella, pero aún no se han cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="ac32e-108">The following command prepares a hard drive when data has already been copied to it, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="ac32e-109">Copia de un único directorio en una unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="ac32e-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="ac32e-110">El comando siguiente copia un único directorio de origen en una unidad de disco duro que aún no se ha cifrado con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="ac32e-110">The following command copies a single source directory to a hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-to-a-hard-drive"></a><span data-ttu-id="ac32e-111">Copia de dos directorios en una unidad de disco duro</span><span class="sxs-lookup"><span data-stu-id="ac32e-111">Copy two directories to a hard drive</span></span>  
 <span data-ttu-id="ac32e-112">Para copiar dos directorios de origen en una unidad, use los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ac32e-112">To copy two source directories to a drive, use the following commands:</span></span>  
  
 <span data-ttu-id="ac32e-113">El primero especifica el directorio de registro, la clave de cuenta de almacenamiento, la letra de la unidad de destino y los requisitos de `format/encrypt`, además de los parámetros comunes:</span><span class="sxs-lookup"><span data-stu-id="ac32e-113">The first command specifies the log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="ac32e-114">El segundo comando especifica el archivo de diario, un nuevo identificador de sesión y las ubicaciones de origen y de destino:</span><span class="sxs-lookup"><span data-stu-id="ac32e-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="ac32e-115">Copia de un archivo grande en una unidad de disco duro en una segunda sesión de copia</span><span class="sxs-lookup"><span data-stu-id="ac32e-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="ac32e-116">El comando siguiente copia un único archivo grande en una unidad de disco duro que se ha preparado en una sesión de copia anterior:</span><span class="sxs-lookup"><span data-stu-id="ac32e-116">The following command copies a single large file to a hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="ac32e-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac32e-117">Next steps</span></span>

* [<span data-ttu-id="ac32e-118">Flujo de trabajo de ejemplo para preparar las unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="ac32e-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
