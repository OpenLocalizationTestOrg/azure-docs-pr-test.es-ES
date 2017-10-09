---
title: "aaa \"evento de inicio de cambio de tamaño de grupo de lote de Azure | Documentos de Microsoft\""
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="eb91e-103">Evento de inicio de cambio de tamaño de grupo</span><span class="sxs-lookup"><span data-stu-id="eb91e-103">Pool resize start event</span></span>

 <span data-ttu-id="eb91e-104">Este evento se genera se inicia el cambio de tamaño de un grupo.</span><span class="sxs-lookup"><span data-stu-id="eb91e-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="eb91e-105">Puesto que el cambio de tamaño de bloque de hello es un evento asíncrono, puede esperar un toobe de evento complete de cambio de tamaño de bloque emitida una vez Hola cambiar el tamaño de operación se completa.</span><span class="sxs-lookup"><span data-stu-id="eb91e-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="eb91e-106">cambiar el tamaño de Hello siguiente ejemplo se muestra hello cuerpo de un evento de inicio de cambio de tamaño de grupo para un cambio de tamaño grupo desde 0 nodos too2 con un manual.</span><span class="sxs-lookup"><span data-stu-id="eb91e-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="eb91e-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="eb91e-107">Element</span></span>|<span data-ttu-id="eb91e-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="eb91e-108">Type</span></span>|<span data-ttu-id="eb91e-109">Notas</span><span class="sxs-lookup"><span data-stu-id="eb91e-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="eb91e-110">poolId</span><span class="sxs-lookup"><span data-stu-id="eb91e-110">poolId</span></span>|<span data-ttu-id="eb91e-111">String</span><span class="sxs-lookup"><span data-stu-id="eb91e-111">String</span></span>|<span data-ttu-id="eb91e-112">Hola Id. de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb91e-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="eb91e-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="eb91e-113">nodeDeallocationOption</span></span>|<span data-ttu-id="eb91e-114">String</span><span class="sxs-lookup"><span data-stu-id="eb91e-114">String</span></span>|<span data-ttu-id="eb91e-115">Especifica cuando debe quitar nodos del grupo de hello, si el tamaño del grupo de hello disminuye.</span><span class="sxs-lookup"><span data-stu-id="eb91e-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="eb91e-116">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="eb91e-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="eb91e-117">**requeue**: finalizar las tareas en ejecución y volver a ponerlas en cola.</span><span class="sxs-lookup"><span data-stu-id="eb91e-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="eb91e-118">tareas de Hola se ejecutarán de nuevo cuando se habilite el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb91e-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="eb91e-119">Elimine los nodos en cuanto finalicen las tareas.</span><span class="sxs-lookup"><span data-stu-id="eb91e-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="eb91e-120">**terminate**: finalizar las tareas en ejecución.</span><span class="sxs-lookup"><span data-stu-id="eb91e-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="eb91e-121">tareas de Hello no se ejecutarán de nuevo.</span><span class="sxs-lookup"><span data-stu-id="eb91e-121">hello tasks will not run again.</span></span> <span data-ttu-id="eb91e-122">Elimine los nodos en cuanto finalicen las tareas.</span><span class="sxs-lookup"><span data-stu-id="eb91e-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="eb91e-123">**taskcompletion** : permitir toocomplete de tareas está ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="eb91e-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="eb91e-124">No programe ninguna tarea nueva mientras espera.</span><span class="sxs-lookup"><span data-stu-id="eb91e-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="eb91e-125">Elimine los nodos cuando se hayan completado todas las tareas.</span><span class="sxs-lookup"><span data-stu-id="eb91e-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="eb91e-126">**Retaineddata** : permitir toocomplete de tareas en ejecución actualmente y luego espere tooexpire de períodos de retención de datos.</span><span class="sxs-lookup"><span data-stu-id="eb91e-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="eb91e-127">No programe ninguna tarea nueva mientras espera.</span><span class="sxs-lookup"><span data-stu-id="eb91e-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="eb91e-128">Elimine los nodos cuando hayan caducado los períodos de retención de todas las tareas.</span><span class="sxs-lookup"><span data-stu-id="eb91e-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="eb91e-129">valor predeterminado de Hello es colocarlo en cola.</span><span class="sxs-lookup"><span data-stu-id="eb91e-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="eb91e-130">Si aumenta el tamaño del grupo de hello, valor de Hola se establece demasiado**válido**.</span><span class="sxs-lookup"><span data-stu-id="eb91e-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="eb91e-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="eb91e-131">currentDedicated</span></span>|<span data-ttu-id="eb91e-132">Int32</span><span class="sxs-lookup"><span data-stu-id="eb91e-132">Int32</span></span>|<span data-ttu-id="eb91e-133">número de Hola de nodos de proceso asignadas actualmente toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="eb91e-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="eb91e-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="eb91e-134">targetDedicated</span></span>|<span data-ttu-id="eb91e-135">Int32</span><span class="sxs-lookup"><span data-stu-id="eb91e-135">Int32</span></span>|<span data-ttu-id="eb91e-136">número de Hola de nodos de proceso que se solicitan para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb91e-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="eb91e-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="eb91e-137">enableAutoScale</span></span>|<span data-ttu-id="eb91e-138">Booleano</span><span class="sxs-lookup"><span data-stu-id="eb91e-138">Bool</span></span>|<span data-ttu-id="eb91e-139">Especifica si el tamaño del grupo de hello ajusta automáticamente con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="eb91e-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="eb91e-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="eb91e-140">isAutoPool</span></span>|<span data-ttu-id="eb91e-141">Booleano</span><span class="sxs-lookup"><span data-stu-id="eb91e-141">Bool</span></span>|<span data-ttu-id="eb91e-142">Especifica si se creó el grupo de Hola a través del mecanismo de grupo de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="eb91e-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
