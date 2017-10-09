---
title: aaaAzure Application Insights compatibilidad con varios componentes, microservicios y contenedores | Documentos de Microsoft
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
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="07326-103">Supervisión de aplicaciones de varios componentes con Application Insights (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="07326-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="07326-104">Puede supervisar aplicaciones que consten de varios componentes, roles o servicios de servidor con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07326-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="07326-105">estado de Hola de componentes de Hola y relaciones de hello entre ellos se muestran en una sola asignación de aplicación.</span><span class="sxs-lookup"><span data-stu-id="07326-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="07326-106">Puede realizar el seguimiento de ciertas operaciones por medio de varios componentes con correlación HTTP automática.</span><span class="sxs-lookup"><span data-stu-id="07326-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="07326-107">El diagnóstico de contenedor se puede integrar y correlacionar con telemetría de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07326-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="07326-108">Utilice un único recurso de Application Insights para todos los componentes de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07326-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Asignación de aplicaciones de varios componentes](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="07326-110">Usamos 'componente' toomean aquí cualquier parte en funcionamiento de una aplicación grande.</span><span class="sxs-lookup"><span data-stu-id="07326-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="07326-111">Por ejemplo, una aplicación empresarial típico puede constar de código de cliente que se ejecuta en los exploradores web, hablando tooone o más servicios de aplicaciones web, que a su vez utilizan volver terminar los servicios.</span><span class="sxs-lookup"><span data-stu-id="07326-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="07326-112">Componentes de servidor pueden hospedarse de forma local en la nube de hello, o pueden ser roles web y trabajador de Azure o se pueden ejecutar en contenedores, como Docker o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="07326-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="07326-113">Uso compartido de un único recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="07326-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="07326-114">Hello técnica clave aquí es toosend telemetría de todos los componentes de la aplicación toohello mismo recurso de Application Insights, pero use hello `cloud_RoleName` componentes toodistinguish de propiedad cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="07326-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="07326-115">Hola Application Insights SDK agrega hello `cloud_RoleName` emiten componentes de telemetría de toohello de propiedad.</span><span class="sxs-lookup"><span data-stu-id="07326-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="07326-116">Por ejemplo, hello SDK agregará un nombre del sitio web o toohello de nombre de rol de servicio `cloud_RoleName` propiedad.</span><span class="sxs-lookup"><span data-stu-id="07326-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="07326-117">Puede invalidar este valor con un valor de telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="07326-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="07326-118">Hola asignación de la aplicación usa hello `cloud_RoleName` componentes de propiedad tooidentify hello en el mapa de Hola.</span><span class="sxs-lookup"><span data-stu-id="07326-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="07326-119">Para obtener más información acerca de cómo invalidar hello `cloud_RoleName` propiedad vea [agregar propiedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="07326-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="07326-120">En algunos casos, esto puede no ser adecuado y, quizás prefiera toouse recursos independientes para distintos grupos de componentes.</span><span class="sxs-lookup"><span data-stu-id="07326-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="07326-121">Por ejemplo, podría necesitar toouse distintos recursos para administración o con fines de facturación.</span><span class="sxs-lookup"><span data-stu-id="07326-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="07326-122">Uso de recursos independientes significa que no vea todos los componentes de hello mostrados en una sola asignación de aplicación; y que no se pueden consultar a través de los componentes de [análisis](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="07326-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="07326-123">También tiene tooset recursos independientes Hola.</span><span class="sxs-lookup"><span data-stu-id="07326-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="07326-124">Con dicha advertencia, supondremos en rest Hola de este documento que desea que los datos de toosend de varios componentes tooone recursos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="07326-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="07326-125">Configuración de aplicaciones de varios componentes</span><span class="sxs-lookup"><span data-stu-id="07326-125">Configure multi-component applications</span></span>

<span data-ttu-id="07326-126">asignar una aplicación de varios componente de tooget, deberá tooachieve estos objetivos:</span><span class="sxs-lookup"><span data-stu-id="07326-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="07326-127">**Instalar la versión preliminar más reciente de hello** paquete de Application Insights en cada componente de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="07326-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="07326-128">**Compartir un único recurso de Application Insights** de Hola a todos los componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07326-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="07326-129">**Habilitar asignación de la aplicación de varios roles** en la hoja de las vistas previas de Hola.</span><span class="sxs-lookup"><span data-stu-id="07326-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="07326-130">Configure cada componente de la aplicación utilizando el método adecuado de Hola para su tipo.</span><span class="sxs-lookup"><span data-stu-id="07326-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="07326-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) o [JavaScript](app-insights-javascript.md)).</span><span class="sxs-lookup"><span data-stu-id="07326-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="07326-132">1. Instalar paquete de versión preliminar más reciente de Hola</span><span class="sxs-lookup"><span data-stu-id="07326-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="07326-133">Actualizar o instalar paquetes de saludo visión correspondientes en el proyecto de Hola para cada componente del servidor.</span><span class="sxs-lookup"><span data-stu-id="07326-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="07326-134">Si usa Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="07326-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="07326-135">Haga clic con el botón derecho en un proyecto y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="07326-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="07326-136">Seleccione **Incluir versión preliminar**.</span><span class="sxs-lookup"><span data-stu-id="07326-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="07326-137">Si los paquetes de Application Insights aparecen en Actualizaciones, selecciónelos.</span><span class="sxs-lookup"><span data-stu-id="07326-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="07326-138">En caso contrario, buscar e instalar el paquete adecuado de hello:</span><span class="sxs-lookup"><span data-stu-id="07326-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="07326-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="07326-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="07326-140">Microsoft.ApplicationInsights.ServiceFabric: para aquellos componentes que se ejecutan como archivos ejecutables invitados y contenedores de Docker que se ejecutan en una aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07326-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="07326-141">Microsoft.ApplicationInsights.ServiceFabric.Native: para instancias de Reliable Services en las aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07326-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="07326-142">Microsoft.ApplicationInsights.Kubernetes: para componentes que se ejecutan en Docker en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="07326-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="07326-143">2. Uso compartido de un único recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="07326-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="07326-144">En Visual Studio, haga clic con el botón derecho en un proyecto y elija **Configurar Application Insights** o **Application Insights > Configurar**.</span><span class="sxs-lookup"><span data-stu-id="07326-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="07326-145">Para el primer proyecto hello, utilice Hola Asistente toocreate un recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="07326-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="07326-146">Para los proyectos posteriores, seleccione Hola mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="07326-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="07326-147">Si no hay ningún menú Application Insights, configúrelo manualmente:</span><span class="sxs-lookup"><span data-stu-id="07326-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="07326-148">En [portal de Azure](https://portal,azure.com), abra el recurso de Application Insights de Hola que ya creado para otro componente.</span><span class="sxs-lookup"><span data-stu-id="07326-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="07326-149">En hoja de información general de hello, pestaña abierta Hola desplegable Essentials y Hola copia **clave de instrumentación.**</span><span class="sxs-lookup"><span data-stu-id="07326-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="07326-150">En el proyecto, abra ApplicationInsights.config e inserte: `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="07326-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copiar el archivo .config de hello Instrumental toohello clave](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="07326-152">3. Habilitación de Asignación de aplicaciones de varios roles</span><span class="sxs-lookup"><span data-stu-id="07326-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="07326-153">Hola portal de Azure, abra el recurso de hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07326-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="07326-154">En la hoja de las vistas previas de hello, habilitar *asignación de la aplicación de varios roles*.</span><span class="sxs-lookup"><span data-stu-id="07326-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="07326-155">4. Habilitación de las métricas de Docker (opcional)</span><span class="sxs-lookup"><span data-stu-id="07326-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="07326-156">Si un componente se ejecuta en una Docker hospedada en una VM de Windows Azure, puede recopilar métricas adicionales de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="07326-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="07326-157">Inserte esto en el archivo de configuración de [Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md):</span><span class="sxs-lookup"><span data-stu-id="07326-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="07326-158">Usar cloud_RoleName tooseparate componentes</span><span class="sxs-lookup"><span data-stu-id="07326-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="07326-159">Hola `cloud_RoleName` propiedad es telemetría tooall adjunto.</span><span class="sxs-lookup"><span data-stu-id="07326-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="07326-160">Identifica el componente de hello - Hola rol o servicio - que se origina la telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="07326-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="07326-161">(Es no Hola igual como cloud_RoleInstance, que separa idénticos roles que se ejecutan en paralelo en varios procesos de servidor o equipos).</span><span class="sxs-lookup"><span data-stu-id="07326-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="07326-162">En el portal de hello, puede filtrar o segmentar la telemetría de uso de esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="07326-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="07326-163">En este ejemplo, hoja de errores de hello es tooshow filtrado sólo la información del servicio de front-end web de hello, filtrando los errores de back-end de hello API de CRM:</span><span class="sxs-lookup"><span data-stu-id="07326-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Gráfico de métricas segmentadas por Nombre del rol en la nube](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="07326-165">Seguimiento de operaciones entre componentes</span><span class="sxs-lookup"><span data-stu-id="07326-165">Trace operations between components</span></span>

<span data-ttu-id="07326-166">Puede realizar un seguimiento de un componente tooanother, llamadas de hello realizadas durante el procesamiento de una operación individual.</span><span class="sxs-lookup"><span data-stu-id="07326-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Mostrar telemetría para la operación](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="07326-168">Haga clic en tooa lista correlacionados de telemetría para realizar esta operación en el servidor de web front-end de Hola y Hola API de back-end:</span><span class="sxs-lookup"><span data-stu-id="07326-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Búsqueda entre componentes](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="07326-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07326-170">Next steps</span></span>

* [<span data-ttu-id="07326-171">Separación de telemetría de desarrollo, prueba y producción</span><span class="sxs-lookup"><span data-stu-id="07326-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
