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
# <a name="testability-scenarios"></a><span data-ttu-id="fd97d-103">Escenarios de Testability</span><span class="sxs-lookup"><span data-stu-id="fd97d-103">Testability scenarios</span></span>
<span data-ttu-id="fd97d-104">Los grandes sistemas distribuidos, como infraestructuras de nube, son inherentemente poco confiables.</span><span class="sxs-lookup"><span data-stu-id="fd97d-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="fd97d-105">Azure Service Fabric proporciona a los desarrolladores Hola capacidad toowrite services toorun encima de infraestructuras no confiables.</span><span class="sxs-lookup"><span data-stu-id="fd97d-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="fd97d-106">En servicios de alta calidad de orden toowrite, los desarrolladores necesitan toobe pueda tooinduce estabilidad de hello tal tootest confiable de infraestructura de sus servicios.</span><span class="sxs-lookup"><span data-stu-id="fd97d-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="fd97d-107">Hola error Analysis Services proporciona a los desarrolladores servicios de tootest de acciones de error de hello capacidad tooinduce en presencia de Hola de errores.</span><span class="sxs-lookup"><span data-stu-id="fd97d-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="fd97d-108">Sin embargo, hasta ahora se obtendrán solo errores simulados dirigidos.</span><span class="sxs-lookup"><span data-stu-id="fd97d-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="fd97d-109">Hola tootake pruebas además, puede utilizar los escenarios de prueba de hello en Service Fabric: una prueba de caos y una prueba de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="fd97d-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="fd97d-110">Estos escenarios simulan continuos errores intercalados, estable e incorrectas, a lo largo de clúster de Hola durante períodos ampliados de tiempo.</span><span class="sxs-lookup"><span data-stu-id="fd97d-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="fd97d-111">Una vez configurada una prueba con velocidad de Hola y el tipo de errores, que se puede iniciar a través de las API de C# o PowerShell, toogenerate errores en el clúster de Hola y el servicio.</span><span class="sxs-lookup"><span data-stu-id="fd97d-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="fd97d-112">ChaosTestScenario va a reemplazarse por una versión de Caos más resistente y basado en servicios.</span><span class="sxs-lookup"><span data-stu-id="fd97d-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="fd97d-113">Consulte toohello nuevo artículo [controla Chaos](service-fabric-controlled-chaos.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="fd97d-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="fd97d-114">Prueba de caos</span><span class="sxs-lookup"><span data-stu-id="fd97d-114">Chaos test</span></span>
<span data-ttu-id="fd97d-115">escenario de caos Hola genera errores en el clúster de Service Fabric todo Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="fd97d-116">escenario de Hello comprime los errores suelen aparecer en tooa meses o años pocas horas.</span><span class="sxs-lookup"><span data-stu-id="fd97d-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="fd97d-117">combinación de Hola de errores intercalados con velocidad de errores alta de hello busca casos más complejos que en caso contrario, se omiten.</span><span class="sxs-lookup"><span data-stu-id="fd97d-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="fd97d-118">Esto conduce tooa significativa mejora en la calidad del código del servicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="fd97d-119">Errores de simular en pruebas de caos Hola</span><span class="sxs-lookup"><span data-stu-id="fd97d-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="fd97d-120">Reinicio de un nodo</span><span class="sxs-lookup"><span data-stu-id="fd97d-120">Restart a node</span></span>
* <span data-ttu-id="fd97d-121">Reinicio de un paquete de código implementado</span><span class="sxs-lookup"><span data-stu-id="fd97d-121">Restart a deployed code package</span></span>
* <span data-ttu-id="fd97d-122">Eliminación de una réplica</span><span class="sxs-lookup"><span data-stu-id="fd97d-122">Remove a replica</span></span>
* <span data-ttu-id="fd97d-123">Reinicio de una réplica</span><span class="sxs-lookup"><span data-stu-id="fd97d-123">Restart a replica</span></span>
* <span data-ttu-id="fd97d-124">Desplazamiento de una réplica principal (opcional)</span><span class="sxs-lookup"><span data-stu-id="fd97d-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="fd97d-125">Desplazamiento de una réplica secundaria (opcional)</span><span class="sxs-lookup"><span data-stu-id="fd97d-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="fd97d-126">prueba de caos Hola ejecuta varias iteraciones de errores y validaciones de clúster para hello período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="fd97d-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="fd97d-127">tiempo de Hola de toostabilize de clúster de Hola y de validación toosucceed también es configurable.</span><span class="sxs-lookup"><span data-stu-id="fd97d-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="fd97d-128">escenario de Hello produce un error cuando se produce un error en la validación de clúster único.</span><span class="sxs-lookup"><span data-stu-id="fd97d-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="fd97d-129">Por ejemplo, considere la posibilidad de que una prueba establecido toorun durante una hora con un máximo de tres errores simultáneos.</span><span class="sxs-lookup"><span data-stu-id="fd97d-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="fd97d-130">prueba de Hello inducir tres errores y, a continuación, validar el estado del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="fd97d-131">prueba de Hello iterará paso anterior Hola hasta que el clúster de hello pasa a ser incorrecto o pasa de una hora.</span><span class="sxs-lookup"><span data-stu-id="fd97d-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="fd97d-132">Si clúster Hola pasa a ser incorrecto en toda iteración, es decir, no estabilizar dentro de un tiempo configurado, se producirá un error de prueba de hello con una excepción.</span><span class="sxs-lookup"><span data-stu-id="fd97d-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="fd97d-133">Esta excepción indica que algo salió mal y que se necesita más investigación.</span><span class="sxs-lookup"><span data-stu-id="fd97d-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="fd97d-134">En su forma actual, motor de generación de errores de hello en pruebas de caos Hola induce a errores solo seguros.</span><span class="sxs-lookup"><span data-stu-id="fd97d-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="fd97d-135">Esto significa que en ausencia de Hola de errores externos, una quórum o pérdida de datos nunca se producirá.</span><span class="sxs-lookup"><span data-stu-id="fd97d-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="fd97d-136">Opciones de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="fd97d-136">Important configuration options</span></span>
* <span data-ttu-id="fd97d-137">**TimeToRun**: Total de tiempo de esa prueba Hola se ejecutará antes de finalizar con éxito.</span><span class="sxs-lookup"><span data-stu-id="fd97d-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="fd97d-138">puede finalizar la prueba de Hello anteriormente en lugar de un error de validación.</span><span class="sxs-lookup"><span data-stu-id="fd97d-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="fd97d-139">**MaxClusterStabilizationTimeout**: cantidad máxima de tiempo toowait para hello clúster toobecome correcto antes de cancelar la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="fd97d-140">Hello comprobaciones realizadas son si el estado de clúster es correcto, el estado de servicio es correcto, tamaño del conjunto de réplica de destino hello se logra una para la partición de servicio de hello y no hay réplicas InBuild existen.</span><span class="sxs-lookup"><span data-stu-id="fd97d-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="fd97d-141">**MaxConcurrentFaults**: número máximo de errores simultáneos inducidos en cada iteración.</span><span class="sxs-lookup"><span data-stu-id="fd97d-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="fd97d-142">Hola mayor número de hello, Hola más agresiva prueba hello, por lo tanto, que han generado las conmutaciones por error más complejas y combinaciones de transición.</span><span class="sxs-lookup"><span data-stu-id="fd97d-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="fd97d-143">prueba de Hello garantiza que en ausencia de errores externos no habrá una quórum o pérdida de datos, con independencia de cómo alto esta configuración.</span><span class="sxs-lookup"><span data-stu-id="fd97d-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="fd97d-144">**EnableMoveReplicaFaults**: habilita o deshabilita los errores de Hola que están causando el movimiento de Hola de hello réplicas principal o secundaria.</span><span class="sxs-lookup"><span data-stu-id="fd97d-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="fd97d-145">Estos errores están deshabilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fd97d-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="fd97d-146">**WaitTimeBetweenIterations**: cantidad de tiempo toowait entre iteraciones, es decir, después de un ciclo de errores y la validación correspondiente.</span><span class="sxs-lookup"><span data-stu-id="fd97d-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="fd97d-147">Cómo probar el caos de hello toorun</span><span class="sxs-lookup"><span data-stu-id="fd97d-147">How toorun hello chaos test</span></span>
<span data-ttu-id="fd97d-148">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="fd97d-148">C# sample</span></span>

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

<span data-ttu-id="fd97d-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd97d-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="fd97d-150">Prueba de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="fd97d-150">Failover test</span></span>
<span data-ttu-id="fd97d-151">escenario de prueba de conmutación por error de Hello es una versión de escenario de prueba de caos Hola destinado a una partición de servicio específico.</span><span class="sxs-lookup"><span data-stu-id="fd97d-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="fd97d-152">Comprueba que efecto Hola de conmutación por error en una partición de servicio específico al Hola otros servicios no se ve afectada.</span><span class="sxs-lookup"><span data-stu-id="fd97d-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="fd97d-153">Una vez que está configurado con la información de partición de destino de Hola y otros parámetros, se ejecuta como una herramienta de cliente que usa las API de C# o PowerShell errores toogenerate para una partición de servicio.</span><span class="sxs-lookup"><span data-stu-id="fd97d-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="fd97d-154">escenario de Hello procesa una iteración a través de una secuencia de errores simulados y la validación de servicio mientras ejecuta la lógica de negocios en hello lado tooprovide una carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fd97d-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="fd97d-155">Un error en la validación de servicio indica un problema que necesita más investigación.</span><span class="sxs-lookup"><span data-stu-id="fd97d-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="fd97d-156">Errores de simular en prueba de conmutación por error de Hola</span><span class="sxs-lookup"><span data-stu-id="fd97d-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="fd97d-157">Reiniciar un paquete de código implementado donde se hospeda la partición de Hola</span><span class="sxs-lookup"><span data-stu-id="fd97d-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="fd97d-158">Eliminación de una instancia sin estado o de una réplica principal/secundaria</span><span class="sxs-lookup"><span data-stu-id="fd97d-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="fd97d-159">Reinicio de una réplica principal/secundaria (si se conserva el servicio)</span><span class="sxs-lookup"><span data-stu-id="fd97d-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="fd97d-160">Desplazamiento de una réplica principal</span><span class="sxs-lookup"><span data-stu-id="fd97d-160">Move a primary replica</span></span>
* <span data-ttu-id="fd97d-161">Desplazamiento de una réplica secundaria</span><span class="sxs-lookup"><span data-stu-id="fd97d-161">Move a secondary replica</span></span>
* <span data-ttu-id="fd97d-162">Reinicie la partición de Hola</span><span class="sxs-lookup"><span data-stu-id="fd97d-162">Restart hello partition</span></span>

<span data-ttu-id="fd97d-163">prueba de conmutación por error de Hello induce a un error seleccionado y, a continuación, ejecuta la validación en hello servicio tooensure su estabilidad.</span><span class="sxs-lookup"><span data-stu-id="fd97d-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="fd97d-164">prueba de conmutación por error de Hello induce a solo uno de error en un tiempo, a diferencia toopossible varios errores de prueba de caos Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="fd97d-165">Si la partición de servicio de hello estabilizar no en tiempo de espera de hello configurado después de cada error, se produce un error en la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="fd97d-166">prueba de Hello induce a solo los errores de prueba de errores.</span><span class="sxs-lookup"><span data-stu-id="fd97d-166">hello test induces only safe faults.</span></span> <span data-ttu-id="fd97d-167">Esto significa que, en ausencia de errores externos, nunca se producirá una pérdida de quórum o de datos.</span><span class="sxs-lookup"><span data-stu-id="fd97d-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="fd97d-168">Opciones de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="fd97d-168">Important configuration options</span></span>
* <span data-ttu-id="fd97d-169">**PartitionSelector**: objeto de Selector que especifica la partición de Hola que necesita toobe de destino.</span><span class="sxs-lookup"><span data-stu-id="fd97d-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="fd97d-170">**TimeToRun**: Total de tiempo de esa prueba Hola se ejecutará antes de finalizar.</span><span class="sxs-lookup"><span data-stu-id="fd97d-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="fd97d-171">**MaxServiceStabilizationTimeout**: cantidad máxima de tiempo toowait para hello clúster toobecome correcto antes de cancelar la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd97d-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="fd97d-172">Hello comprobaciones realizadas son si estado del servicio es correcto, tamaño del conjunto de réplica de destino hello se logra una para todas las particiones y no hay réplicas InBuild existen.</span><span class="sxs-lookup"><span data-stu-id="fd97d-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="fd97d-173">**WaitTimeBetweenFaults**: cantidad de tiempo toowait entre cada ciclo de error y validación.</span><span class="sxs-lookup"><span data-stu-id="fd97d-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="fd97d-174">Cómo probar la conmutación por error de toorun Hola</span><span class="sxs-lookup"><span data-stu-id="fd97d-174">How toorun hello failover test</span></span>
<span data-ttu-id="fd97d-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="fd97d-175">**C#**</span></span>

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


<span data-ttu-id="fd97d-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fd97d-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
