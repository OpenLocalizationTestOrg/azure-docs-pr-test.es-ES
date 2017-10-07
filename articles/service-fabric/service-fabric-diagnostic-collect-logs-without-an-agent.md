---
title: aaaCollect registros directamente desde un servicio de Azure Fabric proceso del servicio | Microsoft Azure
description: "Describe las aplicaciones pueden enviar registros directamente ubicación central tooa como Azure Application Insights o Elasticsearch, sin tener que depender de agente de diagnóstico de Azure de Service Fabric."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Recopilación de registros directamente desde un proceso de servicio de Azure Service Fabric
## <a name="in-process-log-collection"></a>Recopilación de registros en proceso
Aplicación de recopilar registros de uso [extensión de diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) es una buena opción para **Azure Service Fabric** servicios si es pequeña, conjunto de Hola de registro orígenes y destinos no cambia con frecuencia y no existe es una asignación directa entre orígenes de Hola y sus destinos. Si no es así, una alternativa es toohave servicios envían sus registros directamente tooa de ubicación central. Este proceso se conoce como **recopilación de registros en proceso** y tiene varias ventajas posibles:

* *Fácil configuración e implementación*

    * configuración de Hola de recopilación de datos de diagnóstico es parte de la configuración del servicio Hola. Es mantener tooalways fácil que "sincronizados" con hello resto de la aplicación hello.
    * Se puede realizar fácilmente la configuración por aplicación o por servicio.
        * La colección de registros basados en agentes normalmente requiere una implementación independiente y la configuración del agente de diagnóstico de hello, que es una tarea administrativa adicional y un origen potencial de errores. A menudo hay solo una instancia de agente de hello permitido para cada máquina virtual (nodo) y configuración del agente Hola se comparte entre todas las aplicaciones y servicios que se ejecutan en ese nodo. 

* *Flexibilidad*
   
    * aplicación Hello puede enviar datos de hello dondequiera que necesita toogo, siempre que hay una biblioteca de cliente que admite el sistema de almacenamiento de datos de Hola de destino. Se pueden agregar tantos destinos nuevos como se desee.
    * Se pueden implementar reglas complejas de captura, filtrado y agregación de datos.
    * La colección de registros basados en agentes a menudo está limitada por los receptores de datos de Hola que admite el agente de Hola. Algunos agentes se pueden ampliar.

* *Contexto y obtener acceso a datos de aplicación de toointernal*
   
    * subsistema de diagnóstico de Hello ejecuta en proceso de aplicación o un servicio de hello puede ampliar fácilmente la seguimientos de hello junto con información contextual.
    * Recopilación de registro basada en agente, Hola se deben enviar datos tooan agente a través de algún mecanismo de comunicación entre procesos, como el seguimiento de eventos para Windows. Este mecanismo podría imponer limitaciones adicionales.

Es posible toocombine y se benefician de ambos métodos de colección. De hecho, podría ser mejor solución Hola para muchas aplicaciones. Colección basada en agente es una solución natural para la recopilación de clúster en su totalidad registros toohello relacionados y nodos de clúster individuales. Es una forma mucho más confiable, a la colección de registros en curso, problemas de inicio del servicio de toodiagnose y bloqueos. Además, con muchos servicios se ejecutan dentro de un clúster de Service Fabric, cada servicio realizar su propia colección de registros en curso se consiguen en numerosas las conexiones salientes de clúster de Hola. Gran número de conexiones salientes es complicado para el subsistema de red de Hola y de destino del registro de hello. Un agente como [ **Diagnósticos de Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) puede recopilar datos de varios servicios y enviar todos los datos a través de unas pocas conexiones, lo que mejora el rendimiento. 

En este artículo, le mostramos cómo tooset un proceso de registro de colección mediante [ **biblioteca de código abierto de EventFlow**](https://github.com/Azure/diagnostics-eventflow). Otras bibliotecas podrían utilizarse para hello mismo propósito, pero EventFlow tiene las ventajas de Hola de ya han sido diseñadas específicamente para los servicios de Service Fabric de recopilación y toosupport del registro en curso. Usamos [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) como destino del registro de hello. Otros destinos como [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) o [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) también son compatibles. Es simplemente una pregunta de instalación de paquetes de NuGet apropiada y configurar el destino de hello en el archivo de configuración de hello EventFlow. Para obtener más información sobre los destinos de los registros que no sea Application Insights, consulte la [documentación de EventFlow](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>Agregar proyecto de servicio de EventFlow biblioteca tooa Service Fabric
Los archivos binarios de EventFlow están disponibles como un conjunto de paquetes de NuGet. tooadd EventFlow tooa proyecto del servicio Service Fabric, haga clic en proyecto de Hola Hola el Explorador de soluciones y elija "Paquetes de NuGet de administrar". Cambiar toohello "Examinar" pestaña y busque "`Diagnostics.EventFlow`":

![Paquetes de NuGet para EventFlow en la interfaz de usuario del administrador de paquetes de NuGet de Visual Studio][1]

servicio Hola hospedaje EventFlow debe incluir paquetes adecuados según el origen de Hola y de destino para los registros de aplicación Hola. Agregue los siguientes paquetes de saludo: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (datos de toocapture de EventSource (clase) del servicio de Hola y de EventSources estándar como *servicios de Microsoft ServiceFabric* y *Microsoft-ServiceFabric-actores*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (vamos toosend Hola registros tooan Azure Application Insights recursos)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (permite la inicialización de canalización de hello EventFlow de configuración de servicio de Service Fabric y notifica los problemas con el envío de datos de diagnóstico como informes de mantenimiento de Service Fabric)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`el paquete requiere tootarget de proyecto de servicio de hello .NET Framework 4.6 o posterior. Asegúrese de que establezca .NET framework de destino adecuada de hello en Propiedades del proyecto antes de instalar este paquete. 

Después de que todos hello paquetes están instalados, Hola siguiente paso es tooconfigure y habilitar EventFlow en el servicio de Hola.

## <a name="configuring-and-enabling-log-collection"></a>Configuración y habilitación de la recopilación de registros
Canalización de EventFlow, responsable de enviar registros de hello, se crea a partir de una especificación almacenada en un archivo de configuración. El paquete `Microsoft.Diagnostics.EventFlow.ServiceFabric` instala un archivo de configuración inicial de EventFlow en la carpeta de la solución `PackageRoot\Config`. nombre de archivo de Hello es `eventFlowConfig.json`. Este archivo de configuración debe toobe modificar toocapture datos de servicio predeterminado de hello `EventSource` clase y enviar datos tooApplication visión servicio.

> [!NOTE]
> Se supone que está familiarizado con **Azure Application Insights** servicio y que tiene un recurso de Application Insights que planea toouse toomonitor su servicio de Service Fabric. Si necesita más información, consulte [Creación de recursos en Application Insights](../application-insights/app-insights-create-new-resource.md).

Hola abra `eventFlowConfig.json` en el editor de Hola y cambie su contenido, tal y como se muestra a continuación. Asegúrese de que nombre de ServiceEventSource de hello tooreplace y la clave de instrumentación de Application Insights según toocomments. 

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

> [!NOTE]
> nombre de Hola de ServiceEventSource del servicio es valor de Hola de hello propiedad Name de hello `EventSourceAttribute` aplica toohello ServiceEventSource clase. Se especifica en hello `ServiceEventSource.cs` archivo, que forma parte del código de servicio de Hola. Por ejemplo, en hello siguiente nombre de Hola de fragmento de código de hello ServiceEventSource es *MyCompany-Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Tenga en cuenta que el archivo `eventFlowConfig.json` forma parte del paquete de configuración del servicio. Archivo de cambios de toothis puede incluirse en completo o configuración-solo las actualizaciones del servicio de hello, asunto tooService tejido actualizar las comprobaciones de mantenimiento y la reversión automática si hay errores durante la actualización. Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).

Hola último paso es tooinstantiate EventFlow canalización en el código de inicio del servicio, ubicado en `Program.cs` archivo. Hola adiciones de relacionados con el EventFlow de ejemplo siguiente se marcan con comentarios a partir de `****`:

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

## <a name="verification"></a>Comprobación
Iniciar el servicio y observe Hola depuración ventana de resultados de Visual Studio. Una vez iniciado el servicio de hello, debería comenzar a ver evidencia de que el servicio envía las entradas de "Telemetría de visión de la aplicación". Abra un explorador web y navegue vaya tooyour Application Insights recursos. Abra la ficha de "Búsqueda" (en parte superior de Hola de hoja de hello predeterminado "Introducción"). Tras un breve retraso deberá comenzar a ver los seguimientos en el portal de Application Insights hello:

![El portal de Application Insights muestra los registros de una aplicación de Service Fabric][2]

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre cómo diagnosticar y supervisar un servicio Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [Documentación de EventFlow](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
