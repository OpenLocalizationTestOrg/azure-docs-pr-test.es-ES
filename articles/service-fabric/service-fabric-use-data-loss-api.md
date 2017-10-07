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
# <a name="how-tooinvoke-data-loss-on-services"></a>¿Cómo tooInvoke pérdida de datos en los servicios
> [!WARNING]
> Este documento describe cómo toocause pérdida de datos en los servicios y debe utilizarse con cuidado.
> 
> 

## <a name="introduction"></a>Introducción
Puede invocar la pérdida de datos en una partición de su servicio de Service Fabric realizando una llamada a StartPartitionDataLossAsync().  Esta api utiliza Hola por inyección de código de error y el servicio de análisis tooperform Hola trabajo toocause datos pérdida condiciones.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Usar Hola por inyección de código de error y el servicio de análisis
Hola por inyección de código de error y el servicio de análisis actualmente admite Hola siguiendo las API en el siguiente gráfico de Hola.  Hola derecha del gráfico de hello muestra hello cmdlet de PowerShell correspondiente.  Consulte la documentación de msdn toohello de cada API para obtener más información sobre cada uno de ellos.

| API de C# | Cmdlet de PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Información general conceptual de la ejecución de un comando
Hola por inyección de código de error y Analysis Services usa un modelo asincrónico donde se inicia Hola comando con una API denominada API de tooas Hola "Inicio" en este documento, a continuación, las comprobaciones de hello progreso de este comando con una API de "GetProgress" hasta que se ha alcanzado un terminal estado, o hasta que se cancele la descarga.
toostart un comando, llamar a API de "Inicio" hello para API correspondiente Hola.  Esta API devuelve cuando hello inyección de código de error y Analysis Services ha aceptado la solicitud de Hola.  Sin embargo, no indica hasta qué punto se ha ejecutado un comando ni tampoco si se ha iniciado.  En curso de toocheck de orden de un comando, llame a Hola "GetProgress" API correspondiente toohello "Start" API que se ha llamado anteriormente.  Hola "GetProgress" API devolverá un objeto que indica el estado actual de Hola de comando de hello dentro de su propiedad State.  El comando se ejecuta indefinidamente hasta que se produzcan uno de los siguientes eventos:

1. Se completa correctamente.  Si se llama a "GetProgress" en ella en este caso, se completará el estado del objeto de hello progreso.
2. Se produce un error irrecuperable.  Si se llama a "GetProgress" en ella en este caso, se generará un error estado del objeto de hello progreso
3. Cancelar a través de hello [CancelTestCommandAsync] [ cancel] API, o [Stop ServiceFabricTestCommand] [ cancelps] cmdlet de PowerShell.  Si se llama a "GetProgress" en ella en este caso, hello estado del progreso objeto será cancelado o ForceCancelled, dependiendo de una API de toothat de argumento.  Consulte la documentación de Hola para [CancelTestCommandAsync] [ cancel] para obtener más detalles.

## <a name="details-of-running-a-command"></a>Detalles de la ejecución de un comando
En orden toostart un comando, llame a Hola API iniciar con argumentos de hello esperado.  Todas las API de inicio tiene un argumento de Guid denominado "operationId".  Se debe realizar un seguimiento del argumento de operationId hello, porque lo está usando tootrack progreso de este comando.  Esto se debe pasar "GetProgress" API de progreso del pedido tootrack del comando de Hola Hola.  Hola operationId debe ser único.

Después de llamar correctamente a Hola iniciar API, hello GetProgress API debe llamarse en un bucle hasta que Hola devuelto progreso se completa la propiedad de estado del objeto.  Se debe volver a tratar de inicializar todas las clases [FabricTransientException][fte] y OperationCanceledException.
Cuando el comando de hello ha alcanzado un estado terminal (completado, error o cancelado), Hola devuelve propiedad del resultado del objeto de curso tendrá información adicional.  Si se ha completado el estado de hello, Result.SelectedPartition.PartitionId contendrá el Id. de partición de Hola que seleccionó.  El valor de Result.Exception será NULL.  Si se genera un error de estado de hello, Result.Exception tendrá Hola Hola de motivo inyección de código de error y error en el servicio Analysis Hola comando.  Result.SelectedPartition.PartitionId tendrá el Id. de partición de Hola que seleccionó.  En algunas situaciones, comando hello puede no ha realizado lo que sea necesario toochoose una partición.  En ese caso, Hola PartitionId será 0.  Si se cancela el estado de hello, Result.Exception será null.  Como caso Faulted de hello, Result.SelectedPartition.PartitionId tendrá Id. de partición de Hola que se ha elegido, pero si el comando de hello no se han realizado todo lo necesario toodo por lo tanto, será 0.  Consulte también toohello ejemplo siguiente.

Hola ejemplo de código siguiente muestra cómo toostart, a continuación, comprobar el progreso en una pérdida de datos de toocause de comando en una partición específica.

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

ejemplo de Hola siguiente muestra cómo toouse Hola PartitionSelector toochoose una partición aleatoria de un servicio especificado:

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

## <a name="history-and-truncation"></a>Historial y truncamiento
Después de que un comando ha alcanzado un estado terminal, sus metadatos permanecerán en hello inyección de código de error y Analysis Services para un momento determinado, para que pueda quitar espacio toosave.  Si se llama "GetProgress" con operationId Hola de un comando después de que se ha quitado, devolverá un FabricException con un código de error de KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
