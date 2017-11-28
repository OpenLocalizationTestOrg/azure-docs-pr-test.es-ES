---
title: errores de aaaSimulate en Azure microservicios | Documentos de Microsoft
description: "En este artículo se habla sobre acciones de capacidad de prueba de Hola que se encuentran en Microsoft Azure Service Fabric."
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
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="84a1a-103">Acciones de Testability</span><span class="sxs-lookup"><span data-stu-id="84a1a-103">Testability actions</span></span>
<span data-ttu-id="84a1a-104">En orden toosimulate una infraestructura confiable, Azure Service Fabric usted como desarrollador de hello, con formas toosimulate proporciona varios errores reales y las transiciones de estado.</span><span class="sxs-lookup"><span data-stu-id="84a1a-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="84a1a-105">Dichas formas se exponen como acciones de Testability.</span><span class="sxs-lookup"><span data-stu-id="84a1a-105">These are exposed as testability actions.</span></span> <span data-ttu-id="84a1a-106">acciones de Hola se Hola API de bajo nivel que provocan una inyección de código de error concreto, la transición de estado o la validación.</span><span class="sxs-lookup"><span data-stu-id="84a1a-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="84a1a-107">Mediante la combinación de estas acciones, puede escribir escenarios de prueba completos para los servicios.</span><span class="sxs-lookup"><span data-stu-id="84a1a-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="84a1a-108">Service Fabric proporciona varios escenarios de prueba comunes que constan de estas acciones.</span><span class="sxs-lookup"><span data-stu-id="84a1a-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="84a1a-109">Se recomienda encarecidamente que use estos escenarios integrados, que se eligen cuidadosamente las transiciones de estado comunes tootest y casos de error.</span><span class="sxs-lookup"><span data-stu-id="84a1a-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="84a1a-110">Sin embargo, las acciones pueden ser toocreate usado escenarios de prueba personalizada si desea tooadd cobertura para escenarios que no están cubiertas por escenarios integrados Hola aún o que son personalizadas adaptadas a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="84a1a-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="84a1a-111">Las implementaciones de C# de acciones de Hola se encuentran en hello System.Fabric.dll ensamblado.</span><span class="sxs-lookup"><span data-stu-id="84a1a-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="84a1a-112">se encuentra el módulo de PowerShell de tejido de sistema de Hola Hola Microsoft.ServiceFabric.Powershell.dll ensamblado.</span><span class="sxs-lookup"><span data-stu-id="84a1a-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="84a1a-113">Como parte de la instalación de en tiempo de ejecución, Hola módulo ServiceFabric PowerShell está instalado tooallow para facilitar su uso.</span><span class="sxs-lookup"><span data-stu-id="84a1a-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="84a1a-114">Acciones de errores estables frente a inestables</span><span class="sxs-lookup"><span data-stu-id="84a1a-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="84a1a-115">Las acciones de Testability se clasifican en dos cubos principales:</span><span class="sxs-lookup"><span data-stu-id="84a1a-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="84a1a-116">Errores inestables: simulan errores como reinicios de equipos y bloqueos de procesos.</span><span class="sxs-lookup"><span data-stu-id="84a1a-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="84a1a-117">En tales casos de errores, contexto de ejecución de hello del proceso se detiene repentinamente.</span><span class="sxs-lookup"><span data-stu-id="84a1a-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="84a1a-118">Esto significa que no puede ejecutar ninguna limpieza del estado de hello antes de aplicación hello vuelve a empezar.</span><span class="sxs-lookup"><span data-stu-id="84a1a-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="84a1a-119">Errores estables: simulan acciones estables como movimientos y eliminaciones de réplicas desencadenados por el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="84a1a-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="84a1a-120">En tales casos, el servicio de hello recibe una notificación de hello cerrar y puede limpiar el estado de hello antes de salir.</span><span class="sxs-lookup"><span data-stu-id="84a1a-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="84a1a-121">En la validación de mejor calidad, ejecute el servicio de Hola y carga de trabajo de negocios durante la inducción de diversos errores estable e incorrectas.</span><span class="sxs-lookup"><span data-stu-id="84a1a-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="84a1a-122">Errores incorrectas actúan sobre escenarios donde el proceso del servicio de hello cierra abruptamente en medio de Hola de algunos flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="84a1a-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="84a1a-123">Esto permite probar la ruta de recuperación de hello una vez restaurado réplicas del servicio Hola por Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="84a1a-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="84a1a-124">Esto le ayudará a probar la coherencia de los datos y si se mantiene el estado de servicio de hello correctamente después de los errores.</span><span class="sxs-lookup"><span data-stu-id="84a1a-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="84a1a-125">Hello otro conjunto de errores (Hola estable de errores) de prueba que el servicio de hello reacciona correctamente tooreplicas que se mueven por Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="84a1a-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="84a1a-126">Esto permite probar tratamiento de cancelación en el método de hello Coredispatcher.</span><span class="sxs-lookup"><span data-stu-id="84a1a-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="84a1a-127">servicio de Hello necesita toocheck para hello cancelación símbolo (token) que se va a establecer, guardar correctamente su estado y salir del método de hello Coredispatcher.</span><span class="sxs-lookup"><span data-stu-id="84a1a-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="84a1a-128">Lista de acciones de Testability</span><span class="sxs-lookup"><span data-stu-id="84a1a-128">Testability actions list</span></span>
| <span data-ttu-id="84a1a-129">Acción</span><span class="sxs-lookup"><span data-stu-id="84a1a-129">Action</span></span> | <span data-ttu-id="84a1a-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="84a1a-130">Description</span></span> | <span data-ttu-id="84a1a-131">API administrada</span><span class="sxs-lookup"><span data-stu-id="84a1a-131">Managed API</span></span> | <span data-ttu-id="84a1a-132">Cmdlet de PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a1a-132">PowerShell cmdlet</span></span> | <span data-ttu-id="84a1a-133">Errores estables o no estables</span><span class="sxs-lookup"><span data-stu-id="84a1a-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="84a1a-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="84a1a-134">CleanTestState</span></span> |<span data-ttu-id="84a1a-135">Quita todos los Estados de prueba de Hola de clúster de hello en el caso de un cierre incorrecto del controlador de pruebas de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="84a1a-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-136">CleanTestStateAsync</span></span> |<span data-ttu-id="84a1a-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="84a1a-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="84a1a-138">No aplicable</span><span class="sxs-lookup"><span data-stu-id="84a1a-138">Not applicable</span></span> |
| <span data-ttu-id="84a1a-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="84a1a-139">InvokeDataLoss</span></span> |<span data-ttu-id="84a1a-140">Provoca la pérdida de datos en una partición del servicio.</span><span class="sxs-lookup"><span data-stu-id="84a1a-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="84a1a-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="84a1a-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="84a1a-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="84a1a-143">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-143">Graceful</span></span> |
| <span data-ttu-id="84a1a-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="84a1a-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="84a1a-145">Coloca una partición determinada del servicio con estado en pérdida de quórum.</span><span class="sxs-lookup"><span data-stu-id="84a1a-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="84a1a-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="84a1a-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="84a1a-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="84a1a-148">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-148">Graceful</span></span> |
| <span data-ttu-id="84a1a-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="84a1a-149">Move Primary</span></span> |<span data-ttu-id="84a1a-150">Se desplaza Hola había especificado réplica principal de un nodo de clúster especificado de servicio con estado toohello.</span><span class="sxs-lookup"><span data-stu-id="84a1a-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="84a1a-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-151">MovePrimaryAsync</span></span> |<span data-ttu-id="84a1a-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="84a1a-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="84a1a-153">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-153">Graceful</span></span> |
| <span data-ttu-id="84a1a-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="84a1a-154">Move Secondary</span></span> |<span data-ttu-id="84a1a-155">Mueve la réplica secundaria actual de Hola de servicio con estado tooa otro nodo de clúster.</span><span class="sxs-lookup"><span data-stu-id="84a1a-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="84a1a-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="84a1a-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="84a1a-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="84a1a-158">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-158">Graceful</span></span> |
| <span data-ttu-id="84a1a-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="84a1a-159">RemoveReplica</span></span> |<span data-ttu-id="84a1a-160">Simula un error de réplica mediante la eliminación de una réplica de un clúster.</span><span class="sxs-lookup"><span data-stu-id="84a1a-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="84a1a-161">Esto cerrará la réplica de Hola y realizará la transición se toorole 'None', quitar todo su estado de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="84a1a-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="84a1a-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="84a1a-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="84a1a-164">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-164">Graceful</span></span> |
| <span data-ttu-id="84a1a-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="84a1a-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="84a1a-166">Simula un error de proceso del paquete de código mediante el reinicio de un paquete de código implementado en un nodo de un clúster.</span><span class="sxs-lookup"><span data-stu-id="84a1a-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="84a1a-167">Esto anula el proceso de paquete de código de hello, que se reiniciará todas las réplicas de servicio de usuario de hello hospedadas en ese proceso.</span><span class="sxs-lookup"><span data-stu-id="84a1a-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="84a1a-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="84a1a-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="84a1a-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="84a1a-170">Inestable</span><span class="sxs-lookup"><span data-stu-id="84a1a-170">Ungraceful</span></span> |
| <span data-ttu-id="84a1a-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="84a1a-171">RestartNode</span></span> |<span data-ttu-id="84a1a-172">Simula un error de nodo de clúster de Service Fabric mediante el reinicio de un nodo.</span><span class="sxs-lookup"><span data-stu-id="84a1a-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="84a1a-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-173">RestartNodeAsync</span></span> |<span data-ttu-id="84a1a-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="84a1a-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="84a1a-175">Inestable</span><span class="sxs-lookup"><span data-stu-id="84a1a-175">Ungraceful</span></span> |
| <span data-ttu-id="84a1a-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="84a1a-176">RestartPartition</span></span> |<span data-ttu-id="84a1a-177">Simula un escenario de falta de disponibilidad del centro de datos o una falta de disponibilidad del clúster mediante el reinicio de algunas o todas las réplicas de una partición.</span><span class="sxs-lookup"><span data-stu-id="84a1a-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="84a1a-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-178">RestartPartitionAsync</span></span> |<span data-ttu-id="84a1a-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="84a1a-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="84a1a-180">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-180">Graceful</span></span> |
| <span data-ttu-id="84a1a-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="84a1a-181">RestartReplica</span></span> |<span data-ttu-id="84a1a-182">Simula un error de réplica al reiniciar una réplica almacenada en un clúster, cerrar réplica hello y, a continuación, volver a abrirlo.</span><span class="sxs-lookup"><span data-stu-id="84a1a-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="84a1a-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-183">RestartReplicaAsync</span></span> |<span data-ttu-id="84a1a-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="84a1a-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="84a1a-185">Estable</span><span class="sxs-lookup"><span data-stu-id="84a1a-185">Graceful</span></span> |
| <span data-ttu-id="84a1a-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="84a1a-186">StartNode</span></span> |<span data-ttu-id="84a1a-187">Inicia un nodo en un clúster que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="84a1a-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="84a1a-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-188">StartNodeAsync</span></span> |<span data-ttu-id="84a1a-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="84a1a-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="84a1a-190">No aplicable</span><span class="sxs-lookup"><span data-stu-id="84a1a-190">Not applicable</span></span> |
| <span data-ttu-id="84a1a-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="84a1a-191">StopNode</span></span> |<span data-ttu-id="84a1a-192">Simula un error de nodo mediante la detención de un nodo en un clúster.</span><span class="sxs-lookup"><span data-stu-id="84a1a-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="84a1a-193">nodo de Hello permanecerá hacia abajo hasta que se llama StartNode.</span><span class="sxs-lookup"><span data-stu-id="84a1a-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="84a1a-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-194">StopNodeAsync</span></span> |<span data-ttu-id="84a1a-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="84a1a-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="84a1a-196">Inestable</span><span class="sxs-lookup"><span data-stu-id="84a1a-196">Ungraceful</span></span> |
| <span data-ttu-id="84a1a-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="84a1a-197">ValidateApplication</span></span> |<span data-ttu-id="84a1a-198">Valida la disponibilidad de Hola y el estado de todos los servicios de Service Fabric dentro de una aplicación, normalmente después de inducción de algunos errores en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="84a1a-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="84a1a-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="84a1a-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="84a1a-201">No aplicable</span><span class="sxs-lookup"><span data-stu-id="84a1a-201">Not applicable</span></span> |
| <span data-ttu-id="84a1a-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="84a1a-202">ValidateService</span></span> |<span data-ttu-id="84a1a-203">Valida la disponibilidad de Hola y el estado de un servicio de Service Fabric, normalmente después de inducción de algunos errores en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="84a1a-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="84a1a-204">ValidateServiceAsync</span></span> |<span data-ttu-id="84a1a-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="84a1a-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="84a1a-206">No aplicable</span><span class="sxs-lookup"><span data-stu-id="84a1a-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="84a1a-207">Ejecución de una acción de Testability con PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a1a-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="84a1a-208">Este tutorial muestra cómo toorun una acción de la capacidad de prueba mediante el uso de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84a1a-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="84a1a-209">Obtendrá información sobre cómo toorun una acción de la capacidad de prueba en un clúster (cuadro de uno) local o en un clúster de Azure.</span><span class="sxs-lookup"><span data-stu-id="84a1a-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="84a1a-210">Microsoft.Fabric.Powershell.dll--hello módulo de PowerShell de tejido de servicio--se instala automáticamente al instalar Hola MSI de tejido de servicio de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="84a1a-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="84a1a-211">módulo de Hola se carga automáticamente cuando se abre un símbolo del sistema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84a1a-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="84a1a-212">Secciones del tutorial:</span><span class="sxs-lookup"><span data-stu-id="84a1a-212">Tutorial segments:</span></span>

* [<span data-ttu-id="84a1a-213">Ejecución de una acción en un clúster one-box</span><span class="sxs-lookup"><span data-stu-id="84a1a-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="84a1a-214">Ejecución de una acción en un clúster de Azure</span><span class="sxs-lookup"><span data-stu-id="84a1a-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="84a1a-215">Ejecución de una acción en un clúster one-box</span><span class="sxs-lookup"><span data-stu-id="84a1a-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="84a1a-216">toorun una acción de la capacidad de prueba en un clúster local, primero conecte toohello clúster y símbolo del sistema de PowerShell de hello abierto en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="84a1a-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="84a1a-217">Echemos un vistazo en hello **ServiceFabricNode reinicio** acción.</span><span class="sxs-lookup"><span data-stu-id="84a1a-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="84a1a-218">Hola aquí acción **ServiceFabricNode reinicio** se está ejecutando en un nodo denominado "Nodo1".</span><span class="sxs-lookup"><span data-stu-id="84a1a-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="84a1a-219">modo de finalización de Hello especifica que no debe comprobar si acción de reinicio del nodo de Hola se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="84a1a-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="84a1a-220">Especificar el modo de finalización hello como "Verificar" hará que se tooverify si realmente se realizó correctamente la acción de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="84a1a-221">En lugar de especificar directamente el nodo de Hola por su nombre, puede especificar esta a través de un tipo de partición de hello y clave de réplica, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="84a1a-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="84a1a-222">**Reinicio ServiceFabricNode** debe ser un nodo de Service Fabric en un clúster de toorestart usado.</span><span class="sxs-lookup"><span data-stu-id="84a1a-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="84a1a-223">Este comando detiene el proceso Fabric.exe de hello, que se reiniciará todos Hola sistema servicio y usuario servicio réplicas hospedadas en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="84a1a-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="84a1a-224">Mediante este tootest API su servicio ayuda a detectar los errores a lo largo de las rutas de recuperación de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="84a1a-225">Ayuda a simular errores en los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="84a1a-226">Hello captura de pantalla siguiente muestra hello **ServiceFabricNode reinicio** comando de capacidad de prueba de acción.</span><span class="sxs-lookup"><span data-stu-id="84a1a-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="84a1a-227">Hola de salida de hello primero **ServiceFabricNode Get** (un cmdlet del módulo de PowerShell de tejido de servicio de hello) muestra ese clúster local hello tiene cinco nodos: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="84a1a-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="84a1a-228">Después de la acción de capacidad de prueba de hello (cmdlet) **ServiceFabricNode reinicio** se ejecuta en el nodo de hello, denominado Node.4, vemos se ha restablecido el tiempo de actividad de ese nodo Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="84a1a-229">Ejecución de una acción en un clúster de Azure</span><span class="sxs-lookup"><span data-stu-id="84a1a-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="84a1a-230">Ejecutar una acción de la capacidad de prueba (mediante el uso de PowerShell) en un clúster de Azure es la acción de hello toorunning similar en un clúster local.</span><span class="sxs-lookup"><span data-stu-id="84a1a-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="84a1a-231">Hello solo diferencia es que para poder ejecutar la acción de hello, en lugar de conexión toohello clúster local, deberá tooconnect toohello Azure primero del clúster.</span><span class="sxs-lookup"><span data-stu-id="84a1a-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="84a1a-232">Ejecución de una acción de Testability con C&#35;</span><span class="sxs-lookup"><span data-stu-id="84a1a-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="84a1a-233">toorun una acción de la capacidad de prueba mediante el uso de C#, primero debe tooconnect toohello clúster mediante el uso de FabricClient.</span><span class="sxs-lookup"><span data-stu-id="84a1a-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="84a1a-234">A continuación, obtener Hola parámetros necesarios toorun Hola acción.</span><span class="sxs-lookup"><span data-stu-id="84a1a-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="84a1a-235">Parámetros diferentes que pueden utilizarse toorun Hola misma acción.</span><span class="sxs-lookup"><span data-stu-id="84a1a-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="84a1a-236">Examinando hello RestartServiceFabricNode acción, una manera de toorun es mediante el uso de información del nodo hello (nombre de nodo e Id. de instancia de nodo) en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="84a1a-237">Explicación de parámetros:</span><span class="sxs-lookup"><span data-stu-id="84a1a-237">Parameter explanation:</span></span>

* <span data-ttu-id="84a1a-238">**CompleteMode** especifica que el modo de hello no debe comprobar si acción de reinicio de Hola se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="84a1a-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="84a1a-239">Especificar el modo de finalización hello como "Verificar" hará que se tooverify si realmente se realizó correctamente la acción de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="84a1a-240">**OperationTimeout** conjuntos Hola cantidad de tiempo para hello operación toofinish antes de que se produce una excepción TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="84a1a-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="84a1a-241">**CancellationToken** permite un toobe pendiente llamada cancelada.</span><span class="sxs-lookup"><span data-stu-id="84a1a-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="84a1a-242">En lugar de especificar directamente el nodo de Hola por su nombre, puede especificar esta a través de un tipo de hello y clave de partición de réplica.</span><span class="sxs-lookup"><span data-stu-id="84a1a-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="84a1a-243">Para obtener más información, consulte [PartitionSelector y ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="84a1a-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="84a1a-244">PartitionSelector y ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="84a1a-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="84a1a-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="84a1a-245">PartitionSelector</span></span>
<span data-ttu-id="84a1a-246">PartitionSelector es una aplicación auxiliar que se exponen en la capacidad de prueba y se tooselect usado un determinado crear particiones en qué tooperform cualquiera de las acciones de capacidad de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="84a1a-247">Puede ser usado tooselect una partición específica si Hola Id. de partición se conoce de antemano.</span><span class="sxs-lookup"><span data-stu-id="84a1a-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="84a1a-248">O bien, puede proporcionar la clave de partición de Hola y operación Hola resolverá el Id. de partición de hello internamente.</span><span class="sxs-lookup"><span data-stu-id="84a1a-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="84a1a-249">También tiene Hola opción de seleccionar una partición aleatoria.</span><span class="sxs-lookup"><span data-stu-id="84a1a-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="84a1a-250">toouse esta función auxiliar, crear hello PartitionSelector objeto y seleccione partición hello mediante uno de los métodos de hello Select *.</span><span class="sxs-lookup"><span data-stu-id="84a1a-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="84a1a-251">A continuación, pasar en hello PartitionSelector objeto toohello API que lo requiera.</span><span class="sxs-lookup"><span data-stu-id="84a1a-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="84a1a-252">Si no se selecciona ninguna opción, el valor predeterminado es tooa aleatorio partición.</span><span class="sxs-lookup"><span data-stu-id="84a1a-252">If no option is selected, it defaults tooa random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="84a1a-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="84a1a-253">ReplicaSelector</span></span>
<span data-ttu-id="84a1a-254">ReplicaSelector es una aplicación auxiliar que se exponen en la capacidad de prueba y se usa toohelp seleccione una réplica en qué tooperform cualquiera de las acciones de capacidad de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="84a1a-255">Puede ser tooselect usa una réplica específica si Hola Id. de réplica se conoce de antemano.</span><span class="sxs-lookup"><span data-stu-id="84a1a-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="84a1a-256">Además, tiene Hola opción de seleccionar una réplica principal o secundaria aleatoria.</span><span class="sxs-lookup"><span data-stu-id="84a1a-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="84a1a-257">ReplicaSelector se deriva de los PartitionSelector, por lo que necesita tooselect ambos Hola hello y réplica de partición en la que desea operación de capacidad de prueba de tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="84a1a-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="84a1a-258">toouse esta función auxiliar, cree un objeto de ReplicaSelector y establezca Hola que quieras particiones de réplica y Hola Hola tooselect.</span><span class="sxs-lookup"><span data-stu-id="84a1a-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="84a1a-259">A continuación, puede pasar en hello API que lo requiera.</span><span class="sxs-lookup"><span data-stu-id="84a1a-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="84a1a-260">Si no se selecciona ninguna opción, el valor predeterminado es tooa aleatorio réplica y partición aleatoria.</span><span class="sxs-lookup"><span data-stu-id="84a1a-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="84a1a-261">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84a1a-261">Next steps</span></span>
* [<span data-ttu-id="84a1a-262">Escenarios de Testability</span><span class="sxs-lookup"><span data-stu-id="84a1a-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="84a1a-263">Cómo tootest su servicio</span><span class="sxs-lookup"><span data-stu-id="84a1a-263">How tootest your service</span></span>
  * [<span data-ttu-id="84a1a-264">Simulación de errores durante las cargas de trabajo del servicio</span><span class="sxs-lookup"><span data-stu-id="84a1a-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="84a1a-265">Errores de comunicación entre servicios</span><span class="sxs-lookup"><span data-stu-id="84a1a-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

