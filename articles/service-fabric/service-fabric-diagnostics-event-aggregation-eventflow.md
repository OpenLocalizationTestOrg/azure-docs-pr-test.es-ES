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
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="4c2f9-103">Recopilación y agregación de eventos con EventFlow</span><span class="sxs-lookup"><span data-stu-id="4c2f9-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="4c2f9-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) puede enrutar los eventos de un nodo tooone o más destinos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="4c2f9-105">Dado que se incluye como un paquete de NuGet en el proyecto de servicio, configuración y el código de EventFlow viajan con servicio hello, lo que elimina el problema de configuración por nodo Hola se ha mencionado anteriormente sobre los diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="4c2f9-106">EventFlow se ejecuta dentro de su proceso de servicio y se conecta directamente salidas toohello configurado.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="4c2f9-107">Debido a la conexión directa de hello, EventFlow funciona en Azure, el contenedor y las implementaciones de servicio local.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="4c2f9-108">Tenga cuidado si ejecuta EventFlow en escenarios de alta densidad, como un contenedor, ya que cada canalización EventFlow genera una conexión externa.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="4c2f9-109">Por tanto, si hospeda varios procesos, obtendrá varias conexiones salientes.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="4c2f9-110">Esto no es tanto un problema para las aplicaciones de Service Fabric, porque todas las réplicas de un `ServiceType` ejecutar Hola mismo proceso y esto limita el número de Hola de conexiones salientes.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="4c2f9-111">EventFlow también proporciona filtrado de eventos, para que se envíen solo los eventos de Hola que coinciden con el filtro especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="4c2f9-112">Configuración de EventFlow</span><span class="sxs-lookup"><span data-stu-id="4c2f9-112">Setting up EventFlow</span></span>

<span data-ttu-id="4c2f9-113">Los archivos binarios de EventFlow están disponibles como un conjunto de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="4c2f9-114">tooadd EventFlow tooa proyecto del servicio Service Fabric, haga clic en proyecto de Hola Hola el Explorador de soluciones y elija "Paquetes de NuGet de administrar".</span><span class="sxs-lookup"><span data-stu-id="4c2f9-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="4c2f9-115">Cambiar toohello "Examinar" pestaña y busque "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="4c2f9-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Paquetes de NuGet para EventFlow en la interfaz de usuario del administrador de paquetes de NuGet de Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="4c2f9-117">Aparecerá una lista de los diferentes paquetes, marcados con las etiquetas "Entradas" y "Salidas".</span><span class="sxs-lookup"><span data-stu-id="4c2f9-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="4c2f9-118">EventFlow es compatible con varios analizadores y proveedores de registro.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="4c2f9-119">servicio Hola hospedaje EventFlow debe incluir paquetes adecuados según el origen de Hola y de destino para los registros de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="4c2f9-120">Asimismo paquete ServiceFabric de toohello core, también necesita al menos una entrada y salida configurada.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="4c2f9-121">Para el ejemplo, puede agregar Hola después paquetes toosent EventSource eventos tooApplication visión:</span><span class="sxs-lookup"><span data-stu-id="4c2f9-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="4c2f9-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`datos de toocapture de EventSource (clase) del servicio de Hola y de EventSources estándar como *servicios de Microsoft ServiceFabric* y *Microsoft-ServiceFabric-actores*)</span><span class="sxs-lookup"><span data-stu-id="4c2f9-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="4c2f9-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(vamos toosend Hola registros tooan Azure Application Insights recursos)</span><span class="sxs-lookup"><span data-stu-id="4c2f9-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="4c2f9-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(permite la inicialización de canalización de hello EventFlow de configuración de servicio de Service Fabric y notifica los problemas con el envío de datos de diagnóstico como informes de mantenimiento de Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="4c2f9-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="4c2f9-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`el paquete requiere tootarget de proyecto de servicio de hello .NET Framework 4.6 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="4c2f9-126">Asegúrese de que establezca .NET framework de destino adecuada de hello en Propiedades del proyecto antes de instalar este paquete.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="4c2f9-127">Después de que todos hello paquetes están instalados, Hola siguiente paso es tooconfigure y habilitar EventFlow en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="4c2f9-128">Configuración y habilitación de la recopilación de registros</span><span class="sxs-lookup"><span data-stu-id="4c2f9-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="4c2f9-129">canalización de EventFlow Hola responsable del envío de registros de Hola se crea a partir de una especificación almacenada en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="4c2f9-130">Hola `Microsoft.Diagnostics.EventFlow.ServiceFabric` paquete instala un archivo de configuración inicial de EventFlow en `PackageRoot\Config` carpeta de soluciones, denominado `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="4c2f9-131">Este archivo de configuración debe toobe modificar toocapture datos de servicio predeterminado de hello `EventSource` clase y otras entradas que desee tooconfigure y enviar datos toohello el lugar adecuado.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="4c2f9-132">Este es un ejemplo *eventFlowConfig.json* basándose en los paquetes de NuGet Hola mencionados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="4c2f9-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="4c2f9-133">nombre de Hola de ServiceEventSource del servicio es valor de Hola de hello propiedad Name de hello `EventSourceAttribute` aplica toohello ServiceEventSource clase.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="4c2f9-134">Se especifica en hello `ServiceEventSource.cs` archivo, que forma parte del código de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="4c2f9-135">Por ejemplo, en hello siguiente nombre de Hola de fragmento de código de hello ServiceEventSource es *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="4c2f9-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="4c2f9-136">Tenga en cuenta que el archivo `eventFlowConfig.json` forma parte del paquete de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="4c2f9-137">Archivo de cambios de toothis puede incluirse en completo o configuración-solo las actualizaciones del servicio de hello, asunto tooService tejido actualizar las comprobaciones de mantenimiento y la reversión automática si hay errores durante la actualización.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="4c2f9-138">Para más información, consulte el [tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="4c2f9-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="4c2f9-139">Hola *filtros* sección de configuración de hello permite toofurther personalizar información hello toogo continuo a través de hello EventFlow canalización toohello salidas, permitiéndole toodrop o incluir cierta información Hola estructura de datos de evento de saludo.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="4c2f9-140">Para más información sobre filtrado, vea los [filtros de EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="4c2f9-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="4c2f9-141">Hola último paso es tooinstantiate EventFlow canalización en el código de inicio del servicio, ubicado en `Program.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="4c2f9-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="4c2f9-142">nombre Hello pasado como parámetro de Hola de hello `CreatePipeline` método de hello `ServiceFabricDiagnosticsPipelineFactory` es nombre Hola de hello *entidad estado* que representa la canalización de colección de registro de hello EventFlow.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="4c2f9-143">Este nombre se usa si encuentra EventFlow y error y lo notifica a través de hello subsistema de estado de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="4c2f9-144">Con la configuración de Service Fabric y aplicación parámetros tooin eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="4c2f9-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="4c2f9-145">EventFlow admite el uso de configuración de Service Fabric y aplicación parámetros tooconfigure EventFlow.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="4c2f9-146">Puede hacer referencia a parámetros de configuración de tejido tooService con esta sintaxis especial para los valores:</span><span class="sxs-lookup"><span data-stu-id="4c2f9-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="4c2f9-147">`<section-name>`es Hola nombre de sección de configuración de Service Fabric, hello y `<setting-name>` es valor de configuración de hello proporcionar valor Hola que será usado tooconfigure una configuración de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="4c2f9-148">más información acerca de cómo tooread toodo, vaya demasiado[compatibilidad con la configuración de Service Fabric y parámetros de la aplicación](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="4c2f9-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="4c2f9-149">Comprobación</span><span class="sxs-lookup"><span data-stu-id="4c2f9-149">Verification</span></span>

<span data-ttu-id="4c2f9-150">Iniciar el servicio y observe Hola depuración ventana de resultados de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="4c2f9-151">Una vez iniciado el servicio de hello, deberá comenzar a ver la evidencia de que el servicio envía registra la salida de toohello que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="4c2f9-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="4c2f9-152">Navegar por la plataforma de análisis y la visualización de eventos de tooyour y confirme que los registros han iniciado tooshow arriba (puede tardar unos minutos).</span><span class="sxs-lookup"><span data-stu-id="4c2f9-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c2f9-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c2f9-153">Next steps</span></span>

* [<span data-ttu-id="4c2f9-154">Análisis y visualización de eventos con Application Insights</span><span class="sxs-lookup"><span data-stu-id="4c2f9-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="4c2f9-155">Análisis y visualización de eventos con OMS</span><span class="sxs-lookup"><span data-stu-id="4c2f9-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="4c2f9-156">Documentación de EventFlow</span><span class="sxs-lookup"><span data-stu-id="4c2f9-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)