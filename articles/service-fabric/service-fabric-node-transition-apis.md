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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Reemplazar hello nodo Iniciar y detener nodo API con hello API de transición de nodo

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>¿Qué Hola detener nodo y las API de nodo de inicio hacer?

Hola detener API de nodo (administrados: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) se detiene un nodo de Service Fabric.  Un nodo de Service Fabric es el proceso, no es una máquina virtual o máquina: Hola VM o máquina seguirá en ejecución.  Para el resto de saludo del documento de Hola "node" significa el nodo de Fabric de servicio.  Detención de un nodo lo coloca en una *detenido* estado donde no es un miembro de clúster de hello y no puede hospedar servicios, simulando así una *hacia abajo* nodo.  Esto es útil para insertar errores en hello tootest de sistema de la aplicación.  Hola API del nodo de inicio (administrados: [StartNodeAsync()][startnode], PowerShell: [inicio ServiceFabricNode][startnodeps]]) invierte Hola detener API de nodo,  Abre nodo hello tooa espera el estado normal.

## <a name="why-are-we-replacing-these"></a>¿Por qué se realiza la sustitución?

Como se describió anteriormente, un *detenido* Service Fabric trata de un nodo que se ha diseñado intencionalmente mediante Hola detener API de nodo.  A *hacia abajo* trata de un nodo que está inactivo por cualquier otra razón (p. ej. Hola máquina o máquina virtual está desactivada).  Con hello detener API de nodo, sistema de Hola no expone información toodifferentiate entre *detenido* nodos y *hacia abajo* nodos.

Además, algunos errores devueltos por estas API no son tan descriptivos como debieran.  Por ejemplo, invocar Hola detener API de nodo en una ya *detenido* nodo, devolverá el error de hello *InvalidAddress*.  Se puede mejorar esta experiencia.

Además, duración Hola que un nodo se detiene durante es "infinito" hasta Hola que se invoca la API del nodo de inicio.  Se ha detectado que esto puede ocasionar problemas y ser propenso a errores.  Por ejemplo, hemos visto problemas donde un usuario invoca Hola detener API de nodo en un nodo y, a continuación, que se haya olvidado sobre él.  Más adelante, estaba claro si Hola nodo estaba *hacia abajo* o *detenido*.


## <a name="introducing-hello-node-transition-apis"></a>Introducción a hello las API de transición de nodo

Se han solucionado estos problemas anteriores en un nuevo conjunto de API.  Hola nueva transición del nodo API (administrados: [StartNodeTransitionAsync()][snt]) puede ser utilizado tootransition un tooa de nodo de Service Fabric *detenido* estado o tootransition, desde un *detenido* tooa estado normal el estado.  Tenga en cuenta que Hola "Inicio" del nombre de Hola de hello API no hace referencia toostarting un nodo.  Hace referencia a una operación asincrónica que sistema Hola ejecutará tootransition Hola nodo tooeither toobeginning *detenido* o estado de iniciado.

**Uso**

Si Hola API de transición de nodo no produce una excepción cuando se invoca, a continuación, sistema Hola ha aceptado la operación asincrónica de hello y lo ejecuta.  Una llamada correcta no implica la operación de hello ha finalizado aún.  tooget información acerca del estado actual de Hola de operación de hello, Hola llamada API de progreso de transición de nodo (administrados: [GetNodeTransitionProgressAsync()][gntp]) con el guid de hello utilizado al invocar el nodo API de transición para esta operación.  Hola nodo transición de progreso de la API devuelve un objeto NodeTransitionProgress.  Propiedad de estado de este objeto especifica el estado actual de Hola de operación de Hola.  Si el estado de hello es "Running" se está ejecutando la operación Hola.  Si ésta se ha finalizado, la operación de hello ha finalizado sin errores.  Si lo tiene errores, se produjo un problema al ejecutar la operación de Hola.  Excepción de la propiedad del resultado de Hello propiedad indicará qué Hola emitir fue.  Consulte https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate para obtener más información acerca de la propiedad de estado de Hola y la sección de "Uso de ejemplo" Hola a continuación para obtener ejemplos de código.


**Diferenciar entre un nodo detenido y un nodo inactivo** si un nodo es *detenido* utilizando Hola API de transición de nodo, la salida de hello de una consulta de nodo (administrados: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) mostrará que este nodo tiene un *IsStopped* valor de la propiedad es true.  Tenga en cuenta esto es diferente del valor de Hola de hello *NodeStatus* propiedad, que indicará que *hacia abajo*.  Si hello *NodeStatus* propiedad tiene un valor de *hacia abajo*, pero *IsStopped* es false, no se detuvo nodo hello mediante API de transición de nodo de Hola y es  *Profundidad* debido a alguna otra razón.  Si hello *IsStopped* propiedad es true y hello *NodeStatus* propiedad es *hacia abajo*, a continuación, se ha detenido con hello API de transición de nodo.

A partir de un *detenido* nodo mediante la API de transición de nodo de Hola lo devuelva toofunction como un miembro normal del clúster de Hola de nuevo.  Hello resultado de consulta de nodo de hello API mostrará *IsStopped* como false, y *NodeStatus* como algo que no está inactivo (por ejemplo, arriba).


**Otros duración** al usar API de transición de nodo de hello toostop un nodo, uno de hello requiere parámetros, *stopNodeDurationInSeconds*, representa Hola cantidad de tiempo en el nodo de segundos tookeep hello  *detenido*.  Este valor debe estar en el intervalo, que tiene un mínimo de 600 y un máximo de 14400 permitido de Hola.  Después de que expire este tiempo, el nodo de Hola se reiniciará propio en el estado automáticamente.  Consulte tooSample 1 a continuación para obtener un ejemplo de uso.

> [!WARNING]
> Evite mezclar las API de transición de nodo y Hola detener nodo y las API de nodo de inicio.  recomendación de Hello es demasiado utilizar Hola API de transición de nodo.  > Si un nodo ya está detenido con hello detener API de nodo, se debe iniciar utilizando Hola API del nodo de inicio en primer lugar antes de usar hello > API de transición de nodo.

> [!WARNING]
> Hola a varias API de transición de nodo no se pueden realizar llamadas en el mismo nodo en paralelo.  En esta situación, lo Hola API de transición de nodo > producir una FabricException con un valor de la propiedad ErrorCode de NodeTransitionInProgress.  Una vez que tenga una transición de nodo en un nodo específico > está iniciado, debe esperar hasta que la operación de hello alcance un estado terminal (completado, error o ForceCancelled) antes de iniciar un > transición nuevos en hello mismo nodo.  Sí se permiten llamadas paralelas a las API Node Transition en diferentes nodos.


#### <a name="sample-usage"></a>Ejemplo de uso


**Ejemplo 1** -Hola siguientes usos de ejemplo Hola toostop un nodo de API de transición de nodo.

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

**Ejemplo 2** : hello siguiendo el ejemplo inicia una *detenido* nodo.  Usa algunos métodos auxiliares del primer ejemplo de Hola.

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

**Ejemplo 3** : hello en el ejemplo siguiente muestra el uso incorrecto.  Este uso es incorrecto porque hello *stopDurationInSeconds* proporciona es mayor que el intervalo permitido de Hola.  Puesto que StartNodeTransitionAsync() se producirá un error con un error irrecuperable, no se aceptó la operación de Hola y Hola progreso de la API no se debe llamar.  Este ejemplo usa algunos métodos auxiliares del primer ejemplo de Hola.

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

**Ejemplo 4** : hello en el ejemplo siguiente se muestra información de error de Hola que se obtendrán de hello nodo transición de progreso de la API cuando la operación de hello iniciada por hello API de transición de nodo se acepta, pero se produce un error más adelante al ejecutar.  En caso de hello, no como Hola API de transición de nodo trata toostart un nodo que no existe.  Este ejemplo usa algunos métodos auxiliares del primer ejemplo de Hola.

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
