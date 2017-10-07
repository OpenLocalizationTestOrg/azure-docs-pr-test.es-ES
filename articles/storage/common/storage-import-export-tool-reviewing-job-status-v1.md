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
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Revisión del estado de un trabajo de Azure Import/Export con archivos de registro de copia
Cuando Hola servicio de importación y exportación de Microsoft Azure procesa las unidades asociadas a un trabajo de importación o exportación, escribe copia registro archivos toohello almacenamiento cuenta tooor desde la que está importando o exportando blobs. archivo de registro de Hello contiene el estado detallado de cada archivo que se importó o exportó. archivo de registro de copia de Hello URL tooeach se devuelve al consultar el estado de saludo de un trabajo completado; vea [Get Job](/rest/api/storageservices/Get-Job3) para obtener más información.  

## <a name="example-urls"></a>URL de ejemplo

siguiente Hola es direcciones URL de ejemplo para los archivos de registro de copia de un trabajo de importación con dos unidades:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Vea [servicio de importación y exportación de formato de archivo de registro](../storage-import-export-file-format-log.md) para el formato de Hola de registros de copia y la lista completa de Hola de códigos de estado.  
  
## <a name="next-steps"></a>Pasos siguientes
 
 * [Setting Up Hola herramienta de importación y exportación de Azure](storage-import-export-tool-setup-v1.md)   
 * [Preparación de unidades de disco duro para un trabajo de importación](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Reparación de un trabajo de importación](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Reparación de un trabajo de exportación](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Solución de problemas de hello herramienta de importación y exportación de Azure](storage-import-export-tool-troubleshooting-v1.md)
