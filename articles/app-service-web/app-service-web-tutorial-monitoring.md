---
title: "una aplicación Web aaaMonitor | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset la supervisión en la aplicación Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="09859-103">Supervisión de App Service</span><span class="sxs-lookup"><span data-stu-id="09859-103">Monitor App Service</span></span>
<span data-ttu-id="09859-104">Este tutorial le guía a través de la supervisión de la aplicación y con problemas de toosolve de herramientas de hello integradas de la plataforma cuando se producen.</span><span class="sxs-lookup"><span data-stu-id="09859-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="09859-105">En cada sección de este documento se abarca una característica específica.</span><span class="sxs-lookup"><span data-stu-id="09859-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="09859-106">Uso de características de hello juntas permite:</span><span class="sxs-lookup"><span data-stu-id="09859-106">Using hello features together let you:</span></span>
- <span data-ttu-id="09859-107">Identificar problemas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="09859-108">Determinar cuándo se debe problema Hola con la plataforma de código o hello.</span><span class="sxs-lookup"><span data-stu-id="09859-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="09859-109">Restringir origen Hola problema de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="09859-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="09859-110">Depuración y corregir el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="09859-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="09859-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="09859-111">Before you begin</span></span>
- <span data-ttu-id="09859-112">Necesita una aplicación Web toomonitor y siga Hola que se describen los pasos.</span><span class="sxs-lookup"><span data-stu-id="09859-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="09859-113">Puede crear una aplicación siguiendo los pasos de hello descritos en hello [crear una aplicación ASP.NET en Azure con la base de datos SQL](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="09859-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="09859-114">Si desea tootry out **depuración remota** de la aplicación, necesita Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09859-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="09859-115">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello libre [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="09859-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="09859-116">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="09859-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="09859-117"><a name="metrics"></a>Paso 1: Visualización de métricas</span><span class="sxs-lookup"><span data-stu-id="09859-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="09859-118">**Las métricas** son toounderstand útil:</span><span class="sxs-lookup"><span data-stu-id="09859-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="09859-119">Estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="09859-119">Application health</span></span>
- <span data-ttu-id="09859-120">Rendimiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="09859-120">App performance</span></span>
- <span data-ttu-id="09859-121">Consumo de recursos</span><span class="sxs-lookup"><span data-stu-id="09859-121">Resource consumption</span></span>

<span data-ttu-id="09859-122">Cuando se investiga un problema de aplicación, revisar las métricas es un buen lugar toostart.</span><span class="sxs-lookup"><span data-stu-id="09859-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="09859-123">Portal de Azure tiene una forma rápida toovisually inspeccionar las métricas de saludo de la aplicación con **Monitor Azure**.</span><span class="sxs-lookup"><span data-stu-id="09859-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="09859-124">Las métricas proporcionan una vista histórica de varias agregaciones clave para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="09859-125">Para cualquier aplicación hospedada en el servicio de aplicaciones, debe supervisar la aplicación Web de Hola y Hola plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09859-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="09859-126">Un plan de servicio de aplicaciones representa colección de Hola de toohost recursos físicos que usan las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09859-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="09859-127">Todas las aplicaciones tooan servicio de aplicaciones plan recurso compartido Hola recursos asignan definido por dicha permitiéndole toosave costo al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09859-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="09859-128">Los planes de App Service definen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="09859-128">App Service plans define:</span></span>
> * <span data-ttu-id="09859-129">Región: Europa del Norte, este de EE. UU., Sudeste Asiático, etc.</span><span class="sxs-lookup"><span data-stu-id="09859-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="09859-130">Tamaño de la instancia: pequeño, mediano, grande, etc.</span><span class="sxs-lookup"><span data-stu-id="09859-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="09859-131">Recuento de escala: una, dos, tres instancias, etc.</span><span class="sxs-lookup"><span data-stu-id="09859-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="09859-132">SKU: Gratis, Compartido, Básico, Estándar, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="09859-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="09859-133">métricas de tooreview para la aplicación Web, vaya toohello **Introducción** hoja de aplicación hello desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="09859-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="09859-134">En ella, puede ver un gráfico de las métricas de la aplicación en forma de **icono Monitoring** (Supervisión).</span><span class="sxs-lookup"><span data-stu-id="09859-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="09859-135">Haga clic en tooedit de mosaico de Hola y configurar qué tooview métricas y Hola toodisplay de intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="09859-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="09859-136">Por hoja de recursos de hello predeterminada proporciona una vista para las solicitudes de aplicación hello y errores de hello última hora.</span><span class="sxs-lookup"><span data-stu-id="09859-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="09859-137">![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="09859-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="09859-138">Como puede ver en el ejemplo de Hola, tenemos una aplicación que se va a generar muchos **errores del servidor HTTP**.</span><span class="sxs-lookup"><span data-stu-id="09859-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="09859-139">gran volumen de Hola de errores es el primer indicio de hello necesitamos tooinvestigate esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="09859-140">Más información acerca del Monitor de Azure con hello siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="09859-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="09859-141">Introducción a Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="09859-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="09859-142">Métricas de Azure</span><span class="sxs-lookup"><span data-stu-id="09859-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="09859-143">Métricas compatibles con Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="09859-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="09859-144">Paneles de Azure</span><span class="sxs-lookup"><span data-stu-id="09859-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="09859-145"><a name="alerts"></a>Paso 2: Configuración de alertas</span><span class="sxs-lookup"><span data-stu-id="09859-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="09859-146">**Alertas** puede ser configurado tootrigger en condiciones específicas para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="09859-147">En [paso 1: visualice las métricas](#metrics), hemos visto que la aplicación hello tenía un gran número de errores.</span><span class="sxs-lookup"><span data-stu-id="09859-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="09859-148">Permite configurar una alerta tooautomatically recibir notificaciones cuando se producen errores.</span><span class="sxs-lookup"><span data-stu-id="09859-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="09859-149">En este caso, se desea toosend alerta hello y enviar por correo electrónico cada vez que número Hola de errores HTTP 50 X supera un umbral determinado.</span><span class="sxs-lookup"><span data-stu-id="09859-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="09859-150">toocreate una alerta, vaya demasiado**supervisión** > **alertas** y haga clic en **[+] Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="09859-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="09859-152">Proporcione valores de configuración de alertas de hello:</span><span class="sxs-lookup"><span data-stu-id="09859-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="09859-153">**Recurso:** Hola toomonitor de sitio con la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="09859-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="09859-154">**Nombre:** nombre de la alerta, en este caso: *High HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="09859-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="09859-155">**Descripción:** texto sin formato que explica lo que observa esta alerta.</span><span class="sxs-lookup"><span data-stu-id="09859-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="09859-156">**Alerta activada:** las alertas pueden mirar métricas o eventos, en este ejemplo, examinamos las métricas.</span><span class="sxs-lookup"><span data-stu-id="09859-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="09859-157">**Métrica:** qué toomonitor métrica, en este caso: *errores del servidor HTTP*.</span><span class="sxs-lookup"><span data-stu-id="09859-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="09859-158">**Condición:** cuando tooalert, en este caso, seleccione hello *mayor* opción.</span><span class="sxs-lookup"><span data-stu-id="09859-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="09859-159">**Umbral:** ¿qué es toolook de valor, en este caso: *400*.</span><span class="sxs-lookup"><span data-stu-id="09859-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="09859-160">**Período:** alertas funcionan sobre valor medio de Hola de una métrica.</span><span class="sxs-lookup"><span data-stu-id="09859-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="09859-161">Los períodos de tiempo menores suspenden las alertas más sensibles.</span><span class="sxs-lookup"><span data-stu-id="09859-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="09859-162">En este caso examinamos *5 minutos*.</span><span class="sxs-lookup"><span data-stu-id="09859-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="09859-163">**Propietarios y colaboradores de correo electrónico:** en este caso: *Habilitado*.</span><span class="sxs-lookup"><span data-stu-id="09859-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="09859-164">Ahora que hello alerta se crea un correo electrónico se envía cada vez hello aplicación pasa por encima del umbral de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="09859-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="09859-165">También se pueden revisar las alertas activas Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="09859-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Alertas desencadenadas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="09859-167">Más información acerca de las alertas de Azure con hello siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="09859-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="09859-168">¿Qué son las alertas en Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="09859-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="09859-169">Realización de acciones en las métricas</span><span class="sxs-lookup"><span data-stu-id="09859-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="09859-170">Creación de alertas de métrica</span><span class="sxs-lookup"><span data-stu-id="09859-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="09859-171"><a name="companion"></a> Paso 3: App Service Companion</span><span class="sxs-lookup"><span data-stu-id="09859-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="09859-172">**Complementario de servicio de aplicaciones** ofrece una manera cómoda de toomonitor la aplicación con una experiencia nativa en su dispositivo móvil (iOS o Android).</span><span class="sxs-lookup"><span data-stu-id="09859-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="09859-173">Use Azure App Service Companion para:</span><span class="sxs-lookup"><span data-stu-id="09859-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="09859-174">Revisar las métricas de aplicación</span><span class="sxs-lookup"><span data-stu-id="09859-174">Review application metrics</span></span>
- <span data-ttu-id="09859-175">Revisar y realizar acciones sobre alertas y recomendaciones de aplicación</span><span class="sxs-lookup"><span data-stu-id="09859-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="09859-176">Realizar la solución de problemas básicos (Examinar, iniciar, detener, reiniciar aplicación de hello)</span><span class="sxs-lookup"><span data-stu-id="09859-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="09859-177">Obtener notificaciones push de eventos críticos.</span><span class="sxs-lookup"><span data-stu-id="09859-177">Get push notifications for critical events.</span></span>

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="09859-179">[![App Service Companion en App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion en Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="09859-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="09859-180">Puede instalar complementario de servicio de aplicaciones de hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) o [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="09859-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="09859-181"><a name="diagnose"></a> Paso 4: Diagnóstico y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="09859-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="09859-182">**Diagnosticar y resolver problemas** le ayudará a diferenciar los problemas de la aplicación de los de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="09859-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="09859-183">También puede sugerir a posibles mitigaciones tooget su toohealthy atrás de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="09859-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Diagnosticar y resolver problemas](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="09859-185">Continuar con los pasos anteriores del formulario de ejemplo Hola, podemos ver que aplicación hello ha sido problemas de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="09859-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="09859-186">En cambio, la disponibilidad de la plataforma de hello no ha movido de 100%.</span><span class="sxs-lookup"><span data-stu-id="09859-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="09859-187">Cuando aplicación hello tiene el problema y hello plataforma esté activo, es una indicación clara de que estamos trabajando con un problema de aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="09859-188"><a name="logging"></a> Paso 5: Registro</span><span class="sxs-lookup"><span data-stu-id="09859-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="09859-189">Ahora que nos hemos reduce un problema de aplicación Hola errores tooan, podemos observar tooget de registros de servidor y la aplicación hello obtener más información.</span><span class="sxs-lookup"><span data-stu-id="09859-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="09859-190">El registro permite toocollect ambos **Application Diagnostics** y **diagnósticos de servidor Web** registros de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="09859-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="09859-191">Diagnósticos de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="09859-191">Application Diagnostics</span></span>
<span data-ttu-id="09859-192">Diagnósticos de la aplicación permite toocapture seguimientos generados por la aplicación hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="09859-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="09859-193">Agregar seguimiento tooyour aplicación mejora en gran medida su capacidad toodebug y problemas de punto de anclaje.</span><span class="sxs-lookup"><span data-stu-id="09859-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="09859-194">En ASP.NET, puede registrar los seguimientos de aplicación mediante [clase System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate eventos capturados por la infraestructura de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="09859-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="09859-195">También puede especificar la gravedad de Hola de seguimiento de Hola para filtrar más fácil.</span><span class="sxs-lookup"><span data-stu-id="09859-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

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
<span data-ttu-id="09859-196">registro de aplicaciones de tooenable vaya demasiado**supervisión** > **registros de diagnóstico** y habilitar registro de aplicaciones con hello alterna.</span><span class="sxs-lookup"><span data-stu-id="09859-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="09859-198">Registros de la aplicación pueden ser el sistema de archivos de la aplicación Web almacenado tooyour o insertan tooblob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09859-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="09859-199">Los escenarios de producción, es el almacenamiento de blobs toouse recomendada.</span><span class="sxs-lookup"><span data-stu-id="09859-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09859-200">La habilitación del registro tiene un impacto sobre el rendimiento de su aplicación y la utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="09859-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="09859-201">En escenarios de producción, se recomiendan habilitar los registros de errores.</span><span class="sxs-lookup"><span data-stu-id="09859-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="09859-202">Habilite únicamente un registro más detallado al investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="09859-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="09859-203">Diagnósticos del servidor web</span><span class="sxs-lookup"><span data-stu-id="09859-203">Web Server Diagnostics</span></span>
<span data-ttu-id="09859-204">Los registros del servidor web se generan aunque la aplicación no se haya instrumentado.</span><span class="sxs-lookup"><span data-stu-id="09859-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="09859-205">App Service puede recopilar tres tipos diferentes de registros de servidor:</span><span class="sxs-lookup"><span data-stu-id="09859-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="09859-206">**Registro del servidor web**.</span><span class="sxs-lookup"><span data-stu-id="09859-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="09859-207">Obtener información sobre las transacciones HTTP mediante hello [formato de archivo de registro extendido W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="09859-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="09859-208">Resulta útil al determinar las métricas generales de sitio como número de Hola de las solicitudes administradas o cuántas solicitudes provienen de una dirección IP específica.</span><span class="sxs-lookup"><span data-stu-id="09859-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="09859-209">**Registro de error detallado**</span><span class="sxs-lookup"><span data-stu-id="09859-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="09859-210">Información de error detallada de los códigos de estado HTTP que indican un error (código de estado 400 o superior).</span><span class="sxs-lookup"><span data-stu-id="09859-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="09859-211">Más información sobre el registro de errores detallado</span><span class="sxs-lookup"><span data-stu-id="09859-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="09859-212">**Seguimiento de solicitudes erróneas**.</span><span class="sxs-lookup"><span data-stu-id="09859-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="09859-213">Información detallada acerca de solicitudes con error, incluidos un seguimiento de los componentes de IIS de hello usa tooprocess Hola hello y solicitud de tiempo que se tarda en cada componente.</span><span class="sxs-lookup"><span data-stu-id="09859-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="09859-214">Registros de solicitudes con error son útiles al tratar de tooisolate cuál es la causa un error HTTP específico.</span><span class="sxs-lookup"><span data-stu-id="09859-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="09859-215">Más información acerca del seguimiento de solicitudes con error</span><span class="sxs-lookup"><span data-stu-id="09859-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="09859-216">registro del servidor tooenable:</span><span class="sxs-lookup"><span data-stu-id="09859-216">tooenable Server logging:</span></span>
- <span data-ttu-id="09859-217">vaya demasiado**supervisión** > **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="09859-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="09859-218">Habilitar a tipos diferentes de hello de diagnósticos de servidor Web mediante Hola alterna.</span><span class="sxs-lookup"><span data-stu-id="09859-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="09859-220">La habilitación del registro tiene un impacto sobre el rendimiento de su aplicación y la utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="09859-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="09859-221">En escenarios de producción, se recomienda habilitar los registros de errores. Habilite únicamente un registro más detallado al investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="09859-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="09859-222">Acceso a los registros</span><span class="sxs-lookup"><span data-stu-id="09859-222">Accessing Logs</span></span>
<span data-ttu-id="09859-223">El acceso a los registros almacenados en Blob Storage se realiza mediante el Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="09859-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="09859-224">Se obtiene acceso a registros almacenados en el sistema de archivos de la aplicación hello Web a través de FTP en hello siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="09859-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="09859-225">**Registros de la aplicación** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="09859-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="09859-226">Esta carpeta contiene uno o varios archivos de texto con información generada por el registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09859-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="09859-227">**Seguimiento de solicitudes con error** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="09859-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="09859-228">Esta carpeta contiene un archivo XSL y uno o varios archivos XML.</span><span class="sxs-lookup"><span data-stu-id="09859-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="09859-229">**Registros de errores detallados** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="09859-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="09859-230">Esta carpeta contiene uno o varios archivos .htm con información extensa sobre los errores HTTP generados por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="09859-231">**Registros del servidor web** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="09859-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="09859-232">Esta carpeta contiene uno o varios archivos de texto con formato con formato de archivo de registro extendido W3C de Hola.</span><span class="sxs-lookup"><span data-stu-id="09859-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="09859-233"><a name="streaming"></a>Paso 6: Registros de streaming</span><span class="sxs-lookup"><span data-stu-id="09859-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="09859-234">Los registros de streaming resultan prácticos al depurar una aplicación desde que ahorra tiempo en comparación con demasiado[acceso a registros de hello](#Accessing-Logs) a través de FTP.</span><span class="sxs-lookup"><span data-stu-id="09859-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="09859-235">App Service puede transmitir **registros de la aplicación** y **registros del servidor web** a medida que se generan.</span><span class="sxs-lookup"><span data-stu-id="09859-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="09859-236">Antes de intentar toostream registros, asegúrese de que ha habilitado la recopilación de registros como se describe en hello [registro](#logging) sección.</span><span class="sxs-lookup"><span data-stu-id="09859-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="09859-237">registros de toostream, vaya demasiado**supervisión**> **flujo de registro**.</span><span class="sxs-lookup"><span data-stu-id="09859-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="09859-238">Seleccione **Registros de aplicación** o **Registros del servidor web** según la información que busque.</span><span class="sxs-lookup"><span data-stu-id="09859-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="09859-239">Desde aquí, también puede pausar, reiniciar y borrar el búfer de Hola.</span><span class="sxs-lookup"><span data-stu-id="09859-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Registros de transmisión](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="09859-241">Registros solo se generan cuando hay tráfico en la aplicación hello, también puede aumentar el nivel de detalle de Hola de registros tooget más eventos o información.</span><span class="sxs-lookup"><span data-stu-id="09859-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="09859-242"><a name="remote"></a>Paso 7: Depuración remota</span><span class="sxs-lookup"><span data-stu-id="09859-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="09859-243">Una vez que tenga el origen de Hola que señala el pin de problemas de aplicaciones de hello, use **depuración remota** toowalk a través del código de hello.</span><span class="sxs-lookup"><span data-stu-id="09859-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="09859-244">Permite la depuración remota se adjunta una aplicación Web de depurador tooyour ejecutando en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="09859-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="09859-245">Puede establecer puntos de interrupción, manipula la memoria directamente, recorrer el código e incluso cambiar la ruta de acceso de código de hello tal como lo hace para aplicaciones que se ejecutan localmente.</span><span class="sxs-lookup"><span data-stu-id="09859-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="09859-246">tooattach Hola depurador tooyour aplicación que se ejecuta en la nube de hello:</span><span class="sxs-lookup"><span data-stu-id="09859-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="09859-247">Con Visual Studio 2017, solución de hello abierto para la aplicación hello desea toodebug</span><span class="sxs-lookup"><span data-stu-id="09859-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="09859-248">Establezca algunos puntos de interrupción, igual que haría con el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="09859-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="09859-249">Abra **Cloud Explorer** (Ctr + /, Ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="09859-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="09859-250">Inicie sesión con sus credenciales de Azure según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="09859-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="09859-251">Aplicación hello de búsqueda que desee toodebug</span><span class="sxs-lookup"><span data-stu-id="09859-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="09859-252">Seleccione **adjuntar depurador** Hola formulario **acciones** panel.</span><span class="sxs-lookup"><span data-stu-id="09859-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Depuración remota](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="09859-254">Visual Studio configura su aplicación para la depuración remota y abre una ventana del explorador que navega tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="09859-255">Examine los puntos de interrupción de tootrigger de aplicación y recorrer el código de hello.</span><span class="sxs-lookup"><span data-stu-id="09859-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="09859-256">No se recomienda ejecutar el modo de depuración en producción.</span><span class="sxs-lookup"><span data-stu-id="09859-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="09859-257">Si la aplicación de producción no se escala toomultiple instancias de servidor, depuración impedir que servidor de web de Hola desde responde las solicitudes de tooother.</span><span class="sxs-lookup"><span data-stu-id="09859-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="09859-258">Para solucionar problemas de producción, el mejor recurso es demasiado[configurar el registro de](#logging) y [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="09859-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="09859-259"><a name="explorer"></a> Paso 8: Explorador de procesos</span><span class="sxs-lookup"><span data-stu-id="09859-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="09859-260">Cuando la aplicación se escalado toomore más de una instancia, **Explorador de procesos** puede ayudarle a identificar problemas específicos de instancia.</span><span class="sxs-lookup"><span data-stu-id="09859-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="09859-261">Use el **Explorador de procesos** para:</span><span class="sxs-lookup"><span data-stu-id="09859-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="09859-262">Enumerar todos los procesos de hello en instancias diferentes de su plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09859-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="09859-263">Explorar en profundidad y ver identificadores de Hola y módulos asociados a cada proceso.</span><span class="sxs-lookup"><span data-stu-id="09859-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="09859-264">Recuento de CPU de la vista, el espacio de trabajo y el subproceso en hello procesar nivel toohelp identificar procesos descontrolados</span><span class="sxs-lookup"><span data-stu-id="09859-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="09859-265">Encontrar identificadores de archivos abiertos e incluso eliminar una instancia de proceso específica.</span><span class="sxs-lookup"><span data-stu-id="09859-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="09859-266">El explorador de procesos puede estar en **Supervisión** > **Explorador de procesos**.</span><span class="sxs-lookup"><span data-stu-id="09859-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Explorador de procesos](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="09859-268"><a name="insights"></a> Paso 9: Application Insights</span><span class="sxs-lookup"><span data-stu-id="09859-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="09859-269">**Application Insights** proporciona funcionalidades avanzadas de supervisión y generación de perfiles de aplicaciones para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="09859-270">Use Application Insights toodetect y diagnosticar los problemas de rendimiento de la aplicación Web y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="09859-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="09859-271">Puede habilitar Application Insights para su aplicación web en **Supervisión** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="09859-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="09859-272">Visión de la aplicación podría solicitar tooinstall Hola Application Insights sitio extensión toostart recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="09859-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="09859-273">Instalando la extensión de sitio de Hola provoca el reinicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09859-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="09859-275">Visión de la aplicación tiene una característica enriquecida establecido, toolearn más, seguir los vínculos de hello incluido en hello [pasos](#next) sección.</span><span class="sxs-lookup"><span data-stu-id="09859-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="09859-276"><a name="next"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09859-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="09859-277">¿Qué es Application Insights?</span><span class="sxs-lookup"><span data-stu-id="09859-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="09859-278">Supervisión del rendimiento de aplicaciones web de Azure con Application Insights</span><span class="sxs-lookup"><span data-stu-id="09859-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="09859-279">Supervisión de la disponibilidad y la capacidad de respuesta de cualquier sito web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="09859-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
