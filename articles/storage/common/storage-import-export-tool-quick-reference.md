---
title: "Referencia rápida de los comandos de trabajos de importación de la herramienta Azure Import/Export | Microsoft Docs"
description: "Referencia sobre los comandos de la herramienta de Azure Import/Export para comandos de trabajos de importación usados con frecuencia."
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
ms.openlocfilehash: d51ae35ead0e7d8289de663e5b7b48d28271e810
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="273ca-103">Referencia rápida de comandos usados con frecuencia para trabajos de importación</span><span class="sxs-lookup"><span data-stu-id="273ca-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="273ca-104">En este artículo se proporciona una referencia rápida para algunos comandos que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="273ca-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="273ca-105">Para obtener información detallada sobre el uso, vea [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparación de los discos duros para un trabajo de importación).</span><span class="sxs-lookup"><span data-stu-id="273ca-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="273ca-106">Primera sesión</span><span class="sxs-lookup"><span data-stu-id="273ca-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="273ca-107">Segunda sesión</span><span class="sxs-lookup"><span data-stu-id="273ca-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="273ca-108">Anulación de la última sesión</span><span class="sxs-lookup"><span data-stu-id="273ca-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="273ca-109">Reanudación de la última sesión interrumpida</span><span class="sxs-lookup"><span data-stu-id="273ca-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-to-latest-session"></a><span data-ttu-id="273ca-110">Adición de unidades a la última sesión</span><span class="sxs-lookup"><span data-stu-id="273ca-110">Add drives to latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="273ca-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="273ca-111">Next steps</span></span>

* [<span data-ttu-id="273ca-112">Flujo de trabajo de ejemplo para preparar las unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="273ca-112">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
