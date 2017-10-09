---
title: "Hola aaaTroubleshooting herramienta de importación y exportación de Azure | Documentos de Microsoft"
description: "Información sobre algunos de los problemas comunes de hello aparece cuando se usa la herramienta de importación y exportación de Azure de Hola y cómo toohandle ellos."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="9f72c-103">Solución de problemas de hello herramienta de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="9f72c-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="9f72c-104">Hola herramienta de importación y exportación de Microsoft Azure devuelve mensajes de error si encuentra problemas.</span><span class="sxs-lookup"><span data-stu-id="9f72c-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="9f72c-105">En este tema se enumeran algunos problemas comunes con los que los usuarios se pueden encontrar.</span><span class="sxs-lookup"><span data-stu-id="9f72c-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="9f72c-106">Se produce un error en una sesión de copia, ¿qué debo hacer?</span><span class="sxs-lookup"><span data-stu-id="9f72c-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="9f72c-107">Cuando se produce un error en una sesión de copia, tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="9f72c-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="9f72c-108">Si el error de hello es recuperable, por ejemplo, si el recurso compartido de red de hello estaba sin conexión para una breve período y ahora es nuevo en línea, puede reanudar la sesión de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f72c-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="9f72c-109">Si Hola error no es recuperable, por ejemplo, si ha especificado el directorio de archivos de origen incorrecto de hello en parámetros de línea de comandos de hello, deberá sesión de copia de tooabort Hola.</span><span class="sxs-lookup"><span data-stu-id="9f72c-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="9f72c-110">Vea [Preparación de unidades de disco duro para un trabajo de importación](storage-import-export-tool-preparing-hard-drives-import-v1.md) para más información sobre cómo reanudar y anular sesiones de copia.</span><span class="sxs-lookup"><span data-stu-id="9f72c-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="9f72c-111">No puedo reanudar o anular una sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="9f72c-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="9f72c-112">Si es de sesión de copia de Hola Hola primera sesión de copia de una unidad, debería indicar el mensaje de error de Hola: "hello primera sesión de copia se no se puede reanudar o anulado."</span><span class="sxs-lookup"><span data-stu-id="9f72c-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="9f72c-113">En este caso, puede eliminar el archivo de diario anterior de Hola y vuelva a ejecutar el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="9f72c-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="9f72c-114">Si una sesión de copia no es hello primera de ellas para una unidad, siempre puede reanudar o anulado.</span><span class="sxs-lookup"><span data-stu-id="9f72c-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="9f72c-115">He perdido el archivo de diario de hello, ¿todavía puedo crear trabajo de hello?</span><span class="sxs-lookup"><span data-stu-id="9f72c-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="9f72c-116">archivo de diario de Hola para una unidad de disco contiene Hola toda la información de copia de unidad de datos toothis, y es necesario tooadd más unidad de archivos de toohello y será toocreate usa un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="9f72c-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="9f72c-117">Si el archivo de diario de Hola se pierde, tendrá tooredo todas las sesiones de copia de Hola para unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f72c-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="9f72c-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f72c-118">Next steps</span></span>
 
* [<span data-ttu-id="9f72c-119">Configurar la herramienta de importación y exportación de azure Hola</span><span class="sxs-lookup"><span data-stu-id="9f72c-119">Setting up hello azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="9f72c-120">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="9f72c-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="9f72c-121">Revisión del estado del trabajo con archivos de registro de copia</span><span class="sxs-lookup"><span data-stu-id="9f72c-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="9f72c-122">Reparación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="9f72c-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="9f72c-123">Reparación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="9f72c-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
