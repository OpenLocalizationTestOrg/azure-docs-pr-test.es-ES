---
title: "Revisión del estado de un trabajo de Azure Import/Export (versión 1) | Microsoft Docs"
description: "Obtenga información sobre cómo usar los archivos de registro creados cuando se ejecutó el trabajo de importación o exportación para ver el estado del trabajo de importación y exportación."
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
ms.openlocfilehash: bdb30bc28c36ab9e969efc8be3b87b97e4027b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="674ef-103">Revisión del estado de un trabajo de Azure Import/Export con archivos de registro de copia</span><span class="sxs-lookup"><span data-stu-id="674ef-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="674ef-104">Cuando el servicio Microsoft Azure Import/Export procesa las unidades asociadas a un trabajo de importación o exportación, escribe archivos de registro de copia en la cuenta de almacenamiento con origen o destino en la ubicación donde está importando o exportando blobs.</span><span class="sxs-lookup"><span data-stu-id="674ef-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="674ef-105">El archivo de registro contiene el estado detallado de cada archivo que se importó o exportó.</span><span class="sxs-lookup"><span data-stu-id="674ef-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="674ef-106">La dirección URL de cada archivo de registro de copia se devuelve al consultar el estado de un trabajo completado; vea el artículo de [obtención de trabajos](/rest/api/storageservices/Get-Job3) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="674ef-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="674ef-107">URL de ejemplo</span><span class="sxs-lookup"><span data-stu-id="674ef-107">Example URLs</span></span>

<span data-ttu-id="674ef-108">Las siguientes son direcciones URL de ejemplo de los archivos de registro de copia de un trabajo de importación con dos unidades:</span><span class="sxs-lookup"><span data-stu-id="674ef-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="674ef-109">Vea [Formato del archivo de registro del servicio Import-Export](../storage-import-export-file-format-log.md) para consultar el formato de los registros de copia y la lista completa de códigos de estado.</span><span class="sxs-lookup"><span data-stu-id="674ef-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="674ef-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="674ef-110">Next steps</span></span>
 
 * [<span data-ttu-id="674ef-111">Configuración de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="674ef-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="674ef-112">Preparación de unidades de disco duro para un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="674ef-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="674ef-113">Reparación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="674ef-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="674ef-114">Reparación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="674ef-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="674ef-115">Solución de problemas de la herramienta Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="674ef-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
