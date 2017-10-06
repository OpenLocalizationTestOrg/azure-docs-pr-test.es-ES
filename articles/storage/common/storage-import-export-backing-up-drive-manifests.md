---
title: "aaaBacking los manifiestos de unidad de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohave la unidad de manifiestos para servicio de importación y exportación de Microsoft Azure Hola copia automáticamente."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Realización de copias de seguridad de los manifiestos de los trabajos de Azure Import/Export

Manifiestos de unidad pueden automáticamente realizar copias de seguridad tooblobs establecer hello `BackupDriveManifest` propiedad demasiado`true` en hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) operaciones de API de REST. De forma predeterminada, el Hola manifiestos de unidad no se copian. Hola unidad manifiesto las copias de seguridad se almacenan como blobs en bloques en un contenedor dentro de la cuenta de almacenamiento de hello asociada con el trabajo de Hola. De forma predeterminada, es el nombre del contenedor de hello `waimportexport`, pero puede especificar un nombre diferente en hello `DiagnosticsPath` propiedad al llamar a hello `Put Job` o `Update Job Properties` las operaciones. Hello blob de manifiesto de copia de seguridad son Hola siguiendo el formato: `waies/jobname_driveid_timestamp_manifest.xml`.

 Puede recuperar Hola URI de la unidad de copia de seguridad de Hola manifiestos para un trabajo que realiza la llamada hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación. blob de Hello URI se devuelve en hello `ManifestUri` propiedad para cada unidad.

## <a name="next-steps"></a>Pasos siguientes

* [Usar servicio de importación y exportación de hello API de REST](storage-import-export-using-the-rest-api.md)
