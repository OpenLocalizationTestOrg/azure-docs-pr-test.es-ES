---
title: "Realización de copias de seguridad de los manifiestos de las unidades de Azure Import/Export | Microsoft Docs"
description: "Descubra cómo conseguir que se realicen copias de seguridad automáticas de los manifiestos de las unidades del servicio Microsoft Azure Import/Export."
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
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="d59f4-103">Realización de copias de seguridad de los manifiestos de los trabajos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="d59f4-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="d59f4-104">Es posible realizar copias de seguridad automáticas de los manifiestos de las unidades en blobs estableciendo la propiedad `BackupDriveManifest` en `true` en las operaciones de API de REST [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) (Poner trabajo) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) (Actualizar propiedades del trabajo).</span><span class="sxs-lookup"><span data-stu-id="d59f4-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="d59f4-105">De forma predeterminada, no se realizan copias de seguridad de los manifiestos de las unidades.</span><span class="sxs-lookup"><span data-stu-id="d59f4-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="d59f4-106">Las copias de seguridad de los manifiestos de las unidades se almacenan como blobs en bloques en un contenedor dentro de la cuenta de almacenamiento asociada al trabajo.</span><span class="sxs-lookup"><span data-stu-id="d59f4-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="d59f4-107">De forma predeterminada, el nombre del contenedor es `waimportexport`, pero puede especificar uno distinto en la propiedad `DiagnosticsPath` al llamar a las operaciones `Put Job` o `Update Job Properties`.</span><span class="sxs-lookup"><span data-stu-id="d59f4-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="d59f4-108">Los nombres de los blobs de manifiestos de copia de seguridad presentan el siguiente formato: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d59f4-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="d59f4-109">Puede recuperar el identificador URI de los manifiestos de las unidades de copia de seguridad de un trabajo llamando a la operación [Obtener trabajo](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="d59f4-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="d59f4-110">El identificador URI del blob se devuelve en la propiedad `ManifestUri` de cada unidad.</span><span class="sxs-lookup"><span data-stu-id="d59f4-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d59f4-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d59f4-111">Next steps</span></span>

* [<span data-ttu-id="d59f4-112">Uso de la API de REST del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="d59f4-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
