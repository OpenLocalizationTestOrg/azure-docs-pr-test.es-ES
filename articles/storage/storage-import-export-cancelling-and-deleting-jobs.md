---
title: "aaaCancel y eliminar un trabajo de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocancel y eliminar trabajos para hello servicio de importación y exportación de Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Cancelación y eliminación de trabajos de Azure Import/Export

Puede solicitar que se cancele un trabajo antes de que se encuentra en hello `Packaging` estado Hola llamada [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) Hola de operación y configuración `CancelRequested` elemento demasiado`true`. trabajo de Hola se cancelarán de forma óptima. Si las unidades están en proceso de Hola de transferencia de datos, datos pueden seguir toobe transferido incluso después de que ha solicitado la cancelación.

 Un trabajo cancelado pasará toohello `Completed` de estado y se mantendrá durante 90 días, momento en que se eliminarán.

 toodelete un trabajo, llamada hello [Eliminar trabajo](/rest/api/storageimportexport/jobs#Jobs_Delete) operación antes de que se envía el trabajo de hello (*, es decir,*, mientras que el trabajo de Hola Hola `Creating` estado). También puede eliminar un trabajo cuando se encuentra en hello `Completed` estado. Una vez eliminado un trabajo, su información y estado ya no son accesibles a través de la API de REST de Hola u Hola portal de Azure.

## <a name="next-steps"></a>Pasos siguientes

* [Usar servicio de importación y exportación de hello API de REST](storage-import-export-using-the-rest-api.md)
