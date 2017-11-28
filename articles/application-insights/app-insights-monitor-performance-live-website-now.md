---
title: "Supervisión de una aplicación web de ASP.NET con Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="50caa-104">Instrumentar aplicaciones web en tiempo de ejecución con Application Insights</span><span class="sxs-lookup"><span data-stu-id="50caa-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="50caa-105">Puede instrumentar una aplicación web activa con Azure Application Insights sin tener que modificar ni volver a implementar el código.</span><span class="sxs-lookup"><span data-stu-id="50caa-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="50caa-106">Si las aplicaciones se hospedan en un servidor IIS local, instale el Monitor de estado.</span><span class="sxs-lookup"><span data-stu-id="50caa-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="50caa-107">Si son aplicaciones web de Azure o se ejecutan en una máquina virtual de Azure, puede activar la supervisión de Application Insights en el panel de control de Azure.</span><span class="sxs-lookup"><span data-stu-id="50caa-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="50caa-108">(También hay varios artículos sobre cómo configurar [aplicaciones web en directo de J2EE](app-insights-java-live.md) y [Azure Cloud Services](app-insights-cloudservices.md)). Necesita una suscripción a [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="50caa-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![gráficos de ejemplo](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="50caa-110">Puede optar entre tres vías de aplicar Application Insights a sus aplicaciones web .NET:</span><span class="sxs-lookup"><span data-stu-id="50caa-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="50caa-111">**Tiempo de compilación:** [agregue el SDK de Application Insights][greenbrown] al código de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="50caa-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="50caa-112">**Tiempo de ejecución:** instrumenta la aplicación web en el servidor, como se describe a continuación, sin volver a generar e implementar el código.</span><span class="sxs-lookup"><span data-stu-id="50caa-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="50caa-113">**Ambos:** compila el SDK en el código de aplicación web y aplica las extensiones del sistema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="50caa-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="50caa-114">Obtenga lo mejor de ambas opciones.</span><span class="sxs-lookup"><span data-stu-id="50caa-114">Get the best of both options.</span></span>

<span data-ttu-id="50caa-115">A continuación hay un resumen de lo que se obtiene por cada vía:</span><span class="sxs-lookup"><span data-stu-id="50caa-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="50caa-116">Tiempo de compilación</span><span class="sxs-lookup"><span data-stu-id="50caa-116">Build time</span></span> | <span data-ttu-id="50caa-117">Tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="50caa-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50caa-118">Solicitudes y excepciones</span><span class="sxs-lookup"><span data-stu-id="50caa-118">Requests & exceptions</span></span> |<span data-ttu-id="50caa-119">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-119">Yes</span></span> |<span data-ttu-id="50caa-120">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-120">Yes</span></span> |
| [<span data-ttu-id="50caa-121">Excepciones más detalladas</span><span class="sxs-lookup"><span data-stu-id="50caa-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="50caa-122">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-122">Yes</span></span> |
| [<span data-ttu-id="50caa-123">Diagnósticos de dependencia</span><span class="sxs-lookup"><span data-stu-id="50caa-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="50caa-124">En .NET 4.6 +, pero con menos detalle</span><span class="sxs-lookup"><span data-stu-id="50caa-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="50caa-125">Sí, detalles completos: códigos de resultado, texto de comandos SQL, verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="50caa-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="50caa-126">Contadores de rendimiento del sistema</span><span class="sxs-lookup"><span data-stu-id="50caa-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="50caa-127">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-127">Yes</span></span> |<span data-ttu-id="50caa-128">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-128">Yes</span></span> |
| <span data-ttu-id="50caa-129">[API para la telemetría personalizada][api]</span><span class="sxs-lookup"><span data-stu-id="50caa-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="50caa-130">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-130">Yes</span></span> |<span data-ttu-id="50caa-131">No</span><span class="sxs-lookup"><span data-stu-id="50caa-131">No</span></span> |
| [<span data-ttu-id="50caa-132">Integración del registro de seguimiento</span><span class="sxs-lookup"><span data-stu-id="50caa-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="50caa-133">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-133">Yes</span></span> |<span data-ttu-id="50caa-134">No</span><span class="sxs-lookup"><span data-stu-id="50caa-134">No</span></span> |
| [<span data-ttu-id="50caa-135">Datos de usuario y página</span><span class="sxs-lookup"><span data-stu-id="50caa-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="50caa-136">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-136">Yes</span></span> |<span data-ttu-id="50caa-137">No</span><span class="sxs-lookup"><span data-stu-id="50caa-137">No</span></span> |
| <span data-ttu-id="50caa-138">Es necesario volver a compilar el código</span><span class="sxs-lookup"><span data-stu-id="50caa-138">Need to rebuild code</span></span> |<span data-ttu-id="50caa-139">Sí</span><span class="sxs-lookup"><span data-stu-id="50caa-139">Yes</span></span> | <span data-ttu-id="50caa-140">No</span><span class="sxs-lookup"><span data-stu-id="50caa-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="50caa-141">Supervisión de una aplicación web de Azure activa</span><span class="sxs-lookup"><span data-stu-id="50caa-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="50caa-142">Si la aplicación se ejecuta como un servicio web de Azure, aquí se muestra cómo cambiar de supervisión:</span><span class="sxs-lookup"><span data-stu-id="50caa-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="50caa-143">En el panel de control de la aplicación en Azure, seleccione Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Configuración de Application Insights para una aplicación web de Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="50caa-145">Cuando se abre la página de resumen de Application Insights, haga clic en el vínculo situado en la parte inferior para abrir el recurso completo de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Recorrido por Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="50caa-147">[Supervisión de aplicaciones de nube y VM](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="50caa-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="50caa-148">Habilitar la supervisión de cliente en Azure</span><span class="sxs-lookup"><span data-stu-id="50caa-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="50caa-149">Si ha habilitado Application Insights en Azure, puede agregar la vista de página y la telemetría de usuario.</span><span class="sxs-lookup"><span data-stu-id="50caa-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="50caa-150">Seleccione Configuración > Configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50caa-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="50caa-151">En Configuración de la aplicación, agregue un nuevo par clave-valor:</span><span class="sxs-lookup"><span data-stu-id="50caa-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="50caa-152">Clave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="50caa-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="50caa-153">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="50caa-153">Value: `true`</span></span>
3. <span data-ttu-id="50caa-154">**Guarde** la configuración y **reinicie** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50caa-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="50caa-155">El SDK de JavaScript de Application Insights ahora se inserta en cada página web.</span><span class="sxs-lookup"><span data-stu-id="50caa-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="50caa-156">Supervisión de una aplicación web de IIS activa</span><span class="sxs-lookup"><span data-stu-id="50caa-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="50caa-157">Si la aplicación se hospeda en un servidor IIS, habilite Application Insights con el Monitor de estado.</span><span class="sxs-lookup"><span data-stu-id="50caa-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="50caa-158">En el servidor web IIS, inicie sesión con las credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="50caa-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="50caa-159">Si el Monitor de estado de Application Insights no está instalado aún, descargue y ejecute el [instalador del Monitor de estado](http://go.microsoft.com/fwlink/?LinkId=506648) (o ejecute [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) y busque en él el Monitor de estado de Application Insights).</span><span class="sxs-lookup"><span data-stu-id="50caa-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="50caa-160">En el Monitor de estado, seleccione la aplicación web instalada o el sitio web que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="50caa-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="50caa-161">Inicie sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="50caa-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="50caa-162">Configure el recurso donde desee ver los resultados en el portal de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="50caa-163">(Normalmente, es mejor crear un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="50caa-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="50caa-164">Seleccione un recurso existente si ya tiene [pruebas web][availability] o la [supervisión de cliente][client] para esta aplicación).</span><span class="sxs-lookup"><span data-stu-id="50caa-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Elija una aplicación y un recurso.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="50caa-166">Reinicie IIS.</span><span class="sxs-lookup"><span data-stu-id="50caa-166">Restart IIS.</span></span>

    ![Seleccione Reiniciar en la parte superior del cuadro de diálogo.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="50caa-168">El servicio web se interrumpe durante un breve período.</span><span class="sxs-lookup"><span data-stu-id="50caa-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="50caa-169">Personalización de las opciones de supervisión</span><span class="sxs-lookup"><span data-stu-id="50caa-169">Customize monitoring options</span></span>

<span data-ttu-id="50caa-170">Si se habilita Application Insights, se agregan archivos DLL y ApplicationInsights.config a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="50caa-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="50caa-171">También puede [editar el archivo .config](app-insights-configuration-with-applicationinsights-config.md) para cambiar algunas de las opciones.</span><span class="sxs-lookup"><span data-stu-id="50caa-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="50caa-172">Al volver a publicar la aplicación, vuelva a habilitar Application Insights</span><span class="sxs-lookup"><span data-stu-id="50caa-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="50caa-173">Antes de volver a publicar la aplicación, considere la posibilidad de [agregar Application Insights al código de Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="50caa-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="50caa-174">Obtendrá una telemetría más detallada y la capacidad para escribir telemetría personalizada.</span><span class="sxs-lookup"><span data-stu-id="50caa-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="50caa-175">Si desea volver a publicar sin agregar Application Insights al código, tenga en cuenta que el proceso de implementación puede eliminar los archivos DLL y ApplicationInsights.config desde el sitio web publicado.</span><span class="sxs-lookup"><span data-stu-id="50caa-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="50caa-176">Por lo tanto:</span><span class="sxs-lookup"><span data-stu-id="50caa-176">Therefore:</span></span>

1. <span data-ttu-id="50caa-177">Si edita el archivo ApplicationInsights.config, realice una copia del mismo antes de volver a publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50caa-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="50caa-178">Vuelva a publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50caa-178">Republish your app.</span></span>
3. <span data-ttu-id="50caa-179">Vuelva a habilitar la supervisión de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="50caa-180">(Use el método adecuado: ya sea el panel de control de la aplicación web de Azure o el Monitor de estado en un host IIS).</span><span class="sxs-lookup"><span data-stu-id="50caa-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="50caa-181">Restablezca las modificaciones realizadas en el archivo .config.</span><span class="sxs-lookup"><span data-stu-id="50caa-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="50caa-182">Solución de problemas de configuración en tiempo de ejecución de Application Insights</span><span class="sxs-lookup"><span data-stu-id="50caa-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="50caa-183">¿No se puede conectar?</span><span class="sxs-lookup"><span data-stu-id="50caa-183">Can't connect?</span></span> <span data-ttu-id="50caa-184">¿No hay telemetría?</span><span class="sxs-lookup"><span data-stu-id="50caa-184">No telemetry?</span></span>

* <span data-ttu-id="50caa-185">Abra los [puertos de salida necesarios](app-insights-ip-addresses.md#outgoing-ports) en el firewall del servidor para que el Monitor de estado funcione.</span><span class="sxs-lookup"><span data-stu-id="50caa-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="50caa-186">Abrir el Monitor de estado y seleccione la aplicación en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="50caa-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="50caa-187">Compruebe si hay algún mensaje de diagnóstico para esta aplicación en la sección "Notificaciones de configuración":</span><span class="sxs-lookup"><span data-stu-id="50caa-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![Abra la hoja Rendimiento para ver la solicitud, el tiempo de respuesta, la dependencia y otros datos.](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="50caa-189">En el servidor, si ve en un mensaje acerca de "permisos insuficientes", intente lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="50caa-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="50caa-190">En el Administrador de IIS, seleccione el grupo de aplicaciones, abra **Configuración avanzada** y en **Modelo de proceso**, anote la identidad.</span><span class="sxs-lookup"><span data-stu-id="50caa-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="50caa-191">En el panel de control de administración del equipo, agregue esta identidad al grupo Usuarios del monitor de sistema.</span><span class="sxs-lookup"><span data-stu-id="50caa-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="50caa-192">Si tiene instalado MMA/SCOM (Systems Center Operation Manager) en el servidor, algunas versiones pueden entrar en conflicto.</span><span class="sxs-lookup"><span data-stu-id="50caa-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="50caa-193">Desinstale SCOM y el Monitor de estado y vuelva a instalar las versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="50caa-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="50caa-194">Consulte [Solución de problemas][qna].</span><span class="sxs-lookup"><span data-stu-id="50caa-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="50caa-195">Requisitos del sistema</span><span class="sxs-lookup"><span data-stu-id="50caa-195">System Requirements</span></span>
<span data-ttu-id="50caa-196">Compatibilidad de sistema operativo para el Monitor de estado de Application Insights en servidor:</span><span class="sxs-lookup"><span data-stu-id="50caa-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="50caa-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="50caa-197">Windows Server 2008</span></span>
* <span data-ttu-id="50caa-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="50caa-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="50caa-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="50caa-199">Windows Server 2012</span></span>
* <span data-ttu-id="50caa-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="50caa-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="50caa-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="50caa-201">Windows Server 2016</span></span>

<span data-ttu-id="50caa-202">con el último Service Pack y .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="50caa-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="50caa-203">En el lado de cliente: Windows 7, 8, 8.1 y 10, de nuevo con .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="50caa-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="50caa-204">La compatibilidad de IIS es: IIS 7, 7.5, 8 y 8.5 (se requiere IIS)</span><span class="sxs-lookup"><span data-stu-id="50caa-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="50caa-205">Automatización con PowerShell</span><span class="sxs-lookup"><span data-stu-id="50caa-205">Automation with PowerShell</span></span>
<span data-ttu-id="50caa-206">Puede iniciar y detener la supervisión mediante PowerShell en el servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="50caa-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="50caa-207">En primer lugar, importe el módulo de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="50caa-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="50caa-208">Encuentre las aplicaciones en supervisión:</span><span class="sxs-lookup"><span data-stu-id="50caa-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="50caa-209">`-Name` (Opcional) Nombre de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="50caa-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="50caa-210">Muestra el estado de supervisión de Application Insights para cada aplicación web (u otra aplicación con nombre) en este servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="50caa-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="50caa-211">Devuelve `ApplicationInsightsApplication` para cada aplicación:</span><span class="sxs-lookup"><span data-stu-id="50caa-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="50caa-212">`SdkState==EnabledAfterDeployment`: la aplicación se está supervisando y se ha instrumentado en tiempo de ejecución, ya sea con la herramienta Monitor de estado o con `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="50caa-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="50caa-213">`SdkState==Disabled`: la aplicación no se ha instrumentado para Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="50caa-214">Nunca se ha instrumentado, o bien se deshabilitó la supervisión en tiempo de ejecución con la herramienta Monitor de estado o con `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="50caa-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="50caa-215">`SdkState==EnabledByCodeInstrumentation`: se ha instrumentado la aplicación agregando el SDK al código fuente.</span><span class="sxs-lookup"><span data-stu-id="50caa-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="50caa-216">El SDK no se puede actualizar ni detener.</span><span class="sxs-lookup"><span data-stu-id="50caa-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="50caa-217">`SdkVersion` muestra la versión en uso para la supervisión de esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="50caa-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="50caa-218">`LatestAvailableSdkVersion`muestra la versión disponible en la galería de NuGet.</span><span class="sxs-lookup"><span data-stu-id="50caa-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="50caa-219">Para actualizar la aplicación a esta versión, use `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="50caa-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="50caa-220">`-Name` El nombre de la aplicación en IIS</span><span class="sxs-lookup"><span data-stu-id="50caa-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="50caa-221">`-InstrumentationKey` El valor ikey del recurso de Application Insights donde quiere que se muestren los resultados.</span><span class="sxs-lookup"><span data-stu-id="50caa-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="50caa-222">Este cmdlet solo afecta a las aplicaciones que no se han instrumentado, es decir, aquellas cuyo SdkState == NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="50caa-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="50caa-223">El cmdlet no afecta a una aplicación que ya se ha instrumentado.</span><span class="sxs-lookup"><span data-stu-id="50caa-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="50caa-224">No importa que se instrumentara en tiempo de compilación mediante la adición del SDK al código, o en tiempo de ejecución mediante un uso anterior de este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50caa-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="50caa-225">La versión del SDK utilizada para instrumentar la aplicación es la versión que se ha descargado más recientemente en este servidor.</span><span class="sxs-lookup"><span data-stu-id="50caa-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="50caa-226">Para descargar la versión más reciente, use Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="50caa-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="50caa-227">Si se descarga correctamente, devuelve `ApplicationInsightsApplication` .</span><span class="sxs-lookup"><span data-stu-id="50caa-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="50caa-228">Si se produce un error, inicia un seguimiento a stderr.</span><span class="sxs-lookup"><span data-stu-id="50caa-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="50caa-229">`-Name` El nombre de una aplicación en IIS</span><span class="sxs-lookup"><span data-stu-id="50caa-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="50caa-230">`-All` Detiene la supervisión de todas las aplicaciones en este servidor IIS con `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="50caa-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="50caa-231">Detiene la supervisión de las aplicaciones especificadas y quita la instrumentación.</span><span class="sxs-lookup"><span data-stu-id="50caa-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="50caa-232">Solo funciona para las aplicaciones que se han instrumentado en tiempo de ejecución con la herramienta Monitor de estado o Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="50caa-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="50caa-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="50caa-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="50caa-234">Devuelve ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="50caa-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="50caa-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="50caa-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="50caa-236">`-Name`: el nombre de la aplicación web en IIS.</span><span class="sxs-lookup"><span data-stu-id="50caa-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="50caa-237">`-InstrumentationKey` (Opcional). Utilice esto para cambiar el recurso al que se envía la telemetría de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50caa-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="50caa-238">Este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50caa-238">This cmdlet:</span></span>
  * <span data-ttu-id="50caa-239">Permite actualizar la aplicación con nombre a la versión del SDK descargada más recientemente en este equipo.</span><span class="sxs-lookup"><span data-stu-id="50caa-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="50caa-240">(Solo funciona si `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="50caa-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="50caa-241">Si proporciona una clave de instrumentación, se vuelve a configurar la aplicación con nombre para enviar los datos de telemetría al recurso con esa clave.</span><span class="sxs-lookup"><span data-stu-id="50caa-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="50caa-242">(Funciona si `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="50caa-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="50caa-243">Permite descargar el SDK más reciente de Application Insights en el servidor.</span><span class="sxs-lookup"><span data-stu-id="50caa-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="50caa-244"><a name="questions"></a>Preguntas acerca del Monitor de estado</span><span class="sxs-lookup"><span data-stu-id="50caa-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="50caa-245">¿Qué es el Monitor de estado?</span><span class="sxs-lookup"><span data-stu-id="50caa-245">What is Status Monitor?</span></span>

<span data-ttu-id="50caa-246">Una aplicación de escritorio que se instala en el servidor web de IIS.</span><span class="sxs-lookup"><span data-stu-id="50caa-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="50caa-247">Le ayuda a instrumentar y configurar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="50caa-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="50caa-248">¿Cuándo puedo usar el Monitor de estado?</span><span class="sxs-lookup"><span data-stu-id="50caa-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="50caa-249">Para instrumentar cualquier aplicación web que se ejecute en el servidor IIS, incluso si ya se está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="50caa-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="50caa-250">Para habilitar la telemetría adicional para las aplicaciones web que se han [compilado con el SDK de Application Insights](app-insights-asp-net.md) en el momento de la compilación.</span><span class="sxs-lookup"><span data-stu-id="50caa-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="50caa-251">¿Puedo cerrarlo después de ejecutarlo?</span><span class="sxs-lookup"><span data-stu-id="50caa-251">Can I close it after it runs?</span></span>

<span data-ttu-id="50caa-252">Sí.</span><span class="sxs-lookup"><span data-stu-id="50caa-252">Yes.</span></span> <span data-ttu-id="50caa-253">Una vez que se hayan instrumentado los sitios web seleccionados, puede cerrarlo.</span><span class="sxs-lookup"><span data-stu-id="50caa-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="50caa-254">No recopila telemetría por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="50caa-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="50caa-255">Simplemente configura las aplicaciones web y establece algunos permisos.</span><span class="sxs-lookup"><span data-stu-id="50caa-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="50caa-256">¿Qué hace el Monitor de estado?</span><span class="sxs-lookup"><span data-stu-id="50caa-256">What does Status Monitor do?</span></span>

<span data-ttu-id="50caa-257">Cuando selecciona una aplicación web para instrumentarla con el Monitor de estado:</span><span class="sxs-lookup"><span data-stu-id="50caa-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="50caa-258">Descarga y coloca los ensamblados de Application Insights y el archivo .config en la carpeta de archivos binarios de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="50caa-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="50caa-259">Modifica `web.config` para agregar el módulo de seguimiento HTTP de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="50caa-260">Habilita la generación de perfiles de CLR para recopilar llamadas de dependencia.</span><span class="sxs-lookup"><span data-stu-id="50caa-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="50caa-261">¿Tengo que actualizar el Monitor de estado siempre que actualice la aplicación?</span><span class="sxs-lookup"><span data-stu-id="50caa-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="50caa-262">No si reimplementa de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="50caa-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="50caa-263">Si selecciona la opción "eliminar archivos existentes" en el proceso de publicación, necesitará volver a ejecutar el Monitor de estado para configurar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="50caa-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="50caa-264">¿Qué telemetría se recopila?</span><span class="sxs-lookup"><span data-stu-id="50caa-264">What telemetry is collected?</span></span>

<span data-ttu-id="50caa-265">En el caso de las aplicaciones que instrumenta solo en tiempo de ejecución mediante el Monitor de estado:</span><span class="sxs-lookup"><span data-stu-id="50caa-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="50caa-266">Solicitudes HTTP</span><span class="sxs-lookup"><span data-stu-id="50caa-266">HTTP requests</span></span>
* <span data-ttu-id="50caa-267">Llamadas a dependencias</span><span class="sxs-lookup"><span data-stu-id="50caa-267">Calls to dependencies</span></span>
* <span data-ttu-id="50caa-268">Excepciones</span><span class="sxs-lookup"><span data-stu-id="50caa-268">Exceptions</span></span>
* <span data-ttu-id="50caa-269">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="50caa-269">Performance counters</span></span>

<span data-ttu-id="50caa-270">En el caso de las aplicaciones ya instrumentadas en el momento de la compilación:</span><span class="sxs-lookup"><span data-stu-id="50caa-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="50caa-271">Contadores de proceso.</span><span class="sxs-lookup"><span data-stu-id="50caa-271">Process counters.</span></span>
 * <span data-ttu-id="50caa-272">Llamadas de dependencia (.NET 4.5); valores devueltos en las llamadas de dependencia (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="50caa-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="50caa-273">Valores de seguimiento de la pila de excepción.</span><span class="sxs-lookup"><span data-stu-id="50caa-273">Exception stack trace values.</span></span>

[<span data-ttu-id="50caa-274">Más información</span><span class="sxs-lookup"><span data-stu-id="50caa-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="50caa-275">Vídeo</span><span class="sxs-lookup"><span data-stu-id="50caa-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="50caa-276"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50caa-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="50caa-277">Vea la telemetría:</span><span class="sxs-lookup"><span data-stu-id="50caa-277">View your telemetry:</span></span>

* <span data-ttu-id="50caa-278">[Explore las métricas](app-insights-metrics-explorer.md) para supervisar el rendimiento y uso.</span><span class="sxs-lookup"><span data-stu-id="50caa-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="50caa-279">[Busque eventos y registros][diagnostic] para diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="50caa-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="50caa-280">[Análisis](app-insights-analytics.md) para más consultas avanzadas</span><span class="sxs-lookup"><span data-stu-id="50caa-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="50caa-281">Creación de paneles</span><span class="sxs-lookup"><span data-stu-id="50caa-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="50caa-282">Agregue más telemetría:</span><span class="sxs-lookup"><span data-stu-id="50caa-282">Add more telemetry:</span></span>

* <span data-ttu-id="50caa-283">[Cree pruebas web][availability] para asegurarse de que el sitio permanece activo.</span><span class="sxs-lookup"><span data-stu-id="50caa-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="50caa-284">[Agregue telemetría de cliente web][usage] para ver las excepciones de código de la página web y para que le permitan insertar llamadas de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="50caa-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="50caa-285">[Agregue el SDK de Application Insights al código][greenbrown] para que pueda insertar llamadas de seguimiento y registro.</span><span class="sxs-lookup"><span data-stu-id="50caa-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
