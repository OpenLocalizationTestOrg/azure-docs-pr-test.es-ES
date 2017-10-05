---
title: "Solución de problemas de la herramienta Azure Import/Export | Microsoft Docs"
description: "Obtenga información sobre problemas comunes observados al usar la herramienta Import/Export de Azure y cómo abordarlos."
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
ms.openlocfilehash: 7bfda602dbc0ea47828a7c9243b8b9b09ec78432
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="31d43-103">Solución de problemas de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="31d43-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="31d43-104">La herramienta Microsoft Azure Import/Export devuelve mensajes de error si encuentra problemas.</span><span class="sxs-lookup"><span data-stu-id="31d43-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="31d43-105">En este tema se enumeran algunos problemas comunes con los que los usuarios se pueden encontrar.</span><span class="sxs-lookup"><span data-stu-id="31d43-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="31d43-106">Se produce un error en una sesión de copia, ¿qué debo hacer?</span><span class="sxs-lookup"><span data-stu-id="31d43-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="31d43-107">Cuando se produce un error en una sesión de copia, tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="31d43-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="31d43-108">Si el error es recuperable, por ejemplo, si el recurso compartido de red estuvo sin conexión durante un breve período y ahora vuelve a tener conexión, puede reanudar la sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="31d43-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="31d43-109">Si el error no es recuperable, por ejemplo, si especificó el directorio de archivos de origen incorrecto en los parámetros de la línea de comandos, debe anular la sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="31d43-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="31d43-110">Vea [Preparación de unidades de disco duro para un trabajo de importación](../storage-import-export-tool-preparing-hard-drives-import-v1.md) para más información sobre cómo reanudar y anular sesiones de copia.</span><span class="sxs-lookup"><span data-stu-id="31d43-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="31d43-111">No puedo reanudar o anular una sesión de copia.</span><span class="sxs-lookup"><span data-stu-id="31d43-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="31d43-112">Si la sesión de copia es la primera sesión de copia de una unidad, entonces el mensaje de error debe indicar: "La primera sesión de copia se no se puede reanudar o anular".</span><span class="sxs-lookup"><span data-stu-id="31d43-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="31d43-113">En este caso, puede eliminar el archivo de diario antiguo y volver a ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="31d43-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="31d43-114">Si una sesión de copia no es la primera para una unidad, siempre se puede reanudar o anular.</span><span class="sxs-lookup"><span data-stu-id="31d43-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="31d43-115">He perdido el archivo de diario, ¿todavía puedo crear el trabajo?</span><span class="sxs-lookup"><span data-stu-id="31d43-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="31d43-116">El archivo de diario para una unidad contiene toda la información de copia de datos a esta unidad, y es necesario para agregar más archivos a la unidad y se utilizará para crear un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="31d43-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="31d43-117">Si el archivo de diario se pierde, tendrá que rehacer todas las sesiones de copia de la unidad.</span><span class="sxs-lookup"><span data-stu-id="31d43-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="31d43-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31d43-118">Next steps</span></span>
 
* [<span data-ttu-id="31d43-119">Configuración de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="31d43-119">Setting up the azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="31d43-120">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="31d43-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="31d43-121">Revisión del estado del trabajo con archivos de registro de copia</span><span class="sxs-lookup"><span data-stu-id="31d43-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="31d43-122">Reparación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="31d43-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="31d43-123">Reparación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="31d43-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
