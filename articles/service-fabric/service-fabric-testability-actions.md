---
title: "Simulación de errores en microservicios de Azure | Microsoft Docs"
description: "En este artículo se habla sobre las acciones de capacidad de prueba que se encuentra en el servicio de Microsoft Azure Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="4e4ec-103">Acciones de Testability</span><span class="sxs-lookup"><span data-stu-id="4e4ec-103">Testability actions</span></span>
<span data-ttu-id="4e4ec-104">Para simular una infraestructura no confiable, Azure Service Fabric proporciona a los desarrolladores distintas formas de simular varios errores y transiciones de estados que se producen en escenarios reales.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="4e4ec-105">Dichas formas se exponen como acciones de Testability.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-105">These are exposed as testability actions.</span></span> <span data-ttu-id="4e4ec-106">Las acciones son las API de bajo nivel que provocan una inserción de errores específicos, una transición de estado o una validación.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="4e4ec-107">Mediante la combinación de estas acciones, puede escribir escenarios de prueba completos para los servicios.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="4e4ec-108">Service Fabric proporciona varios escenarios de prueba comunes que constan de estas acciones.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="4e4ec-109">Recomendamos encarecidamente usar estos escenarios integrados, que se seleccionan meticulosamente, para probar las transiciones de estado comunes y los casos de error.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="4e4ec-110">Sin embargo, las acciones se pueden utilizar para crear escenarios de prueba personalizados cuando desee agregar cobertura a aquellos escenarios que no aún estén cubiertos por los escenarios integrados o adaptados de manera personalizada a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="4e4ec-111">Las implementaciones en C# de las acciones se encuentran en el ensamblado System.Fabric.dll.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="4e4ec-112">El módulo System Fabric PowerShell se encuentra en el ensamblado Microsoft.ServiceFabric.Powershell.dll.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="4e4ec-113">Como parte de la instalación en tiempo de ejecución, se instala el módulo ServiceFabric PowerShell para facilitar su uso.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="4e4ec-114">Acciones de errores estables frente a inestables</span><span class="sxs-lookup"><span data-stu-id="4e4ec-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="4e4ec-115">Las acciones de Testability se clasifican en dos cubos principales:</span><span class="sxs-lookup"><span data-stu-id="4e4ec-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="4e4ec-116">Errores inestables: simulan errores como reinicios de equipos y bloqueos de procesos.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="4e4ec-117">En tales casos, el contexto de ejecución del proceso se detiene abruptamente,</span><span class="sxs-lookup"><span data-stu-id="4e4ec-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="4e4ec-118">lo que significa que no se puede ejecutar ninguna limpieza de estado antes de que se vuelva a iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="4e4ec-119">Errores estables: simulan acciones estables como movimientos y eliminaciones de réplicas desencadenados por el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="4e4ec-120">En tales casos, el servicio recibe una notificación de cierre y puede limpiar el estado antes de salir.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="4e4ec-121">Para mejorar la calidad de la validación, ejecute la carga de trabajo del servicio y del negocio mientras provoca varios errores estables e inestables.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="4e4ec-122">Los errores inestables crean escenarios en que el proceso se cierra abruptamente en medio de algún flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="4e4ec-123">Así se prueba la ruta de recuperación una vez que Service Fabric restaura la réplica del servicio.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="4e4ec-124">Esto facilitará la comprobación de la coherencia de los datos y de si el estado del servicio se mantiene correctamente después de los errores.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="4e4ec-125">El otro conjunto de errores (los errores estables) prueban que el servicio reacciona correctamente al hecho de que Service Fabric mueva las réplicas.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="4e4ec-126">Así se prueba el control de la cancelación en el método RunAsync.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="4e4ec-127">El servicio debe comprobar si se ha establecido el token de cancelación, guardar correctamente su estado y salir del método RunAsync.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="4e4ec-128">Lista de acciones de Testability</span><span class="sxs-lookup"><span data-stu-id="4e4ec-128">Testability actions list</span></span>
| <span data-ttu-id="4e4ec-129">Acción</span><span class="sxs-lookup"><span data-stu-id="4e4ec-129">Action</span></span> | <span data-ttu-id="4e4ec-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="4e4ec-130">Description</span></span> | <span data-ttu-id="4e4ec-131">API administrada</span><span class="sxs-lookup"><span data-stu-id="4e4ec-131">Managed API</span></span> | <span data-ttu-id="4e4ec-132">Cmdlet de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4ec-132">PowerShell cmdlet</span></span> | <span data-ttu-id="4e4ec-133">Errores estables o no estables</span><span class="sxs-lookup"><span data-stu-id="4e4ec-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="4e4ec-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="4e4ec-134">CleanTestState</span></span> |<span data-ttu-id="4e4ec-135">Quita todo el estado de prueba del clúster en caso de un cierre incorrecto del controlador de prueba.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="4e4ec-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-136">CleanTestStateAsync</span></span> |<span data-ttu-id="4e4ec-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="4e4ec-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="4e4ec-138">No aplicable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-138">Not applicable</span></span> |
| <span data-ttu-id="4e4ec-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="4e4ec-139">InvokeDataLoss</span></span> |<span data-ttu-id="4e4ec-140">Provoca la pérdida de datos en una partición del servicio.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="4e4ec-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="4e4ec-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="4e4ec-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="4e4ec-143">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-143">Graceful</span></span> |
| <span data-ttu-id="4e4ec-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="4e4ec-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="4e4ec-145">Coloca una partición determinada del servicio con estado en pérdida de quórum.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="4e4ec-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="4e4ec-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="4e4ec-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="4e4ec-148">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-148">Graceful</span></span> |
| <span data-ttu-id="4e4ec-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="4e4ec-149">Move Primary</span></span> |<span data-ttu-id="4e4ec-150">Mueve la réplica principal especificada del servicio con estado al nodo de clúster especificado.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="4e4ec-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-151">MovePrimaryAsync</span></span> |<span data-ttu-id="4e4ec-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="4e4ec-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="4e4ec-153">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-153">Graceful</span></span> |
| <span data-ttu-id="4e4ec-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="4e4ec-154">Move Secondary</span></span> |<span data-ttu-id="4e4ec-155">Mueve la réplica secundaria actual de un servicio con estado a otro nodo de clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="4e4ec-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="4e4ec-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="4e4ec-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="4e4ec-158">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-158">Graceful</span></span> |
| <span data-ttu-id="4e4ec-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="4e4ec-159">RemoveReplica</span></span> |<span data-ttu-id="4e4ec-160">Simula un error de réplica mediante la eliminación de una réplica de un clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="4e4ec-161">Esto cerrará la réplica y realizará su transición al rol 'None', con lo que quitará todo su estado del clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="4e4ec-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="4e4ec-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="4e4ec-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="4e4ec-164">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-164">Graceful</span></span> |
| <span data-ttu-id="4e4ec-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="4e4ec-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="4e4ec-166">Simula un error de proceso del paquete de código mediante el reinicio de un paquete de código implementado en un nodo de un clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="4e4ec-167">Esto anula el proceso del paquete de código que reiniciará todas las réplicas del servicio de usuario hospedadas en dicho proceso.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="4e4ec-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="4e4ec-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="4e4ec-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="4e4ec-170">Inestable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-170">Ungraceful</span></span> |
| <span data-ttu-id="4e4ec-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="4e4ec-171">RestartNode</span></span> |<span data-ttu-id="4e4ec-172">Simula un error de nodo de clúster de Service Fabric mediante el reinicio de un nodo.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="4e4ec-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-173">RestartNodeAsync</span></span> |<span data-ttu-id="4e4ec-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4e4ec-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="4e4ec-175">Inestable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-175">Ungraceful</span></span> |
| <span data-ttu-id="4e4ec-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="4e4ec-176">RestartPartition</span></span> |<span data-ttu-id="4e4ec-177">Simula un escenario de falta de disponibilidad del centro de datos o una falta de disponibilidad del clúster mediante el reinicio de algunas o todas las réplicas de una partición.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="4e4ec-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-178">RestartPartitionAsync</span></span> |<span data-ttu-id="4e4ec-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="4e4ec-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="4e4ec-180">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-180">Graceful</span></span> |
| <span data-ttu-id="4e4ec-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="4e4ec-181">RestartReplica</span></span> |<span data-ttu-id="4e4ec-182">Simula un error de réplica mediante el reinicio de una réplica persistente en un clúster, para lo que cierra la réplica y vuelva a abrirla.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="4e4ec-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-183">RestartReplicaAsync</span></span> |<span data-ttu-id="4e4ec-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="4e4ec-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="4e4ec-185">Estable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-185">Graceful</span></span> |
| <span data-ttu-id="4e4ec-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="4e4ec-186">StartNode</span></span> |<span data-ttu-id="4e4ec-187">Inicia un nodo en un clúster que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="4e4ec-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-188">StartNodeAsync</span></span> |<span data-ttu-id="4e4ec-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4e4ec-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="4e4ec-190">No aplicable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-190">Not applicable</span></span> |
| <span data-ttu-id="4e4ec-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="4e4ec-191">StopNode</span></span> |<span data-ttu-id="4e4ec-192">Simula un error de nodo mediante la detención de un nodo en un clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="4e4ec-193">El nodo permanecerá inactivo hasta que se llame a StartNode.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="4e4ec-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-194">StopNodeAsync</span></span> |<span data-ttu-id="4e4ec-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4e4ec-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="4e4ec-196">Inestable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-196">Ungraceful</span></span> |
| <span data-ttu-id="4e4ec-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="4e4ec-197">ValidateApplication</span></span> |<span data-ttu-id="4e4ec-198">Valida la disponibilidad y mantenimiento de todos los servicios de Service Fabric de una aplicación, normalmente después de provocar algunos errores en el sistema.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="4e4ec-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="4e4ec-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4e4ec-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="4e4ec-201">No aplicable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-201">Not applicable</span></span> |
| <span data-ttu-id="4e4ec-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="4e4ec-202">ValidateService</span></span> |<span data-ttu-id="4e4ec-203">Valida la disponibilidad y mantenimiento de todos un servicios de Service Fabric, normalmente después de provocar algunos errores en el sistema.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="4e4ec-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="4e4ec-204">ValidateServiceAsync</span></span> |<span data-ttu-id="4e4ec-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="4e4ec-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="4e4ec-206">No aplicable</span><span class="sxs-lookup"><span data-stu-id="4e4ec-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="4e4ec-207">Ejecución de una acción de Testability con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4ec-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="4e4ec-208">Este tutorial muestra cómo ejecutar una acción de Testability con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="4e4ec-209">Aprenderá a ejecutar una acción de Testability en un clúster local (one-box) o un clúster de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="4e4ec-210">Microsoft.Fabric.Powershell.dll, el módulo Service Fabric PowerShell, se instala automáticamente al instalar el MSI de Microsoft Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="4e4ec-211">El módulo se carga automáticamente al abrir un aviso de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="4e4ec-212">Secciones del tutorial:</span><span class="sxs-lookup"><span data-stu-id="4e4ec-212">Tutorial segments:</span></span>

* [<span data-ttu-id="4e4ec-213">Ejecución de una acción en un clúster one-box</span><span class="sxs-lookup"><span data-stu-id="4e4ec-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="4e4ec-214">Ejecución de una acción en un clúster de Azure</span><span class="sxs-lookup"><span data-stu-id="4e4ec-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="4e4ec-215">Ejecución de una acción en un clúster one-box</span><span class="sxs-lookup"><span data-stu-id="4e4ec-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="4e4ec-216">Para ejecutar una acción de Testability en un clúster local, primero es preciso conectarse al clúster y, a continuación, abrir el aviso de PowerShell en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="4e4ec-217">Examinemos la acción **Restart-ServiceFabricNode** .</span><span class="sxs-lookup"><span data-stu-id="4e4ec-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="4e4ec-218">Aquí, la acción **Restart-ServiceFabricNode** se ejecuta en un nodo denominado "Node1".</span><span class="sxs-lookup"><span data-stu-id="4e4ec-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="4e4ec-219">El modo de finalización especifica que no debe comprobar si la acción restart-node se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="4e4ec-220">La especificación del modo de finalización como comprobación provocará que se compruebe si la acción de reinicio se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="4e4ec-221">En lugar de especificar directamente el nodo por su nombre, puede especificarlo a través de una clave de partición y el tipo de réplica, tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="4e4ec-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="4e4ec-222">**Restart-ServiceFabricNode** debe utilizarse para reiniciar un nodo de Service Fabric en un clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="4e4ec-223">Esto detendrá el proceso Fabric.exe, que reiniciará todas las réplicas de los servicios de sistema y de los servicios de usuario hospedados en dicho nodo.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="4e4ec-224">Si usa esta API para probar el servicio, le ayudará a revelar los errores a lo largo de las rutas de recuperación de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="4e4ec-225">Le ayuda a simular errores en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="4e4ec-226">La siguiente captura de pantalla muestra el comando **Restart-ServiceFabricNode** de Testability en acción.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="4e4ec-227">El resultado del primer **Get ServiceFabricNode** (un cmdlet del módulo de PowerShell de Service Fabric) muestra que el clúster local tiene cinco nodos: de Node.1 a Node.5.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="4e4ec-228">Una vez que la acción de Testability (cmdlet) **Restart-ServiceFabricNode** se ejecute en el nodo, denominado Node.4, veremos que se ha restablecido el tiempo de actividad del nodo.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="4e4ec-229">Ejecución de una acción en un clúster de Azure</span><span class="sxs-lookup"><span data-stu-id="4e4ec-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="4e4ec-230">La ejecución de una acción de Testability (mediante el uso de PowerShell) en un clúster de Azure es similar a la ejecución de la acción en un clúster local.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="4e4ec-231">La única diferencia es que, para poder ejecutar la acción, en lugar de conectarse al clúster local, debe conectarse primero al clúster de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="4e4ec-232">Ejecución de una acción de Testability con C&#35;</span><span class="sxs-lookup"><span data-stu-id="4e4ec-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="4e4ec-233">Para ejecutar una acción de Testability con C#, primero es preciso conectarse al clúster mediante FabricClient.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="4e4ec-234">A continuación, hay que obtener los parámetros necesarios para ejecutar la acción.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="4e4ec-235">Se pueden usar distintos parámetros para ejecutar la misma acción.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="4e4ec-236">Examinando la acción RestartServiceFabricNode, una forma de ejecutarla es usar la información (nombre del nodo e Id. de instancia de nodo) del nodo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="4e4ec-237">Explicación de parámetros:</span><span class="sxs-lookup"><span data-stu-id="4e4ec-237">Parameter explanation:</span></span>

* <span data-ttu-id="4e4ec-238">**CompleteMode** especifica que el modo no debe comprobar si la acción de reinicio se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="4e4ec-239">La especificación del modo de finalización como comprobación provocará que se compruebe si la acción de reinicio se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="4e4ec-240">**OperationTimeout** : establece la cantidad de tiempo que falta para que la operación finalice antes de que se inicie una excepción TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="4e4ec-241">**CancellationToken** : permite cancelar una llamada pendiente.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="4e4ec-242">En lugar de especificar directamente el nodo por su nombre, se puede especificar a través de una clave de partición y el tipo de réplica.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="4e4ec-243">Para obtener más información, consulte [PartitionSelector y ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="4e4ec-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="4e4ec-244">PartitionSelector y ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="4e4ec-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="4e4ec-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="4e4ec-245">PartitionSelector</span></span>
<span data-ttu-id="4e4ec-246">PartitionSelector es una aplicación auxiliar que se expone en Testability y que se utiliza para seleccionar una partición concreta en la que se va a realizar cualquiera de las acciones de Testability.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="4e4ec-247">Se puede usar para seleccionar una partición concreta si se conoce de antemano el Id. de la partición.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="4e4ec-248">O bien, se puede proporcionar la clave de partición y la operación resolverá internamente el Id. de la partición.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="4e4ec-249">También existe la opción de seleccionar una partición aleatoria.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="4e4ec-250">Para usar esta aplicación auxiliar, cree el objeto PartitionSelector y seleccione la partición mediante uno de los métodos Select*.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="4e4ec-251">A continuación, pase el objeto PartitionSelector a la API que lo requiera.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="4e4ec-252">Si no se selecciona ninguna opción, el valor predeterminado es una partición aleatoria.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-252">If no option is selected, it defaults to a random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="4e4ec-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="4e4ec-253">ReplicaSelector</span></span>
<span data-ttu-id="4e4ec-254">ReplicaSelector es una aplicación auxiliar que se expone en Testability y que se utiliza para ayudar a seleccionar una réplica en la que se va a realizar cualquiera de las acciones de Testability.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="4e4ec-255">Se puede usar para seleccionar una réplica concreta si se conoce de antemano el identificador de la réplica.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="4e4ec-256">Además, existe la opción de seleccionar una réplica principal o secundaria aleatoria.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="4e4ec-257">ReplicaSelector se deriva de PartitionSelector, por lo que es preciso seleccionar tanto la réplica como la partición en la que se desea realizar la operación de la Testability.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="4e4ec-258">Para esta aplicación auxiliar, cree un objeto ReplicaSelector y establezca la forma en que desea seleccionar la réplica y la partición.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="4e4ec-259">A continuación, puede pasarlo a la API que lo requiera.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="4e4ec-260">Si no se selecciona ninguna opción, el valor predeterminado es una réplica aleatoria y una partición aleatoria.</span><span class="sxs-lookup"><span data-stu-id="4e4ec-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="4e4ec-261">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e4ec-261">Next steps</span></span>
* [<span data-ttu-id="4e4ec-262">Escenarios de Testability</span><span class="sxs-lookup"><span data-stu-id="4e4ec-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="4e4ec-263">Procedimientos para probar un servicio</span><span class="sxs-lookup"><span data-stu-id="4e4ec-263">How to test your service</span></span>
  * [<span data-ttu-id="4e4ec-264">Simulación de errores durante las cargas de trabajo del servicio</span><span class="sxs-lookup"><span data-stu-id="4e4ec-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="4e4ec-265">Errores de comunicación entre servicios</span><span class="sxs-lookup"><span data-stu-id="4e4ec-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

