---
title: "estado del trabajo de importación y exportación de Azure - v1 aaaReviewing | Documentos de Microsoft"
description: "Obtenga información acerca de cómo archivos de registro de hello toouse creados cuando Hola importar o exportación un trabajo se ejecutó el estado de hello toosee de trabajo de importación y exportación de Hola."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="16159-103">Revisión del estado de un trabajo de Azure Import/Export con archivos de registro de copia</span><span class="sxs-lookup"><span data-stu-id="16159-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="16159-104">Cuando Hola servicio de importación y exportación de Microsoft Azure procesa las unidades asociadas a un trabajo de importación o exportación, escribe copia registro archivos toohello almacenamiento cuenta tooor desde la que está importando o exportando blobs.</span><span class="sxs-lookup"><span data-stu-id="16159-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="16159-105">archivo de registro de Hello contiene el estado detallado de cada archivo que se importó o exportó.</span><span class="sxs-lookup"><span data-stu-id="16159-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="16159-106">archivo de registro de copia de Hello URL tooeach se devuelve al consultar el estado de saludo de un trabajo completado; vea [Get Job](/rest/api/storageservices/Get-Job3) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="16159-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="16159-107">URL de ejemplo</span><span class="sxs-lookup"><span data-stu-id="16159-107">Example URLs</span></span>

<span data-ttu-id="16159-108">siguiente Hola es direcciones URL de ejemplo para los archivos de registro de copia de un trabajo de importación con dos unidades:</span><span class="sxs-lookup"><span data-stu-id="16159-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="16159-109">Vea [servicio de importación y exportación de formato de archivo de registro](../storage-import-export-file-format-log.md) para el formato de Hola de registros de copia y la lista completa de Hola de códigos de estado.</span><span class="sxs-lookup"><span data-stu-id="16159-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="16159-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16159-110">Next steps</span></span>
 
 * [<span data-ttu-id="16159-111">Setting Up Hola herramienta de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="16159-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="16159-112">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="16159-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="16159-113">Reparación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="16159-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="16159-114">Reparación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="16159-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="16159-115">Solución de problemas de hello herramienta de importación y exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="16159-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
