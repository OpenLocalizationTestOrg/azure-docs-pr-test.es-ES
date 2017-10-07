---
title: "aaaHow tooInvoke pérdida de datos en servicios de Service Fabric | Documentos de Microsoft"
description: "Describe cómo toouse Hola pérdida de datos api"
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
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="9d994-103">¿Cómo tooInvoke pérdida de datos en los servicios</span><span class="sxs-lookup"><span data-stu-id="9d994-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="9d994-104">Este documento describe cómo toocause pérdida de datos en los servicios y debe utilizarse con cuidado.</span><span class="sxs-lookup"><span data-stu-id="9d994-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="9d994-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="9d994-105">Introduction</span></span>
<span data-ttu-id="9d994-106">Puede invocar la pérdida de datos en una partición de su servicio de Service Fabric realizando una llamada a StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="9d994-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="9d994-107">Esta api utiliza Hola por inyección de código de error y el servicio de análisis tooperform Hola trabajo toocause datos pérdida condiciones.</span><span class="sxs-lookup"><span data-stu-id="9d994-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="9d994-108">Usar Hola por inyección de código de error y el servicio de análisis</span><span class="sxs-lookup"><span data-stu-id="9d994-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="9d994-109">Hola por inyección de código de error y el servicio de análisis actualmente admite Hola siguiendo las API en el siguiente gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d994-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="9d994-110">Hola derecha del gráfico de hello muestra hello cmdlet de PowerShell correspondiente.</span><span class="sxs-lookup"><span data-stu-id="9d994-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="9d994-111">Consulte la documentación de msdn toohello de cada API para obtener más información sobre cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="9d994-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="9d994-112">API de C#</span><span class="sxs-lookup"><span data-stu-id="9d994-112">C# API</span></span> | <span data-ttu-id="9d994-113">Cmdlet de PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d994-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="9d994-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="9d994-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="9d994-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="9d994-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="9d994-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="9d994-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="9d994-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="9d994-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="9d994-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="9d994-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="9d994-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="9d994-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="9d994-120">Información general conceptual de la ejecución de un comando</span><span class="sxs-lookup"><span data-stu-id="9d994-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="9d994-121">Hola por inyección de código de error y Analysis Services usa un modelo asincrónico donde se inicia Hola comando con una API denominada API de tooas Hola "Inicio" en este documento, a continuación, las comprobaciones de hello progreso de este comando con una API de "GetProgress" hasta que se ha alcanzado un terminal estado, o hasta que se cancele la descarga.</span><span class="sxs-lookup"><span data-stu-id="9d994-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="9d994-122">toostart un comando, llamar a API de "Inicio" hello para API correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9d994-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="9d994-123">Esta API devuelve cuando hello inyección de código de error y Analysis Services ha aceptado la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d994-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="9d994-124">Sin embargo, no indica hasta qué punto se ha ejecutado un comando ni tampoco si se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="9d994-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="9d994-125">En curso de toocheck de orden de un comando, llame a Hola "GetProgress" API correspondiente toohello "Start" API que se ha llamado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9d994-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="9d994-126">Hola "GetProgress" API devolverá un objeto que indica el estado actual de Hola de comando de hello dentro de su propiedad State.</span><span class="sxs-lookup"><span data-stu-id="9d994-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="9d994-127">El comando se ejecuta indefinidamente hasta que se produzcan uno de los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="9d994-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="9d994-128">Se completa correctamente.</span><span class="sxs-lookup"><span data-stu-id="9d994-128">It completes successfully.</span></span>  <span data-ttu-id="9d994-129">Si se llama a "GetProgress" en ella en este caso, se completará el estado del objeto de hello progreso.</span><span class="sxs-lookup"><span data-stu-id="9d994-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="9d994-130">Se produce un error irrecuperable.</span><span class="sxs-lookup"><span data-stu-id="9d994-130">It encounters a fatal error.</span></span>  <span data-ttu-id="9d994-131">Si se llama a "GetProgress" en ella en este caso, se generará un error estado del objeto de hello progreso</span><span class="sxs-lookup"><span data-stu-id="9d994-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="9d994-132">Cancelar a través de hello [CancelTestCommandAsync] [ cancel] API, o [Stop ServiceFabricTestCommand] [ cancelps] cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d994-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="9d994-133">Si se llama a "GetProgress" en ella en este caso, hello estado del progreso objeto será cancelado o ForceCancelled, dependiendo de una API de toothat de argumento.</span><span class="sxs-lookup"><span data-stu-id="9d994-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="9d994-134">Consulte la documentación de Hola para [CancelTestCommandAsync] [ cancel] para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="9d994-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="9d994-135">Detalles de la ejecución de un comando</span><span class="sxs-lookup"><span data-stu-id="9d994-135">Details of Running a Command</span></span>
<span data-ttu-id="9d994-136">En orden toostart un comando, llame a Hola API iniciar con argumentos de hello esperado.</span><span class="sxs-lookup"><span data-stu-id="9d994-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="9d994-137">Todas las API de inicio tiene un argumento de Guid denominado "operationId".</span><span class="sxs-lookup"><span data-stu-id="9d994-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="9d994-138">Se debe realizar un seguimiento del argumento de operationId hello, porque lo está usando tootrack progreso de este comando.</span><span class="sxs-lookup"><span data-stu-id="9d994-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="9d994-139">Esto se debe pasar "GetProgress" API de progreso del pedido tootrack del comando de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="9d994-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="9d994-140">Hola operationId debe ser único.</span><span class="sxs-lookup"><span data-stu-id="9d994-140">hello operationId must be unique.</span></span>

<span data-ttu-id="9d994-141">Después de llamar correctamente a Hola iniciar API, hello GetProgress API debe llamarse en un bucle hasta que Hola devuelto progreso se completa la propiedad de estado del objeto.</span><span class="sxs-lookup"><span data-stu-id="9d994-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="9d994-142">Se debe volver a tratar de inicializar todas las clases [FabricTransientException][fte] y OperationCanceledException.</span><span class="sxs-lookup"><span data-stu-id="9d994-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="9d994-143">Cuando el comando de hello ha alcanzado un estado terminal (completado, error o cancelado), Hola devuelve propiedad del resultado del objeto de curso tendrá información adicional.</span><span class="sxs-lookup"><span data-stu-id="9d994-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="9d994-144">Si se ha completado el estado de hello, Result.SelectedPartition.PartitionId contendrá el Id. de partición de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="9d994-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="9d994-145">El valor de Result.Exception será NULL.</span><span class="sxs-lookup"><span data-stu-id="9d994-145">Result.Exception will be null.</span></span>  <span data-ttu-id="9d994-146">Si se genera un error de estado de hello, Result.Exception tendrá Hola Hola de motivo inyección de código de error y error en el servicio Analysis Hola comando.</span><span class="sxs-lookup"><span data-stu-id="9d994-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="9d994-147">Result.SelectedPartition.PartitionId tendrá el Id. de partición de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="9d994-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="9d994-148">En algunas situaciones, comando hello puede no ha realizado lo que sea necesario toochoose una partición.</span><span class="sxs-lookup"><span data-stu-id="9d994-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="9d994-149">En ese caso, Hola PartitionId será 0.</span><span class="sxs-lookup"><span data-stu-id="9d994-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="9d994-150">Si se cancela el estado de hello, Result.Exception será null.</span><span class="sxs-lookup"><span data-stu-id="9d994-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="9d994-151">Como caso Faulted de hello, Result.SelectedPartition.PartitionId tendrá Id. de partición de Hola que se ha elegido, pero si el comando de hello no se han realizado todo lo necesario toodo por lo tanto, será 0.</span><span class="sxs-lookup"><span data-stu-id="9d994-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="9d994-152">Consulte también toohello ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9d994-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="9d994-153">Hola ejemplo de código siguiente muestra cómo toostart, a continuación, comprobar el progreso en una pérdida de datos de toocause de comando en una partición específica.</span><span class="sxs-lookup"><span data-stu-id="9d994-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="9d994-154">ejemplo de Hola siguiente muestra cómo toouse Hola PartitionSelector toochoose una partición aleatoria de un servicio especificado:</span><span class="sxs-lookup"><span data-stu-id="9d994-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="9d994-155">Historial y truncamiento</span><span class="sxs-lookup"><span data-stu-id="9d994-155">History and Truncation</span></span>
<span data-ttu-id="9d994-156">Después de que un comando ha alcanzado un estado terminal, sus metadatos permanecerán en hello inyección de código de error y Analysis Services para un momento determinado, para que pueda quitar espacio toosave.</span><span class="sxs-lookup"><span data-stu-id="9d994-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="9d994-157">Si se llama "GetProgress" con operationId Hola de un comando después de que se ha quitado, devolverá un FabricException con un código de error de KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="9d994-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
