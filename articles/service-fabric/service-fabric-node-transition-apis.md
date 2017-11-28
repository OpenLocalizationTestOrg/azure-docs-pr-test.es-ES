---
title: "aaaStart y detener tootest de nodos de clúster microservicios Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse error inyección tootest una aplicación de Service Fabric iniciando o deteniendo los nodos del clúster."
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="eb6d3-103">Reemplazar hello nodo Iniciar y detener nodo API con hello API de transición de nodo</span><span class="sxs-lookup"><span data-stu-id="eb6d3-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="eb6d3-104">¿Qué Hola detener nodo y las API de nodo de inicio hacer?</span><span class="sxs-lookup"><span data-stu-id="eb6d3-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="eb6d3-105">Hola detener API de nodo (administrados: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) se detiene un nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="eb6d3-106">Un nodo de Service Fabric es el proceso, no es una máquina virtual o máquina: Hola VM o máquina seguirá en ejecución.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="eb6d3-107">Para el resto de saludo del documento de Hola "node" significa el nodo de Fabric de servicio.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="eb6d3-108">Detención de un nodo lo coloca en una *detenido* estado donde no es un miembro de clúster de hello y no puede hospedar servicios, simulando así una *hacia abajo* nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="eb6d3-109">Esto es útil para insertar errores en hello tootest de sistema de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="eb6d3-110">Hola API del nodo de inicio (administrados: [StartNodeAsync()][startnode], PowerShell: [inicio ServiceFabricNode][startnodeps]]) invierte Hola detener API de nodo,  Abre nodo hello tooa espera el estado normal.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="eb6d3-111">¿Por qué se realiza la sustitución?</span><span class="sxs-lookup"><span data-stu-id="eb6d3-111">Why are we replacing these?</span></span>

<span data-ttu-id="eb6d3-112">Como se describió anteriormente, un *detenido* Service Fabric trata de un nodo que se ha diseñado intencionalmente mediante Hola detener API de nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="eb6d3-113">A *hacia abajo* trata de un nodo que está inactivo por cualquier otra razón (p. ej. Hola máquina o máquina virtual está desactivada).</span><span class="sxs-lookup"><span data-stu-id="eb6d3-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="eb6d3-114">Con hello detener API de nodo, sistema de Hola no expone información toodifferentiate entre *detenido* nodos y *hacia abajo* nodos.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="eb6d3-115">Además, algunos errores devueltos por estas API no son tan descriptivos como debieran.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="eb6d3-116">Por ejemplo, invocar Hola detener API de nodo en una ya *detenido* nodo, devolverá el error de hello *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="eb6d3-117">Se puede mejorar esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-117">This experience could be improved.</span></span>

<span data-ttu-id="eb6d3-118">Además, duración Hola que un nodo se detiene durante es "infinito" hasta Hola que se invoca la API del nodo de inicio.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="eb6d3-119">Se ha detectado que esto puede ocasionar problemas y ser propenso a errores.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="eb6d3-120">Por ejemplo, hemos visto problemas donde un usuario invoca Hola detener API de nodo en un nodo y, a continuación, que se haya olvidado sobre él.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="eb6d3-121">Más adelante, estaba claro si Hola nodo estaba *hacia abajo* o *detenido*.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="eb6d3-122">Introducción a hello las API de transición de nodo</span><span class="sxs-lookup"><span data-stu-id="eb6d3-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="eb6d3-123">Se han solucionado estos problemas anteriores en un nuevo conjunto de API.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="eb6d3-124">Hola nueva transición del nodo API (administrados: [StartNodeTransitionAsync()][snt]) puede ser utilizado tootransition un tooa de nodo de Service Fabric *detenido* estado o tootransition, desde un *detenido* tooa estado normal el estado.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="eb6d3-125">Tenga en cuenta que Hola "Inicio" del nombre de Hola de hello API no hace referencia toostarting un nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="eb6d3-126">Hace referencia a una operación asincrónica que sistema Hola ejecutará tootransition Hola nodo tooeither toobeginning *detenido* o estado de iniciado.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="eb6d3-127">**Uso**</span><span class="sxs-lookup"><span data-stu-id="eb6d3-127">**Usage**</span></span>

<span data-ttu-id="eb6d3-128">Si Hola API de transición de nodo no produce una excepción cuando se invoca, a continuación, sistema Hola ha aceptado la operación asincrónica de hello y lo ejecuta.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="eb6d3-129">Una llamada correcta no implica la operación de hello ha finalizado aún.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="eb6d3-130">tooget información acerca del estado actual de Hola de operación de hello, Hola llamada API de progreso de transición de nodo (administrados: [GetNodeTransitionProgressAsync()][gntp]) con el guid de hello utilizado al invocar el nodo API de transición para esta operación.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="eb6d3-131">Hola nodo transición de progreso de la API devuelve un objeto NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="eb6d3-132">Propiedad de estado de este objeto especifica el estado actual de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="eb6d3-133">Si el estado de hello es "Running" se está ejecutando la operación Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="eb6d3-134">Si ésta se ha finalizado, la operación de hello ha finalizado sin errores.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="eb6d3-135">Si lo tiene errores, se produjo un problema al ejecutar la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="eb6d3-136">Excepción de la propiedad del resultado de Hello propiedad indicará qué Hola emitir fue.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="eb6d3-137">Consulte https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate para obtener más información acerca de la propiedad de estado de Hola y la sección de "Uso de ejemplo" Hola a continuación para obtener ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="eb6d3-138">**Diferenciar entre un nodo detenido y un nodo inactivo** si un nodo es *detenido* utilizando Hola API de transición de nodo, la salida de hello de una consulta de nodo (administrados: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) mostrará que este nodo tiene un *IsStopped* valor de la propiedad es true.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="eb6d3-139">Tenga en cuenta esto es diferente del valor de Hola de hello *NodeStatus* propiedad, que indicará que *hacia abajo*.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="eb6d3-140">Si hello *NodeStatus* propiedad tiene un valor de *hacia abajo*, pero *IsStopped* es false, no se detuvo nodo hello mediante API de transición de nodo de Hola y es  *Profundidad* debido a alguna otra razón.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="eb6d3-141">Si hello *IsStopped* propiedad es true y hello *NodeStatus* propiedad es *hacia abajo*, a continuación, se ha detenido con hello API de transición de nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="eb6d3-142">A partir de un *detenido* nodo mediante la API de transición de nodo de Hola lo devuelva toofunction como un miembro normal del clúster de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="eb6d3-143">Hello resultado de consulta de nodo de hello API mostrará *IsStopped* como false, y *NodeStatus* como algo que no está inactivo (por ejemplo, arriba).</span><span class="sxs-lookup"><span data-stu-id="eb6d3-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="eb6d3-144">**Otros duración** al usar API de transición de nodo de hello toostop un nodo, uno de hello requiere parámetros, *stopNodeDurationInSeconds*, representa Hola cantidad de tiempo en el nodo de segundos tookeep hello  *detenido*.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="eb6d3-145">Este valor debe estar en el intervalo, que tiene un mínimo de 600 y un máximo de 14400 permitido de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="eb6d3-146">Después de que expire este tiempo, el nodo de Hola se reiniciará propio en el estado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="eb6d3-147">Consulte tooSample 1 a continuación para obtener un ejemplo de uso.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="eb6d3-148">Evite mezclar las API de transición de nodo y Hola detener nodo y las API de nodo de inicio.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="eb6d3-149">recomendación de Hello es demasiado utilizar Hola API de transición de nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="eb6d3-150">> Si un nodo ya está detenido con hello detener API de nodo, se debe iniciar utilizando Hola API del nodo de inicio en primer lugar antes de usar hello > API de transición de nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="eb6d3-151">Hola a varias API de transición de nodo no se pueden realizar llamadas en el mismo nodo en paralelo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="eb6d3-152">En esta situación, lo Hola API de transición de nodo > producir una FabricException con un valor de la propiedad ErrorCode de NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="eb6d3-153">Una vez que tenga una transición de nodo en un nodo específico > está iniciado, debe esperar hasta que la operación de hello alcance un estado terminal (completado, error o ForceCancelled) antes de iniciar un > transición nuevos en hello mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="eb6d3-154">Sí se permiten llamadas paralelas a las API Node Transition en diferentes nodos.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="eb6d3-155">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="eb6d3-155">Sample Usage</span></span>


<span data-ttu-id="eb6d3-156">**Ejemplo 1** -Hola siguientes usos de ejemplo Hola toostop un nodo de API de transición de nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="eb6d3-157">**Ejemplo 2** : hello siguiendo el ejemplo inicia una *detenido* nodo.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="eb6d3-158">Usa algunos métodos auxiliares del primer ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="eb6d3-159">**Ejemplo 3** : hello en el ejemplo siguiente muestra el uso incorrecto.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="eb6d3-160">Este uso es incorrecto porque hello *stopDurationInSeconds* proporciona es mayor que el intervalo permitido de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="eb6d3-161">Puesto que StartNodeTransitionAsync() se producirá un error con un error irrecuperable, no se aceptó la operación de Hola y Hola progreso de la API no se debe llamar.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="eb6d3-162">Este ejemplo usa algunos métodos auxiliares del primer ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="eb6d3-163">**Ejemplo 4** : hello en el ejemplo siguiente se muestra información de error de Hola que se obtendrán de hello nodo transición de progreso de la API cuando la operación de hello iniciada por hello API de transición de nodo se acepta, pero se produce un error más adelante al ejecutar.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="eb6d3-164">En caso de hello, no como Hola API de transición de nodo trata toostart un nodo que no existe.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="eb6d3-165">Este ejemplo usa algunos métodos auxiliares del primer ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb6d3-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
