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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="a2abb-103">Realización de copias de seguridad de los manifiestos de los trabajos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="a2abb-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="a2abb-104">Manifiestos de unidad pueden automáticamente realizar copias de seguridad tooblobs establecer hello `BackupDriveManifest` propiedad demasiado`true` en hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) operaciones de API de REST.</span><span class="sxs-lookup"><span data-stu-id="a2abb-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="a2abb-105">De forma predeterminada, el Hola manifiestos de unidad no se copian.</span><span class="sxs-lookup"><span data-stu-id="a2abb-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="a2abb-106">Hola unidad manifiesto las copias de seguridad se almacenan como blobs en bloques en un contenedor dentro de la cuenta de almacenamiento de hello asociada con el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2abb-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="a2abb-107">De forma predeterminada, es el nombre del contenedor de hello `waimportexport`, pero puede especificar un nombre diferente en hello `DiagnosticsPath` propiedad al llamar a hello `Put Job` o `Update Job Properties` las operaciones.</span><span class="sxs-lookup"><span data-stu-id="a2abb-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="a2abb-108">Hello blob de manifiesto de copia de seguridad son Hola siguiendo el formato: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a2abb-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="a2abb-109">Puede recuperar Hola URI de la unidad de copia de seguridad de Hola manifiestos para un trabajo que realiza la llamada hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación.</span><span class="sxs-lookup"><span data-stu-id="a2abb-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a2abb-110">blob de Hello URI se devuelve en hello `ManifestUri` propiedad para cada unidad.</span><span class="sxs-lookup"><span data-stu-id="a2abb-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2abb-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2abb-111">Next steps</span></span>

* [<span data-ttu-id="a2abb-112">Usar servicio de importación y exportación de hello API de REST</span><span class="sxs-lookup"><span data-stu-id="a2abb-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
