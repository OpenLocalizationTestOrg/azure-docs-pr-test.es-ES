---
title: "Evento completo de eliminación de grupo de Azure Batch | Microsoft Docs"
description: "Referencia del evento completo de eliminación de grupo de Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="4031d-103">Evento de finalización de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="4031d-103">Pool delete complete event</span></span>

 <span data-ttu-id="4031d-104">Este evento se genera cuando se finaliza una operación de eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="4031d-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="4031d-105">En el siguiente ejemplo, se muestra el cuerpo de un evento de finalización de eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="4031d-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="4031d-106">Elemento</span><span class="sxs-lookup"><span data-stu-id="4031d-106">Element</span></span>|<span data-ttu-id="4031d-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="4031d-107">Type</span></span>|<span data-ttu-id="4031d-108">Notas</span><span class="sxs-lookup"><span data-stu-id="4031d-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="4031d-109">id</span><span class="sxs-lookup"><span data-stu-id="4031d-109">id</span></span>|<span data-ttu-id="4031d-110">String</span><span class="sxs-lookup"><span data-stu-id="4031d-110">String</span></span>|<span data-ttu-id="4031d-111">El identificador del grupo.</span><span class="sxs-lookup"><span data-stu-id="4031d-111">The id of the pool.</span></span>|
|<span data-ttu-id="4031d-112">startTime</span><span class="sxs-lookup"><span data-stu-id="4031d-112">startTime</span></span>|<span data-ttu-id="4031d-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="4031d-113">DateTime</span></span>|<span data-ttu-id="4031d-114">La hora en que se inició la eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="4031d-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="4031d-115">endTime</span><span class="sxs-lookup"><span data-stu-id="4031d-115">endTime</span></span>|<span data-ttu-id="4031d-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="4031d-116">DateTime</span></span>|<span data-ttu-id="4031d-117">La hora en que finalizó la eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="4031d-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="4031d-118">Comentarios</span><span class="sxs-lookup"><span data-stu-id="4031d-118">Remarks</span></span>
<span data-ttu-id="4031d-119">Para más información sobre los estados y códigos de error para la operación de cambio de tamaño del grupo, consulte [Eliminar un grupo de una cuenta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="4031d-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>