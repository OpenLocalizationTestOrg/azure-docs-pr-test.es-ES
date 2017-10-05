---
title: "Procedimiento para invocar la pérdida de datos en los servicios de Service Fabric | Microsoft Docs"
description: "En este documento se describe cómo utilizar la API de pérdida de datos."
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
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="a83b4-103">Procedimiento para invocar la pérdida de datos en los servicios</span><span class="sxs-lookup"><span data-stu-id="a83b4-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="a83b4-104">En este documento se describe cómo provocar la pérdida de datos en los servicios. Debe utilizar con precaución este procedimiento.</span><span class="sxs-lookup"><span data-stu-id="a83b4-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a83b4-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="a83b4-105">Introduction</span></span>
<span data-ttu-id="a83b4-106">Puede invocar la pérdida de datos en una partición de su servicio de Service Fabric realizando una llamada a StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="a83b4-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="a83b4-107">Esta API utiliza el servicio de análisis e inserción de errores para provocar condiciones de pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="a83b4-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="a83b4-108">Uso del servicio de análisis e inserción de errores</span><span class="sxs-lookup"><span data-stu-id="a83b4-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="a83b4-109">En estos momentos, el servicio de análisis e inserción de errores admite las siguientes API descritas en el gráfico siguiente.</span><span class="sxs-lookup"><span data-stu-id="a83b4-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="a83b4-110">En la parte derecha del gráfico se muestra el cmdlet de PowerShell correspondiente.</span><span class="sxs-lookup"><span data-stu-id="a83b4-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="a83b4-111">Consulte la documentación de MSDN de cada API para obtener más información sobre cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="a83b4-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="a83b4-112">API de C#</span><span class="sxs-lookup"><span data-stu-id="a83b4-112">C# API</span></span> | <span data-ttu-id="a83b4-113">Cmdlet de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a83b4-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="a83b4-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="a83b4-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="a83b4-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="a83b4-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="a83b4-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="a83b4-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="a83b4-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="a83b4-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="a83b4-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="a83b4-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="a83b4-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="a83b4-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="a83b4-120">Información general conceptual de la ejecución de un comando</span><span class="sxs-lookup"><span data-stu-id="a83b4-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="a83b4-121">El servicio de análisis e inserción de errores emplea un modelo asincrónico en el que se utiliza el comando con una API, a la que denominaremos "API de inicio" en este documento. Después, se comprueba el progreso de este comando con una API GetProgress hasta que se haya alcanzado un estado terminal o se cancele.</span><span class="sxs-lookup"><span data-stu-id="a83b4-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="a83b4-122">Para iniciar un comando, llame a la API de inicio de la API correspondiente.</span><span class="sxs-lookup"><span data-stu-id="a83b4-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="a83b4-123">Esta API se devuelve cuando el servicio de análisis e inserción de errores haya aceptado la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a83b4-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="a83b4-124">Sin embargo, no indica hasta qué punto se ha ejecutado un comando ni tampoco si se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="a83b4-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="a83b4-125">Para comprobar el progreso de un comando, llame a la API GetProgress que corresponde a la API de inicio que llamamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a83b4-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="a83b4-126">La API GetProgress devolverá un objeto que indica el estado actual del comando dentro de su propiedad State.</span><span class="sxs-lookup"><span data-stu-id="a83b4-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="a83b4-127">El comando se ejecuta indefinidamente hasta que se produzcan uno de los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="a83b4-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="a83b4-128">Se completa correctamente.</span><span class="sxs-lookup"><span data-stu-id="a83b4-128">It completes successfully.</span></span>  <span data-ttu-id="a83b4-129">Si, en este caso, se llama a GetProgress en ella, la propiedad State del objeto de progreso tendrá el valor Completado.</span><span class="sxs-lookup"><span data-stu-id="a83b4-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="a83b4-130">Se produce un error irrecuperable.</span><span class="sxs-lookup"><span data-stu-id="a83b4-130">It encounters a fatal error.</span></span>  <span data-ttu-id="a83b4-131">Si, en este caso, se llama a GetProgress en ella, la propiedad State del objeto de progreso tendrá el valor Error.</span><span class="sxs-lookup"><span data-stu-id="a83b4-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="a83b4-132">La operación puede cancelarse mediante la API [CancelTestCommandAsync][cancel] o el cmdlet de PowerShell [Stop ServiceFabricTestCommand][cancelps].</span><span class="sxs-lookup"><span data-stu-id="a83b4-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="a83b4-133">Si, en este caso, se llama a GetProgress en ella, la propiedad State del objeto de progreso tendrá el valor Cancelado o ForceCancelled, en función de cuál sea el argumento para dicha API.</span><span class="sxs-lookup"><span data-stu-id="a83b4-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="a83b4-134">Consulte la documentación de [CancelTestCommandAsync][cancel] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a83b4-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="a83b4-135">Detalles de la ejecución de un comando</span><span class="sxs-lookup"><span data-stu-id="a83b4-135">Details of Running a Command</span></span>
<span data-ttu-id="a83b4-136">Para iniciar un comando, llame a la API de inicio con los argumentos esperados.</span><span class="sxs-lookup"><span data-stu-id="a83b4-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="a83b4-137">Todas las API de inicio tiene un argumento de Guid denominado "operationId".</span><span class="sxs-lookup"><span data-stu-id="a83b4-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="a83b4-138">Se debe realizar un seguimiento del argumento operationId, ya que se utiliza para seguir el progreso de este comando.</span><span class="sxs-lookup"><span data-stu-id="a83b4-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="a83b4-139">Este argumento debe pasarse a la API GetProgress con el fin de realizar un seguimiento del progreso del comando.</span><span class="sxs-lookup"><span data-stu-id="a83b4-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="a83b4-140">El argumento operationId debe ser único.</span><span class="sxs-lookup"><span data-stu-id="a83b4-140">The operationId must be unique.</span></span>

<span data-ttu-id="a83b4-141">Después de llamar correctamente a la API de inicio, la API GetProgress debe llamarse en un bucle hasta que la propiedad State del objeto de progreso devuelto tenga el valor Completado.</span><span class="sxs-lookup"><span data-stu-id="a83b4-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="a83b4-142">Se debe volver a tratar de inicializar todas las clases [FabricTransientException][fte] y OperationCanceledException.</span><span class="sxs-lookup"><span data-stu-id="a83b4-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="a83b4-143">Cuando el comando haya alcanzado un estado terminal (Completado, Error o Cancelado), la propiedad Result del objeto de progreso devuelto contendrá más información.</span><span class="sxs-lookup"><span data-stu-id="a83b4-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="a83b4-144">Si el estado es Completado, Result.SelectedPartition.PartitionId incluirá el id. de partición que se seleccionó.</span><span class="sxs-lookup"><span data-stu-id="a83b4-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="a83b4-145">El valor de Result.Exception será NULL.</span><span class="sxs-lookup"><span data-stu-id="a83b4-145">Result.Exception will be null.</span></span>  <span data-ttu-id="a83b4-146">Si el estado es Error, Result.Exception incluirá la razón por la que el servicio de análisis e inserción de errores no pudo ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="a83b4-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="a83b4-147">Result.SelectedPartition.PartitionId tendrá el id. de partición que se haya seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a83b4-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="a83b4-148">En algunos casos, es posible que el comando no haya podido elegir correctamente una partición.</span><span class="sxs-lookup"><span data-stu-id="a83b4-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="a83b4-149">En ese caso, el valor de PartitionId será 0.</span><span class="sxs-lookup"><span data-stu-id="a83b4-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="a83b4-150">Si el estado es Cancelado, el valor de Result.Exception será NULL.</span><span class="sxs-lookup"><span data-stu-id="a83b4-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="a83b4-151">Al igual que en el caso del estado Error, Result.SelectedPartition.PartitionId tendrá el id. de partición que se seleccionó, pero si el comando no ha podido elegir correctamente la partición, el valor será 0.</span><span class="sxs-lookup"><span data-stu-id="a83b4-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="a83b4-152">Consulte también el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a83b4-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="a83b4-153">En el código de ejemplo siguiente se muestra cómo iniciar un comando y, luego, comprobar su progreso para provocar una pérdida de datos en una partición concreta.</span><span class="sxs-lookup"><span data-stu-id="a83b4-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

<span data-ttu-id="a83b4-154">En el ejemplo siguiente se muestra cómo utilizar PartitionSelector para elegir una partición aleatoria de un servicio especificado:</span><span class="sxs-lookup"><span data-stu-id="a83b4-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

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
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

## <a name="history-and-truncation"></a><span data-ttu-id="a83b4-155">Historial y truncamiento</span><span class="sxs-lookup"><span data-stu-id="a83b4-155">History and Truncation</span></span>
<span data-ttu-id="a83b4-156">Cuando un comando haya alcanzado un estado terminal, sus metadatos permanecerán en el servicio de análisis e inserción de errores durante un periodo determinado antes de que se quiten para ahorrar espacio.</span><span class="sxs-lookup"><span data-stu-id="a83b4-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="a83b4-157">Si se llama a GetProgress con el argumento operationId de un comando después de que se haya quitado, devolverá una excepción FabricException con un código de error de KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="a83b4-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
