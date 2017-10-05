---
title: "Inicio y detención de nodos de clúster para probar los microservicios de Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo iniciar o detener nodos de clúster para usar la inserción de errores con el fin de probar una aplicación de Service Fabric."
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
ms.openlocfilehash: 850fbc0c74811ec942292da64064dec867cd1b9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replacing-the-start-node-and-stop-node-apis-with-the-node-transition-api"></a><span data-ttu-id="b0a66-103">Sustitución de las API Start Node y Stop node con la API Node Transition</span><span class="sxs-lookup"><span data-stu-id="b0a66-103">Replacing the Start Node and Stop node APIs with the Node Transition API</span></span>

## <a name="what-do-the-stop-node-and-start-node-apis-do"></a><span data-ttu-id="b0a66-104">¿Qué hacen las API Stop Node y Start Node?</span><span class="sxs-lookup"><span data-stu-id="b0a66-104">What do the Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="b0a66-105">La API Stop Node (administrada: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) detiene un nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0a66-105">The Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="b0a66-106">Un nodo de Service Fabric es un proceso, no un equipo ni una máquina virtual: el equipo o la máquina virtual seguirán en ejecución.</span><span class="sxs-lookup"><span data-stu-id="b0a66-106">A Service Fabric node is process, not a VM or machine – the VM or machine will still be running.</span></span>  <span data-ttu-id="b0a66-107">Para el resto del documento, "nodo" hace referencia a un nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0a66-107">For the rest of the document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="b0a66-108">Al detener un nodo, este adquiere el estado *detenido*, en el que no es un miembro del clúster y no puede hospedar servicios, por lo que simula un nodo *apagado*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-108">Stopping a node puts it into a *stopped* state where it is not a member of the cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="b0a66-109">Esto es útil para insertar errores en el sistema a fin de probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0a66-109">This is useful for injecting faults into the system to test your application.</span></span>  <span data-ttu-id="b0a66-110">La API Start Node (administrada: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) invierte la API Stop Node, por lo que el nodo vuelve a un estado normal.</span><span class="sxs-lookup"><span data-stu-id="b0a66-110">The Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses the Stop Node API,  which brings the node back to a normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="b0a66-111">¿Por qué se realiza la sustitución?</span><span class="sxs-lookup"><span data-stu-id="b0a66-111">Why are we replacing these?</span></span>

<span data-ttu-id="b0a66-112">Como se ha descrito anteriormente, un nodo de Service Fabric *detenido* es un nodo intencionalmente dirigido con la API Stop Node.</span><span class="sxs-lookup"><span data-stu-id="b0a66-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using the Stop Node API.</span></span>  <span data-ttu-id="b0a66-113">Un nodo *apagado* es un nodo que está apagado por cualquier otra razón (por ejemplo, porque el equipo o la máquina virtual están apagados).</span><span class="sxs-lookup"><span data-stu-id="b0a66-113">A *down* node is a node that is down for any other reason (e.g. the VM or machine is off).</span></span>  <span data-ttu-id="b0a66-114">Con la API Stop Node, el sistema no expone información para diferenciar entre los nodos *detenidos* y los nodos *apagados*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-114">With the Stop Node API, the system does not expose information to differentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="b0a66-115">Además, algunos errores devueltos por estas API no son tan descriptivos como debieran.</span><span class="sxs-lookup"><span data-stu-id="b0a66-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="b0a66-116">Por ejemplo, al invocar la API Stop Node en un nodo que ya está *detenido*, se devolverá el error *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-116">For example, invoking the Stop Node API on an already *stopped* node will return the error *InvalidAddress*.</span></span>  <span data-ttu-id="b0a66-117">Se puede mejorar esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="b0a66-117">This experience could be improved.</span></span>

<span data-ttu-id="b0a66-118">Además, el tiempo durante el cual un nodo está detenido es "infinito" hasta que se invoca la API Start Node.</span><span class="sxs-lookup"><span data-stu-id="b0a66-118">Also, the duration a node is stopped for is “infinite” until the Start Node API is invoked.</span></span>  <span data-ttu-id="b0a66-119">Se ha detectado que esto puede ocasionar problemas y ser propenso a errores.</span><span class="sxs-lookup"><span data-stu-id="b0a66-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="b0a66-120">Por ejemplo, se han observado problemas en los que un usuario ha invocado la API Stop Node en un nodo y luego se ha olvidado de ello.</span><span class="sxs-lookup"><span data-stu-id="b0a66-120">For example, we’ve seen problems where a user invoked the Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="b0a66-121">Luego no está claro si un nodo está *apagado* o *detenido*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-121">Later, it was unclear if the node was *down* or *stopped*.</span></span>


## <a name="introducing-the-node-transition-apis"></a><span data-ttu-id="b0a66-122">Introducción a las API Node Transition</span><span class="sxs-lookup"><span data-stu-id="b0a66-122">Introducing the Node Transition APIs</span></span>

<span data-ttu-id="b0a66-123">Se han solucionado estos problemas anteriores en un nuevo conjunto de API.</span><span class="sxs-lookup"><span data-stu-id="b0a66-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="b0a66-124">La nueva API Node Transition (administrada: [StartNodeTransitionAsync()][snt]) puede utilizarse para realizar la transición de un nodo de Service Fabric a un estado *detenido*, o bien para realizar su transición de un estado *detenido* a un estado normal.</span><span class="sxs-lookup"><span data-stu-id="b0a66-124">The new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used to transition a Service Fabric node to a *stopped* state, or to transition it from a *stopped* state to a normal up state.</span></span>  <span data-ttu-id="b0a66-125">Tenga en cuenta que la palabra "Start" en el nombre de la API no hace referencia a iniciar un nodo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-125">Please note that the “Start” in the name of the API does not refer to starting a node.</span></span>  <span data-ttu-id="b0a66-126">Se refiere a comenzar una operación asincrónica que el sistema ejecutará para realizar la transición del nodo a un estado *detenido* o iniciado.</span><span class="sxs-lookup"><span data-stu-id="b0a66-126">It refers to beginning an asynchronous operation that the system will execute to transition the node to either *stopped* or started state.</span></span>

<span data-ttu-id="b0a66-127">**Uso**</span><span class="sxs-lookup"><span data-stu-id="b0a66-127">**Usage**</span></span>

<span data-ttu-id="b0a66-128">Si la API Node Transition no lanza una excepción al invocarla, significa que el sistema ha aceptado la operación asincrónica y que la ejecutará.</span><span class="sxs-lookup"><span data-stu-id="b0a66-128">If the Node Transition API does not throw an exception when invoked, then the system has accepted the asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="b0a66-129">Una llamada correcta no implica que la operación haya finalizado aún.</span><span class="sxs-lookup"><span data-stu-id="b0a66-129">A successful call does not imply the operation is finished yet.</span></span>  <span data-ttu-id="b0a66-130">Para obtener información sobre el estado actual de la operación, llame a la API Node Transition Progress (administrada: [GetNodeTransitionProgressAsync()][gntp]) con el GUID utilizado al invocar la API Node Transition para realizar esta operación.</span><span class="sxs-lookup"><span data-stu-id="b0a66-130">To get information about the current state of the operation, call the Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with the guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="b0a66-131">La API Node Transition Progress devuelve un objeto NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="b0a66-131">The Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="b0a66-132">La propiedad State de este objeto especifica el estado actual de la operación.</span><span class="sxs-lookup"><span data-stu-id="b0a66-132">This object’s State property specifies the current state of the operation.</span></span>  <span data-ttu-id="b0a66-133">Si el estado es "Running", significa que la operación está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="b0a66-133">If the state is “Running” then the operation is executing.</span></span>  <span data-ttu-id="b0a66-134">Si el estado es Completed, significa que la operación ha finalizado sin errores.</span><span class="sxs-lookup"><span data-stu-id="b0a66-134">If it is Completed, the operation finished without error.</span></span>  <span data-ttu-id="b0a66-135">Si el estado es Faulted, significa que se ha producido un problema al ejecutar la operación.</span><span class="sxs-lookup"><span data-stu-id="b0a66-135">If it is Faulted, there was a problem executing the operation.</span></span>  <span data-ttu-id="b0a66-136">La propiedad Exception de la propiedad Result indica de qué problema se trata.</span><span class="sxs-lookup"><span data-stu-id="b0a66-136">The Result property’s Exception property will indicate what the issue was.</span></span>  <span data-ttu-id="b0a66-137">Vea https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate para obtener más información sobre la propiedad State y la sección "Ejemplo de uso" a continuación para obtener ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="b0a66-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about the State property, and the “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="b0a66-138">**Diferenciar entre un nodo detenido y un nodo inactivo** Si un nodo está *detenido* con la API Node Transition, el resultado de una consulta de nodo (administrada [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) mostrará que este nodo tiene un valor true para la propiedad *IsStopped*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using the Node Transition API, the output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="b0a66-139">Tenga en cuenta que este valor es diferente del valor de la propiedad *NodeStatus*, que será *Down* (Apagado).</span><span class="sxs-lookup"><span data-stu-id="b0a66-139">Note this is different from the value of the *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="b0a66-140">Si la propiedad *NodeStatus* tiene el valor *Down*, pero *IsStopped* es false, entonces significa que el nodo no se ha detenido con la API Node Transition y que está *apagado* por alguna otra razón.</span><span class="sxs-lookup"><span data-stu-id="b0a66-140">If the *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then the node was not stopped using the Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="b0a66-141">Si la propiedad *IsStopped* es true y la propiedad *NodeStatus* es *Down*, entonces significa que se ha detenido con la API Node Transition.</span><span class="sxs-lookup"><span data-stu-id="b0a66-141">If the *IsStopped* property is true, and the *NodeStatus* property is *Down*, then it was stopped using the Node Transition API.</span></span>

<span data-ttu-id="b0a66-142">Al iniciar un nodo *detenido* con la API Node Transition, el nodo volverá a funcionar como un miembro normal del clúster.</span><span class="sxs-lookup"><span data-stu-id="b0a66-142">Starting a *stopped* node using the Node Transition API will return it to function as a normal member of the cluster again.</span></span>  <span data-ttu-id="b0a66-143">El resultado de la API de consulta de nodo mostrará *IsStopped* como false, y *NodeStatus* con un estado distinto a apagado, como por ejemplo, Up (encendido).</span><span class="sxs-lookup"><span data-stu-id="b0a66-143">The output of the node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="b0a66-144">**Duración limitada** Al usar la API Node Transition para detener un nodo, uno de los parámetros necesarios *stopNodeDurationInSeconds*, representa la duración en segundos durante la cual el nodo debe estar *detenido*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-144">**Limited Duration** When using the Node Transition API to stop a node, one of the required parameters, *stopNodeDurationInSeconds*, represents the amount of time in seconds to keep the node *stopped*.</span></span>  <span data-ttu-id="b0a66-145">Este valor debe estar dentro del intervalo permitido, que tiene un mínimo de 600, y un máximo de 14400.</span><span class="sxs-lookup"><span data-stu-id="b0a66-145">This value must be in the allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="b0a66-146">Después de que expire este tiempo, el propio nodo se reiniciará automáticamente con el estado Up.</span><span class="sxs-lookup"><span data-stu-id="b0a66-146">After this time expires, the node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="b0a66-147">Consulte el Ejemplo 1 a continuación para ver un ejemplo de uso.</span><span class="sxs-lookup"><span data-stu-id="b0a66-147">Refer to Sample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="b0a66-148">Evite mezclar las API Node Transition y las API Stop Node y Start Node.</span><span class="sxs-lookup"><span data-stu-id="b0a66-148">Avoid mixing Node Transition APIs and the Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="b0a66-149">Se recomienda usar solo la API Node Transition.</span><span class="sxs-lookup"><span data-stu-id="b0a66-149">The recommendation is to  use the Node Transition API only.</span></span>  <span data-ttu-id="b0a66-150">Si un nodo ya está detenido con la API Stop Node, debe iniciarse con la API Start Node primero antes de usar las API Node Transition.</span><span class="sxs-lookup"><span data-stu-id="b0a66-150">> If a node has been already been stopped using the Stop Node API, it should be started using the Start Node API first before using the > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="b0a66-151">No se pueden realizar en paralelo varias llamadas a las API Node Transition en el mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-151">Multiple Node Transition APIs calls cannot be made on the same node in parallel.</span></span>  <span data-ttu-id="b0a66-152">En esta situación, la API Node Transition lanzará una excepción FabricException, donde el valor de la propiedad ErrorCode será NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="b0a66-152">In such a situation, the Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="b0a66-153">Una vez iniciada una transición de nodo de un nodo específico, debe esperar hasta que la operación llega a un estado terminal (Completed, Faulted o ForceCancelled) antes de iniciar una transición nueva en el mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-153">Once a node transition on a specific node has  > been started, you should wait until the operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on the same node.</span></span>  <span data-ttu-id="b0a66-154">Sí se permiten llamadas paralelas a las API Node Transition en diferentes nodos.</span><span class="sxs-lookup"><span data-stu-id="b0a66-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="b0a66-155">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="b0a66-155">Sample Usage</span></span>


<span data-ttu-id="b0a66-156">**Ejemplo 1** - El ejemplo siguiente utiliza la API Node Transition para detener un nodo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-156">**Sample 1** - The following sample uses the Node Transition API to stop a node.</span></span>

```csharp
        // Helper function to get information about a node
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
                        // Inspect the progress object's Result.Exception.HResult to get the error code.
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
            // Uses the GetNodeListAsync() API to get information about the target node
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
                    // Invoke StartNodeTransitionAsync with the NodeStopDescription from above, which will stop the target node.  Retry transient errors.
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

<span data-ttu-id="b0a66-157">**Ejemplo 2** - El ejemplo siguiente inicia un nodo *detenido*.</span><span class="sxs-lookup"><span data-stu-id="b0a66-157">**Sample 2** - The following sample starts a *stopped* node.</span></span>  <span data-ttu-id="b0a66-158">Usa algunos métodos auxiliares del primer ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-158">It uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
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
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
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

<span data-ttu-id="b0a66-159">**Ejemplo 3** - El ejemplo siguiente muestra un uso incorrecto.</span><span class="sxs-lookup"><span data-stu-id="b0a66-159">**Sample 3** - The following sample shows incorrect usage.</span></span>  <span data-ttu-id="b0a66-160">Este uso es incorrecto porque el valor *stopDurationInSeconds* que proporciona es mayor que el intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="b0a66-160">This usage is incorrect because the *stopDurationInSeconds* it provides is greater than the allowed range.</span></span>  <span data-ttu-id="b0a66-161">Teniendo en cuenta que StartNodeTransitionAsync() provocará un error grave, la operación no se acepta y no se debe realizar ninguna llamada a la API de progreso.</span><span class="sxs-lookup"><span data-stu-id="b0a66-161">Since StartNodeTransitionAsync() will fail with a fatal error, the operation was not accepted, and the progress API should not be called.</span></span>  <span data-ttu-id="b0a66-162">Este ejemplo usa algunos métodos auxiliares del primer ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-162">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds to demonstrate error
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

<span data-ttu-id="b0a66-163">**Ejemplo 4** - El ejemplo siguiente muestra la información del error que la API Node Transition Progress devolverá cuando se acepte la operación iniciada por la API Node Transition, pero se produce un error más adelante durante la ejecución.</span><span class="sxs-lookup"><span data-stu-id="b0a66-163">**Sample 4** - The following sample shows the error information that will be returned from the Node Transition Progress API when the operation initiated by the Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="b0a66-164">En este caso, el error se produce porque la API Node Transition trata de iniciar un nodo que no existe.</span><span class="sxs-lookup"><span data-stu-id="b0a66-164">In the case, it fails because the Node Transition API attempts to start a node that does not exist.</span></span>  <span data-ttu-id="b0a66-165">Este ejemplo usa algunos métodos auxiliares del primer ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b0a66-165">This sample uses some helper methods from the first sample.</span></span>

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
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
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

            // Now call StartNodeTransitionProgressAsync() until the desired state is reached.  In this case, it will end up in the Faulted state since the node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect the progress object's Result.Exception.HResult to get the error code.
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
