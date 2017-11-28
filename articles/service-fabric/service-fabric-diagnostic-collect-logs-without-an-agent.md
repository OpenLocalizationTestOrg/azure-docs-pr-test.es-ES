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
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="458e3-103">Recopilación de registros directamente desde un proceso de servicio de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="458e3-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="458e3-104">Recopilación de registros en proceso</span><span class="sxs-lookup"><span data-stu-id="458e3-104">In-process log collection</span></span>
<span data-ttu-id="458e3-105">Aplicación de recopilar registros de uso [extensión de diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) es una buena opción para **Azure Service Fabric** servicios si es pequeña, conjunto de Hola de registro orígenes y destinos no cambia con frecuencia y no existe es una asignación directa entre orígenes de Hola y sus destinos.</span><span class="sxs-lookup"><span data-stu-id="458e3-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="458e3-106">Si no es así, una alternativa es toohave servicios envían sus registros directamente tooa de ubicación central.</span><span class="sxs-lookup"><span data-stu-id="458e3-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="458e3-107">Este proceso se conoce como **recopilación de registros en proceso** y tiene varias ventajas posibles:</span><span class="sxs-lookup"><span data-stu-id="458e3-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="458e3-108">*Fácil configuración e implementación*</span><span class="sxs-lookup"><span data-stu-id="458e3-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="458e3-109">configuración de Hola de recopilación de datos de diagnóstico es parte de la configuración del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="458e3-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="458e3-110">Es mantener tooalways fácil que "sincronizados" con hello resto de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="458e3-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="458e3-111">Se puede realizar fácilmente la configuración por aplicación o por servicio.</span><span class="sxs-lookup"><span data-stu-id="458e3-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="458e3-112">La colección de registros basados en agentes normalmente requiere una implementación independiente y la configuración del agente de diagnóstico de hello, que es una tarea administrativa adicional y un origen potencial de errores.</span><span class="sxs-lookup"><span data-stu-id="458e3-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="458e3-113">A menudo hay solo una instancia de agente de hello permitido para cada máquina virtual (nodo) y configuración del agente Hola se comparte entre todas las aplicaciones y servicios que se ejecutan en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="458e3-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="458e3-114">*Flexibilidad*</span><span class="sxs-lookup"><span data-stu-id="458e3-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="458e3-115">aplicación Hello puede enviar datos de hello dondequiera que necesita toogo, siempre que hay una biblioteca de cliente que admite el sistema de almacenamiento de datos de Hola de destino.</span><span class="sxs-lookup"><span data-stu-id="458e3-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="458e3-116">Se pueden agregar tantos destinos nuevos como se desee.</span><span class="sxs-lookup"><span data-stu-id="458e3-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="458e3-117">Se pueden implementar reglas complejas de captura, filtrado y agregación de datos.</span><span class="sxs-lookup"><span data-stu-id="458e3-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="458e3-118">La colección de registros basados en agentes a menudo está limitada por los receptores de datos de Hola que admite el agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e3-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="458e3-119">Algunos agentes se pueden ampliar.</span><span class="sxs-lookup"><span data-stu-id="458e3-119">Some agents are extensible.</span></span>

* <span data-ttu-id="458e3-120">*Contexto y obtener acceso a datos de aplicación de toointernal*</span><span class="sxs-lookup"><span data-stu-id="458e3-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="458e3-121">subsistema de diagnóstico de Hello ejecuta en proceso de aplicación o un servicio de hello puede ampliar fácilmente la seguimientos de hello junto con información contextual.</span><span class="sxs-lookup"><span data-stu-id="458e3-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="458e3-122">Recopilación de registro basada en agente, Hola se deben enviar datos tooan agente a través de algún mecanismo de comunicación entre procesos, como el seguimiento de eventos para Windows.</span><span class="sxs-lookup"><span data-stu-id="458e3-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="458e3-123">Este mecanismo podría imponer limitaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="458e3-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="458e3-124">Es posible toocombine y se benefician de ambos métodos de colección.</span><span class="sxs-lookup"><span data-stu-id="458e3-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="458e3-125">De hecho, podría ser mejor solución Hola para muchas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="458e3-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="458e3-126">Colección basada en agente es una solución natural para la recopilación de clúster en su totalidad registros toohello relacionados y nodos de clúster individuales.</span><span class="sxs-lookup"><span data-stu-id="458e3-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="458e3-127">Es una forma mucho más confiable, a la colección de registros en curso, problemas de inicio del servicio de toodiagnose y bloqueos.</span><span class="sxs-lookup"><span data-stu-id="458e3-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="458e3-128">Además, con muchos servicios se ejecutan dentro de un clúster de Service Fabric, cada servicio realizar su propia colección de registros en curso se consiguen en numerosas las conexiones salientes de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e3-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="458e3-129">Gran número de conexiones salientes es complicado para el subsistema de red de Hola y de destino del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="458e3-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="458e3-130">Un agente como [ **Diagnósticos de Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) puede recopilar datos de varios servicios y enviar todos los datos a través de unas pocas conexiones, lo que mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="458e3-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="458e3-131">En este artículo, le mostramos cómo tooset un proceso de registro de colección mediante [ **biblioteca de código abierto de EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="458e3-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="458e3-132">Otras bibliotecas podrían utilizarse para hello mismo propósito, pero EventFlow tiene las ventajas de Hola de ya han sido diseñadas específicamente para los servicios de Service Fabric de recopilación y toosupport del registro en curso.</span><span class="sxs-lookup"><span data-stu-id="458e3-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="458e3-133">Usamos [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) como destino del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="458e3-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="458e3-134">Otros destinos como [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) o [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) también son compatibles.</span><span class="sxs-lookup"><span data-stu-id="458e3-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="458e3-135">Es simplemente una pregunta de instalación de paquetes de NuGet apropiada y configurar el destino de hello en el archivo de configuración de hello EventFlow.</span><span class="sxs-lookup"><span data-stu-id="458e3-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="458e3-136">Para obtener más información sobre los destinos de los registros que no sea Application Insights, consulte la [documentación de EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="458e3-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="458e3-137">Agregar proyecto de servicio de EventFlow biblioteca tooa Service Fabric</span><span class="sxs-lookup"><span data-stu-id="458e3-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="458e3-138">Los archivos binarios de EventFlow están disponibles como un conjunto de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="458e3-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="458e3-139">tooadd EventFlow tooa proyecto del servicio Service Fabric, haga clic en proyecto de Hola Hola el Explorador de soluciones y elija "Paquetes de NuGet de administrar".</span><span class="sxs-lookup"><span data-stu-id="458e3-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="458e3-140">Cambiar toohello "Examinar" pestaña y busque "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="458e3-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Paquetes de NuGet para EventFlow en la interfaz de usuario del administrador de paquetes de NuGet de Visual Studio][1]

<span data-ttu-id="458e3-142">servicio Hola hospedaje EventFlow debe incluir paquetes adecuados según el origen de Hola y de destino para los registros de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="458e3-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="458e3-143">Agregue los siguientes paquetes de saludo:</span><span class="sxs-lookup"><span data-stu-id="458e3-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="458e3-144">(datos de toocapture de EventSource (clase) del servicio de Hola y de EventSources estándar como *servicios de Microsoft ServiceFabric* y *Microsoft-ServiceFabric-actores*)</span><span class="sxs-lookup"><span data-stu-id="458e3-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="458e3-145">(vamos toosend Hola registros tooan Azure Application Insights recursos)</span><span class="sxs-lookup"><span data-stu-id="458e3-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="458e3-146">(permite la inicialización de canalización de hello EventFlow de configuración de servicio de Service Fabric y notifica los problemas con el envío de datos de diagnóstico como informes de mantenimiento de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="458e3-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="458e3-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`el paquete requiere tootarget de proyecto de servicio de hello .NET Framework 4.6 o posterior.</span><span class="sxs-lookup"><span data-stu-id="458e3-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="458e3-148">Asegúrese de que establezca .NET framework de destino adecuada de hello en Propiedades del proyecto antes de instalar este paquete.</span><span class="sxs-lookup"><span data-stu-id="458e3-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="458e3-149">Después de que todos hello paquetes están instalados, Hola siguiente paso es tooconfigure y habilitar EventFlow en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e3-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="458e3-150">Configuración y habilitación de la recopilación de registros</span><span class="sxs-lookup"><span data-stu-id="458e3-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="458e3-151">Canalización de EventFlow, responsable de enviar registros de hello, se crea a partir de una especificación almacenada en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="458e3-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="458e3-152">El paquete `Microsoft.Diagnostics.EventFlow.ServiceFabric` instala un archivo de configuración inicial de EventFlow en la carpeta de la solución `PackageRoot\Config`.</span><span class="sxs-lookup"><span data-stu-id="458e3-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="458e3-153">nombre de archivo de Hello es `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="458e3-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="458e3-154">Este archivo de configuración debe toobe modificar toocapture datos de servicio predeterminado de hello `EventSource` clase y enviar datos tooApplication visión servicio.</span><span class="sxs-lookup"><span data-stu-id="458e3-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="458e3-155">Se supone que está familiarizado con **Azure Application Insights** servicio y que tiene un recurso de Application Insights que planea toouse toomonitor su servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="458e3-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="458e3-156">Si necesita más información, consulte [Creación de recursos en Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="458e3-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="458e3-157">Hola abra `eventFlowConfig.json` en el editor de Hola y cambie su contenido, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="458e3-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="458e3-158">Asegúrese de que nombre de ServiceEventSource de hello tooreplace y la clave de instrumentación de Application Insights según toocomments.</span><span class="sxs-lookup"><span data-stu-id="458e3-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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
> <span data-ttu-id="458e3-159">nombre de Hola de ServiceEventSource del servicio es valor de Hola de hello propiedad Name de hello `EventSourceAttribute` aplica toohello ServiceEventSource clase.</span><span class="sxs-lookup"><span data-stu-id="458e3-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="458e3-160">Se especifica en hello `ServiceEventSource.cs` archivo, que forma parte del código de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e3-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="458e3-161">Por ejemplo, en hello siguiente nombre de Hola de fragmento de código de hello ServiceEventSource es *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="458e3-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="458e3-162">Tenga en cuenta que el archivo `eventFlowConfig.json` forma parte del paquete de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="458e3-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="458e3-163">Archivo de cambios de toothis puede incluirse en completo o configuración-solo las actualizaciones del servicio de hello, asunto tooService tejido actualizar las comprobaciones de mantenimiento y la reversión automática si hay errores durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="458e3-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="458e3-164">Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="458e3-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="458e3-165">Hola último paso es tooinstantiate EventFlow canalización en el código de inicio del servicio, ubicado en `Program.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="458e3-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="458e3-166">Hola adiciones de relacionados con el EventFlow de ejemplo siguiente se marcan con comentarios a partir de `****`:</span><span class="sxs-lookup"><span data-stu-id="458e3-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="458e3-167">nombre Hello pasado como parámetro de Hola de hello `CreatePipeline` método de hello `ServiceFabricDiagnosticsPipelineFactory` es nombre Hola de hello *entidad estado* que representa la canalización de colección de registro de hello EventFlow.</span><span class="sxs-lookup"><span data-stu-id="458e3-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="458e3-168">Este nombre se usa si encuentra EventFlow y error y lo notifica a través de hello subsistema de estado de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="458e3-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="458e3-169">Comprobación</span><span class="sxs-lookup"><span data-stu-id="458e3-169">Verification</span></span>
<span data-ttu-id="458e3-170">Iniciar el servicio y observe Hola depuración ventana de resultados de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="458e3-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="458e3-171">Una vez iniciado el servicio de hello, debería comenzar a ver evidencia de que el servicio envía las entradas de "Telemetría de visión de la aplicación".</span><span class="sxs-lookup"><span data-stu-id="458e3-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="458e3-172">Abra un explorador web y navegue vaya tooyour Application Insights recursos.</span><span class="sxs-lookup"><span data-stu-id="458e3-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="458e3-173">Abra la ficha de "Búsqueda" (en parte superior de Hola de hoja de hello predeterminado "Introducción").</span><span class="sxs-lookup"><span data-stu-id="458e3-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="458e3-174">Tras un breve retraso deberá comenzar a ver los seguimientos en el portal de Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="458e3-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![El portal de Application Insights muestra los registros de una aplicación de Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="458e3-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="458e3-176">Next steps</span></span>
* [<span data-ttu-id="458e3-177">Más información sobre cómo diagnosticar y supervisar un servicio Service Fabric</span><span class="sxs-lookup"><span data-stu-id="458e3-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="458e3-178">Documentación de EventFlow</span><span class="sxs-lookup"><span data-stu-id="458e3-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
