---
title: "Cancelación y eliminación de un trabajo de Azure Import/Export | Microsoft Docs"
description: "Descubra cómo cancelar y eliminar trabajos del servicio Microsoft Azure Import/Export."
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
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="05dbe-103">Cancelación y eliminación de trabajos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="05dbe-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="05dbe-104">Puede solicitar la cancelación de un trabajo antes de que adquiera el estado `Packaging` llamando a la operación de [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) (Actualizar propiedades del trabajo) y establecer el elemento `CancelRequested` en `true`.</span><span class="sxs-lookup"><span data-stu-id="05dbe-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="05dbe-105">El cancelará el trabajo en función de la mejor opción.</span><span class="sxs-lookup"><span data-stu-id="05dbe-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="05dbe-106">Si las unidades están transfiriendo datos, es posible que estos sigan transmitiéndose incluso después de haber solicitado la cancelación.</span><span class="sxs-lookup"><span data-stu-id="05dbe-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="05dbe-107">Un trabajo cancelado adquirirá el estado `Completed` y se conservará durante 90 días; transcurrido ese plazo, se eliminará.</span><span class="sxs-lookup"><span data-stu-id="05dbe-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="05dbe-108">Para eliminar un trabajo, llame a la operación [Eliminar trabajo](/rest/api/storageimportexport/jobs#Jobs_Delete) antes de que este se haya procesado (*es decir*, mientras el trabajo muestre el estado `Creating`).</span><span class="sxs-lookup"><span data-stu-id="05dbe-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="05dbe-109">También puede eliminar un trabajo cuando se encuentra en el estado `Completed`.</span><span class="sxs-lookup"><span data-stu-id="05dbe-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="05dbe-110">Una vez eliminado un trabajo, ya no se podrá acceder a su información y estado mediante la API de REST o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="05dbe-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05dbe-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05dbe-111">Next steps</span></span>

* [<span data-ttu-id="05dbe-112">Uso de la API de REST del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="05dbe-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
