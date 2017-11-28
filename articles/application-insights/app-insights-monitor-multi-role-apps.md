---
title: Compatibilidad de Azure Application Insights con varios componentes, microservicios y contenedores | Microsoft Docs
description: "Supervisión de aplicaciones que constan de varios componentes o roles para uso y rendimiento."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="44f0e-103">Supervisión de aplicaciones de varios componentes con Application Insights (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="44f0e-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="44f0e-104">Puede supervisar aplicaciones que consten de varios componentes, roles o servicios de servidor con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44f0e-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="44f0e-105">El mantenimiento de los componentes y las relaciones entre ellos se muestran en una sola asignación de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="44f0e-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="44f0e-106">Puede realizar el seguimiento de ciertas operaciones por medio de varios componentes con correlación HTTP automática.</span><span class="sxs-lookup"><span data-stu-id="44f0e-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="44f0e-107">El diagnóstico de contenedor se puede integrar y correlacionar con telemetría de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44f0e-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="44f0e-108">Use un único recurso de Application Insights para todos los componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44f0e-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Asignación de aplicaciones de varios componentes](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="44f0e-110">El término "componente" se usa aquí para hacer referencia a cualquier parte funcional de una aplicación grande.</span><span class="sxs-lookup"><span data-stu-id="44f0e-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="44f0e-111">Por ejemplo, una aplicación empresarial típica puede constar de código de cliente que se ejecuta en exploradores web y que se comunica con uno o varios servicios de aplicaciones web, que a su vez usan servicios back-end.</span><span class="sxs-lookup"><span data-stu-id="44f0e-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="44f0e-112">Los componentes del servidor pueden estar hospedados de forma local o en la nube, puede ser roles de trabajo o roles web de Azure, o bien pueden ejecutarse en contenedores como Docker o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="44f0e-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="44f0e-113">Uso compartido de un único recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="44f0e-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="44f0e-114">La técnica clave aquí es enviar telemetría desde cada componente de la aplicación al mismo recurso de Application Insights, pero usar la propiedad `cloud_RoleName` para distinguir entre componentes cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="44f0e-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="44f0e-115">El SDK de Application Insights agrega la propiedad `cloud_RoleName` a los componentes de telemetría para emitir.</span><span class="sxs-lookup"><span data-stu-id="44f0e-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="44f0e-116">Por ejemplo, el SDK agregará un nombre de sitio web o un nombre de rol de servicio a la propiedad `cloud_RoleName`.</span><span class="sxs-lookup"><span data-stu-id="44f0e-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="44f0e-117">Puede invalidar este valor con un valor de telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="44f0e-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="44f0e-118">El mapa de la aplicación utiliza la propiedad `cloud_RoleName` para identificar los componentes en el mapa.</span><span class="sxs-lookup"><span data-stu-id="44f0e-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="44f0e-119">Para más información acerca de cómo invalidar la propiedad `cloud_RoleName`, consulte [Incorporación de propiedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="44f0e-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="44f0e-120">En algunos casos, puede que esto no sea adecuado y quizás prefiera usar recursos independientes para distintos grupos de componentes.</span><span class="sxs-lookup"><span data-stu-id="44f0e-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="44f0e-121">Por ejemplo, podría tener que usar recursos diferentes para administración o facturación.</span><span class="sxs-lookup"><span data-stu-id="44f0e-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="44f0e-122">El uso de recursos independientes significa que no verá todos los componentes en una sola asignación de aplicaciones y que no puede realizar consultas entre componentes de [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="44f0e-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="44f0e-123">También tendrá que configurar los recursos independientes.</span><span class="sxs-lookup"><span data-stu-id="44f0e-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="44f0e-124">Con dicha advertencia, se da por supuesto en el resto de este documento que quiere enviar datos desde varios componentes a un recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="44f0e-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="44f0e-125">Configuración de aplicaciones de varios componentes</span><span class="sxs-lookup"><span data-stu-id="44f0e-125">Configure multi-component applications</span></span>

<span data-ttu-id="44f0e-126">Para obtener una asignación de aplicaciones de varios componentes, debe lograr estos objetivos:</span><span class="sxs-lookup"><span data-stu-id="44f0e-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="44f0e-127">**Instale la versión preliminar más reciente** del paquete de Application Insights en cada componente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44f0e-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="44f0e-128">**Comparta un único recurso de Application Insights** para todos los componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44f0e-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="44f0e-129">**Habilite Asignación de aplicaciones de varios roles** en la hoja Versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="44f0e-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="44f0e-130">Configure cada componente de la aplicación con el método adecuado para el tipo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="44f0e-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="44f0e-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) o [JavaScript](app-insights-javascript.md)).</span><span class="sxs-lookup"><span data-stu-id="44f0e-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="44f0e-132">1. Instalación del paquete de versión preliminar más reciente</span><span class="sxs-lookup"><span data-stu-id="44f0e-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="44f0e-133">Actualice los paquetes de Application Insights o instálelos en el proyecto para cada componente del servidor.</span><span class="sxs-lookup"><span data-stu-id="44f0e-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="44f0e-134">Si usa Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="44f0e-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="44f0e-135">Haga clic con el botón derecho en un proyecto y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="44f0e-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="44f0e-136">Seleccione **Incluir versión preliminar**.</span><span class="sxs-lookup"><span data-stu-id="44f0e-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="44f0e-137">Si los paquetes de Application Insights aparecen en Actualizaciones, selecciónelos.</span><span class="sxs-lookup"><span data-stu-id="44f0e-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="44f0e-138">De lo contrario, busque el paquete adecuado e instálelo:</span><span class="sxs-lookup"><span data-stu-id="44f0e-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="44f0e-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="44f0e-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="44f0e-140">Microsoft.ApplicationInsights.ServiceFabric: para aquellos componentes que se ejecutan como archivos ejecutables invitados y contenedores de Docker que se ejecutan en una aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="44f0e-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="44f0e-141">Microsoft.ApplicationInsights.ServiceFabric.Native: para instancias de Reliable Services en las aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="44f0e-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="44f0e-142">Microsoft.ApplicationInsights.Kubernetes: para componentes que se ejecutan en Docker en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44f0e-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="44f0e-143">2. Uso compartido de un único recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="44f0e-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="44f0e-144">En Visual Studio, haga clic con el botón derecho en un proyecto y elija **Configurar Application Insights** o **Application Insights > Configurar**.</span><span class="sxs-lookup"><span data-stu-id="44f0e-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="44f0e-145">Para el primer proyecto, use el asistente para crear un recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="44f0e-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="44f0e-146">Para proyectos posteriores, seleccione el mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="44f0e-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="44f0e-147">Si no hay ningún menú Application Insights, configúrelo manualmente:</span><span class="sxs-lookup"><span data-stu-id="44f0e-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="44f0e-148">En [Azure Portal](https://portal,azure.com), abra el recurso de Application Insights que ya creó para otro componente.</span><span class="sxs-lookup"><span data-stu-id="44f0e-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="44f0e-149">En la hoja Información general, abra la pestaña desplegable Essentials y copie el valor de **Clave de instrumentación**.</span><span class="sxs-lookup"><span data-stu-id="44f0e-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="44f0e-150">En el proyecto, abra ApplicationInsights.config e inserte: `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="44f0e-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copiar la clave de instrumentación en el archivo .config](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="44f0e-152">3. Habilitación de Asignación de aplicaciones de varios roles</span><span class="sxs-lookup"><span data-stu-id="44f0e-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="44f0e-153">En Azure Portal, abra el recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44f0e-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="44f0e-154">En la hoja Versiones preliminares, habilite *Asignación de aplicaciones de varios roles*.</span><span class="sxs-lookup"><span data-stu-id="44f0e-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="44f0e-155">4. Habilitación de las métricas de Docker (opcional)</span><span class="sxs-lookup"><span data-stu-id="44f0e-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="44f0e-156">Si un componente se ejecuta en un elemento de Docker hospedado en una máquina virtual Windows de Azure, puede recopilar métricas adicionales a partir del contenedor.</span><span class="sxs-lookup"><span data-stu-id="44f0e-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="44f0e-157">Inserte esto en el archivo de configuración de [Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md):</span><span class="sxs-lookup"><span data-stu-id="44f0e-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="44f0e-158">Uso de cloud_RoleName para separar componentes</span><span class="sxs-lookup"><span data-stu-id="44f0e-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="44f0e-159">La propiedad `cloud_RoleName` está conectada a toda la telemetría.</span><span class="sxs-lookup"><span data-stu-id="44f0e-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="44f0e-160">Identifica el componente (el rol o servicio) que origina la telemetría.</span><span class="sxs-lookup"><span data-stu-id="44f0e-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="44f0e-161">(No es lo mismo que cloud_RoleInstance, que separa roles idénticos que se ejecutan en paralelo en varios procesos de servidor o máquinas).</span><span class="sxs-lookup"><span data-stu-id="44f0e-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="44f0e-162">En el portal, puede filtrar o segmentar la telemetría mediante esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="44f0e-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="44f0e-163">En este ejemplo, la hoja Errores se filtra para mostrar solo información del servicio web front-end y oculta errores de la API de CRM de back-end:</span><span class="sxs-lookup"><span data-stu-id="44f0e-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Gráfico de métricas segmentadas por Nombre del rol en la nube](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="44f0e-165">Seguimiento de operaciones entre componentes</span><span class="sxs-lookup"><span data-stu-id="44f0e-165">Trace operations between components</span></span>

<span data-ttu-id="44f0e-166">Puede realizar el seguimiento de las llamadas realizadas durante el procesamiento de una operación concreta de un componente a otro.</span><span class="sxs-lookup"><span data-stu-id="44f0e-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![Mostrar telemetría para la operación](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="44f0e-168">Haga clic para acceder a una lista correlacionada de telemetría para esta operación en el servidor web front-end y la API de back-end:</span><span class="sxs-lookup"><span data-stu-id="44f0e-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Búsqueda entre componentes](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="44f0e-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44f0e-170">Next steps</span></span>

* [<span data-ttu-id="44f0e-171">Separación de telemetría de desarrollo, prueba y producción</span><span class="sxs-lookup"><span data-stu-id="44f0e-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
