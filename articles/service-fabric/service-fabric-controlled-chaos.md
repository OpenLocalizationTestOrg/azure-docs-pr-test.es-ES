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
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Inducción de errores controlados con Caos en clústeres de Service Fabric
Los sistemas distribuidos a gran escala, como las infraestructuras en la nube, por naturaleza, no son confiables. Azure Service Fabric permite servicios distribuidos de los desarrolladores toowrite confiable encima de una infraestructura no confiable. toowrite sólida servicios distribuidos por encima de una infraestructura no confiable, los desarrolladores necesitan toobe estabilidad de hello tootest capaz de sus servicios mientras Hola confiable infraestructura subyacente está pasando por las transiciones de estado complicado toofaults due.

Hola [por inyección de código de error y el servicio de Cluster Server Analysis](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (también conocido como Hola error Analysis Services) permite a los desarrolladores hello tooinduce errores tootest sus servicios. Estos destino simulación errores, como [reiniciar una partición](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), puede ayudar a ejercer las transiciones de estado más común de Hola. Sin embargo, los errores simulados de destino están sesgados por definición y, por consiguiente, pueden perder errores que se muestran solo en una secuencia de transiciones de estado larga, complicada y difícil de predecir. Para una prueba no sesgada, se puede usar Chaos.

Caos simulan periódicos, intercalados errores (estable e incorrectas) a lo largo de clúster de Hola durante períodos ampliados de tiempo. Una vez haya configurado el caos con velocidad de Hola y tipo de Hola de errores, puede iniciar Chaos mediante C# o Powershell API toostart generar errores en clúster de Hola y en los servicios. Puede configurar Chaos toorun durante un período de tiempo especificado (por ejemplo, para una hora), después del cual el caos se detiene automáticamente, o puede llamar a toostop StopChaos API (C# o Powershell) en cualquier momento.

> [!NOTE]
> En su forma actual, Chaos induce errores solo seguros, lo que implica que en ausencia de Hola de errores externos una pérdida de quórum, o la pérdida de datos nunca se produce.
>

Mientras se ejecuta Chaos, genera eventos diferentes que capturan el estado de Hola de hello ejecutar en el momento de Hola. Por ejemplo, un ExecutingFaultsEvent contiene todos los errores de Hola que Chaos ha decidido tooexecute en esa iteración. Un ValidationFailedEvent contiene los detalles de Hola de un error de validación (problemas de estabilidad o de mantenimiento) que se ha encontrado durante la validación de Hola de clúster de Hola. Puede invocar el informe de hello GetChaosReport API (C# o Powershell) tooget Hola de ejecuciones de caos. Estos eventos se guardan en un [diccionario confiable](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), que tiene una directiva de truncamiento dictada por dos configuraciones: **MaxStoredChaosEventCount** (el valor predeterminado es 25 000) y **StoredActionCleanupIntervalInSeconds** (el valor predeterminado es 3600). Cada *StoredActionCleanupIntervalInSeconds* comprobaciones de caos y todos pero Hola más reciente *MaxStoredChaosEventCount* eventos, se purgan de diccionario de hello confiable.

## <a name="faults-induced-in-chaos"></a>Errores inducidos en Caos
Caos genera errores en el clúster de Service Fabric todo hello y comprimen los errores que se ven en meses o años en unas pocas horas. combinación de Hola de errores intercalados con velocidad de errores alta de hello busca casos más complejos que pueden faltar en caso contrario. Este ejercicio de caos produce tooa significativa mejora en la calidad del código del servicio de Hola Hola.

Caos induce a errores de hello siguientes categorías:

* Reinicio de un nodo
* Reinicio de un paquete de código implementado
* Eliminación de una réplica
* Reinicio de una réplica
* Desplazamiento de una réplica principal (configurable)
* Desplazamiento de una réplica secundaria (configurable)

Caos se ejecuta en varias iteraciones. Cada iteración se compone de los errores y validación de clúster para hello período especificado. Puede configurar tiempo de hello empleado para hello clúster toostabilize y toosucceed de validación. Si se encuentra un error en la validación de clúster, Chaos genera y continúa una ValidationFailedEvent con marca de tiempo de UTC de Hola y detalles del error Hola. Por ejemplo, considere la posibilidad de una instancia de caos establecido toorun durante una hora con un máximo de tres errores simultáneos. Caos induce a tres errores y, a continuación, valida el estado del clúster Hola. Se recorre en iteración Hola anterior pasa paso hasta que esté explícitamente detenido a través de hello StopChaosAsync API o una hora. Si el clúster de hello pasa a ser incorrecto en toda iteración (es decir, no se estabilizan dentro de hello pasado en MaxClusterStabilizationTimeout), Chaos genera un ValidationFailedEvent. Este evento indica que algo salió mal y que podría necesitar más investigación.

tooget que Chaos inducido produce un error, puede usar la API de GetChaosReport (powershell o C#). Hola API Obtiene el siguiente segmento de Hola de hello Chaos informe basada en token de continuación pasada de Hola u Hola pasado en el tiempo de intervalo. Puede especificar Hola segmento siguiente Hola de ContinuationToken tooget de informe de caos Hola o puede especificar el intervalo de tiempo de Hola a través de StartTimeUtc y EndTimeUtc, pero no se puede especificar hello ContinuationToken y el intervalo de tiempo de Hola Hola misma llamada. Cuando hay más de 100 eventos Chaos, Hola informe caos se devuelve en segmentos donde un segmento contiene ya no más de 100 eventos de caos.

## <a name="important-configuration-options"></a>Opciones de configuración importantes
* **TimeToRun**: Tiempo total durante el cual se ejecutará Caos antes de finalice correctamente. Puede detener Chaos antes de que se ejecute para el período de hello TimeToRun a través de hello StopChaos API.

* **MaxClusterStabilizationTimeout**: cantidad máxima de Hola de toowait de tiempo para hello clúster toobecome correcto antes de generar un ValidationFailedEvent. Esta espera es tooreduce Hola carga en el clúster de hello, mientras que se está recuperando. realiza las comprobaciones de Hello son:
  * Si el estado del clúster de hello es correcto
  * Si el estado del servicio de hello es correcto
  * Si el tamaño del conjunto de réplicas de destino de Hola se logra de partición de servicio de Hola
  * Que no existan réplicas InBuild.
* **MaxConcurrentFaults**: Hola número máximo de errores simultáneos que induce en cada iteración. Hola mayor sea el número de hello, hello más exigente es caos y Hola hello y las conmutaciones por error estado transición combinaciones que Hola clúster lleva a cabo también son más complejas. 

> [!NOTE]
> A pesar de todo un valor alto cómo *MaxConcurrentFaults* tiene, Chaos garantiza - en ausencia de Hola de errores externos - no hay ninguna pérdida de quórum o pérdida de datos.
>

* **EnableMoveReplicaFaults**: habilita o deshabilita los errores de Hola que provocan Hola réplicas principal o secundaria toomove. Estos errores están deshabilitados de forma predeterminada.
* **WaitTimeBetweenIterations**: cantidad de Hola de toowait de tiempo entre iteraciones. Es decir, Hola cantidad de tiempo que se pausará al caos tras ejecutar una ronda de errores y tener acabado de validación correspondiente de hello del estado de Hola de clúster de Hola. Hola valor más alto de hello, Hola inferior es la velocidad de inyección de código de error promedio de Hola.
* **WaitTimeBetweenFaults**: cantidad de Hola de toowait de tiempo entre dos errores consecutivos en una sola iteración. Hola valor más alto de hello, Hola inferior simultaneidad Hola de (u Hola superposición entre) errores.
* **ClusterHealthPolicy**: directiva de mantenimiento de clúster es toovalidate usado Hola mantenimiento del clúster de hello entre iteraciones de caos. Si el estado del clúster hello es un error o si se produce una excepción inesperada durante la ejecución del error, Chaos esperará 30 minutos antes de hello siguiente comprobación de estado de clúster de hello tooprovide con algunos toorecuperate de tiempo.
* **Context**: colección de (cadena, cadena) pares de tipo clave-valor. mapa de Hello puede ser usado toorecord saber Hola Chaos ejecutar. No puede haber más de 100 de dicho pares y cada cadena (clave o valor) puede tener una longitud máxima de 4095. Esta asignación se establece por starter Hola del contexto de Hola Hola Chaos ejecutar toooptionally almacén sobre Hola específico ejecutar.

## <a name="how-toorun-chaos"></a>¿Cómo toorun Chaos

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
