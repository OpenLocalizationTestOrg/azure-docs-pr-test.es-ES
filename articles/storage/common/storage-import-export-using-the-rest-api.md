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
# <a name="using-hello-azure-importexport-service-rest-api"></a>Usar servicio de importación y exportación de Azure Hola API de REST

Hola servicio de importación y exportación de Microsoft Azure expone un control mediante programación de tooenable de API de REST de los trabajos de importación y exportación. Puede usar la API de REST de hello tooperform todos hello las operaciones que puede realizar con hello de importación y exportación [portal de Azure](https://portal.azure.com/). Además, puede usar tooperform de API de REST de hello determinadas operaciones pormenorizadas, como la consulta de porcentaje de finalización de Hola de un trabajo, que no está disponible actualmente en hello portal de Azure clásico.

Vea [con hello importación y exportación de Microsoft Azure service tooTransfer datos tooBlob almacenamiento](../storage-import-export-service.md) para obtener información general del servicio de importación y exportación de Hola y un tutorial que muestra cómo toouse Hola toocreate portal clásico y administrar la importación y trabajos de exportación.

## <a name="service-endpoints"></a>Puntos de conexión de servicio

Hola servicio de importación y exportación de Azure es un proveedor de recursos para el Administrador de recursos de Azure y proporciona un conjunto de API de REST en hello siguiente extremo HTTPS para administrar los trabajos de importación y exportación:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Control de versiones

Las solicitudes de servicio de importación/exportación de toohello debe especificar hello `api-version` parámetro y establezca su valor demasiado`2016-11-01`.

## <a name="importexport-service-operations"></a>Operaciones del servicio Import/Export

[Creación de un trabajo de importación](../storage-import-export-creating-an-import-job.md)

[Creación de un trabajo de exportación](../storage-import-export-creating-an-export-job.md)

[Recuperación de la información de estado de un trabajo](storage-import-export-retrieving-state-info-for-a-job.md)

[Enumeración de trabajos](../storage-import-export-enumerating-jobs.md)

[Cancelación y eliminación de trabajos](storage-import-export-cancelling-and-deleting-jobs.md)

[Realización de una copia de seguridad de los manifiestos de la unidad](../storage-import-export-backing-up-drive-manifests.md)

[Diagnóstico y recuperación de errores para los trabajos de Import/Export](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Pasos siguientes

* [Azure Storage Import-Export REST API Reference](/rest/api/storageimportexport) (Referencia de la API de REST de Azure Storage Import-Export)
