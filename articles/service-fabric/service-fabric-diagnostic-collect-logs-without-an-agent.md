---
title: "Recopilación de registros directamente desde un proceso de servicio de Azure Service Fabric | Microsoft Azure"
description: "Describe las aplicaciones de Service Fabric que pueden enviar registros directamente a una ubicación central, como Azure Application Insights o Elasticsearch, sin tener que depender del agente Diagnósticos de Azure."
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
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="1b857-103">Recopilación de registros directamente desde un proceso de servicio de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1b857-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="1b857-104">Recopilación de registros en proceso</span><span class="sxs-lookup"><span data-stu-id="1b857-104">In-process log collection</span></span>
<span data-ttu-id="1b857-105">La recopilación de registros de aplicación mediante [la extensión Diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md) es una buena opción para los servicios de **Azure Service Fabric** si el conjunto de orígenes y destinos de los registros es pequeño, no cambian con frecuencia y hay una asignación directa entre los orígenes y sus destinos.</span><span class="sxs-lookup"><span data-stu-id="1b857-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="1b857-106">Si no es así, una alternativa es hacer que los servicios envíen sus registros directamente a una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="1b857-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="1b857-107">Este proceso se conoce como **recopilación de registros en proceso** y tiene varias ventajas posibles:</span><span class="sxs-lookup"><span data-stu-id="1b857-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="1b857-108">*Fácil configuración e implementación*</span><span class="sxs-lookup"><span data-stu-id="1b857-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="1b857-109">La configuración de la recopilación de datos de diagnóstico es parte de la configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="1b857-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="1b857-110">Es fácil mantenerla siempre "sincronizada" con el resto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b857-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="1b857-111">Se puede realizar fácilmente la configuración por aplicación o por servicio.</span><span class="sxs-lookup"><span data-stu-id="1b857-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="1b857-112">La recopilación de registros basada en agente normalmente requiere una implementación y configuración independientes del agente de diagnóstico, lo que supone una tarea administrativa adicional y una posible fuente de errores.</span><span class="sxs-lookup"><span data-stu-id="1b857-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="1b857-113">A menudo solo se permite una instancia del agente por máquina virtual (nodo) y la configuración del agente se comparte entre todas las aplicaciones y los servicios que se ejecutan en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="1b857-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="1b857-114">*Flexibilidad*</span><span class="sxs-lookup"><span data-stu-id="1b857-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="1b857-115">La aplicación puede enviar los datos dondequiera que deban ir siempre que haya una biblioteca de cliente que admita el sistema de almacenamiento de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="1b857-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="1b857-116">Se pueden agregar tantos destinos nuevos como se desee.</span><span class="sxs-lookup"><span data-stu-id="1b857-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="1b857-117">Se pueden implementar reglas complejas de captura, filtrado y agregación de datos.</span><span class="sxs-lookup"><span data-stu-id="1b857-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="1b857-118">Una recopilación de registros basada en agente suele estar limitada por los receptores de datos que el agente admite.</span><span class="sxs-lookup"><span data-stu-id="1b857-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="1b857-119">Algunos agentes se pueden ampliar.</span><span class="sxs-lookup"><span data-stu-id="1b857-119">Some agents are extensible.</span></span>

* <span data-ttu-id="1b857-120">*Acceso a los datos y el contexto internos de la aplicación*</span><span class="sxs-lookup"><span data-stu-id="1b857-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="1b857-121">El subsistema de diagnóstico que se ejecuta dentro del proceso de la aplicación o servicio puede ampliar fácilmente los seguimientos con información contextual.</span><span class="sxs-lookup"><span data-stu-id="1b857-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="1b857-122">Con la recopilación de registros basada en agente, los datos se deben enviar a un agente mediante algún mecanismo de comunicación entre procesos, como el Seguimiento de eventos para Windows.</span><span class="sxs-lookup"><span data-stu-id="1b857-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="1b857-123">Este mecanismo podría imponer limitaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="1b857-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="1b857-124">Por supuesto, es posible combinar y beneficiarse de ambos métodos de recopilación.</span><span class="sxs-lookup"><span data-stu-id="1b857-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="1b857-125">de hecho, puede que sea la mejor solución para muchas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1b857-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="1b857-126">La recopilación basada en agente es una solución natural para recopilar los registros relacionados con el clúster en su totalidad y con nodos de clúster individuales.</span><span class="sxs-lookup"><span data-stu-id="1b857-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="1b857-127">Es una manera mucho más confiable que la recopilación de registros en proceso para diagnosticar problemas de inicio y bloqueos del servicio.</span><span class="sxs-lookup"><span data-stu-id="1b857-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="1b857-128">Además, como hay muchos servicios en ejecución dentro de un clúster de Service Fabric y cada servicio realiza su propia recopilación de registros en proceso, se producen numerosas conexiones salientes desde el clúster.</span><span class="sxs-lookup"><span data-stu-id="1b857-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="1b857-129">Un gran número de conexiones salientes supone una carga para el subsistema de red y para el destino de registros.</span><span class="sxs-lookup"><span data-stu-id="1b857-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="1b857-130">Un agente como [ **Diagnósticos de Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) puede recopilar datos de varios servicios y enviar todos los datos a través de unas pocas conexiones, lo que mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1b857-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="1b857-131">En este artículo se muestra cómo configurar una recopilación de registros en proceso mediante la [**biblioteca de código abierto EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="1b857-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="1b857-132">Podrían utilizarse otras bibliotecas para el mismo propósito, pero EventFlow tiene la ventaja de que ha sido diseñada específicamente para la recopilación de registros en proceso y para admitir los servicios de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1b857-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="1b857-133">Usamos [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) como destino de los registros.</span><span class="sxs-lookup"><span data-stu-id="1b857-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="1b857-134">Otros destinos como [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) o [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) también son compatibles.</span><span class="sxs-lookup"><span data-stu-id="1b857-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="1b857-135">Es simplemente una cuestión de instalar los paquetes de NuGet apropiados y configurar el destino en el archivo de configuración EventFlow.</span><span class="sxs-lookup"><span data-stu-id="1b857-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="1b857-136">Para obtener más información sobre los destinos de los registros que no sea Application Insights, consulte la [documentación de EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="1b857-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="1b857-137">Incorporación de la biblioteca EventFlow a un proyecto de servicio de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1b857-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="1b857-138">Los archivos binarios de EventFlow están disponibles como un conjunto de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b857-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="1b857-139">Para agregar EventFlow a un proyecto de servicio de Service Fabric, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto y elija "Administrar paquetes de NuGet".</span><span class="sxs-lookup"><span data-stu-id="1b857-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="1b857-140">Cambie a la pestaña "Examinar" y busque "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="1b857-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Paquetes de NuGet para EventFlow en la interfaz de usuario del administrador de paquetes de NuGet de Visual Studio][1]

<span data-ttu-id="1b857-142">El servicio que hospede EventFlow debe incluir los paquetes adecuados según el origen y destino de los registros de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1b857-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="1b857-143">Agregue los siguientes paquetes:</span><span class="sxs-lookup"><span data-stu-id="1b857-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="1b857-144">(para capturar datos de la clase EventSource del servicio y de las clases EventSource estándar como *Microsoft-ServiceFabric-Services* y *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="1b857-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="1b857-145">(vamos a enviar los registros a un recurso de Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="1b857-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="1b857-146">(permite inicializar la canalización de EventFlow desde la configuración del servicio de Service Fabric, y notifica los problemas con el envío de datos de diagnóstico como informes de estado de mantenimiento de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="1b857-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="1b857-147">El paquete `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` necesita que proyecto de servicio sea para .NET Framework 4.6 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="1b857-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="1b857-148">Asegúrese de establecer la plataforma de destino adecuada en las propiedades del proyecto antes de instalar este paquete.</span><span class="sxs-lookup"><span data-stu-id="1b857-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="1b857-149">Una vez instalados todos los paquetes, el siguiente paso es configurar y habilitar EventFlow en el servicio.</span><span class="sxs-lookup"><span data-stu-id="1b857-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="1b857-150">Configuración y habilitación de la recopilación de registros</span><span class="sxs-lookup"><span data-stu-id="1b857-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="1b857-151">La canalización de EventFlow, responsable del envío de los registros, se crea a partir de una especificación almacenada en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1b857-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="1b857-152">El paquete `Microsoft.Diagnostics.EventFlow.ServiceFabric` instala un archivo de configuración inicial de EventFlow en la carpeta de la solución `PackageRoot\Config`.</span><span class="sxs-lookup"><span data-stu-id="1b857-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="1b857-153">El nombre de archivo es `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="1b857-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="1b857-154">Este archivo de configuración debe modificarse para capturar los datos de la clase `EventSource` del servicio predeterminado y enviar los datos al servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b857-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="1b857-155">Se da por hecho que está familiarizado con el servicio **Azure Application Insights** y que tiene un recurso de Application Insights que va a usar para supervisar el servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1b857-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="1b857-156">Si necesita más información, consulte [Creación de recursos en Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1b857-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="1b857-157">Abra el archivo `eventFlowConfig.json` en el editor y cambie su contenido tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="1b857-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="1b857-158">Asegúrese de reemplazar el nombre ServiceEventSource y la clave de instrumentación de Application Insights según los comentarios.</span><span class="sxs-lookup"><span data-stu-id="1b857-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="1b857-159">El nombre del origen ServiceEventSource del servicio es el valor de la propiedad Name de `EventSourceAttribute` aplicado a la clase ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="1b857-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="1b857-160">Se especifica todo en el archivo `ServiceEventSource.cs`, que forma parte del código del servicio.</span><span class="sxs-lookup"><span data-stu-id="1b857-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="1b857-161">Por ejemplo, en el siguiente fragmento de código, el nombre del origen ServiceEventSource es *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="1b857-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="1b857-162">Tenga en cuenta que el archivo `eventFlowConfig.json` forma parte del paquete de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="1b857-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="1b857-163">Los cambios en este archivo pueden incluirse en actualizaciones completas o de solo configuración del servicio; están sujetos a las comprobaciones del estado de actualización de Service Fabric y se revierten automáticamente en caso de errores durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="1b857-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="1b857-164">Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="1b857-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="1b857-165">El último paso consiste en crear una instancia de la canalización de EventFlow en el código de inicio del servicio, ubicado en el archivo `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="1b857-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="1b857-166">En el siguiente ejemplo, se han marcado las incorporaciones relacionadas con EventFlow con comentarios que comienzan con `****`:</span><span class="sxs-lookup"><span data-stu-id="1b857-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="1b857-167">El nombre que se pasa como parámetro del método `CreatePipeline` de `ServiceFabricDiagnosticsPipelineFactory` es el nombre de la *entidad de estado de mantenimiento* que representa la canalización de recopilación de registros de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="1b857-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="1b857-168">Este nombre se usa si EventFlow encuentra un error y lo notifica a través del subsistema de estado de mantenimiento de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1b857-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="1b857-169">Comprobación</span><span class="sxs-lookup"><span data-stu-id="1b857-169">Verification</span></span>
<span data-ttu-id="1b857-170">Inicie el servicio y observe la ventana de resultados de depuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b857-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="1b857-171">Una vez iniciado el servicio, deberá comenzar a ver la evidencia de que el servicio está enviando registros de "Telemetría de Application Insights".</span><span class="sxs-lookup"><span data-stu-id="1b857-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="1b857-172">Abra un explorador web y vaya al recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b857-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="1b857-173">Abra la pestaña "Buscar" (en la parte superior de la hoja "Información general" predeterminada).</span><span class="sxs-lookup"><span data-stu-id="1b857-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="1b857-174">Tras una breve demora, comenzará a ver sus seguimientos en el portal de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="1b857-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![El portal de Application Insights muestra los registros de una aplicación de Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="1b857-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b857-176">Next steps</span></span>
* [<span data-ttu-id="1b857-177">Más información sobre cómo diagnosticar y supervisar un servicio Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1b857-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="1b857-178">Documentación de EventFlow</span><span class="sxs-lookup"><span data-stu-id="1b857-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
