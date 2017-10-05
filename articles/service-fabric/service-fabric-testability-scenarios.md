---
title: "Creación de pruebas de conmutación por error y caos para microservicios de Azure | Microsoft Docs"
description: "Uso de los escenarios de prueba de conmutación por error y pruebas de caos de Service Fabric para inducir acciones de error y comprobar la confiabilidad de los servicios."
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
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="000cb-103">Escenarios de Testability</span><span class="sxs-lookup"><span data-stu-id="000cb-103">Testability scenarios</span></span>
<span data-ttu-id="000cb-104">Los grandes sistemas distribuidos, como infraestructuras de nube, son inherentemente poco confiables.</span><span class="sxs-lookup"><span data-stu-id="000cb-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="000cb-105">Azure Service Fabric ofrece a los desarrolladores la capacidad de escribir servicios para ejecutarse sobre infraestructuras poco confiables.</span><span class="sxs-lookup"><span data-stu-id="000cb-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="000cb-106">Para poder escribir servicios de alta calidad, los desarrolladores deben poder inducir tal infraestructura confiable para probar la estabilidad de sus servicios.</span><span class="sxs-lookup"><span data-stu-id="000cb-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="000cb-107">El servicio de análisis de errores proporciona a los desarrolladores la capacidad de inducir acciones de error para probar los servicios en casos de mal funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="000cb-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="000cb-108">Sin embargo, hasta ahora se obtendrán solo errores simulados dirigidos.</span><span class="sxs-lookup"><span data-stu-id="000cb-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="000cb-109">Para realizar más pruebas, puede usar los escenarios de prueba en Service Fabric: una prueba de caos y una prueba de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="000cb-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="000cb-110">Estos escenarios simulan errores continuos intercalados, tanto correctos como incorrectos, en todo el clúster durante períodos prolongados de tiempo.</span><span class="sxs-lookup"><span data-stu-id="000cb-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="000cb-111">Una vez configurada una prueba con la tasa y el tipo de errores, se puede iniciar mediante las API de C# o de PowerShell para generar errores en el clúster y en el servicio.</span><span class="sxs-lookup"><span data-stu-id="000cb-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="000cb-112">ChaosTestScenario va a reemplazarse por una versión de Caos más resistente y basado en servicios.</span><span class="sxs-lookup"><span data-stu-id="000cb-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="000cb-113">Consulte el artículo nuevo sobre [inducción de errores controlados con Caos](service-fabric-controlled-chaos.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="000cb-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="000cb-114">Prueba de caos</span><span class="sxs-lookup"><span data-stu-id="000cb-114">Chaos test</span></span>
<span data-ttu-id="000cb-115">El escenario de caos genera errores en todo el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="000cb-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="000cb-116">El escenario comprime los errores que se ven por lo general durante meses o años en unas pocas horas.</span><span class="sxs-lookup"><span data-stu-id="000cb-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="000cb-117">Esta combinación de errores intercalados con una elevada tasa de errores encuentra casos excepcionales que de otra manera pasan desapercibidos.</span><span class="sxs-lookup"><span data-stu-id="000cb-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="000cb-118">Esto conduce a una mejora considerable en la calidad del código del servicio.</span><span class="sxs-lookup"><span data-stu-id="000cb-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="000cb-119">Errores simulados en la prueba de caos</span><span class="sxs-lookup"><span data-stu-id="000cb-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="000cb-120">Reinicio de un nodo</span><span class="sxs-lookup"><span data-stu-id="000cb-120">Restart a node</span></span>
* <span data-ttu-id="000cb-121">Reinicio de un paquete de código implementado</span><span class="sxs-lookup"><span data-stu-id="000cb-121">Restart a deployed code package</span></span>
* <span data-ttu-id="000cb-122">Eliminación de una réplica</span><span class="sxs-lookup"><span data-stu-id="000cb-122">Remove a replica</span></span>
* <span data-ttu-id="000cb-123">Reinicio de una réplica</span><span class="sxs-lookup"><span data-stu-id="000cb-123">Restart a replica</span></span>
* <span data-ttu-id="000cb-124">Desplazamiento de una réplica principal (opcional)</span><span class="sxs-lookup"><span data-stu-id="000cb-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="000cb-125">Desplazamiento de una réplica secundaria (opcional)</span><span class="sxs-lookup"><span data-stu-id="000cb-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="000cb-126">La prueba de caos ejecuta varias iteraciones de errores y las validaciones de clúster para el período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="000cb-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="000cb-127">También se puede configurar el tiempo empleado por el clúster para que la estabilización y la validación sean correctas.</span><span class="sxs-lookup"><span data-stu-id="000cb-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="000cb-128">Se produce un error en el escenario cuando se encuentra un error en la validación del clúster.</span><span class="sxs-lookup"><span data-stu-id="000cb-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="000cb-129">Por ejemplo, considere un conjunto de pruebas que se va a ejecutar durante una hora con un máximo de tres errores simultáneos.</span><span class="sxs-lookup"><span data-stu-id="000cb-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="000cb-130">La prueba inducirá tres errores y después validará el mantenimiento del clúster.</span><span class="sxs-lookup"><span data-stu-id="000cb-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="000cb-131">La prueba recorrerá en iteración el paso anterior hasta que el clúster pase a ser incorrecto o transcurra una hora.</span><span class="sxs-lookup"><span data-stu-id="000cb-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="000cb-132">Si el clúster pasa a ser incorrecto en cualquier iteración, es decir, no se estabiliza dentro de un tiempo configurado, la prueba producirá un error con una excepción.</span><span class="sxs-lookup"><span data-stu-id="000cb-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="000cb-133">Esta excepción indica que algo salió mal y que se necesita más investigación.</span><span class="sxs-lookup"><span data-stu-id="000cb-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="000cb-134">En su forma actual, el motor de generación de errores de la prueba de caos induce solo errores seguros.</span><span class="sxs-lookup"><span data-stu-id="000cb-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="000cb-135">Esto significa que en ausencia de errores externos nunca se producirá una pérdida de quórum o de datos.</span><span class="sxs-lookup"><span data-stu-id="000cb-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="000cb-136">Opciones de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="000cb-136">Important configuration options</span></span>
* <span data-ttu-id="000cb-137">**TimeToRun**: tiempo total en el que se ejecutará la prueba antes de finalizarse con éxito.</span><span class="sxs-lookup"><span data-stu-id="000cb-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="000cb-138">La prueba puede finalizarse antes en lugar de un error de validación.</span><span class="sxs-lookup"><span data-stu-id="000cb-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="000cb-139">**MaxClusterStabilizationTimeout**: cantidad máxima de tiempo de espera para que el mantenimiento del clúster sea correcto antes de cancelar la prueba.</span><span class="sxs-lookup"><span data-stu-id="000cb-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="000cb-140">Las comprobaciones realizadas son si el mantenimiento del clúster es correcto, el mantenimiento del servicio es correcto, se consigue el tamaño del conjunto de réplicas de destino para la partición de servicio y si no hay réplicas InBuild.</span><span class="sxs-lookup"><span data-stu-id="000cb-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="000cb-141">**MaxConcurrentFaults**: número máximo de errores simultáneos inducidos en cada iteración.</span><span class="sxs-lookup"><span data-stu-id="000cb-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="000cb-142">Cuanto mayor sea el número, más agresiva será la prueba. Por lo tanto, dará como resultado combinaciones de conmutaciones por error y de transición más complejas.</span><span class="sxs-lookup"><span data-stu-id="000cb-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="000cb-143">La prueba garantiza que en ausencia de errores externos no habrá pérdida de quórum o de datos, con independencia de lo elevado del número de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="000cb-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="000cb-144">**EnableMoveReplicaFaults**: habilita o deshabilita los errores provocando el movimiento de las réplicas principales o secundarias.</span><span class="sxs-lookup"><span data-stu-id="000cb-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="000cb-145">Estos errores están deshabilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="000cb-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="000cb-146">**WaitTimeBetweenIterations**: cantidad de tiempo de espera entre iteraciones, es decir, después de una ronda de errores y de su validación correspondiente.</span><span class="sxs-lookup"><span data-stu-id="000cb-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="000cb-147">Ejecución de una prueba de caos</span><span class="sxs-lookup"><span data-stu-id="000cb-147">How to run the chaos test</span></span>
<span data-ttu-id="000cb-148">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="000cb-148">C# sample</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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

<span data-ttu-id="000cb-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="000cb-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="000cb-150">Prueba de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="000cb-150">Failover test</span></span>
<span data-ttu-id="000cb-151">El escenario de prueba de conmutación por error es una versión del escenario de prueba de caos dirigida a una partición de servicio específica.</span><span class="sxs-lookup"><span data-stu-id="000cb-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="000cb-152">Comprueba el efecto de la conmutación por error en una partición de servicio específica al mismo tiempo que deja sin afectar los otros servicios.</span><span class="sxs-lookup"><span data-stu-id="000cb-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="000cb-153">Una vez configurada con la información de la partición de destino y otros parámetros, se ejecuta como una herramienta de cliente mediante las API de C# o PowerShell para generar errores para una partición de servicio.</span><span class="sxs-lookup"><span data-stu-id="000cb-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="000cb-154">El escenario se itera por una secuencia de errores simulados y una validación de servicio mientras la lógica de negocios se ejecuta en paralelo para proporcionar una carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="000cb-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="000cb-155">Un error en la validación de servicio indica un problema que necesita más investigación.</span><span class="sxs-lookup"><span data-stu-id="000cb-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="000cb-156">Errores simulados en la prueba de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="000cb-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="000cb-157">Reinicio de un paquete de código implementado donde se hospeda la partición</span><span class="sxs-lookup"><span data-stu-id="000cb-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="000cb-158">Eliminación de una instancia sin estado o de una réplica principal/secundaria</span><span class="sxs-lookup"><span data-stu-id="000cb-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="000cb-159">Reinicio de una réplica principal/secundaria (si se conserva el servicio)</span><span class="sxs-lookup"><span data-stu-id="000cb-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="000cb-160">Desplazamiento de una réplica principal</span><span class="sxs-lookup"><span data-stu-id="000cb-160">Move a primary replica</span></span>
* <span data-ttu-id="000cb-161">Desplazamiento de una réplica secundaria</span><span class="sxs-lookup"><span data-stu-id="000cb-161">Move a secondary replica</span></span>
* <span data-ttu-id="000cb-162">Reinicio de la partición</span><span class="sxs-lookup"><span data-stu-id="000cb-162">Restart the partition</span></span>

<span data-ttu-id="000cb-163">La prueba de conmutación por error provoca un error seleccionado y después ejecuta la validación en el servicio para garantizar su estabilidad.</span><span class="sxs-lookup"><span data-stu-id="000cb-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="000cb-164">La prueba de conmutación por error solo provoca un error a la ver en lugar de varios errores posibles en la prueba de caos.</span><span class="sxs-lookup"><span data-stu-id="000cb-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="000cb-165">Si la partición de servicio no se estabiliza en el tiempo de espera configurado después del error, la prueba produce un error.</span><span class="sxs-lookup"><span data-stu-id="000cb-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="000cb-166">La prueba provoca únicamente errores seguros.</span><span class="sxs-lookup"><span data-stu-id="000cb-166">The test induces only safe faults.</span></span> <span data-ttu-id="000cb-167">Esto significa que, en ausencia de errores externos, nunca se producirá una pérdida de quórum o de datos.</span><span class="sxs-lookup"><span data-stu-id="000cb-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="000cb-168">Opciones de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="000cb-168">Important configuration options</span></span>
* <span data-ttu-id="000cb-169">**PartitionSelector**: objeto selector que especifica la partición a la que debe dirigirse.</span><span class="sxs-lookup"><span data-stu-id="000cb-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="000cb-170">**TimeToRun**: tiempo total en el que se ejecutará la prueba antes de finalizarse.</span><span class="sxs-lookup"><span data-stu-id="000cb-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="000cb-171">**MaxClusterStabilizationTimeout**: cantidad máxima de tiempo de espera para que el mantenimiento del clúster sea correcto antes que la prueba produzca un error.</span><span class="sxs-lookup"><span data-stu-id="000cb-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="000cb-172">Las comprobaciones realizadas son si el mantenimiento del servicio es correcto, el tamaño del conjunto de réplicas de destino conseguido para todas las particiones y si no hay réplicas InBuild.</span><span class="sxs-lookup"><span data-stu-id="000cb-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="000cb-173">**WaitTimeBetweenFaults**: cantidad de tiempo de espera entre cada ciclo de error y validación.</span><span class="sxs-lookup"><span data-stu-id="000cb-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="000cb-174">Ejecución de la prueba de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="000cb-174">How to run the failover test</span></span>
<span data-ttu-id="000cb-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="000cb-175">**C#**</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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


<span data-ttu-id="000cb-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="000cb-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
