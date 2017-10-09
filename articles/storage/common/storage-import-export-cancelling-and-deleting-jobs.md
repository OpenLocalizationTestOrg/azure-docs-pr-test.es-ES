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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="1a17c-103">Cancelación y eliminación de trabajos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="1a17c-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="1a17c-104">toorequest que un trabajo se canceló antes de que se encuentra en hello `Packaging` estado, llamada hello [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) hello de conjunto y operación `CancelRequested` elemento demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="1a17c-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="1a17c-105">Hola trabajos se cancelan en forma de mejor esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="1a17c-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="1a17c-106">Si las unidades están en proceso de Hola de transferencia de datos, datos pueden seguir toobe transferido incluso después de que ha solicitado la cancelación.</span><span class="sxs-lookup"><span data-stu-id="1a17c-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="1a17c-107">Un trabajo cancelado está desplazada toohello `Completed` estado de error y se mantendrá durante 90 días, momento en que se elimina.</span><span class="sxs-lookup"><span data-stu-id="1a17c-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="1a17c-108">toodelete un trabajo, llamada hello [Eliminar trabajo](/rest/api/storageimportexport/jobs#Jobs_Delete) operación antes de que se envía el trabajo de hello (es decir, mientras se está de trabajo de Hola Hola `Creating` estado).</span><span class="sxs-lookup"><span data-stu-id="1a17c-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="1a17c-109">También puede eliminar un trabajo cuando se encuentra en hello `Completed` estado.</span><span class="sxs-lookup"><span data-stu-id="1a17c-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="1a17c-110">Después de elimina un trabajo, su información y estado ya no son accesibles a través de la API de REST de Hola u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a17c-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a17c-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a17c-111">Next steps</span></span>

* [<span data-ttu-id="1a17c-112">Usar servicio de importación y exportación de hello API de REST</span><span class="sxs-lookup"><span data-stu-id="1a17c-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
