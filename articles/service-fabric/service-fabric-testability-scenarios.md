---
title: "pruebas de caos y conmutación por error de aaaCreate para microservicios Azure | Documentos de Microsoft"
description: "Con conmutación por error y prueba de hello Service Fabric chaos errores tooinduce de escenarios de prueba y comprobar la confiabilidad de Hola de los servicios."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a>Escenarios de Testability
Los grandes sistemas distribuidos, como infraestructuras de nube, son inherentemente poco confiables. Azure Service Fabric proporciona a los desarrolladores Hola capacidad toowrite services toorun encima de infraestructuras no confiables. En servicios de alta calidad de orden toowrite, los desarrolladores necesitan toobe pueda tooinduce estabilidad de hello tal tootest confiable de infraestructura de sus servicios.

Hola error Analysis Services proporciona a los desarrolladores servicios de tootest de acciones de error de hello capacidad tooinduce en presencia de Hola de errores. Sin embargo, hasta ahora se obtendrán solo errores simulados dirigidos. Hola tootake pruebas además, puede utilizar los escenarios de prueba de hello en Service Fabric: una prueba de caos y una prueba de conmutación por error. Estos escenarios simulan continuos errores intercalados, estable e incorrectas, a lo largo de clúster de Hola durante períodos ampliados de tiempo. Una vez configurada una prueba con velocidad de Hola y el tipo de errores, que se puede iniciar a través de las API de C# o PowerShell, toogenerate errores en el clúster de Hola y el servicio.

> [!WARNING]
> ChaosTestScenario va a reemplazarse por una versión de Caos más resistente y basado en servicios. Consulte toohello nuevo artículo [controla Chaos](service-fabric-controlled-chaos.md) para obtener más detalles.
> 
> 

## <a name="chaos-test"></a>Prueba de caos
escenario de caos Hola genera errores en el clúster de Service Fabric todo Hola. escenario de Hello comprime los errores suelen aparecer en tooa meses o años pocas horas. combinación de Hola de errores intercalados con velocidad de errores alta de hello busca casos más complejos que en caso contrario, se omiten. Esto conduce tooa significativa mejora en la calidad del código del servicio de Hola Hola.

### <a name="faults-simulated-in-hello-chaos-test"></a>Errores de simular en pruebas de caos Hola
* Reinicio de un nodo
* Reinicio de un paquete de código implementado
* Eliminación de una réplica
* Reinicio de una réplica
* Desplazamiento de una réplica principal (opcional)
* Desplazamiento de una réplica secundaria (opcional)

prueba de caos Hola ejecuta varias iteraciones de errores y validaciones de clúster para hello período de tiempo especificado. tiempo de Hola de toostabilize de clúster de Hola y de validación toosucceed también es configurable. escenario de Hello produce un error cuando se produce un error en la validación de clúster único.

Por ejemplo, considere la posibilidad de que una prueba establecido toorun durante una hora con un máximo de tres errores simultáneos. prueba de Hello inducir tres errores y, a continuación, validar el estado del clúster Hola. prueba de Hello iterará paso anterior Hola hasta que el clúster de hello pasa a ser incorrecto o pasa de una hora. Si clúster Hola pasa a ser incorrecto en toda iteración, es decir, no estabilizar dentro de un tiempo configurado, se producirá un error de prueba de hello con una excepción. Esta excepción indica que algo salió mal y que se necesita más investigación.

En su forma actual, motor de generación de errores de hello en pruebas de caos Hola induce a errores solo seguros. Esto significa que en ausencia de Hola de errores externos, una quórum o pérdida de datos nunca se producirá.

### <a name="important-configuration-options"></a>Opciones de configuración importantes
* **TimeToRun**: Total de tiempo de esa prueba Hola se ejecutará antes de finalizar con éxito. puede finalizar la prueba de Hello anteriormente en lugar de un error de validación.
* **MaxClusterStabilizationTimeout**: cantidad máxima de tiempo toowait para hello clúster toobecome correcto antes de cancelar la prueba de Hola. Hello comprobaciones realizadas son si el estado de clúster es correcto, el estado de servicio es correcto, tamaño del conjunto de réplica de destino hello se logra una para la partición de servicio de hello y no hay réplicas InBuild existen.
* **MaxConcurrentFaults**: número máximo de errores simultáneos inducidos en cada iteración. Hola mayor número de hello, Hola más agresiva prueba hello, por lo tanto, que han generado las conmutaciones por error más complejas y combinaciones de transición. prueba de Hello garantiza que en ausencia de errores externos no habrá una quórum o pérdida de datos, con independencia de cómo alto esta configuración.
* **EnableMoveReplicaFaults**: habilita o deshabilita los errores de Hola que están causando el movimiento de Hola de hello réplicas principal o secundaria. Estos errores están deshabilitados de forma predeterminada.
* **WaitTimeBetweenIterations**: cantidad de tiempo toowait entre iteraciones, es decir, después de un ciclo de errores y la validación correspondiente.

### <a name="how-toorun-hello-chaos-test"></a>Cómo probar el caos de hello toorun
Ejemplo de C#

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Prueba de conmutación por error
escenario de prueba de conmutación por error de Hello es una versión de escenario de prueba de caos Hola destinado a una partición de servicio específico. Comprueba que efecto Hola de conmutación por error en una partición de servicio específico al Hola otros servicios no se ve afectada. Una vez que está configurado con la información de partición de destino de Hola y otros parámetros, se ejecuta como una herramienta de cliente que usa las API de C# o PowerShell errores toogenerate para una partición de servicio. escenario de Hello procesa una iteración a través de una secuencia de errores simulados y la validación de servicio mientras ejecuta la lógica de negocios en hello lado tooprovide una carga de trabajo. Un error en la validación de servicio indica un problema que necesita más investigación.

### <a name="faults-simulated-in-hello-failover-test"></a>Errores de simular en prueba de conmutación por error de Hola
* Reiniciar un paquete de código implementado donde se hospeda la partición de Hola
* Eliminación de una instancia sin estado o de una réplica principal/secundaria
* Reinicio de una réplica principal/secundaria (si se conserva el servicio)
* Desplazamiento de una réplica principal
* Desplazamiento de una réplica secundaria
* Reinicie la partición de Hola

prueba de conmutación por error de Hello induce a un error seleccionado y, a continuación, ejecuta la validación en hello servicio tooensure su estabilidad. prueba de conmutación por error de Hello induce a solo uno de error en un tiempo, a diferencia toopossible varios errores de prueba de caos Hola. Si la partición de servicio de hello estabilizar no en tiempo de espera de hello configurado después de cada error, se produce un error en la prueba de Hola. prueba de Hello induce a solo los errores de prueba de errores. Esto significa que, en ausencia de errores externos, nunca se producirá una pérdida de quórum o de datos.

### <a name="important-configuration-options"></a>Opciones de configuración importantes
* **PartitionSelector**: objeto de Selector que especifica la partición de Hola que necesita toobe de destino.
* **TimeToRun**: Total de tiempo de esa prueba Hola se ejecutará antes de finalizar.
* **MaxServiceStabilizationTimeout**: cantidad máxima de tiempo toowait para hello clúster toobecome correcto antes de cancelar la prueba de Hola. Hello comprobaciones realizadas son si estado del servicio es correcto, tamaño del conjunto de réplica de destino hello se logra una para todas las particiones y no hay réplicas InBuild existen.
* **WaitTimeBetweenFaults**: cantidad de tiempo toowait entre cada ciclo de error y validación.

### <a name="how-toorun-hello-failover-test"></a>Cómo probar la conmutación por error de toorun Hola
**C#**

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
