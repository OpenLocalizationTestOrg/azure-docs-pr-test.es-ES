---
title: aaa "grupo de lote de Azure eliminar evento complete | Documentos de Microsoft"
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="8eb54-103">Evento de finalización de eliminación del grupo</span><span class="sxs-lookup"><span data-stu-id="8eb54-103">Pool delete complete event</span></span>

 <span data-ttu-id="8eb54-104">Este evento se genera cuando se finaliza una operación de eliminación del grupo.</span><span class="sxs-lookup"><span data-stu-id="8eb54-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="8eb54-105">Hello en el ejemplo siguiente se muestra hello cuerpo de un evento complete de eliminación de grupo.</span><span class="sxs-lookup"><span data-stu-id="8eb54-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="8eb54-106">Elemento</span><span class="sxs-lookup"><span data-stu-id="8eb54-106">Element</span></span>|<span data-ttu-id="8eb54-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="8eb54-107">Type</span></span>|<span data-ttu-id="8eb54-108">Notas</span><span class="sxs-lookup"><span data-stu-id="8eb54-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="8eb54-109">id</span><span class="sxs-lookup"><span data-stu-id="8eb54-109">id</span></span>|<span data-ttu-id="8eb54-110">String</span><span class="sxs-lookup"><span data-stu-id="8eb54-110">String</span></span>|<span data-ttu-id="8eb54-111">Hola Id. de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb54-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="8eb54-112">startTime</span><span class="sxs-lookup"><span data-stu-id="8eb54-112">startTime</span></span>|<span data-ttu-id="8eb54-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="8eb54-113">DateTime</span></span>|<span data-ttu-id="8eb54-114">Hola eliminar grupo Hola comenzó.</span><span class="sxs-lookup"><span data-stu-id="8eb54-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="8eb54-115">endTime</span><span class="sxs-lookup"><span data-stu-id="8eb54-115">endTime</span></span>|<span data-ttu-id="8eb54-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="8eb54-116">DateTime</span></span>|<span data-ttu-id="8eb54-117">Hello tiempo eliminar grupo Hola completado.</span><span class="sxs-lookup"><span data-stu-id="8eb54-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="8eb54-118">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8eb54-118">Remarks</span></span>
<span data-ttu-id="8eb54-119">Para más información sobre los estados y códigos de error para la operación de cambio de tamaño del grupo, consulte [Eliminar un grupo de una cuenta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="8eb54-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>