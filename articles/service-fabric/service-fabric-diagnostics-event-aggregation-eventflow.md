---
title: "Agregación de eventos de servicio de tejido con EventFlow aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre la agregación y la recopilación de eventos con EventFlow para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a>Recopilación y agregación de eventos con EventFlow

[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) puede enrutar los eventos de un nodo tooone o más destinos de supervisión. Dado que se incluye como un paquete de NuGet en el proyecto de servicio, configuración y el código de EventFlow viajan con servicio hello, lo que elimina el problema de configuración por nodo Hola se ha mencionado anteriormente sobre los diagnósticos de Azure. EventFlow se ejecuta dentro de su proceso de servicio y se conecta directamente salidas toohello configurado. Debido a la conexión directa de hello, EventFlow funciona en Azure, el contenedor y las implementaciones de servicio local. Tenga cuidado si ejecuta EventFlow en escenarios de alta densidad, como un contenedor, ya que cada canalización EventFlow genera una conexión externa. Por tanto, si hospeda varios procesos, obtendrá varias conexiones salientes. Esto no es tanto un problema para las aplicaciones de Service Fabric, porque todas las réplicas de un `ServiceType` ejecutar Hola mismo proceso y esto limita el número de Hola de conexiones salientes. EventFlow también proporciona filtrado de eventos, para que se envíen solo los eventos de Hola que coinciden con el filtro especificado Hola.

## <a name="setting-up-eventflow"></a>Configuración de EventFlow

Los archivos binarios de EventFlow están disponibles como un conjunto de paquetes de NuGet. tooadd EventFlow tooa proyecto del servicio Service Fabric, haga clic en proyecto de Hola Hola el Explorador de soluciones y elija "Paquetes de NuGet de administrar". Cambiar toohello "Examinar" pestaña y busque "`Diagnostics.EventFlow`":

![Paquetes de NuGet para EventFlow en la interfaz de usuario del administrador de paquetes de NuGet de Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Aparecerá una lista de los diferentes paquetes, marcados con las etiquetas "Entradas" y "Salidas". EventFlow es compatible con varios analizadores y proveedores de registro. servicio Hola hospedaje EventFlow debe incluir paquetes adecuados según el origen de Hola y de destino para los registros de aplicación Hola. Asimismo paquete ServiceFabric de toohello core, también necesita al menos una entrada y salida configurada. Para el ejemplo, puede agregar Hola después paquetes toosent EventSource eventos tooApplication visión:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`datos de toocapture de EventSource (clase) del servicio de Hola y de EventSources estándar como *servicios de Microsoft ServiceFabric* y *Microsoft-ServiceFabric-actores*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(vamos toosend Hola registros tooan Azure Application Insights recursos)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(permite la inicialización de canalización de hello EventFlow de configuración de servicio de Service Fabric y notifica los problemas con el envío de datos de diagnóstico como informes de mantenimiento de Service Fabric)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`el paquete requiere tootarget de proyecto de servicio de hello .NET Framework 4.6 o posterior. Asegúrese de que establezca .NET framework de destino adecuada de hello en Propiedades del proyecto antes de instalar este paquete.

Después de que todos hello paquetes están instalados, Hola siguiente paso es tooconfigure y habilitar EventFlow en el servicio de Hola.

## <a name="configuring-and-enabling-log-collection"></a>Configuración y habilitación de la recopilación de registros
canalización de EventFlow Hola responsable del envío de registros de Hola se crea a partir de una especificación almacenada en un archivo de configuración. Hola `Microsoft.Diagnostics.EventFlow.ServiceFabric` paquete instala un archivo de configuración inicial de EventFlow en `PackageRoot\Config` carpeta de soluciones, denominado `eventFlowConfig.json`. Este archivo de configuración debe toobe modificar toocapture datos de servicio predeterminado de hello `EventSource` clase y otras entradas que desee tooconfigure y enviar datos toohello el lugar adecuado.

Este es un ejemplo *eventFlowConfig.json* basándose en los paquetes de NuGet Hola mencionados anteriormente:
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

nombre de Hola de ServiceEventSource del servicio es valor de Hola de hello propiedad Name de hello `EventSourceAttribute` aplica toohello ServiceEventSource clase. Se especifica en hello `ServiceEventSource.cs` archivo, que forma parte del código de servicio de Hola. Por ejemplo, en hello siguiente nombre de Hola de fragmento de código de hello ServiceEventSource es *MyCompany-Application1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Tenga en cuenta que el archivo `eventFlowConfig.json` forma parte del paquete de configuración del servicio. Archivo de cambios de toothis puede incluirse en completo o configuración-solo las actualizaciones del servicio de hello, asunto tooService tejido actualizar las comprobaciones de mantenimiento y la reversión automática si hay errores durante la actualización. Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).

Hola *filtros* sección de configuración de hello permite toofurther personalizar información hello toogo continuo a través de hello EventFlow canalización toohello salidas, permitiéndole toodrop o incluir cierta información Hola estructura de datos de evento de saludo. Para más información sobre filtrado, vea los [filtros de EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).

Hola último paso es tooinstantiate EventFlow canalización en el código de inicio del servicio, ubicado en `Program.cs` archivo:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

nombre Hello pasado como parámetro de Hola de hello `CreatePipeline` método de hello `ServiceFabricDiagnosticsPipelineFactory` es nombre Hola de hello *entidad estado* que representa la canalización de colección de registro de hello EventFlow. Este nombre se usa si encuentra EventFlow y error y lo notifica a través de hello subsistema de estado de Service Fabric.

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>Con la configuración de Service Fabric y aplicación parámetros tooin eventFlowConfig

EventFlow admite el uso de configuración de Service Fabric y aplicación parámetros tooconfigure EventFlow. Puede hacer referencia a parámetros de configuración de tejido tooService con esta sintaxis especial para los valores:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`es Hola nombre de sección de configuración de Service Fabric, hello y `<setting-name>` es valor de configuración de hello proporcionar valor Hola que será usado tooconfigure una configuración de EventFlow. más información acerca de cómo tooread toodo, vaya demasiado[compatibilidad con la configuración de Service Fabric y parámetros de la aplicación](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Comprobación

Iniciar el servicio y observe Hola depuración ventana de resultados de Visual Studio. Una vez iniciado el servicio de hello, deberá comenzar a ver la evidencia de que el servicio envía registra la salida de toohello que ha configurado. Navegar por la plataforma de análisis y la visualización de eventos de tooyour y confirme que los registros han iniciado tooshow arriba (puede tardar unos minutos).

## <a name="next-steps"></a>Pasos siguientes

* [Análisis y visualización de eventos con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Análisis y visualización de eventos con OMS](service-fabric-diagnostics-event-analysis-oms.md)
* [Documentación de EventFlow](https://github.com/Azure/diagnostics-eventflow)