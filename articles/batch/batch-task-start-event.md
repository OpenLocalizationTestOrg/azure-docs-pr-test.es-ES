---
title: aaa "eventos de inicio de tarea de lote de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="02fbd-103">Evento de inicio de tarea</span><span class="sxs-lookup"><span data-stu-id="02fbd-103">Task start event</span></span>

 <span data-ttu-id="02fbd-104">Este evento se genera cuando una tarea ha estado toostart programada en un nodo de proceso por el programador de Hola.</span><span class="sxs-lookup"><span data-stu-id="02fbd-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="02fbd-105">Tenga en cuenta que si se vuelve a intentar o poner en cola tareas Hola este evento se emitirá nuevo para hello misma tarea pero Hola número de reintentos y versión de la tarea de sistema se actualizará según corresponda.</span><span class="sxs-lookup"><span data-stu-id="02fbd-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="02fbd-106">Hello en el ejemplo siguiente se muestra hello cuerpo de un evento de inicio de la tarea.</span><span class="sxs-lookup"><span data-stu-id="02fbd-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="02fbd-107">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="02fbd-107">Element name</span></span>|<span data-ttu-id="02fbd-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="02fbd-108">Type</span></span>|<span data-ttu-id="02fbd-109">Notas</span><span class="sxs-lookup"><span data-stu-id="02fbd-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="02fbd-110">jobId</span><span class="sxs-lookup"><span data-stu-id="02fbd-110">jobId</span></span>|<span data-ttu-id="02fbd-111">String</span><span class="sxs-lookup"><span data-stu-id="02fbd-111">String</span></span>|<span data-ttu-id="02fbd-112">Hola Id. de trabajo de Hola que contiene la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="02fbd-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="02fbd-113">id</span><span class="sxs-lookup"><span data-stu-id="02fbd-113">id</span></span>|<span data-ttu-id="02fbd-114">String</span><span class="sxs-lookup"><span data-stu-id="02fbd-114">String</span></span>|<span data-ttu-id="02fbd-115">Hola Id. de tarea hello.</span><span class="sxs-lookup"><span data-stu-id="02fbd-115">hello id of hello task.</span></span>|
|<span data-ttu-id="02fbd-116">taskType</span><span class="sxs-lookup"><span data-stu-id="02fbd-116">taskType</span></span>|<span data-ttu-id="02fbd-117">String</span><span class="sxs-lookup"><span data-stu-id="02fbd-117">String</span></span>|<span data-ttu-id="02fbd-118">tipo de Hola de tarea hello.</span><span class="sxs-lookup"><span data-stu-id="02fbd-118">hello type of hello task.</span></span> <span data-ttu-id="02fbd-119">Puede ser "JobManager", que indica que es una tarea del administrador de trabajos, o "User", que indica que no lo es.</span><span class="sxs-lookup"><span data-stu-id="02fbd-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="02fbd-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="02fbd-120">systemTaskVersion</span></span>|<span data-ttu-id="02fbd-121">Int32</span><span class="sxs-lookup"><span data-stu-id="02fbd-121">Int32</span></span>|<span data-ttu-id="02fbd-122">Se trata de un contador de reintentos interno de hello en una tarea.</span><span class="sxs-lookup"><span data-stu-id="02fbd-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="02fbd-123">Internamente el servicio por lotes Hola puede volver a intentar una tooaccount de tarea para problemas transitorios.</span><span class="sxs-lookup"><span data-stu-id="02fbd-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="02fbd-124">Estos problemas pueden incluir toorecover interno de intentos de contraseña o errores de programación de nodos de ejecución en un estado incorrecto.</span><span class="sxs-lookup"><span data-stu-id="02fbd-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="02fbd-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="02fbd-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="02fbd-126">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="02fbd-126">Complex Type</span></span>|<span data-ttu-id="02fbd-127">Contiene información sobre el nodo de proceso de hello en qué Hola se ejecutó la tarea.</span><span class="sxs-lookup"><span data-stu-id="02fbd-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="02fbd-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="02fbd-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="02fbd-129">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="02fbd-129">Complex Type</span></span>|<span data-ttu-id="02fbd-130">Especifica que la tarea hello es tarea de varias instancias que requieren varios nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="02fbd-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="02fbd-131">Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para detalles.</span><span class="sxs-lookup"><span data-stu-id="02fbd-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="02fbd-132">constraints</span><span class="sxs-lookup"><span data-stu-id="02fbd-132">constraints</span></span>](#constraints)|<span data-ttu-id="02fbd-133">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="02fbd-133">Complex Type</span></span>|<span data-ttu-id="02fbd-134">restricciones de ejecución de Hola que se aplican toothis tarea.</span><span class="sxs-lookup"><span data-stu-id="02fbd-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="02fbd-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="02fbd-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="02fbd-136">Tipo complejo</span><span class="sxs-lookup"><span data-stu-id="02fbd-136">Complex Type</span></span>|<span data-ttu-id="02fbd-137">Contiene información sobre la ejecución de Hola de tarea hello.</span><span class="sxs-lookup"><span data-stu-id="02fbd-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="02fbd-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="02fbd-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="02fbd-139">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="02fbd-139">Element name</span></span>|<span data-ttu-id="02fbd-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="02fbd-140">Type</span></span>|<span data-ttu-id="02fbd-141">Notas</span><span class="sxs-lookup"><span data-stu-id="02fbd-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="02fbd-142">poolId</span><span class="sxs-lookup"><span data-stu-id="02fbd-142">poolId</span></span>|<span data-ttu-id="02fbd-143">String</span><span class="sxs-lookup"><span data-stu-id="02fbd-143">String</span></span>|<span data-ttu-id="02fbd-144">Hola Id. del grupo de hello en qué Hola se ejecutó la tarea.</span><span class="sxs-lookup"><span data-stu-id="02fbd-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="02fbd-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="02fbd-145">nodeId</span></span>|<span data-ttu-id="02fbd-146">String</span><span class="sxs-lookup"><span data-stu-id="02fbd-146">String</span></span>|<span data-ttu-id="02fbd-147">Hola el identificador del nodo de hello en qué Hola se ejecutó la tarea.</span><span class="sxs-lookup"><span data-stu-id="02fbd-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="02fbd-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="02fbd-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="02fbd-149">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="02fbd-149">Element name</span></span>|<span data-ttu-id="02fbd-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="02fbd-150">Type</span></span>|<span data-ttu-id="02fbd-151">Notas</span><span class="sxs-lookup"><span data-stu-id="02fbd-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="02fbd-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="02fbd-152">numberOfInstances</span></span>|<span data-ttu-id="02fbd-153">int</span><span class="sxs-lookup"><span data-stu-id="02fbd-153">Int</span></span>|<span data-ttu-id="02fbd-154">número de Hola de nodos de proceso requeridos por la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="02fbd-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="02fbd-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="02fbd-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="02fbd-156">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="02fbd-156">Element name</span></span>|<span data-ttu-id="02fbd-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="02fbd-157">Type</span></span>|<span data-ttu-id="02fbd-158">Notas</span><span class="sxs-lookup"><span data-stu-id="02fbd-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="02fbd-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="02fbd-159">maxTaskRetryCount</span></span>|<span data-ttu-id="02fbd-160">Int32</span><span class="sxs-lookup"><span data-stu-id="02fbd-160">Int32</span></span>|<span data-ttu-id="02fbd-161">Hola número máximo de veces que se puede reintentar la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="02fbd-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="02fbd-162">Hola servicio por lotes vuelve a intentar una tarea si su código de salida es distinto de cero.</span><span class="sxs-lookup"><span data-stu-id="02fbd-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="02fbd-163">Tenga en cuenta que este valor controla específicamente número Hola de reintentos.</span><span class="sxs-lookup"><span data-stu-id="02fbd-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="02fbd-164">servicio de lote de Hello intentará tarea hello una vez y, a continuación, puede volver a intentar la toothis límite.</span><span class="sxs-lookup"><span data-stu-id="02fbd-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="02fbd-165">Por ejemplo, si el número máximo de reintentos de hello es 3, lote intenta una tarea too4 horas (un intento de inicial y 3 reintentos).</span><span class="sxs-lookup"><span data-stu-id="02fbd-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="02fbd-166">Si el número máximo de reintentos de hello es 0, Hola servicio por lotes no vuelva a intentar tareas.</span><span class="sxs-lookup"><span data-stu-id="02fbd-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="02fbd-167">Si el número máximo de reintentos de hello es -1, el servicio de lote de hello reintenta tareas sin límite.</span><span class="sxs-lookup"><span data-stu-id="02fbd-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="02fbd-168">valor predeterminado de Hello es 0 (no hay ningún reintento).</span><span class="sxs-lookup"><span data-stu-id="02fbd-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="02fbd-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="02fbd-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="02fbd-170">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="02fbd-170">Element name</span></span>|<span data-ttu-id="02fbd-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="02fbd-171">Type</span></span>|<span data-ttu-id="02fbd-172">Notas</span><span class="sxs-lookup"><span data-stu-id="02fbd-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="02fbd-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="02fbd-173">retryCount</span></span>|<span data-ttu-id="02fbd-174">Int32</span><span class="sxs-lookup"><span data-stu-id="02fbd-174">Int32</span></span>|<span data-ttu-id="02fbd-175">Hola número de veces que se ha reintentado la tarea hello Hola servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="02fbd-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="02fbd-176">tarea Hello se vuelve a intentar si finaliza con un código de salida distinto de cero, los toohello especifica MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="02fbd-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
