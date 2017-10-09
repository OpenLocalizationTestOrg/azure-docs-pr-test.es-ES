---
title: "clústeres de caos en Service Fabric aaaInduce | Documentos de Microsoft"
description: "Uso de inyección de código de error y las API de servicios de análisis de clúster toomanage caos en clúster de Hola."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="3bd0b-103">Inducción de errores controlados con Caos en clústeres de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3bd0b-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="3bd0b-104">Los sistemas distribuidos a gran escala, como las infraestructuras en la nube, por naturaleza, no son confiables.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="3bd0b-105">Azure Service Fabric permite servicios distribuidos de los desarrolladores toowrite confiable encima de una infraestructura no confiable.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="3bd0b-106">toowrite sólida servicios distribuidos por encima de una infraestructura no confiable, los desarrolladores necesitan toobe estabilidad de hello tootest capaz de sus servicios mientras Hola confiable infraestructura subyacente está pasando por las transiciones de estado complicado toofaults due.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="3bd0b-107">Hola [por inyección de código de error y el servicio de Cluster Server Analysis](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (también conocido como Hola error Analysis Services) permite a los desarrolladores hello tooinduce errores tootest sus servicios.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="3bd0b-108">Estos destino simulación errores, como [reiniciar una partición](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), puede ayudar a ejercer las transiciones de estado más común de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="3bd0b-109">Sin embargo, los errores simulados de destino están sesgados por definición y, por consiguiente, pueden perder errores que se muestran solo en una secuencia de transiciones de estado larga, complicada y difícil de predecir.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="3bd0b-110">Para una prueba no sesgada, se puede usar Chaos.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="3bd0b-111">Caos simulan periódicos, intercalados errores (estable e incorrectas) a lo largo de clúster de Hola durante períodos ampliados de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="3bd0b-112">Una vez haya configurado el caos con velocidad de Hola y tipo de Hola de errores, puede iniciar Chaos mediante C# o Powershell API toostart generar errores en clúster de Hola y en los servicios.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="3bd0b-113">Puede configurar Chaos toorun durante un período de tiempo especificado (por ejemplo, para una hora), después del cual el caos se detiene automáticamente, o puede llamar a toostop StopChaos API (C# o Powershell) en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="3bd0b-114">En su forma actual, Chaos induce errores solo seguros, lo que implica que en ausencia de Hola de errores externos una pérdida de quórum, o la pérdida de datos nunca se produce.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="3bd0b-115">Mientras se ejecuta Chaos, genera eventos diferentes que capturan el estado de Hola de hello ejecutar en el momento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="3bd0b-116">Por ejemplo, un ExecutingFaultsEvent contiene todos los errores de Hola que Chaos ha decidido tooexecute en esa iteración.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="3bd0b-117">Un ValidationFailedEvent contiene los detalles de Hola de un error de validación (problemas de estabilidad o de mantenimiento) que se ha encontrado durante la validación de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="3bd0b-118">Puede invocar el informe de hello GetChaosReport API (C# o Powershell) tooget Hola de ejecuciones de caos.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="3bd0b-119">Estos eventos se guardan en un [diccionario confiable](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), que tiene una directiva de truncamiento dictada por dos configuraciones: **MaxStoredChaosEventCount** (el valor predeterminado es 25 000) y **StoredActionCleanupIntervalInSeconds** (el valor predeterminado es 3600).</span><span class="sxs-lookup"><span data-stu-id="3bd0b-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="3bd0b-120">Cada *StoredActionCleanupIntervalInSeconds* comprobaciones de caos y todos pero Hola más reciente *MaxStoredChaosEventCount* eventos, se purgan de diccionario de hello confiable.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="3bd0b-121">Errores inducidos en Caos</span><span class="sxs-lookup"><span data-stu-id="3bd0b-121">Faults induced in Chaos</span></span>
<span data-ttu-id="3bd0b-122">Caos genera errores en el clúster de Service Fabric todo hello y comprimen los errores que se ven en meses o años en unas pocas horas.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="3bd0b-123">combinación de Hola de errores intercalados con velocidad de errores alta de hello busca casos más complejos que pueden faltar en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="3bd0b-124">Este ejercicio de caos produce tooa significativa mejora en la calidad del código del servicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="3bd0b-125">Caos induce a errores de hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="3bd0b-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="3bd0b-126">Reinicio de un nodo</span><span class="sxs-lookup"><span data-stu-id="3bd0b-126">Restart a node</span></span>
* <span data-ttu-id="3bd0b-127">Reinicio de un paquete de código implementado</span><span class="sxs-lookup"><span data-stu-id="3bd0b-127">Restart a deployed code package</span></span>
* <span data-ttu-id="3bd0b-128">Eliminación de una réplica</span><span class="sxs-lookup"><span data-stu-id="3bd0b-128">Remove a replica</span></span>
* <span data-ttu-id="3bd0b-129">Reinicio de una réplica</span><span class="sxs-lookup"><span data-stu-id="3bd0b-129">Restart a replica</span></span>
* <span data-ttu-id="3bd0b-130">Desplazamiento de una réplica principal (configurable)</span><span class="sxs-lookup"><span data-stu-id="3bd0b-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="3bd0b-131">Desplazamiento de una réplica secundaria (configurable)</span><span class="sxs-lookup"><span data-stu-id="3bd0b-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="3bd0b-132">Caos se ejecuta en varias iteraciones.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="3bd0b-133">Cada iteración se compone de los errores y validación de clúster para hello período especificado.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="3bd0b-134">Puede configurar tiempo de hello empleado para hello clúster toostabilize y toosucceed de validación.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="3bd0b-135">Si se encuentra un error en la validación de clúster, Chaos genera y continúa una ValidationFailedEvent con marca de tiempo de UTC de Hola y detalles del error Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="3bd0b-136">Por ejemplo, considere la posibilidad de una instancia de caos establecido toorun durante una hora con un máximo de tres errores simultáneos.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="3bd0b-137">Caos induce a tres errores y, a continuación, valida el estado del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="3bd0b-138">Se recorre en iteración Hola anterior pasa paso hasta que esté explícitamente detenido a través de hello StopChaosAsync API o una hora.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="3bd0b-139">Si el clúster de hello pasa a ser incorrecto en toda iteración (es decir, no se estabilizan dentro de hello pasado en MaxClusterStabilizationTimeout), Chaos genera un ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="3bd0b-140">Este evento indica que algo salió mal y que podría necesitar más investigación.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="3bd0b-141">tooget que Chaos inducido produce un error, puede usar la API de GetChaosReport (powershell o C#).</span><span class="sxs-lookup"><span data-stu-id="3bd0b-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="3bd0b-142">Hola API Obtiene el siguiente segmento de Hola de hello Chaos informe basada en token de continuación pasada de Hola u Hola pasado en el tiempo de intervalo.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="3bd0b-143">Puede especificar Hola segmento siguiente Hola de ContinuationToken tooget de informe de caos Hola o puede especificar el intervalo de tiempo de Hola a través de StartTimeUtc y EndTimeUtc, pero no se puede especificar hello ContinuationToken y el intervalo de tiempo de Hola Hola misma llamada.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="3bd0b-144">Cuando hay más de 100 eventos Chaos, Hola informe caos se devuelve en segmentos donde un segmento contiene ya no más de 100 eventos de caos.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="3bd0b-145">Opciones de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="3bd0b-145">Important configuration options</span></span>
* <span data-ttu-id="3bd0b-146">**TimeToRun**: Tiempo total durante el cual se ejecutará Caos antes de finalice correctamente.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="3bd0b-147">Puede detener Chaos antes de que se ejecute para el período de hello TimeToRun a través de hello StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="3bd0b-148">**MaxClusterStabilizationTimeout**: cantidad máxima de Hola de toowait de tiempo para hello clúster toobecome correcto antes de generar un ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="3bd0b-149">Esta espera es tooreduce Hola carga en el clúster de hello, mientras que se está recuperando.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="3bd0b-150">realiza las comprobaciones de Hello son:</span><span class="sxs-lookup"><span data-stu-id="3bd0b-150">hello checks performed are:</span></span>
  * <span data-ttu-id="3bd0b-151">Si el estado del clúster de hello es correcto</span><span class="sxs-lookup"><span data-stu-id="3bd0b-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="3bd0b-152">Si el estado del servicio de hello es correcto</span><span class="sxs-lookup"><span data-stu-id="3bd0b-152">If hello service health is OK</span></span>
  * <span data-ttu-id="3bd0b-153">Si el tamaño del conjunto de réplicas de destino de Hola se logra de partición de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="3bd0b-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="3bd0b-154">Que no existan réplicas InBuild.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="3bd0b-155">**MaxConcurrentFaults**: Hola número máximo de errores simultáneos que induce en cada iteración.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="3bd0b-156">Hola mayor sea el número de hello, hello más exigente es caos y Hola hello y las conmutaciones por error estado transición combinaciones que Hola clúster lleva a cabo también son más complejas.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="3bd0b-157">A pesar de todo un valor alto cómo *MaxConcurrentFaults* tiene, Chaos garantiza - en ausencia de Hola de errores externos - no hay ninguna pérdida de quórum o pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="3bd0b-158">**EnableMoveReplicaFaults**: habilita o deshabilita los errores de Hola que provocan Hola réplicas principal o secundaria toomove.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="3bd0b-159">Estos errores están deshabilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="3bd0b-160">**WaitTimeBetweenIterations**: cantidad de Hola de toowait de tiempo entre iteraciones.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="3bd0b-161">Es decir, Hola cantidad de tiempo que se pausará al caos tras ejecutar una ronda de errores y tener acabado de validación correspondiente de hello del estado de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="3bd0b-162">Hola valor más alto de hello, Hola inferior es la velocidad de inyección de código de error promedio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="3bd0b-163">**WaitTimeBetweenFaults**: cantidad de Hola de toowait de tiempo entre dos errores consecutivos en una sola iteración.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="3bd0b-164">Hola valor más alto de hello, Hola inferior simultaneidad Hola de (u Hola superposición entre) errores.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="3bd0b-165">**ClusterHealthPolicy**: directiva de mantenimiento de clúster es toovalidate usado Hola mantenimiento del clúster de hello entre iteraciones de caos.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="3bd0b-166">Si el estado del clúster hello es un error o si se produce una excepción inesperada durante la ejecución del error, Chaos esperará 30 minutos antes de hello siguiente comprobación de estado de clúster de hello tooprovide con algunos toorecuperate de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="3bd0b-167">**Context**: colección de (cadena, cadena) pares de tipo clave-valor.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="3bd0b-168">mapa de Hello puede ser usado toorecord saber Hola Chaos ejecutar.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="3bd0b-169">No puede haber más de 100 de dicho pares y cada cadena (clave o valor) puede tener una longitud máxima de 4095.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="3bd0b-170">Esta asignación se establece por starter Hola del contexto de Hola Hola Chaos ejecutar toooptionally almacén sobre Hola específico ejecutar.</span><span class="sxs-lookup"><span data-stu-id="3bd0b-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="3bd0b-171">¿Cómo toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="3bd0b-171">How toorun Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
