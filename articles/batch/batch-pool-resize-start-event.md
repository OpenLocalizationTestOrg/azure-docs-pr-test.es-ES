---
title: "Evento de inicio de cambio de tamaño de grupo de Azure Batch | Microsoft Docs"
description: "Referencia del evento de inicio de cambio de tamaño de grupo de Batch."
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="c0c88-103">Evento de inicio de cambio de tamaño de grupo</span><span class="sxs-lookup"><span data-stu-id="c0c88-103">Pool resize start event</span></span>

 <span data-ttu-id="c0c88-104">Este evento se genera se inicia el cambio de tamaño de un grupo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="c0c88-105">Puesto que el cambio de tamaño de grupo es un evento asincrónico, puede esperar que se genere un evento completo de cambio de tamaño de grupo cuando se haya completado la operación de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="c0c88-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="c0c88-106">En el ejemplo siguiente se muestra el cuerpo de un evento de inicio de cambio de tamaño de grupo de 0 a 2 nodos con un cambio de tamaño manual.</span><span class="sxs-lookup"><span data-stu-id="c0c88-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="c0c88-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="c0c88-107">Element</span></span>|<span data-ttu-id="c0c88-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="c0c88-108">Type</span></span>|<span data-ttu-id="c0c88-109">Notas</span><span class="sxs-lookup"><span data-stu-id="c0c88-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="c0c88-110">poolId</span><span class="sxs-lookup"><span data-stu-id="c0c88-110">poolId</span></span>|<span data-ttu-id="c0c88-111">String</span><span class="sxs-lookup"><span data-stu-id="c0c88-111">String</span></span>|<span data-ttu-id="c0c88-112">El identificador del grupo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-112">The id of the pool.</span></span>|
|<span data-ttu-id="c0c88-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="c0c88-113">nodeDeallocationOption</span></span>|<span data-ttu-id="c0c88-114">String</span><span class="sxs-lookup"><span data-stu-id="c0c88-114">String</span></span>|<span data-ttu-id="c0c88-115">Especifica cuándo se pueden quitar los nodos del grupo, si disminuye el tamaño del grupo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="c0c88-116">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="c0c88-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="c0c88-117">**requeue**: finalizar las tareas en ejecución y volver a ponerlas en cola.</span><span class="sxs-lookup"><span data-stu-id="c0c88-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="c0c88-118">Las tareas volverán a ejecutarse cuando se habilite el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="c0c88-119">Elimine los nodos en cuanto finalicen las tareas.</span><span class="sxs-lookup"><span data-stu-id="c0c88-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="c0c88-120">**terminate**: finalizar las tareas en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c0c88-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="c0c88-121">Las tareas no se ejecutarán de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-121">The tasks will not run again.</span></span> <span data-ttu-id="c0c88-122">Elimine los nodos en cuanto finalicen las tareas.</span><span class="sxs-lookup"><span data-stu-id="c0c88-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="c0c88-123">**taskcompletion**: permita que finalicen las tareas actualmente en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c0c88-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="c0c88-124">No programe ninguna tarea nueva mientras espera.</span><span class="sxs-lookup"><span data-stu-id="c0c88-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="c0c88-125">Elimine los nodos cuando se hayan completado todas las tareas.</span><span class="sxs-lookup"><span data-stu-id="c0c88-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="c0c88-126">**Retaineddata**: permite que finalicen las tareas actualmente en ejecución, luego espera que caduquen los períodos de retención de datos de todas las tareas.</span><span class="sxs-lookup"><span data-stu-id="c0c88-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="c0c88-127">No programe ninguna tarea nueva mientras espera.</span><span class="sxs-lookup"><span data-stu-id="c0c88-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="c0c88-128">Elimine los nodos cuando hayan caducado los períodos de retención de todas las tareas.</span><span class="sxs-lookup"><span data-stu-id="c0c88-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="c0c88-129">El valor predeterminado es requeue.</span><span class="sxs-lookup"><span data-stu-id="c0c88-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="c0c88-130">Si aumenta el tamaño del grupo, entonces el valor se establece en **invalid**.</span><span class="sxs-lookup"><span data-stu-id="c0c88-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="c0c88-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="c0c88-131">currentDedicated</span></span>|<span data-ttu-id="c0c88-132">Int32</span><span class="sxs-lookup"><span data-stu-id="c0c88-132">Int32</span></span>|<span data-ttu-id="c0c88-133">El número de nodos de proceso actualmente asignados al grupo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="c0c88-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="c0c88-134">targetDedicated</span></span>|<span data-ttu-id="c0c88-135">Int32</span><span class="sxs-lookup"><span data-stu-id="c0c88-135">Int32</span></span>|<span data-ttu-id="c0c88-136">El número de nodos de proceso solicitados para el grupo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="c0c88-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="c0c88-137">enableAutoScale</span></span>|<span data-ttu-id="c0c88-138">Booleano</span><span class="sxs-lookup"><span data-stu-id="c0c88-138">Bool</span></span>|<span data-ttu-id="c0c88-139">Especifica si el tamaño del grupo se ajusta automáticamente con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="c0c88-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="c0c88-140">isAutoPool</span></span>|<span data-ttu-id="c0c88-141">Booleano</span><span class="sxs-lookup"><span data-stu-id="c0c88-141">Bool</span></span>|<span data-ttu-id="c0c88-142">Especifica si el grupo se creó a través del mecanismo AutoPool de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0c88-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
