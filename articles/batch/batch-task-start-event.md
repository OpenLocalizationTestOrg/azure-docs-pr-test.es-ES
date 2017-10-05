---
title: Evento de inicio de tarea de Azure Batch | Microsoft Docs
description: Referencia del evento de inicio de tarea de Batch.
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="65898-103">Evento de inicio de tarea</span><span class="sxs-lookup"><span data-stu-id="65898-103">Task start event</span></span>

 <span data-ttu-id="65898-104">Este evento se emite una vez que el programador programa que una tarea se inicie en un nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="65898-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="65898-105">Tenga en cuenta que si la tarea se reintenta o se vuelve a poner en cola, este evento se volverá a emitir para la misma tarea, pero el conteo de reintentos y la versión de tarea del sistema se actualizarán en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="65898-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="65898-106">En el ejemplo siguiente se muestra el cuerpo de un evento de inicio de tareas.</span><span class="sxs-lookup"><span data-stu-id="65898-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="65898-107">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="65898-107">Element name</span></span>|<span data-ttu-id="65898-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="65898-108">Type</span></span>|<span data-ttu-id="65898-109">Notas</span><span class="sxs-lookup"><span data-stu-id="65898-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="65898-110">jobId</span><span class="sxs-lookup"><span data-stu-id="65898-110">jobId</span></span>|<span data-ttu-id="65898-111">String</span><span class="sxs-lookup"><span data-stu-id="65898-111">String</span></span>|<span data-ttu-id="65898-112">Identificador del trabajo que contiene la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="65898-113">id</span><span class="sxs-lookup"><span data-stu-id="65898-113">id</span></span>|<span data-ttu-id="65898-114">String</span><span class="sxs-lookup"><span data-stu-id="65898-114">String</span></span>|<span data-ttu-id="65898-115">Identificador de la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-115">The id of the task.</span></span>|
|<span data-ttu-id="65898-116">taskType</span><span class="sxs-lookup"><span data-stu-id="65898-116">taskType</span></span>|<span data-ttu-id="65898-117">String</span><span class="sxs-lookup"><span data-stu-id="65898-117">String</span></span>|<span data-ttu-id="65898-118">Tipo de la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-118">The type of the task.</span></span> <span data-ttu-id="65898-119">Puede ser "JobManager", que indica que es una tarea del administrador de trabajos, o "User", que indica que no lo es.</span><span class="sxs-lookup"><span data-stu-id="65898-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="65898-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="65898-120">systemTaskVersion</span></span>|<span data-ttu-id="65898-121">Int32</span><span class="sxs-lookup"><span data-stu-id="65898-121">Int32</span></span>|<span data-ttu-id="65898-122">Se trata del contador interno de reintentos de una tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="65898-123">De manera interna, el servicio de Batch puede reintentar una tarea para tener en cuenta los problemas transitorios.</span><span class="sxs-lookup"><span data-stu-id="65898-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="65898-124">Estos problemas pueden incluir errores internos de programación o intentos de recuperación a partir de nodos de proceso en estado no válido.</span><span class="sxs-lookup"><span data-stu-id="65898-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="65898-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="65898-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="65898-126">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="65898-126">Complex Type</span></span>|<span data-ttu-id="65898-127">Contiene información sobre el nodo de ejecución en que se ejecutó la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="65898-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="65898-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="65898-129">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="65898-129">Complex Type</span></span>|<span data-ttu-id="65898-130">Especifica que la tarea es una tarea de instancias múltiples que requiere varios nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="65898-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="65898-131">Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para detalles.</span><span class="sxs-lookup"><span data-stu-id="65898-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="65898-132">constraints</span><span class="sxs-lookup"><span data-stu-id="65898-132">constraints</span></span>](#constraints)|<span data-ttu-id="65898-133">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="65898-133">Complex Type</span></span>|<span data-ttu-id="65898-134">Restricciones de ejecución que se aplican a esta tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="65898-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="65898-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="65898-136">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="65898-136">Complex Type</span></span>|<span data-ttu-id="65898-137">Contiene información sobre la ejecución de la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="65898-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="65898-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="65898-139">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="65898-139">Element name</span></span>|<span data-ttu-id="65898-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="65898-140">Type</span></span>|<span data-ttu-id="65898-141">Notas</span><span class="sxs-lookup"><span data-stu-id="65898-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="65898-142">poolId</span><span class="sxs-lookup"><span data-stu-id="65898-142">poolId</span></span>|<span data-ttu-id="65898-143">String</span><span class="sxs-lookup"><span data-stu-id="65898-143">String</span></span>|<span data-ttu-id="65898-144">Identificador del grupo en que se ejecutó la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="65898-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="65898-145">nodeId</span></span>|<span data-ttu-id="65898-146">String</span><span class="sxs-lookup"><span data-stu-id="65898-146">String</span></span>|<span data-ttu-id="65898-147">Identificador del nodo en que se ejecutó la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="65898-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="65898-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="65898-149">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="65898-149">Element name</span></span>|<span data-ttu-id="65898-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="65898-150">Type</span></span>|<span data-ttu-id="65898-151">Notas</span><span class="sxs-lookup"><span data-stu-id="65898-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="65898-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="65898-152">numberOfInstances</span></span>|<span data-ttu-id="65898-153">int</span><span class="sxs-lookup"><span data-stu-id="65898-153">Int</span></span>|<span data-ttu-id="65898-154">Número de nodos de proceso que requiere la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="65898-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="65898-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="65898-156">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="65898-156">Element name</span></span>|<span data-ttu-id="65898-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="65898-157">Type</span></span>|<span data-ttu-id="65898-158">Notas</span><span class="sxs-lookup"><span data-stu-id="65898-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="65898-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="65898-159">maxTaskRetryCount</span></span>|<span data-ttu-id="65898-160">Int32</span><span class="sxs-lookup"><span data-stu-id="65898-160">Int32</span></span>|<span data-ttu-id="65898-161">Número máximo de veces que se puede reintentar la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="65898-162">El servicio de Batch reintenta una tarea su el código de salida es distinto de cero.</span><span class="sxs-lookup"><span data-stu-id="65898-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="65898-163">Tenga en cuenta que este valor controla específicamente el número de reintentos.</span><span class="sxs-lookup"><span data-stu-id="65898-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="65898-164">El servicio de Batch intentará una vez la tarea y podría reintentarla hasta alcanzar este límite.</span><span class="sxs-lookup"><span data-stu-id="65898-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="65898-165">Por ejemplo, si el conteo de reintentos máximo es 3, Batch intenta una tarea hasta 4 veces (un intento inicial y 3 reintentos).</span><span class="sxs-lookup"><span data-stu-id="65898-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="65898-166">Si el conteo de intentos máximo es 0, el servicio de Batch no reintenta las tareas.</span><span class="sxs-lookup"><span data-stu-id="65898-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="65898-167">Si el conteo de intentos máximo es -1, el servicio de Batch reintenta las tareas sin ningún límite.</span><span class="sxs-lookup"><span data-stu-id="65898-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="65898-168">El valor predeterminado es 0 (sin ningún reintento).</span><span class="sxs-lookup"><span data-stu-id="65898-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="65898-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="65898-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="65898-170">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="65898-170">Element name</span></span>|<span data-ttu-id="65898-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="65898-171">Type</span></span>|<span data-ttu-id="65898-172">Notas</span><span class="sxs-lookup"><span data-stu-id="65898-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="65898-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="65898-173">retryCount</span></span>|<span data-ttu-id="65898-174">Int32</span><span class="sxs-lookup"><span data-stu-id="65898-174">Int32</span></span>|<span data-ttu-id="65898-175">Cantidad de veces que el servicio de Batch reintentó la tarea.</span><span class="sxs-lookup"><span data-stu-id="65898-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="65898-176">La tarea se reintenta si el código de salida es distinto de cero, hasta el valor MaxTaskRetryCount especificado</span><span class="sxs-lookup"><span data-stu-id="65898-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
