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
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a>Uso de la API de REST del servicio Azure Import/Export

El servicio Microsoft Azure Import/Export ofrece una API de REST con la que se puede ejercer un control mediante programación de los trabajos de importación y exportación. Puede utilizar la API de REST para realizar las mismas operaciones de importación y exportación que se llevan a cabo con [Azure Portal](https://portal.azure.com/). Además, puede utilizar la API de REST para realizar determinadas operaciones muy concretas, como consultar el porcentaje de finalización de un trabajo, que no están disponibles en el portal clásico por el momento.

Consulte [Uso del servicio Microsoft Azure Import/Export para transferir datos a Blob Storage](storage-import-export-service.md) para leer una introducción al servicio Import/Export y ver un tutorial en el que se demuestra cómo usar el portal clásico para crear y administrar trabajos de importación y exportación.

## <a name="service-endpoints"></a>Puntos de conexión de servicio

El servicio Azure Import/Export actúa como proveedor de recursos de Azure Resource Manager y proporciona un conjunto de API de REST en el siguiente punto de conexión HTTPS para administrar trabajos de importación y exportación:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Control de versiones

Las solicitudes al servicio Import/Export deben incluir el parámetro `api-version` y establecer su valor en `2016-11-01`.

## <a name="importexport-service-operations"></a>Operaciones del servicio Import/Export

[Creación de un trabajo de importación](storage-import-export-creating-an-import-job.md)

[Creación de un trabajo de exportación](storage-import-export-creating-an-export-job.md)

[Recuperación de la información de estado de un trabajo](storage-import-export-retrieving-state-info-for-a-job.md)

[Enumeración de trabajos](storage-import-export-enumerating-jobs.md)

[Cancelación y eliminación de trabajos](storage-import-export-cancelling-and-deleting-jobs.md)

[Realización de una copia de seguridad de los manifiestos de la unidad](storage-import-export-backing-up-drive-manifests.md)

[Diagnóstico y recuperación de errores para los trabajos de Import/Export](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Pasos siguientes

* [Azure Storage Import-Export REST API Reference](/rest/api/storageimportexport) (Referencia de la API de REST de Azure Storage Import-Export)
