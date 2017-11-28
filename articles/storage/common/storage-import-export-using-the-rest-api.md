---
title: "Hola aaaUsing API de REST del servicio de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de dónde toofind recursos para usar Hola importación/exportación de Azure servicio API de REST, incluidos ambos material de referencia de tooand cómo."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="d31b1-103">Usar servicio de importación y exportación de Azure Hola API de REST</span><span class="sxs-lookup"><span data-stu-id="d31b1-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="d31b1-104">Hola servicio de importación y exportación de Microsoft Azure expone un control mediante programación de tooenable de API de REST de los trabajos de importación y exportación.</span><span class="sxs-lookup"><span data-stu-id="d31b1-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="d31b1-105">Puede usar la API de REST de hello tooperform todos hello las operaciones que puede realizar con hello de importación y exportación [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d31b1-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d31b1-106">Además, puede usar tooperform de API de REST de hello determinadas operaciones pormenorizadas, como la consulta de porcentaje de finalización de Hola de un trabajo, que no está disponible actualmente en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="d31b1-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which is not currently available in hello Azure classic portal.</span></span>

<span data-ttu-id="d31b1-107">Vea [con hello importación y exportación de Microsoft Azure service tooTransfer datos tooBlob almacenamiento](../storage-import-export-service.md) para obtener información general del servicio de importación y exportación de Hola y un tutorial que muestra cómo toouse Hola toocreate portal clásico y administrar la importación y trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="d31b1-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](../storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="d31b1-108">Puntos de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="d31b1-108">Service endpoints</span></span>

<span data-ttu-id="d31b1-109">Hola servicio de importación y exportación de Azure es un proveedor de recursos para el Administrador de recursos de Azure y proporciona un conjunto de API de REST en hello siguiente extremo HTTPS para administrar los trabajos de importación y exportación:</span><span class="sxs-lookup"><span data-stu-id="d31b1-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="d31b1-110">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="d31b1-110">Versioning</span></span>

<span data-ttu-id="d31b1-111">Las solicitudes de servicio de importación/exportación de toohello debe especificar hello `api-version` parámetro y establezca su valor demasiado`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="d31b1-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="d31b1-112">Operaciones del servicio Import/Export</span><span class="sxs-lookup"><span data-stu-id="d31b1-112">Import/Export service operations</span></span>

[<span data-ttu-id="d31b1-113">Creación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="d31b1-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="d31b1-114">Creación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="d31b1-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="d31b1-115">Recuperación de la información de estado de un trabajo</span><span class="sxs-lookup"><span data-stu-id="d31b1-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="d31b1-116">Enumeración de trabajos</span><span class="sxs-lookup"><span data-stu-id="d31b1-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="d31b1-117">Cancelación y eliminación de trabajos</span><span class="sxs-lookup"><span data-stu-id="d31b1-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="d31b1-118">Realización de una copia de seguridad de los manifiestos de la unidad</span><span class="sxs-lookup"><span data-stu-id="d31b1-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="d31b1-119">Diagnóstico y recuperación de errores para los trabajos de Import/Export</span><span class="sxs-lookup"><span data-stu-id="d31b1-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="d31b1-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d31b1-120">Next steps</span></span>

* <span data-ttu-id="d31b1-121">[Azure Storage Import-Export REST API Reference](/rest/api/storageimportexport) (Referencia de la API de REST de Azure Storage Import-Export)</span><span class="sxs-lookup"><span data-stu-id="d31b1-121">[Storage Import/Export REST](/rest/api/storageimportexport)</span></span>
