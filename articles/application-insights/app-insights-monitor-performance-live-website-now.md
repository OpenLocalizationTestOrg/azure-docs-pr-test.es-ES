---
title: aaaMonitor un live ASP.NET web app con Azure Application Insights | Documentos de Microsoft
description: "Supervise el rendimiento de un sitio web sin volver a implementarlo. Funciona con las aplicaciones web de ASP.NET hospedadas en local, en las máquinas virtuales o en Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="e557d-104">Instrumentar aplicaciones web en tiempo de ejecución con Application Insights</span><span class="sxs-lookup"><span data-stu-id="e557d-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="e557d-105">Puede instrumentar una aplicación web en directo con Azure Application Insights, sin necesidad de toomodify o volver a implementar el código.</span><span class="sxs-lookup"><span data-stu-id="e557d-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="e557d-106">Si las aplicaciones se hospedan en un servidor IIS local, instale el Monitor de estado.</span><span class="sxs-lookup"><span data-stu-id="e557d-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="e557d-107">Aplicaciones web de Azure o ejecutar en una máquina virtual de Azure, puede activar la supervisión de Application Insights hello Azure del panel de control.</span><span class="sxs-lookup"><span data-stu-id="e557d-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="e557d-108">(También hay varios artículos sobre cómo configurar [aplicaciones web en directo de J2EE](app-insights-java-live.md) y [Azure Cloud Services](app-insights-cloudservices.md)). Necesita una suscripción a [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="e557d-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![gráficos de ejemplo](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="e557d-110">Tiene la opción de tres rutas tooapply Application Insights tooyour .NET las aplicaciones web:</span><span class="sxs-lookup"><span data-stu-id="e557d-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="e557d-111">**Tiempo de compilación:** [Hola agregar Application Insights SDK] [ greenbrown] tooyour código de la aplicación de web.</span><span class="sxs-lookup"><span data-stu-id="e557d-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="e557d-112">**Tiempo de ejecución:** instrumentar la aplicación web en el servidor de hello, tal y como se describe a continuación, sin volver a generar e implementar código de hello.</span><span class="sxs-lookup"><span data-stu-id="e557d-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="e557d-113">**Both:** compilar Hola SDK en el código de aplicación web y también se aplican las extensiones de tiempo de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="e557d-114">Obtener Hola lo mejor de ambas opciones.</span><span class="sxs-lookup"><span data-stu-id="e557d-114">Get hello best of both options.</span></span>

<span data-ttu-id="e557d-115">A continuación hay un resumen de lo que se obtiene por cada vía:</span><span class="sxs-lookup"><span data-stu-id="e557d-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="e557d-116">Tiempo de compilación</span><span class="sxs-lookup"><span data-stu-id="e557d-116">Build time</span></span> | <span data-ttu-id="e557d-117">Tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="e557d-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e557d-118">Solicitudes y excepciones</span><span class="sxs-lookup"><span data-stu-id="e557d-118">Requests & exceptions</span></span> |<span data-ttu-id="e557d-119">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-119">Yes</span></span> |<span data-ttu-id="e557d-120">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-120">Yes</span></span> |
| [<span data-ttu-id="e557d-121">Excepciones más detalladas</span><span class="sxs-lookup"><span data-stu-id="e557d-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="e557d-122">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-122">Yes</span></span> |
| [<span data-ttu-id="e557d-123">Diagnósticos de dependencia</span><span class="sxs-lookup"><span data-stu-id="e557d-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="e557d-124">En .NET 4.6 +, pero con menos detalle</span><span class="sxs-lookup"><span data-stu-id="e557d-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="e557d-125">Sí, detalles completos: códigos de resultado, texto de comandos SQL, verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="e557d-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="e557d-126">Contadores de rendimiento del sistema</span><span class="sxs-lookup"><span data-stu-id="e557d-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="e557d-127">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-127">Yes</span></span> |<span data-ttu-id="e557d-128">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-128">Yes</span></span> |
| <span data-ttu-id="e557d-129">[API para la telemetría personalizada][api]</span><span class="sxs-lookup"><span data-stu-id="e557d-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="e557d-130">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-130">Yes</span></span> |<span data-ttu-id="e557d-131">No</span><span class="sxs-lookup"><span data-stu-id="e557d-131">No</span></span> |
| [<span data-ttu-id="e557d-132">Integración del registro de seguimiento</span><span class="sxs-lookup"><span data-stu-id="e557d-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="e557d-133">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-133">Yes</span></span> |<span data-ttu-id="e557d-134">No</span><span class="sxs-lookup"><span data-stu-id="e557d-134">No</span></span> |
| [<span data-ttu-id="e557d-135">Datos de usuario y página</span><span class="sxs-lookup"><span data-stu-id="e557d-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="e557d-136">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-136">Yes</span></span> |<span data-ttu-id="e557d-137">No</span><span class="sxs-lookup"><span data-stu-id="e557d-137">No</span></span> |
| <span data-ttu-id="e557d-138">Necesita un código toorebuild</span><span class="sxs-lookup"><span data-stu-id="e557d-138">Need toorebuild code</span></span> |<span data-ttu-id="e557d-139">Sí</span><span class="sxs-lookup"><span data-stu-id="e557d-139">Yes</span></span> | <span data-ttu-id="e557d-140">No</span><span class="sxs-lookup"><span data-stu-id="e557d-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="e557d-141">Supervisión de una aplicación web de Azure activa</span><span class="sxs-lookup"><span data-stu-id="e557d-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="e557d-142">Si la aplicación se ejecuta como un servicio web de Azure, aquí de cómo tooswitch acerca de cómo supervisar:</span><span class="sxs-lookup"><span data-stu-id="e557d-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="e557d-143">Seleccionar Application Insights en panel de control de la aplicación hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="e557d-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Configuración de Application Insights para una aplicación web de Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="e557d-145">Cuando se abre la página de resumen de Application Insights de hello, haga clic en vínculo hello en hello inferior tooopen Hola completa Application Insights a recursos.</span><span class="sxs-lookup"><span data-stu-id="e557d-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Haga clic en a través de tooApplication visión](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="e557d-147">[Supervisión de aplicaciones de nube y VM](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e557d-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="e557d-148">Habilitar la supervisión de cliente en Azure</span><span class="sxs-lookup"><span data-stu-id="e557d-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="e557d-149">Si ha habilitado Application Insights en Azure, puede agregar la vista de página y la telemetría de usuario.</span><span class="sxs-lookup"><span data-stu-id="e557d-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="e557d-150">Seleccione Configuración > Configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e557d-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="e557d-151">En Configuración de la aplicación, agregue un nuevo par clave-valor:</span><span class="sxs-lookup"><span data-stu-id="e557d-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="e557d-152">Clave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="e557d-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="e557d-153">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="e557d-153">Value: `true`</span></span>
3. <span data-ttu-id="e557d-154">**Guardar** Hola configuración y **reiniciar** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e557d-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="e557d-155">Hola Application Insights JavaScript SDK ahora se aplica en cada página web.</span><span class="sxs-lookup"><span data-stu-id="e557d-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="e557d-156">Supervisión de una aplicación web de IIS activa</span><span class="sxs-lookup"><span data-stu-id="e557d-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="e557d-157">Si la aplicación se hospeda en un servidor IIS, habilite Application Insights con el Monitor de estado.</span><span class="sxs-lookup"><span data-stu-id="e557d-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="e557d-158">En el servidor web IIS, inicie sesión con las credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="e557d-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="e557d-159">Si ya no está instalado el Monitor de estado de aplicación visión, descargue y ejecute hello [instalador del Monitor de estado](http://go.microsoft.com/fwlink/?LinkId=506648) (o ejecute [instalador de plataforma Web](https://www.microsoft.com/web/downloads/platform.aspx) y busque en el mismo estado de visión de la aplicación Monitor).</span><span class="sxs-lookup"><span data-stu-id="e557d-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="e557d-160">En el Monitor de estado, seleccione aplicación web de hello instalado o el sitio Web que desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e557d-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="e557d-161">Inicie sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e557d-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="e557d-162">Configurar recursos de Hola donde desea toosee resultados de hello en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="e557d-163">(Normalmente, es mejor toocreate un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="e557d-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="e557d-164">Seleccione un recurso existente si ya tiene [pruebas web][availability] o la [supervisión de cliente][client] para esta aplicación).</span><span class="sxs-lookup"><span data-stu-id="e557d-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Elija una aplicación y un recurso.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="e557d-166">Reinicie IIS.</span><span class="sxs-lookup"><span data-stu-id="e557d-166">Restart IIS.</span></span>

    ![Elija reiniciar en parte superior de saludo del cuadro de diálogo de Hola.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="e557d-168">El servicio web se interrumpe durante un breve período.</span><span class="sxs-lookup"><span data-stu-id="e557d-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="e557d-169">Personalización de las opciones de supervisión</span><span class="sxs-lookup"><span data-stu-id="e557d-169">Customize monitoring options</span></span>

<span data-ttu-id="e557d-170">La habilitación de Application Insights agrega archivos DLL y ApplicationInsights.config tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="e557d-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="e557d-171">También puede [editar el archivo .config de hello](app-insights-configuration-with-applicationinsights-config.md) toochange algunas de las opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="e557d-172">Al volver a publicar la aplicación, vuelva a habilitar Application Insights</span><span class="sxs-lookup"><span data-stu-id="e557d-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="e557d-173">Antes de volver a publicar la aplicación, considere la posibilidad de [agregar código de toohello de Application Insights en Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="e557d-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="e557d-174">Obtendrá más detallada telemetría y telemetría personalizada de hello capacidad toowrite.</span><span class="sxs-lookup"><span data-stu-id="e557d-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="e557d-175">Si desea que toore-publicar sin agregar Application Insights toohello código, tenga en cuenta que el proceso de implementación de hello puede eliminar archivos DLL de Hola y ApplicationInsights.config de hello Publicar sitio web.</span><span class="sxs-lookup"><span data-stu-id="e557d-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="e557d-176">Por lo tanto:</span><span class="sxs-lookup"><span data-stu-id="e557d-176">Therefore:</span></span>

1. <span data-ttu-id="e557d-177">Si edita el archivo ApplicationInsights.config, realice una copia del mismo antes de volver a publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e557d-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="e557d-178">Vuelva a publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e557d-178">Republish your app.</span></span>
3. <span data-ttu-id="e557d-179">Vuelva a habilitar la supervisión de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e557d-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="e557d-180">(Use el método adecuado de hello: panel de control de aplicación web de Azure de Hola u Hola Monitor de estado en un host IIS.)</span><span class="sxs-lookup"><span data-stu-id="e557d-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="e557d-181">Volver a aplicar las modificaciones realizadas en el archivo .config de Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="e557d-182">Solución de problemas de configuración en tiempo de ejecución de Application Insights</span><span class="sxs-lookup"><span data-stu-id="e557d-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="e557d-183">¿No se puede conectar?</span><span class="sxs-lookup"><span data-stu-id="e557d-183">Can't connect?</span></span> <span data-ttu-id="e557d-184">¿No hay telemetría?</span><span class="sxs-lookup"><span data-stu-id="e557d-184">No telemetry?</span></span>

* <span data-ttu-id="e557d-185">Abra [Hola puertos salientes necesarios](app-insights-ip-addresses.md#outgoing-ports) en toowork de Monitor de estado de su servidor firewall tooallow.</span><span class="sxs-lookup"><span data-stu-id="e557d-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="e557d-186">Abrir el Monitor de estado y seleccione la aplicación en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="e557d-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="e557d-187">Compruebe si hay algún mensaje de diagnóstico para esta aplicación en la sección "Notificaciones de configuración" hello:</span><span class="sxs-lookup"><span data-stu-id="e557d-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Abra la solicitud de toosee de hoja de rendimiento de hello, tiempo de respuesta, dependencias y otros datos](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="e557d-189">En el servidor de hello, si ve un mensaje de "permisos insuficientes", pruebe siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e557d-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="e557d-190">En el Administrador de IIS, seleccione el grupo de aplicaciones, abra **configuración avanzada**y en **modelo de proceso** tenga en cuenta Hola identidad.</span><span class="sxs-lookup"><span data-stu-id="e557d-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="e557d-191">En el panel de control de administración de equipo, agregue este grupo de usuarios del Monitor de rendimiento de toohello de identidad.</span><span class="sxs-lookup"><span data-stu-id="e557d-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="e557d-192">Si tiene instalado MMA/SCOM (Systems Center Operation Manager) en el servidor, algunas versiones pueden entrar en conflicto.</span><span class="sxs-lookup"><span data-stu-id="e557d-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="e557d-193">Desinstalar SCOM y Monitor de estado y volver a instalar versiones más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="e557d-194">Consulte [Solución de problemas][qna].</span><span class="sxs-lookup"><span data-stu-id="e557d-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="e557d-195">Requisitos del sistema</span><span class="sxs-lookup"><span data-stu-id="e557d-195">System Requirements</span></span>
<span data-ttu-id="e557d-196">Compatibilidad de sistema operativo para el Monitor de estado de Application Insights en servidor:</span><span class="sxs-lookup"><span data-stu-id="e557d-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="e557d-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="e557d-197">Windows Server 2008</span></span>
* <span data-ttu-id="e557d-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="e557d-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="e557d-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e557d-199">Windows Server 2012</span></span>
* <span data-ttu-id="e557d-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e557d-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="e557d-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e557d-201">Windows Server 2016</span></span>

<span data-ttu-id="e557d-202">con el último Service Pack y .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e557d-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="e557d-203">En el lado del cliente de hello: Windows 7, 8, 8.1 y 10, con .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e557d-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="e557d-204">La compatibilidad de IIS es: IIS 7, 7.5, 8 y 8.5 (se requiere IIS)</span><span class="sxs-lookup"><span data-stu-id="e557d-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="e557d-205">Automatización con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e557d-205">Automation with PowerShell</span></span>
<span data-ttu-id="e557d-206">Puede iniciar y detener la supervisión mediante PowerShell en el servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="e557d-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="e557d-207">Importar módulo de Application Insights de hello en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="e557d-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="e557d-208">Encuentre las aplicaciones en supervisión:</span><span class="sxs-lookup"><span data-stu-id="e557d-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="e557d-209">`-Name`Nombre de hello (opcional) de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e557d-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="e557d-210">Muestra Hola estado de supervisión de Application Insights para cada aplicación web (u Hola con el nombre de aplicación) en este servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="e557d-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="e557d-211">Devuelve `ApplicationInsightsApplication` para cada aplicación:</span><span class="sxs-lookup"><span data-stu-id="e557d-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="e557d-212">`SdkState==EnabledAfterDeployment`: La aplicación se está supervisando y se ha instrumentado en tiempo de ejecución mediante la herramienta Monitor de estado de hello, o por `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="e557d-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="e557d-213">`SdkState==Disabled`: no se ha instrumentado aplicación hello para Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e557d-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="e557d-214">Nunca se ha instrumentado o se deshabilitó la supervisión de tiempo de ejecución con la herramienta Monitor de estado de Hola o con `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="e557d-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="e557d-215">`SdkState==EnabledByCodeInstrumentation`: se ha instrumentado aplicación hello mediante la adición de código fuente de hello SDK toohello.</span><span class="sxs-lookup"><span data-stu-id="e557d-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="e557d-216">El SDK no se puede actualizar ni detener.</span><span class="sxs-lookup"><span data-stu-id="e557d-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="e557d-217">`SdkVersion`Muestra la versión de Hola en uso para la supervisión de esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="e557d-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="e557d-218">`LatestAvailableSdkVersion`Muestra la versión de Hola actualmente disponible en la Galería de NuGet Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="e557d-219">versión de toothis aplicación tooupgrade hello, use `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="e557d-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="e557d-220">`-Name`nombre de saludo de la aplicación hello en IIS</span><span class="sxs-lookup"><span data-stu-id="e557d-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="e557d-221">`-InstrumentationKey`Hola ikey de hello donde desea hello toobe de resultados muestra el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e557d-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="e557d-222">Este cmdlet solo afecta a las aplicaciones que no se han instrumentado, es decir, aquellas cuyo SdkState == NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="e557d-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="e557d-223">Hola cmdlet no afecta a una aplicación que ya se ha instrumentado.</span><span class="sxs-lookup"><span data-stu-id="e557d-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="e557d-224">No importa si se ha instrumentado aplicación hello en tiempo de compilación mediante la adición de código de hello SDK toohello o en tiempo de ejecución por un uso anterior de este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e557d-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="e557d-225">Hola SDK versión utilizada tooinstrument Hola aplicación es server toothis de descarga de la versión de Hola último.</span><span class="sxs-lookup"><span data-stu-id="e557d-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="e557d-226">versión más reciente de toodownload hello, use Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="e557d-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="e557d-227">Si se descarga correctamente, devuelve `ApplicationInsightsApplication` .</span><span class="sxs-lookup"><span data-stu-id="e557d-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="e557d-228">Si se produce un error, registra un toostderr de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="e557d-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="e557d-229">`-Name`nombre de Hola de una aplicación en IIS</span><span class="sxs-lookup"><span data-stu-id="e557d-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="e557d-230">`-All` Detiene la supervisión de todas las aplicaciones en este servidor IIS con `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="e557d-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="e557d-231">Detiene la supervisión de hello aplicaciones especificadas y quita la instrumentación.</span><span class="sxs-lookup"><span data-stu-id="e557d-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="e557d-232">Solo funciona para las aplicaciones que se han instrumentado en tiempo de ejecución mediante Hola herramienta de supervisión de estado o ApplicationInsightsApplication de inicio.</span><span class="sxs-lookup"><span data-stu-id="e557d-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="e557d-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="e557d-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="e557d-234">Devuelve ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="e557d-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="e557d-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="e557d-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="e557d-236">`-Name`: nombre de Hola de una aplicación web en IIS.</span><span class="sxs-lookup"><span data-stu-id="e557d-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="e557d-237">`-InstrumentationKey` (Opcional). Use que este toochange Hola recursos toowhich Hola telemetría de la aplicación se envía.</span><span class="sxs-lookup"><span data-stu-id="e557d-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="e557d-238">Este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e557d-238">This cmdlet:</span></span>
  * <span data-ttu-id="e557d-239">Hola de actualizaciones con el nombre de versión de toohello la aplicación de hello SDK descargada más recientemente toothis máquina.</span><span class="sxs-lookup"><span data-stu-id="e557d-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="e557d-240">(Solo funciona si `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="e557d-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="e557d-241">Si proporciona una clave de instrumentación, Hola con el nombre de aplicación es toosend ha vuelto a configurar telemetría toohello recursos con esa clave.</span><span class="sxs-lookup"><span data-stu-id="e557d-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="e557d-242">(Funciona si `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="e557d-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="e557d-243">Descarga el servidor de toohello de Application Insights SDK más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="e557d-244"><a name="questions"></a>Preguntas acerca del Monitor de estado</span><span class="sxs-lookup"><span data-stu-id="e557d-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="e557d-245">¿Qué es el Monitor de estado?</span><span class="sxs-lookup"><span data-stu-id="e557d-245">What is Status Monitor?</span></span>

<span data-ttu-id="e557d-246">Una aplicación de escritorio que se instala en el servidor web de IIS.</span><span class="sxs-lookup"><span data-stu-id="e557d-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="e557d-247">Le ayuda a instrumentar y configurar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="e557d-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="e557d-248">¿Cuándo puedo usar el Monitor de estado?</span><span class="sxs-lookup"><span data-stu-id="e557d-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="e557d-249">tooinstrument cualquier aplicación que se ejecuta en el servidor IIS - de web incluso si ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="e557d-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="e557d-250">tooenable telemetría adicionales para las aplicaciones web que se han [compiladas con hello Application Insights SDK](app-insights-asp-net.md) en tiempo de compilación.</span><span class="sxs-lookup"><span data-stu-id="e557d-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="e557d-251">¿Puedo cerrarlo después de ejecutarlo?</span><span class="sxs-lookup"><span data-stu-id="e557d-251">Can I close it after it runs?</span></span>

<span data-ttu-id="e557d-252">Sí.</span><span class="sxs-lookup"><span data-stu-id="e557d-252">Yes.</span></span> <span data-ttu-id="e557d-253">Una vez se ha instrumentado sitios Web de Hola que seleccione, puede cerrarlo.</span><span class="sxs-lookup"><span data-stu-id="e557d-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="e557d-254">No recopila telemetría por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="e557d-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="e557d-255">Simplemente configura las aplicaciones web hello y establece algunos permisos.</span><span class="sxs-lookup"><span data-stu-id="e557d-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="e557d-256">¿Qué hace el Monitor de estado?</span><span class="sxs-lookup"><span data-stu-id="e557d-256">What does Status Monitor do?</span></span>

<span data-ttu-id="e557d-257">Al seleccionar una aplicación web para tooinstrument de Monitor de estado:</span><span class="sxs-lookup"><span data-stu-id="e557d-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="e557d-258">Descarga y coloca ensamblados de Application Insights de Hola y el archivo .config en carpeta de archivos binarios de la aplicación hello web.</span><span class="sxs-lookup"><span data-stu-id="e557d-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="e557d-259">Modifica `web.config` módulo de seguimiento de información de aplicaciones HTTP tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="e557d-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="e557d-260">Permite llamadas de dependencia toocollect de generación de perfiles de CLR.</span><span class="sxs-lookup"><span data-stu-id="e557d-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="e557d-261">¿Es necesario toorun Monitor de estado cada vez que actualice la aplicación hello?</span><span class="sxs-lookup"><span data-stu-id="e557d-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="e557d-262">No si reimplementa de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="e557d-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="e557d-263">Si seleccionó la opción de 'eliminar los archivos existentes' de Hola Hola proceso de publicación, necesitaría toore y ejecutar el Monitor de estado tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e557d-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="e557d-264">¿Qué telemetría se recopila?</span><span class="sxs-lookup"><span data-stu-id="e557d-264">What telemetry is collected?</span></span>

<span data-ttu-id="e557d-265">En el caso de las aplicaciones que instrumenta solo en tiempo de ejecución mediante el Monitor de estado:</span><span class="sxs-lookup"><span data-stu-id="e557d-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="e557d-266">Solicitudes HTTP</span><span class="sxs-lookup"><span data-stu-id="e557d-266">HTTP requests</span></span>
* <span data-ttu-id="e557d-267">Llamadas toodependencies</span><span class="sxs-lookup"><span data-stu-id="e557d-267">Calls toodependencies</span></span>
* <span data-ttu-id="e557d-268">Excepciones</span><span class="sxs-lookup"><span data-stu-id="e557d-268">Exceptions</span></span>
* <span data-ttu-id="e557d-269">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e557d-269">Performance counters</span></span>

<span data-ttu-id="e557d-270">En el caso de las aplicaciones ya instrumentadas en el momento de la compilación:</span><span class="sxs-lookup"><span data-stu-id="e557d-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="e557d-271">Contadores de proceso.</span><span class="sxs-lookup"><span data-stu-id="e557d-271">Process counters.</span></span>
 * <span data-ttu-id="e557d-272">Llamadas de dependencia (.NET 4.5); valores devueltos en las llamadas de dependencia (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="e557d-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="e557d-273">Valores de seguimiento de la pila de excepción.</span><span class="sxs-lookup"><span data-stu-id="e557d-273">Exception stack trace values.</span></span>

[<span data-ttu-id="e557d-274">Más información</span><span class="sxs-lookup"><span data-stu-id="e557d-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="e557d-275">Vídeo</span><span class="sxs-lookup"><span data-stu-id="e557d-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="e557d-276"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e557d-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="e557d-277">Vea la telemetría:</span><span class="sxs-lookup"><span data-stu-id="e557d-277">View your telemetry:</span></span>

* <span data-ttu-id="e557d-278">[Explorar las métricas](app-insights-metrics-explorer.md) toomonitor rendimiento y uso</span><span class="sxs-lookup"><span data-stu-id="e557d-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="e557d-279">[Buscar eventos y registros] [ diagnostic] toodiagnose problemas</span><span class="sxs-lookup"><span data-stu-id="e557d-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="e557d-280">[Análisis](app-insights-analytics.md) para más consultas avanzadas</span><span class="sxs-lookup"><span data-stu-id="e557d-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="e557d-281">Creación de paneles</span><span class="sxs-lookup"><span data-stu-id="e557d-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="e557d-282">Agregue más telemetría:</span><span class="sxs-lookup"><span data-stu-id="e557d-282">Add more telemetry:</span></span>

* <span data-ttu-id="e557d-283">[Crear pruebas web] [ availability] toomake seguro el sitio permanece activo.</span><span class="sxs-lookup"><span data-stu-id="e557d-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="e557d-284">[Agregar telemetría de cliente web] [ usage] toosee excepciones de código de la página web y toolet insertar seguimiento de llamadas.</span><span class="sxs-lookup"><span data-stu-id="e557d-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="e557d-285">[Agregar código de aplicación visión SDK tooyour] [ greenbrown] para que pueda insertar seguimiento y registrar las llamadas</span><span class="sxs-lookup"><span data-stu-id="e557d-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
