---
title: "Agregación de eventos de Azure Service Fabric con EventFlow | Microsoft Docs"
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
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="8886c-103">Recopilación y agregación de eventos con EventFlow</span><span class="sxs-lookup"><span data-stu-id="8886c-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="8886c-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) puede enrutar los eventos de un nodo a uno o varios destinos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="8886c-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="8886c-105">Dado que se incluye como un paquete de NuGet en el proyecto de servicio, el código y la configuración de EventFlow van con el servicio, por lo que se elimina el problema de la configuración por nodo que se mencionó antes sobre Diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8886c-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="8886c-106">EventFlow se ejecuta dentro del proceso de servicio y se conecta directamente con las salidas configuradas.</span><span class="sxs-lookup"><span data-stu-id="8886c-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="8886c-107">Gracias a esta conexión directa, EventFlow funciona en implementaciones de servicios de Azure, de contenedor o locales.</span><span class="sxs-lookup"><span data-stu-id="8886c-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="8886c-108">Tenga cuidado si ejecuta EventFlow en escenarios de alta densidad, como un contenedor, ya que cada canalización EventFlow genera una conexión externa.</span><span class="sxs-lookup"><span data-stu-id="8886c-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="8886c-109">Por tanto, si hospeda varios procesos, obtendrá varias conexiones salientes.</span><span class="sxs-lookup"><span data-stu-id="8886c-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="8886c-110">Esto no supone un problema para las aplicaciones de Service Fabric, ya que todas las réplicas de `ServiceType` se ejecutan en el mismo proceso, lo que limita el número de conexiones salientes.</span><span class="sxs-lookup"><span data-stu-id="8886c-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="8886c-111">EventFlow también proporciona filtrado de eventos, de manera que solo se envían los eventos que coinciden con el filtro especificado.</span><span class="sxs-lookup"><span data-stu-id="8886c-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="8886c-112">Configuración de EventFlow</span><span class="sxs-lookup"><span data-stu-id="8886c-112">Setting up EventFlow</span></span>

<span data-ttu-id="8886c-113">Los archivos binarios de EventFlow están disponibles como un conjunto de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8886c-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="8886c-114">Para agregar EventFlow a un proyecto de servicio de Service Fabric, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto y elija "Administrar paquetes de NuGet".</span><span class="sxs-lookup"><span data-stu-id="8886c-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="8886c-115">Cambie a la pestaña "Examinar" y busque "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="8886c-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Paquetes de NuGet para EventFlow en la interfaz de usuario del administrador de paquetes de NuGet de Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="8886c-117">Aparecerá una lista de los diferentes paquetes, marcados con las etiquetas "Entradas" y "Salidas".</span><span class="sxs-lookup"><span data-stu-id="8886c-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="8886c-118">EventFlow es compatible con varios analizadores y proveedores de registro.</span><span class="sxs-lookup"><span data-stu-id="8886c-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="8886c-119">El servicio que hospede EventFlow debe incluir los paquetes adecuados según el origen y destino de los registros de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8886c-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="8886c-120">Además del paquete principal de Service Fabric, también necesita tener configurado al menos un paquete de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="8886c-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="8886c-121">Para el ejemplo, puede agregar los siguientes paquetes para enviar eventos de EventSource a Application Insights:</span><span class="sxs-lookup"><span data-stu-id="8886c-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="8886c-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` (para capturar datos de la clase EventSource del servicio y de las clases EventSource estándar como *Microsoft-ServiceFabric-Services* y *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="8886c-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="8886c-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (vamos a enviar los registros a un recurso de Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="8886c-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="8886c-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric` (permite inicializar la canalización de EventFlow desde la configuración del servicio de Service Fabric, y notifica los problemas con el envío de datos de diagnóstico como informes de mantenimiento de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="8886c-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="8886c-125">El paquete `Microsoft.Diagnostics.EventFlow.Input.EventSource` necesita que proyecto de servicio sea para .NET Framework 4.6 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="8886c-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="8886c-126">Asegúrese de establecer la plataforma de destino adecuada en las propiedades del proyecto antes de instalar este paquete.</span><span class="sxs-lookup"><span data-stu-id="8886c-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="8886c-127">Una vez instalados todos los paquetes, el siguiente paso es configurar y habilitar EventFlow en el servicio.</span><span class="sxs-lookup"><span data-stu-id="8886c-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="8886c-128">Configuración y habilitación de la recopilación de registros</span><span class="sxs-lookup"><span data-stu-id="8886c-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="8886c-129">La canalización de EventFlow, responsable del envío de los registros, se crea a partir de una especificación almacenada en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8886c-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="8886c-130">El paquete `Microsoft.Diagnostics.EventFlow.ServiceFabric` instala un archivo de configuración inicial de EventFlow en la carpeta de la solución `PackageRoot\Config`, llamada `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="8886c-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="8886c-131">Este archivo de configuración debe modificarse para capturar los datos de la clase `EventSource` del servicio predeterminado y cualquier otra entrada que desee configurar y enviar los datos al servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8886c-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="8886c-132">A continuación, se presenta un ejemplo de *eventFlowConfig.json* basado en los paquetes NuGet mencionados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8886c-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="8886c-133">El nombre del origen ServiceEventSource del servicio es el valor de la propiedad Name de `EventSourceAttribute` aplicado a la clase ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="8886c-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="8886c-134">Se especifica todo en el archivo `ServiceEventSource.cs`, que forma parte del código del servicio.</span><span class="sxs-lookup"><span data-stu-id="8886c-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="8886c-135">Por ejemplo, en el siguiente fragmento de código, el nombre del origen ServiceEventSource es *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="8886c-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="8886c-136">Tenga en cuenta que el archivo `eventFlowConfig.json` forma parte del paquete de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="8886c-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="8886c-137">Los cambios en este archivo pueden incluirse en actualizaciones completas o de solo configuración del servicio; están sujetos a las comprobaciones del estado de actualización de Service Fabric y se revierten automáticamente en caso de errores durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="8886c-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="8886c-138">Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="8886c-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="8886c-139">La sección de *filtros* de la configuración permite personalizar aún más la información que se va a enviar a las salidas a través de la canalización de EventFlow, de tal forma que se puede quitar o incluir información concreta o cambiar la estructura de los datos del evento.</span><span class="sxs-lookup"><span data-stu-id="8886c-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="8886c-140">Para más información sobre filtrado, vea los [filtros de EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="8886c-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="8886c-141">El último paso consiste en crear una instancia de la canalización de EventFlow en el código de inicio del servicio, ubicado en el archivo `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8886c-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="8886c-142">El nombre que se pasa como parámetro del método `CreatePipeline` de `ServiceFabricDiagnosticsPipelineFactory` es el nombre de la *entidad de estado de mantenimiento* que representa la canalización de recopilación de registros de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="8886c-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="8886c-143">Este nombre se usa si EventFlow encuentra un error y lo notifica a través del subsistema de estado de mantenimiento de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8886c-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="8886c-144">Uso de los parámetros de la aplicación y de la configuración de Service Fabric en eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="8886c-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="8886c-145">EventFlow permite usar los parámetros de la aplicación y la configuración de Service Fabric para configurar EventFlow.</span><span class="sxs-lookup"><span data-stu-id="8886c-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="8886c-146">Puede hacer referencia a los parámetros de configuración de Service Fabric mediante la utilización de esta sintaxis especial para los valores:</span><span class="sxs-lookup"><span data-stu-id="8886c-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="8886c-147">`<section-name>` es el nombre de la sección de configuración de Service Fabric, y `<setting-name>` es el conjunto de configuración que proporciona el valor que se usará para configurar una opción de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="8886c-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="8886c-148">Para leer más información sobre cómo realizar esto, vaya a [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters) (Compatibilidad de los parámetros de la aplicación y la configuración de Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="8886c-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="8886c-149">Comprobación</span><span class="sxs-lookup"><span data-stu-id="8886c-149">Verification</span></span>

<span data-ttu-id="8886c-150">Inicie el servicio y observe la ventana de resultados de depuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8886c-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="8886c-151">Una vez iniciado el servicio, deberá comenzar a ver la evidencia de que el servicio está enviando registros a la salida configurada.</span><span class="sxs-lookup"><span data-stu-id="8886c-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="8886c-152">Vaya a la plataforma de visualización y análisis de eventos y confirme que los registros han empezado a mostrarse, una operación que puede tardar algunos minutos.</span><span class="sxs-lookup"><span data-stu-id="8886c-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8886c-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8886c-153">Next steps</span></span>

* [<span data-ttu-id="8886c-154">Análisis y visualización de eventos con Application Insights</span><span class="sxs-lookup"><span data-stu-id="8886c-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="8886c-155">Análisis y visualización de eventos con OMS</span><span class="sxs-lookup"><span data-stu-id="8886c-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="8886c-156">Documentación de EventFlow</span><span class="sxs-lookup"><span data-stu-id="8886c-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)