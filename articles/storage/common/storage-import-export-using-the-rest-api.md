---
title: Uso de la API de REST del servicio Azure Import/Export | Microsoft Docs
description: "Obtenga información sobre dónde encontrar recursos para usar la API de REST del servicio Azure Import/Export, incluido el material de instrucciones y de referencia."
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
ms.openlocfilehash: b780385ad0af34bcb15639683d1aa5d689b38b50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="b4baa-103">Uso de la API de REST del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="b4baa-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="b4baa-104">El servicio Microsoft Azure Import/Export ofrece una API de REST con la que se puede ejercer un control mediante programación de los trabajos de importación y exportación.</span><span class="sxs-lookup"><span data-stu-id="b4baa-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="b4baa-105">Puede utilizar la API de REST para realizar las mismas operaciones de importación y exportación que se llevan a cabo con [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4baa-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b4baa-106">Además, puede utilizar la API de REST para realizar determinadas operaciones muy concretas, como consultar el porcentaje de finalización de un trabajo, que no están disponibles en el Portal de Azure clásico por el momento.</span><span class="sxs-lookup"><span data-stu-id="b4baa-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which is not currently available in the Azure classic portal.</span></span>

<span data-ttu-id="b4baa-107">Consulte [Uso del servicio Microsoft Azure Import/Export para transferir datos a Blob Storage](../storage-import-export-service.md) para leer una introducción al servicio Import/Export y ver un tutorial en el que se demuestra cómo usar el portal clásico para crear y administrar trabajos de importación y exportación.</span><span class="sxs-lookup"><span data-stu-id="b4baa-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](../storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="b4baa-108">Puntos de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="b4baa-108">Service endpoints</span></span>

<span data-ttu-id="b4baa-109">El servicio Azure Import/Export actúa como proveedor de recursos de Azure Resource Manager y proporciona un conjunto de API de REST en el siguiente punto de conexión HTTPS para administrar trabajos de importación y exportación:</span><span class="sxs-lookup"><span data-stu-id="b4baa-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="b4baa-110">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="b4baa-110">Versioning</span></span>

<span data-ttu-id="b4baa-111">Las solicitudes al servicio Import/Export deben incluir el parámetro `api-version` y establecer su valor en `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="b4baa-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="b4baa-112">Operaciones del servicio Import/Export</span><span class="sxs-lookup"><span data-stu-id="b4baa-112">Import/Export service operations</span></span>

[<span data-ttu-id="b4baa-113">Creación de un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="b4baa-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="b4baa-114">Creación de un trabajo de exportación</span><span class="sxs-lookup"><span data-stu-id="b4baa-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="b4baa-115">Recuperación de la información de estado de un trabajo</span><span class="sxs-lookup"><span data-stu-id="b4baa-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="b4baa-116">Enumeración de trabajos</span><span class="sxs-lookup"><span data-stu-id="b4baa-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="b4baa-117">Cancelación y eliminación de trabajos</span><span class="sxs-lookup"><span data-stu-id="b4baa-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="b4baa-118">Realización de una copia de seguridad de los manifiestos de la unidad</span><span class="sxs-lookup"><span data-stu-id="b4baa-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="b4baa-119">Diagnóstico y recuperación de errores para los trabajos de Import/Export</span><span class="sxs-lookup"><span data-stu-id="b4baa-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="b4baa-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4baa-120">Next steps</span></span>

* <span data-ttu-id="b4baa-121">[Azure Storage Import-Export REST API Reference](/rest/api/storageimportexport) (Referencia de la API de REST de Azure Storage Import-Export)</span><span class="sxs-lookup"><span data-stu-id="b4baa-121">[Storage Import/Export REST](/rest/api/storageimportexport)</span></span>
