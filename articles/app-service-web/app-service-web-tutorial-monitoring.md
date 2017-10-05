---
title: "Supervisión de una aplicación web | Microsoft Docs"
description: "Aprenda a configurar la supervisión en su aplicación web."
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="409f3-103">Supervisión de App Service</span><span class="sxs-lookup"><span data-stu-id="409f3-103">Monitor App Service</span></span>
<span data-ttu-id="409f3-104">Este tutorial le guiará a través de la supervisión de la aplicación y el uso de las herramientas integradas en la plataforma para solucionar problemas cuando se produzcan.</span><span class="sxs-lookup"><span data-stu-id="409f3-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="409f3-105">En cada sección de este documento se abarca una característica específica.</span><span class="sxs-lookup"><span data-stu-id="409f3-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="409f3-106">El uso conjunto de las características le permite:</span><span class="sxs-lookup"><span data-stu-id="409f3-106">Using the features together let you:</span></span>
- <span data-ttu-id="409f3-107">Identificar problemas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="409f3-108">Determinar si el problema se debe al código o a la plataforma.</span><span class="sxs-lookup"><span data-stu-id="409f3-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="409f3-109">Restringir el origen del problema en el código.</span><span class="sxs-lookup"><span data-stu-id="409f3-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="409f3-110">Depurar y corregir el problema.</span><span class="sxs-lookup"><span data-stu-id="409f3-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="409f3-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="409f3-111">Before you begin</span></span>
- <span data-ttu-id="409f3-112">Necesita una aplicación web para supervisar y seguir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="409f3-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="409f3-113">Para crear una aplicación, siga los pasos que se describen en el tutorial [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) (Creación de una aplicación ASP.NET en Azure con SQL Database).</span><span class="sxs-lookup"><span data-stu-id="409f3-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="409f3-114">Si quiere probar la **depuración remota** de la aplicación, necesita Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="409f3-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="409f3-115">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar la versión [gratuita de Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="409f3-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="409f3-116">Asegúrese de que habilita **Desarrollo de Azure** durante la instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="409f3-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="409f3-117"><a name="metrics"></a>Paso 1: Visualización de métricas</span><span class="sxs-lookup"><span data-stu-id="409f3-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="409f3-118">Las **métricas** son útiles para comprender lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="409f3-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="409f3-119">Estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="409f3-119">Application health</span></span>
- <span data-ttu-id="409f3-120">Rendimiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="409f3-120">App performance</span></span>
- <span data-ttu-id="409f3-121">Consumo de recursos</span><span class="sxs-lookup"><span data-stu-id="409f3-121">Resource consumption</span></span>

<span data-ttu-id="409f3-122">Cuando se investiga un problema de aplicación, revisar las métricas es un buen comienzo.</span><span class="sxs-lookup"><span data-stu-id="409f3-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="409f3-123">El portal de Azure cuenta con una forma rápida de inspeccionar visualmente las métricas de su aplicación mediante **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="409f3-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="409f3-124">Las métricas proporcionan una vista histórica de varias agregaciones clave para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="409f3-125">Para cualquier aplicación hospedada en App Service, debe supervisar tanto la aplicación web como el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="409f3-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="409f3-126">Un plan de App Service representa la colección de recursos físicos que se utiliza para hospedar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="409f3-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="409f3-127">Todas las aplicaciones asignadas a un plan de App Service comparten los recursos definidos por él, lo que permite ahorrar costos al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="409f3-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="409f3-128">Los planes de App Service definen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="409f3-128">App Service plans define:</span></span>
> * <span data-ttu-id="409f3-129">Región: Europa del Norte, este de EE. UU., Sudeste Asiático, etc.</span><span class="sxs-lookup"><span data-stu-id="409f3-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="409f3-130">Tamaño de la instancia: pequeño, mediano, grande, etc.</span><span class="sxs-lookup"><span data-stu-id="409f3-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="409f3-131">Recuento de escala: una, dos, tres instancias, etc.</span><span class="sxs-lookup"><span data-stu-id="409f3-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="409f3-132">SKU: Gratis, Compartido, Básico, Estándar, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="409f3-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="409f3-133">Para revisar las métricas de la aplicación web, vaya a la hoja **Overview** (Información general) de la aplicación que quiera supervisar.</span><span class="sxs-lookup"><span data-stu-id="409f3-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="409f3-134">En ella, puede ver un gráfico de las métricas de la aplicación en forma de **icono Monitoring** (Supervisión).</span><span class="sxs-lookup"><span data-stu-id="409f3-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="409f3-135">Haga clic en el icono para editar y configurar qué métricas ver y el intervalo de tiempo durante el cual se muestran.</span><span class="sxs-lookup"><span data-stu-id="409f3-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="409f3-136">De forma predeterminada, la hoja de recursos proporciona una vista de las solicitudes de la aplicación y los errores de la última hora.</span><span class="sxs-lookup"><span data-stu-id="409f3-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="409f3-137">![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="409f3-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="409f3-138">Como puede ver en el ejemplo, tenemos una aplicación que genera muchos **errores del servidor HTTP**.</span><span class="sxs-lookup"><span data-stu-id="409f3-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="409f3-139">El gran volumen de errores es el primer indicio de que necesitamos investigar esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="409f3-140">Más información sobre Azure Monitor con los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="409f3-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="409f3-141">Introducción a Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="409f3-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="409f3-142">Métricas de Azure</span><span class="sxs-lookup"><span data-stu-id="409f3-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="409f3-143">Métricas compatibles con Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="409f3-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="409f3-144">Paneles de Azure</span><span class="sxs-lookup"><span data-stu-id="409f3-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="409f3-145"><a name="alerts"></a>Paso 2: Configuración de alertas</span><span class="sxs-lookup"><span data-stu-id="409f3-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="409f3-146">Las **alertas** se pueden configurar para que se desencadenen cuando se produzcan condiciones específicas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="409f3-147">En el [Paso 1: Visualización de métricas](#metrics), hemos visto que la aplicación tenía un gran número de errores.</span><span class="sxs-lookup"><span data-stu-id="409f3-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="409f3-148">Vamos a configurar una alerta de notificación automática cuando se produzcan errores.</span><span class="sxs-lookup"><span data-stu-id="409f3-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="409f3-149">En este caso, queremos que con la alerta se envíe un correo electrónico cada vez que el número de errores HTTP 50X supere un umbral determinado.</span><span class="sxs-lookup"><span data-stu-id="409f3-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="409f3-150">Para crear una alerta, vaya a **Supervisión** > **Alertas** y haga clic en **[+] Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="409f3-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="409f3-152">Proporcione valores para la configuración de la Alerta:</span><span class="sxs-lookup"><span data-stu-id="409f3-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="409f3-153">**Recurso:** sitio para supervisar con la alerta.</span><span class="sxs-lookup"><span data-stu-id="409f3-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="409f3-154">**Nombre:** nombre de la alerta, en este caso: *High HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="409f3-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="409f3-155">**Descripción:** texto sin formato que explica lo que observa esta alerta.</span><span class="sxs-lookup"><span data-stu-id="409f3-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="409f3-156">**Alerta activada:** las alertas pueden mirar métricas o eventos, en este ejemplo, examinamos las métricas.</span><span class="sxs-lookup"><span data-stu-id="409f3-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="409f3-157">**Métrica:** métrica que se va a supervisar, en este caso: *Errores del servidor HTTP*.</span><span class="sxs-lookup"><span data-stu-id="409f3-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="409f3-158">**Condición:** cuándo se activa la alerta, en este caso, seleccione la opción *mayor que*.</span><span class="sxs-lookup"><span data-stu-id="409f3-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="409f3-159">**Umbral:** valor que se desea buscar, en este caso: *400*.</span><span class="sxs-lookup"><span data-stu-id="409f3-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="409f3-160">**Período:** las alertas funcionan sobre el valor medio de una métrica.</span><span class="sxs-lookup"><span data-stu-id="409f3-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="409f3-161">Los períodos de tiempo menores suspenden las alertas más sensibles.</span><span class="sxs-lookup"><span data-stu-id="409f3-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="409f3-162">En este caso examinamos *5 minutos*.</span><span class="sxs-lookup"><span data-stu-id="409f3-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="409f3-163">**Propietarios y colaboradores de correo electrónico:** en este caso: *Habilitado*.</span><span class="sxs-lookup"><span data-stu-id="409f3-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="409f3-164">Ahora que se creó la alerta, se enviará un correo electrónico cada vez que la aplicación supere el umbral configurado.</span><span class="sxs-lookup"><span data-stu-id="409f3-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="409f3-165">Las alertas activas también se pueden revisar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="409f3-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Alertas desencadenadas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="409f3-167">Más información sobre las alertas de Azure con los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="409f3-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="409f3-168">¿Qué son las alertas en Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="409f3-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="409f3-169">Realización de acciones en las métricas</span><span class="sxs-lookup"><span data-stu-id="409f3-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="409f3-170">Creación de alertas de métrica</span><span class="sxs-lookup"><span data-stu-id="409f3-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="409f3-171"><a name="companion"></a> Paso 3: App Service Companion</span><span class="sxs-lookup"><span data-stu-id="409f3-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="409f3-172">**App Service Companion** ofrece un método cómodo de supervisar la aplicación con una experiencia nativa en su dispositivo móvil (iOS o Android).</span><span class="sxs-lookup"><span data-stu-id="409f3-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="409f3-173">Use Azure App Service Companion para:</span><span class="sxs-lookup"><span data-stu-id="409f3-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="409f3-174">Revisar las métricas de aplicación</span><span class="sxs-lookup"><span data-stu-id="409f3-174">Review application metrics</span></span>
- <span data-ttu-id="409f3-175">Revisar y realizar acciones sobre alertas y recomendaciones de aplicación</span><span class="sxs-lookup"><span data-stu-id="409f3-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="409f3-176">Realizar solución de problemas básicos (examinar, iniciar, detener, reiniciar la aplicación)</span><span class="sxs-lookup"><span data-stu-id="409f3-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="409f3-177">Obtener notificaciones push de eventos críticos.</span><span class="sxs-lookup"><span data-stu-id="409f3-177">Get push notifications for critical events.</span></span>

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="409f3-179">[![App Service Companion en App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion en Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="409f3-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="409f3-180">Puede instalar App Service Companion desde [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) o [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps).</span><span class="sxs-lookup"><span data-stu-id="409f3-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="409f3-181"><a name="diagnose"></a> Paso 4: Diagnóstico y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="409f3-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="409f3-182">**Diagnosticar y resolver problemas** le ayudará a diferenciar los problemas de la aplicación de los de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="409f3-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="409f3-183">También puede sugerir mitigaciones para que la aplicación web se recupere.</span><span class="sxs-lookup"><span data-stu-id="409f3-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Diagnosticar y resolver problemas](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="409f3-185">Siguiendo con los pasos anteriores del formulario de ejemplo, podemos ver que la aplicación ha tenido problemas de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="409f3-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="409f3-186">En cambio, la disponibilidad de la plataforma no ha cambiado del 100 %.</span><span class="sxs-lookup"><span data-stu-id="409f3-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="409f3-187">Cuando la aplicación tenga un problema y la plataforma no, es evidente que se trata de un problema de aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="409f3-188"><a name="logging"></a> Paso 5: Registro</span><span class="sxs-lookup"><span data-stu-id="409f3-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="409f3-189">Ahora que nos hemos reducido los errores a un problema de aplicación, podemos observar los registros de aplicación y servidor para más información.</span><span class="sxs-lookup"><span data-stu-id="409f3-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="409f3-190">El registro le permite recopilar registros de **Diagnósticos de aplicaciones** y de **Diagnóstico del servidor web** para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="409f3-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="409f3-191">Diagnósticos de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="409f3-191">Application Diagnostics</span></span>
<span data-ttu-id="409f3-192">Diagnósticos de aplicaciones le permite capturar seguimientos generados por la aplicación en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="409f3-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="409f3-193">Agregar la funcionalidad de seguimiento a la aplicación mejora en gran medida la capacidad de depuración y e identificación de problemas.</span><span class="sxs-lookup"><span data-stu-id="409f3-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="409f3-194">En ASP.NET, puede registrar los seguimientos de aplicación mediante la [clase System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) para generar eventos que se capturan mediante la infraestructura de registro.</span><span class="sxs-lookup"><span data-stu-id="409f3-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="409f3-195">También puede especificar la gravedad del seguimiento para facilitar el filtrado.</span><span class="sxs-lookup"><span data-stu-id="409f3-195">You can also specify the severity of the trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="409f3-196">Para habilitar el registro de la aplicación, vaya a **Supervisión** > **Registros de diagnóstico** y habilite los registros de la aplicación con los conmutadores.</span><span class="sxs-lookup"><span data-stu-id="409f3-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="409f3-198">Los registros de aplicación se pueden almacenar en el sistema de archivos de la aplicación web o se pueden insertar en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="409f3-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="409f3-199">En los escenarios de producción se recomienda usar una instancia de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="409f3-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="409f3-200">La habilitación del registro tiene un impacto sobre el rendimiento de su aplicación y la utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="409f3-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="409f3-201">En escenarios de producción, se recomiendan habilitar los registros de errores.</span><span class="sxs-lookup"><span data-stu-id="409f3-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="409f3-202">Habilite únicamente un registro más detallado al investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="409f3-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="409f3-203">Diagnósticos del servidor web</span><span class="sxs-lookup"><span data-stu-id="409f3-203">Web Server Diagnostics</span></span>
<span data-ttu-id="409f3-204">Los registros del servidor web se generan aunque la aplicación no se haya instrumentado.</span><span class="sxs-lookup"><span data-stu-id="409f3-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="409f3-205">App Service puede recopilar tres tipos diferentes de registros de servidor:</span><span class="sxs-lookup"><span data-stu-id="409f3-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="409f3-206">**Registro del servidor web**.</span><span class="sxs-lookup"><span data-stu-id="409f3-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="409f3-207">Información sobre las transacciones HTTP mediante el [formato de archivo de registro extendido W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="409f3-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="409f3-208">Resulta útil para determinar las métricas totales del sitio, como el número de solicitudes tramitadas o cuántas solicitudes proceden de una dirección IP específica.</span><span class="sxs-lookup"><span data-stu-id="409f3-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="409f3-209">**Registro de error detallado**</span><span class="sxs-lookup"><span data-stu-id="409f3-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="409f3-210">Información de error detallada de los códigos de estado HTTP que indican un error (código de estado 400 o superior).</span><span class="sxs-lookup"><span data-stu-id="409f3-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="409f3-211">Más información sobre el registro de errores detallado</span><span class="sxs-lookup"><span data-stu-id="409f3-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="409f3-212">**Seguimiento de solicitudes erróneas**.</span><span class="sxs-lookup"><span data-stu-id="409f3-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="409f3-213">Información detallada sobre solicitudes erróneas, lo que incluye un seguimiento de los componentes de IIS usados para procesar la solicitud y el tiempo dedicado a cada componente.</span><span class="sxs-lookup"><span data-stu-id="409f3-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="409f3-214">Los registros de solicitudes erróneas son útiles al intentar aislar lo que está provocando un error HTTP específico.</span><span class="sxs-lookup"><span data-stu-id="409f3-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="409f3-215">Más información acerca del seguimiento de solicitudes con error</span><span class="sxs-lookup"><span data-stu-id="409f3-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="409f3-216">Para habilitar el registro del servidor:</span><span class="sxs-lookup"><span data-stu-id="409f3-216">To enable Server logging:</span></span>
- <span data-ttu-id="409f3-217">Vaya a **Supervisión** > **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="409f3-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="409f3-218">Habilite los diferentes tipos de diagnósticos del servidor web mediante los botones de alternancia.</span><span class="sxs-lookup"><span data-stu-id="409f3-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="409f3-220">La habilitación del registro tiene un impacto sobre el rendimiento de su aplicación y la utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="409f3-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="409f3-221">En escenarios de producción, se recomienda habilitar los registros de errores. Habilite únicamente un registro más detallado al investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="409f3-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="409f3-222">Acceso a los registros</span><span class="sxs-lookup"><span data-stu-id="409f3-222">Accessing Logs</span></span>
<span data-ttu-id="409f3-223">El acceso a los registros almacenados en Blob Storage se realiza mediante el Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="409f3-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="409f3-224">El acceso a los registros almacenados en el sistema de archivos de la aplicación web se realiza mediante FTP en las siguientes rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="409f3-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="409f3-225">**Registros de la aplicación** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="409f3-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="409f3-226">Esta carpeta contiene uno o varios archivos de texto con información generada por el registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="409f3-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="409f3-227">**Seguimiento de solicitudes con error** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="409f3-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="409f3-228">Esta carpeta contiene un archivo XSL y uno o varios archivos XML.</span><span class="sxs-lookup"><span data-stu-id="409f3-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="409f3-229">**Registros de errores detallados** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="409f3-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="409f3-230">Esta carpeta contiene uno o varios archivos .htm con información extensa sobre los errores HTTP generados por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="409f3-231">**Registros del servidor web** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="409f3-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="409f3-232">Esta carpeta contiene uno o varios archivos de texto con formato de archivo de registro extendido W3C.</span><span class="sxs-lookup"><span data-stu-id="409f3-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="409f3-233"><a name="streaming"></a>Paso 6: Registros de streaming</span><span class="sxs-lookup"><span data-stu-id="409f3-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="409f3-234">Los registros de streaming resultan prácticos cuando se depurar una aplicación, dado que ahorran tiempo en comparación con el [acceso a los registros](#Accessing-Logs) desde el FTP.</span><span class="sxs-lookup"><span data-stu-id="409f3-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="409f3-235">App Service puede transmitir **registros de la aplicación** y **registros del servidor web** a medida que se generan.</span><span class="sxs-lookup"><span data-stu-id="409f3-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="409f3-236">Antes de intentar transmitir registros, asegúrese de que ha habilitado la recopilación de registros como se describe en la sección [Registro](#logging).</span><span class="sxs-lookup"><span data-stu-id="409f3-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="409f3-237">Para transmitir registros, vaya a **Supervisión**> **Secuencia de registro**.</span><span class="sxs-lookup"><span data-stu-id="409f3-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="409f3-238">Seleccione **Registros de aplicación** o **Registros del servidor web** según la información que busque.</span><span class="sxs-lookup"><span data-stu-id="409f3-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="409f3-239">Desde aquí, también puede pausar, reiniciar y borrar el búfer.</span><span class="sxs-lookup"><span data-stu-id="409f3-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Registros de transmisión](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="409f3-241">Solo se generan registros cuando hay tráfico en la aplicación; también puede aumentar el nivel de detalle de los registros para obtener más eventos o información.</span><span class="sxs-lookup"><span data-stu-id="409f3-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="409f3-242"><a name="remote"></a>Paso 7: Depuración remota</span><span class="sxs-lookup"><span data-stu-id="409f3-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="409f3-243">Una vez que se haya identificado el origen de los problemas de aplicación, use **Depuración remota** para desplazarse por el código.</span><span class="sxs-lookup"><span data-stu-id="409f3-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="409f3-244">Depuración remota le permite asociar un depurador a la aplicación web que se ejecuta en la nube.</span><span class="sxs-lookup"><span data-stu-id="409f3-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="409f3-245">Puede establecer puntos de interrupción, manipular la memoria directamente, recorrer el código e incluso cambiar la ruta de acceso del código, al igual que haría con una aplicación que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="409f3-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="409f3-246">Para asociar el depurador a la aplicación que se ejecuta en la nube:</span><span class="sxs-lookup"><span data-stu-id="409f3-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="409f3-247">Con Visual Studio de 2017, abra la solución para la aplicación que desea depurar.</span><span class="sxs-lookup"><span data-stu-id="409f3-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="409f3-248">Establezca algunos puntos de interrupción, igual que haría con el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="409f3-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="409f3-249">Abra **Cloud Explorer** (Ctr + /, Ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="409f3-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="409f3-250">Inicie sesión con sus credenciales de Azure según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="409f3-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="409f3-251">Busque la aplicación que quiere depurar.</span><span class="sxs-lookup"><span data-stu-id="409f3-251">Find the app you want to debug</span></span>
- <span data-ttu-id="409f3-252">Seleccione el formulario **Asociar depurador** en el panel **Acciones**.</span><span class="sxs-lookup"><span data-stu-id="409f3-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Depuración remota](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="409f3-254">Visual Studio configura su aplicación para la depuración remota y abre una ventana de explorador que lleva a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="409f3-255">Examine la aplicación para desencadenar puntos de interrupción y recorrer el código.</span><span class="sxs-lookup"><span data-stu-id="409f3-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="409f3-256">No se recomienda ejecutar el modo de depuración en producción.</span><span class="sxs-lookup"><span data-stu-id="409f3-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="409f3-257">Si su aplicación de producción no está escalada horizontalmente a varias instancias de servidor, la depuración impide que el servidor web responda a otras solicitudes.</span><span class="sxs-lookup"><span data-stu-id="409f3-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="409f3-258">Para solucionar problemas de producción, los mejores recursos son [configurar el registro](#logging) y [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="409f3-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="409f3-259"><a name="explorer"></a> Paso 8: Explorador de procesos</span><span class="sxs-lookup"><span data-stu-id="409f3-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="409f3-260">Cuando la aplicación se escala horizontalmente a más de una instancia, el **explorador de procesos** puede ayudarle a identificar problemas específicos de instancia.</span><span class="sxs-lookup"><span data-stu-id="409f3-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="409f3-261">Use el **Explorador de procesos** para:</span><span class="sxs-lookup"><span data-stu-id="409f3-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="409f3-262">Enumerar todos los procesos entre distintas instancias de su plan de App Service</span><span class="sxs-lookup"><span data-stu-id="409f3-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="409f3-263">Explorar en profundidad y ver los identificadores y módulos asociados con cada proceso</span><span class="sxs-lookup"><span data-stu-id="409f3-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="409f3-264">Ver el recuento de CPU, espacio de trabajo y subproceso en el nivel de proceso para ayudarle a identificar los procesos descontrolados</span><span class="sxs-lookup"><span data-stu-id="409f3-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="409f3-265">Encontrar identificadores de archivos abiertos e incluso eliminar una instancia de proceso específica.</span><span class="sxs-lookup"><span data-stu-id="409f3-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="409f3-266">El explorador de procesos puede estar en **Supervisión** > **Explorador de procesos**.</span><span class="sxs-lookup"><span data-stu-id="409f3-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Explorador de procesos](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="409f3-268"><a name="insights"></a> Paso 9: Application Insights</span><span class="sxs-lookup"><span data-stu-id="409f3-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="409f3-269">**Application Insights** proporciona funcionalidades avanzadas de supervisión y generación de perfiles de aplicaciones para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="409f3-270">Use Application Insights para detectar y diagnosticar excepciones y problemas de rendimiento en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="409f3-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="409f3-271">Puede habilitar Application Insights para su aplicación web en **Supervisión** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="409f3-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="409f3-272">Application Insights podría solicitarle instalar las extensiones del sitio de Application Insights para iniciar la recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="409f3-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="409f3-273">La instalación de la extensión del sitio provoca un reinicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="409f3-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="409f3-275">Application Insights contiene un conjunto completo de características; para aprender más, siga los vínculos que se incluyen en la sección [Pasos siguientes](#next).</span><span class="sxs-lookup"><span data-stu-id="409f3-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="409f3-276"><a name="next"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="409f3-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="409f3-277">¿Qué es Application Insights?</span><span class="sxs-lookup"><span data-stu-id="409f3-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="409f3-278">Supervisión del rendimiento de aplicaciones web de Azure con Application Insights</span><span class="sxs-lookup"><span data-stu-id="409f3-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="409f3-279">Supervisión de la disponibilidad y la capacidad de respuesta de cualquier sito web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="409f3-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
