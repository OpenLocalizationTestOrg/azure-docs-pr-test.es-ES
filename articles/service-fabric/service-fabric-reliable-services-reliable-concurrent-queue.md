---
title: aaaReliableConcurrentQueue en Azure Service Fabric
description: ReliableConcurrentQueue es una cola de alto rendimiento que permite puestas en cola y eliminaciones de la cola paralelas.
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="411fe-103">Introducción tooReliableConcurrentQueue en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="411fe-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="411fe-104">La cola simultánea confiable es una cola asincrónica, transaccional y replicada que presenta una alta simultaneidad para las operaciones de puesta en cola y eliminación de la cola.</span><span class="sxs-lookup"><span data-stu-id="411fe-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="411fe-105">Está diseñado toodeliver alto rendimiento y baja latencia por relaja Hola FIFO ordenación estricta proporcionada por [cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) y en su lugar, proporciona una ordenación de mejor esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="411fe-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="411fe-106">API existentes</span><span class="sxs-lookup"><span data-stu-id="411fe-106">APIs</span></span>

|<span data-ttu-id="411fe-107">Cola simultánea</span><span class="sxs-lookup"><span data-stu-id="411fe-107">Concurrent Queue</span></span>                |<span data-ttu-id="411fe-108">Cola simultánea confiable</span><span class="sxs-lookup"><span data-stu-id="411fe-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="411fe-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="411fe-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="411fe-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="411fe-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="411fe-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="411fe-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="411fe-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="411fe-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="411fe-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="411fe-113">int Count()</span></span>                    | <span data-ttu-id="411fe-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="411fe-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="411fe-115">Comparación con la [cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="411fe-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="411fe-116">Confiable cola simultánea se ofrece como alternativa demasiado[cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="411fe-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="411fe-117">Debe usarse en aquellos casos en que no se requiere la ordenación FIFO estricta, ya que para garantizar FIFO se requiere un compromiso con la simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="411fe-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="411fe-118">[Cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) utiliza bloqueos tooenforce FIFO ordenación, con permiten tooenqueue como máximo una transacción y en la mayoría de una transacción permite toodequeue a la vez.</span><span class="sxs-lookup"><span data-stu-id="411fe-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="411fe-119">En comparación, cola simultánea confiable relaja Hola restricción de ordenación y permite cualquier número toointerleave de las transacciones simultáneas su poner en cola y las operaciones de eliminación de cola.</span><span class="sxs-lookup"><span data-stu-id="411fe-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="411fe-120">El orden de mejor esfuerzo es siempre, sin embargo Hola el orden relativo de dos valores en una cola simultánea confiable puede nunca puede garantizar.</span><span class="sxs-lookup"><span data-stu-id="411fe-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="411fe-121">La cola simultánea confiable proporciona un rendimiento mayor y menor latencia que la [cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) siempre que existen varias transacciones simultáneas que realizan puestas en cola y/o eliminaciones de la cola.</span><span class="sxs-lookup"><span data-stu-id="411fe-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="411fe-122">Un ejemplo de uso de hello ReliableConcurrentQueue es hello [cola de mensajes](https://en.wikipedia.org/wiki/Message_queue) escenario.</span><span class="sxs-lookup"><span data-stu-id="411fe-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="411fe-123">En este escenario, crean y agregar elementos toohello cola productores de mensajes de uno o más, y uno o varios de los consumidores del mensaje extracción mensajes de cola de Hola y procesan.</span><span class="sxs-lookup"><span data-stu-id="411fe-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="411fe-124">Varios productores y consumidores pueden trabajar independientemente, con las transacciones simultáneas en cola la orden tooprocess Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="411fe-125">Directrices de uso</span><span class="sxs-lookup"><span data-stu-id="411fe-125">Usage Guidelines</span></span>
* <span data-ttu-id="411fe-126">cola de Hello espera que los elementos de hello en cola Hola tienen un período de retención baja.</span><span class="sxs-lookup"><span data-stu-id="411fe-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="411fe-127">Es decir, los elementos de hello no quedaría en cola de Hola durante mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="411fe-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="411fe-128">cola de Hello no garantiza la ordenación de FIFO estricta.</span><span class="sxs-lookup"><span data-stu-id="411fe-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="411fe-129">cola de Hello no lee su propia escritura.</span><span class="sxs-lookup"><span data-stu-id="411fe-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="411fe-130">Si un elemento está en cola dentro de una transacción, no estará visible tooa dequeuer dentro de Hola misma transacción.</span><span class="sxs-lookup"><span data-stu-id="411fe-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="411fe-131">Las eliminaciones de la cola no están aisladas entre sí.</span><span class="sxs-lookup"><span data-stu-id="411fe-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="411fe-132">Si el elemento *A* se quitan de la cola de transacciones *txnA*, aunque *txnA* no se confirma, elemento *A* no sería tooa visible simultáneas transacción *txnB*.</span><span class="sxs-lookup"><span data-stu-id="411fe-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="411fe-133">Si *txnA* anula, *A* dejarán de estar visible demasiado*txnB* inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="411fe-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="411fe-134">*TryPeekAsync* comportamiento puede implementarse mediante un *TryDequeueAsync* y, a continuación, anular la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="411fe-135">Un ejemplo de esto puede encontrarse en la sección de patrones de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="411fe-136">El recuento es no transaccional.</span><span class="sxs-lookup"><span data-stu-id="411fe-136">Count is non-transactional.</span></span> <span data-ttu-id="411fe-137">Puede ser tooget usa una idea del número de Hola de elementos en cola de hello, pero representa un punto en el tiempo y no se puede confiar en ellos.</span><span class="sxs-lookup"><span data-stu-id="411fe-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="411fe-138">Un procesamiento costoso en hello elementos quitados de la cola no deben realizarse mientras está activa, la transacción hello tooavoid transacciones de larga ejecución que pueden tener un impacto en el rendimiento en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="411fe-139">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="411fe-139">Code Snippets</span></span>
<span data-ttu-id="411fe-140">Echemos un vistazo a algunos fragmentos de código y a sus resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="411fe-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="411fe-141">El control de excepciones se omite en esta sección.</span><span class="sxs-lookup"><span data-stu-id="411fe-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="411fe-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="411fe-142">EnqueueAsync</span></span>
<span data-ttu-id="411fe-143">A continuación, se muestran algunos fragmentos de código para usar EnqueueAsync, seguido de los resultados previstos.</span><span class="sxs-lookup"><span data-stu-id="411fe-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="411fe-144">*Caso 1: Tarea de puesta en cola única*</span><span class="sxs-lookup"><span data-stu-id="411fe-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="411fe-145">Suponga esa tarea Hola se completó correctamente y que no hubo ninguna transacción simultánea modificar cola Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="411fe-146">usuario de Hello, puede esperar Hola cola toocontain Hola los elementos en cualquiera de hello después de pedidos:</span><span class="sxs-lookup"><span data-stu-id="411fe-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="411fe-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="411fe-147">10, 20</span></span>

> <span data-ttu-id="411fe-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="411fe-148">20, 10</span></span>


- <span data-ttu-id="411fe-149">*Caso 2: Tarea de puesta en cola paralela*</span><span class="sxs-lookup"><span data-stu-id="411fe-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="411fe-150">Suponga que tareas Hola completan correctamente, que se ha ejecutado tareas hello en paralelo y que no había ninguna otra transacción simultánea modificar cola Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="411fe-151">La inferencia no se puede realizar sobre orden Hola de elementos en cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="411fe-152">Este fragmento de código, elementos Hola pueden aparecer en cualquiera de los 4 hello!</span><span class="sxs-lookup"><span data-stu-id="411fe-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="411fe-153">órdenes posibles.</span><span class="sxs-lookup"><span data-stu-id="411fe-153">possible orderings.</span></span>  <span data-ttu-id="411fe-154">cola de Hello tratará de elementos de hello tookeep en orden de hello original (en cola), pero puede ser tooreorder forzada ellas debido a operaciones de tooconcurrent o errores.</span><span class="sxs-lookup"><span data-stu-id="411fe-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="411fe-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="411fe-155">DequeueAsync</span></span>
<span data-ttu-id="411fe-156">Estos son algunos fragmentos de código para usar TryDequeueAsync seguido de salidas de hello esperado.</span><span class="sxs-lookup"><span data-stu-id="411fe-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="411fe-157">Suponga que esa cola Hola ya se rellena con hello siguientes elementos en cola de hello:</span><span class="sxs-lookup"><span data-stu-id="411fe-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="411fe-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="411fe-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="411fe-159">*Caso 1: Tarea de quitar de la cola única*</span><span class="sxs-lookup"><span data-stu-id="411fe-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="411fe-160">Suponga esa tarea Hola se completó correctamente y que no hubo ninguna transacción simultánea modificar cola Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="411fe-161">Puesto que no puede realizarse inferencia sobre orden Hola de elementos de hello en cola de hello, los tres elementos de hello pueden se quita de la cola, en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="411fe-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="411fe-162">cola de Hello tratará de elementos de hello tookeep en orden de hello original (en cola), pero puede ser tooreorder forzada ellas debido a operaciones de tooconcurrent o errores.</span><span class="sxs-lookup"><span data-stu-id="411fe-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="411fe-163">*Caso 2: Tarea de eliminación de la cola paralela*</span><span class="sxs-lookup"><span data-stu-id="411fe-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="411fe-164">Suponga que tareas Hola completan correctamente, que se ha ejecutado tareas hello en paralelo y que no había ninguna otra transacción simultánea modificar cola Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="411fe-165">Puesto que no puede realizarse inferencia sobre orden Hola de elementos de hello en cola de hello, Hola listas *dequeue1* y *dequeue2* contendrá entre los dos elementos, en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="411fe-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="411fe-166">Hola le mismo elemento *no* aparecen en ambas listas.</span><span class="sxs-lookup"><span data-stu-id="411fe-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="411fe-167">Por lo tanto, si dequeue1 tiene *10*, *30*, dequeue2 tendrá *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="411fe-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="411fe-168">*Caso 3: Ordenación de eliminación de la cola con anulación de transacción*</span><span class="sxs-lookup"><span data-stu-id="411fe-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="411fe-169">Anular una transacción con sobre la marcha quita vuelve a colocar elementos de hello en el encabezado de Hola de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="411fe-170">no se garantiza el orden de Hello en el que los elementos de Hola se vuelven a poner en el encabezado de Hola de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="411fe-171">Echemos un vistazo al siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="411fe-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="411fe-172">Suponga que elementos de Hola se han quitado de la cola en hello siguiendo el orden:</span><span class="sxs-lookup"><span data-stu-id="411fe-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="411fe-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="411fe-173">10, 20</span></span>

<span data-ttu-id="411fe-174">Cuando se anule la transacción de hello, elementos de Hola se agregaría toohello back-head de cola de hello en cualquiera de hello después de pedidos:</span><span class="sxs-lookup"><span data-stu-id="411fe-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="411fe-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="411fe-175">10, 20</span></span>

> <span data-ttu-id="411fe-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="411fe-176">20, 10</span></span>

<span data-ttu-id="411fe-177">Hello mismo sirve para todos los casos donde hello no estaba correctamente *confirmado*.</span><span class="sxs-lookup"><span data-stu-id="411fe-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="411fe-178">Modelos de programación</span><span class="sxs-lookup"><span data-stu-id="411fe-178">Programming Patterns</span></span>
<span data-ttu-id="411fe-179">En esta sección, vamos a echar un vistazo a algunos modelos de programación que podrían resultar útiles para usar ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="411fe-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="411fe-180">Eliminaciones de la cola por lotes</span><span class="sxs-lookup"><span data-stu-id="411fe-180">Batch Dequeues</span></span>
<span data-ttu-id="411fe-181">Recomienda modelo de programación es para hello consumidor tarea toobatch su quita de la cola en lugar de realizar una eliminación de cola a la vez.</span><span class="sxs-lookup"><span data-stu-id="411fe-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="411fe-182">usuario de Hello puede toothrottle retrasos entre cada tamaño de lote de proceso por lotes o hello.</span><span class="sxs-lookup"><span data-stu-id="411fe-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="411fe-183">Hello fragmento de código siguiente muestra este modelo de programación.</span><span class="sxs-lookup"><span data-stu-id="411fe-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="411fe-184">Tenga en cuenta que en este ejemplo, el procesamiento de Hola se realiza después de hello transacción se confirma, por lo que si un error fuera toooccur durante el procesamiento, hello elementos sin procesar se perderán sin haber sido transformado.</span><span class="sxs-lookup"><span data-stu-id="411fe-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="411fe-185">O bien, se puede realizar el procesamiento de hello en el ámbito de la transacción de hello, sin embargo esto puede tener un impacto negativo en el rendimiento y requiere un tratamiento de los elementos de hello ya procesan.</span><span class="sxs-lookup"><span data-stu-id="411fe-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="411fe-186">Procesamiento basado en notificaciones de mejor esfuerzo</span><span class="sxs-lookup"><span data-stu-id="411fe-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="411fe-187">Otro patrón de programación interesante usa Hola API de recuento.</span><span class="sxs-lookup"><span data-stu-id="411fe-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="411fe-188">En este caso, podemos implementar procesamiento basado en notificaciones de mejor esfuerzo para cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="411fe-189">Hola cola número puede ser usado toothrottle un poner en cola o una tarea de eliminación de cola.</span><span class="sxs-lookup"><span data-stu-id="411fe-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="411fe-190">Tenga en cuenta que como en el ejemplo anterior de hello, puesto que se produce el procesamiento de hello fuera de la transacción de hello, sin procesar elementos pueden perderse si se produce un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="411fe-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="411fe-191">Descarga de mejor esfuerzo</span><span class="sxs-lookup"><span data-stu-id="411fe-191">Best-Effort Drain</span></span>
<span data-ttu-id="411fe-192">No se puede garantizar una descarga de la cola de hello debido toohello naturaleza simultáneas de estructura de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="411fe-193">Es posible que, incluso si no hay operaciones de usuario de cola de hello en curso, una determinada llamada tooTryDequeueAsync no puede devolver un elemento que antes era en cola y confirmada.</span><span class="sxs-lookup"><span data-stu-id="411fe-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="411fe-194">elemento de Hello en cola se garantiza demasiado*finalmente* se convierten en toodequeue visible, sin embargo, sin un mecanismo de comunicación fuera de banda, un consumidor independiente no puede saber a esa cola Hola ha alcanzado un estado estable incluso si todos los se han detenido los productores y no se permite ninguna operación nueva de puesta en cola.</span><span class="sxs-lookup"><span data-stu-id="411fe-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="411fe-195">Por lo tanto, operación de vaciado de hello es mejor esfuerzo tal y como se implementan bajo.</span><span class="sxs-lookup"><span data-stu-id="411fe-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="411fe-196">usuario de Hello debe detener toda la demás productor y las tareas del consumidor y espere anulación, antes de intentar la cola de hello toodrain ni toocommit de transacciones en curso.</span><span class="sxs-lookup"><span data-stu-id="411fe-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="411fe-197">Si usuario Hola conoce número Hola esperado de elementos en cola de hello, puede configurar una notificación que indica que todos los elementos se han quitado de la cola.</span><span class="sxs-lookup"><span data-stu-id="411fe-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="411fe-198">Peek</span><span class="sxs-lookup"><span data-stu-id="411fe-198">Peek</span></span>
<span data-ttu-id="411fe-199">ReliableConcurrentQueue no proporciona hello *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="411fe-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="411fe-200">Los usuarios pueden obtener peek Hola a semántica mediante el uso de un *TryDequeueAsync* y, a continuación, anular la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="411fe-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="411fe-201">En este ejemplo, quita de la cola se procesan sólo si el valor del elemento de hello es mayor que *10*.</span><span class="sxs-lookup"><span data-stu-id="411fe-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="411fe-202">Lecturas obligatorias</span><span class="sxs-lookup"><span data-stu-id="411fe-202">Must Read</span></span>
* [<span data-ttu-id="411fe-203">Inicio rápido de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="411fe-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="411fe-204">Trabajo con Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="411fe-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="411fe-205">Notificaciones de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="411fe-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="411fe-206">Copia de seguridad y restauración de Reliable Services (recuperación ante desastres)</span><span class="sxs-lookup"><span data-stu-id="411fe-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="411fe-207">Configuración del administrador de estado confiable</span><span class="sxs-lookup"><span data-stu-id="411fe-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="411fe-208">Introducción a los servicios de la API web de Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="411fe-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="411fe-209">Uso avanzado de hello modelo de programación de servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="411fe-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="411fe-210">Referencia para desarrolladores de colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="411fe-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
