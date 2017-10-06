---
title: "aaaFix 502 puerta de enlace errónea, 503 Servicio disponible errores | Documentos de Microsoft"
description: "Solucionar los errores 502 Puerta de enlace no válida y 503 Servicio no disponible en su aplicación web hospedada en Servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 Puerta de enlace no válida, 503 Servicio no disponible, error 503, error 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="48e93-104">Solucionar los errores HTTP de "502 Puerta de enlace no válida" y "503 Servicio no disponible" en las aplicaciones web de Azure</span><span class="sxs-lookup"><span data-stu-id="48e93-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="48e93-105">"502 Puerta de enlace no válida" y "503 Servicio no disponible" son errores comunes de su aplicación web hospedada en [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="48e93-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="48e93-106">Este artículo le ayuda a solucionar estos errores.</span><span class="sxs-lookup"><span data-stu-id="48e93-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="48e93-107">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="48e93-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="48e93-108">Como alternativa, también puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="48e93-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="48e93-109">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="48e93-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="48e93-110">Síntoma</span><span class="sxs-lookup"><span data-stu-id="48e93-110">Symptom</span></span>
<span data-ttu-id="48e93-111">Al examinar la aplicación web de toohello, devuelve un HTTP error "502 pasarela incorrecta" o un HTTP error "503 Servicio no disponible".</span><span class="sxs-lookup"><span data-stu-id="48e93-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="48e93-112">Causa</span><span class="sxs-lookup"><span data-stu-id="48e93-112">Cause</span></span>
<span data-ttu-id="48e93-113">Con frecuencia este problema se debe a problemas en el nivel de la aplicación, como, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48e93-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="48e93-114">Solicitudes que tardan mucho tiempo</span><span class="sxs-lookup"><span data-stu-id="48e93-114">requests taking a long time</span></span>
* <span data-ttu-id="48e93-115">Aplicaciones que hacen un uso elevado de memoria y CPU</span><span class="sxs-lookup"><span data-stu-id="48e93-115">application using high memory/CPU</span></span>
* <span data-ttu-id="48e93-116">aplicación bloqueado debido a excepción de tooan.</span><span class="sxs-lookup"><span data-stu-id="48e93-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="48e93-117">Solución de problemas de errores de "503 Servicio no disponible" y pasos toosolve "502 puerta de enlace incorrecta"</span><span class="sxs-lookup"><span data-stu-id="48e93-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="48e93-118">El procedimiento de solución de problemas se puede dividir en tres tareas distintas, en orden secuencial:</span><span class="sxs-lookup"><span data-stu-id="48e93-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="48e93-119">Observación y supervisión del comportamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="48e93-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="48e93-120">Recopilación de datos</span><span class="sxs-lookup"><span data-stu-id="48e93-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="48e93-121">Mitigar el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="48e93-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="48e93-122">[Azure App Service Web Apps](/services/app-service/web/) ofrece diversas opciones en cada paso.</span><span class="sxs-lookup"><span data-stu-id="48e93-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="48e93-123">1. Observación y supervisión del comportamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="48e93-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="48e93-124">Seguimiento del estado del servicio</span><span class="sxs-lookup"><span data-stu-id="48e93-124">Track Service health</span></span>
<span data-ttu-id="48e93-125">Cada vez que hay una interrupción del servicio o una degradación del rendimiento, Microsoft Azure lo anuncia.</span><span class="sxs-lookup"><span data-stu-id="48e93-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="48e93-126">Puede realizar el seguimiento del estado de saludo del servicio de hello en hello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="48e93-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="48e93-127">Para más información, consulte [Track service health](../monitoring-and-diagnostics/insights-service-health.md) (Seguimiento del estado del servicio).</span><span class="sxs-lookup"><span data-stu-id="48e93-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="48e93-128">Supervisión de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="48e93-128">Monitor your web app</span></span>
<span data-ttu-id="48e93-129">Esta opción permite toofind out si la aplicación está teniendo problemas.</span><span class="sxs-lookup"><span data-stu-id="48e93-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="48e93-130">En la hoja de la aplicación web, haga clic en hello **solicitudes y errores** icono.</span><span class="sxs-lookup"><span data-stu-id="48e93-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="48e93-131">Hola **métrica** hoja mostrará todas las métricas de hello puede agregar.</span><span class="sxs-lookup"><span data-stu-id="48e93-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="48e93-132">Algunas de las métricas de Hola que podría interesarle toomonitor para su aplicación web son</span><span class="sxs-lookup"><span data-stu-id="48e93-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="48e93-133">Espacio de trabajo de memoria promedio</span><span class="sxs-lookup"><span data-stu-id="48e93-133">Average memory working set</span></span>
* <span data-ttu-id="48e93-134">Tiempo medio de respuesta</span><span class="sxs-lookup"><span data-stu-id="48e93-134">Average response time</span></span>
* <span data-ttu-id="48e93-135">Tiempo de CPU</span><span class="sxs-lookup"><span data-stu-id="48e93-135">CPU time</span></span>
* <span data-ttu-id="48e93-136">Espacio de trabajo de memoria</span><span class="sxs-lookup"><span data-stu-id="48e93-136">Memory working set</span></span>
* <span data-ttu-id="48e93-137">Solicitudes</span><span class="sxs-lookup"><span data-stu-id="48e93-137">Requests</span></span>

![supervisar la aplicación web para solucionar los errores HTTP de 502 Puerta de enlace no válida y 503 Servicio no disponible](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="48e93-139">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="48e93-139">For more information, see:</span></span>

* [<span data-ttu-id="48e93-140">Supervisión de Aplicaciones web en Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="48e93-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="48e93-141">Recibir notificaciones de alerta</span><span class="sxs-lookup"><span data-stu-id="48e93-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="48e93-142">2. Recopilación de datos</span><span class="sxs-lookup"><span data-stu-id="48e93-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="48e93-143">Usar hello Portal de soporte técnico de servicio de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="48e93-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="48e93-144">Aplicaciones Web proporciona Hola capacidad tootroubleshoot problemas relacionados tooyour web app examinando los registros, registros de eventos, los volcados de proceso HTTP y más.</span><span class="sxs-lookup"><span data-stu-id="48e93-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="48e93-145">Puede tener acceso a toda esta información con nuestro Portal de soporte técnico en **http://&lt;Nombre de la aplicación>.scm.azurewebsites.net/Support**.</span><span class="sxs-lookup"><span data-stu-id="48e93-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="48e93-146">portal de servicio de aplicaciones son compatibles con Azure Hola proporciona tres pestañas independientes toosupport Hola tres pasos de un escenario habitual de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="48e93-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="48e93-147">Observación del comportamiento actual</span><span class="sxs-lookup"><span data-stu-id="48e93-147">Observe current behavior</span></span>
2. <span data-ttu-id="48e93-148">Analizar la recopilación de información de diagnóstico y ejecución Hola analizadores integrados</span><span class="sxs-lookup"><span data-stu-id="48e93-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="48e93-149">Mitigación</span><span class="sxs-lookup"><span data-stu-id="48e93-149">Mitigate</span></span>

<span data-ttu-id="48e93-150">Si el problema de saludo se está realizando ahora mismo, haga clic en **analizar** > **diagnósticos** > **diagnosticar ahora** toocreate una sesión de diagnóstico para usted, que recopilará HTTP registra, registros del Visor de eventos, memoria volcados, registros de errores PHP y PHP procesan el informe.</span><span class="sxs-lookup"><span data-stu-id="48e93-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="48e93-151">Una vez que se recopilan los datos de hello, también se ejecutar un análisis de datos de Hola y proporcionarle un informe HTML.</span><span class="sxs-lookup"><span data-stu-id="48e93-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="48e93-152">En caso de que desea que toodownload Hola datos, de forma predeterminada, se almacenaría en la carpeta de D:\home\data\DaaS Hola.</span><span class="sxs-lookup"><span data-stu-id="48e93-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="48e93-153">Para obtener más información sobre el portal de servicio de aplicaciones son compatibles con Azure hello, consulte [tooSupport nuevas actualizaciones extensión del sitio para los sitios Web de Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="48e93-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="48e93-154">Usar hello Kudu consola de depuración</span><span class="sxs-lookup"><span data-stu-id="48e93-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="48e93-155">El servicio Web Apps incluye una consola de depuración que puede usar para depurar, explorar o cargar archivos, e incluye también puntos de conexión JSON para obtener información sobre su entorno.</span><span class="sxs-lookup"><span data-stu-id="48e93-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="48e93-156">Esto se denomina hello *Kudu consola* o hello *SCM panel* de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="48e93-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="48e93-157">Se puede tener acceso a este panel va toohello vínculo **https://&lt;el nombre de la aplicación >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="48e93-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="48e93-158">Algunos de los aspectos de Hola que Kudu ofrece son:</span><span class="sxs-lookup"><span data-stu-id="48e93-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="48e93-159">Configuración del entorno de la aplicación</span><span class="sxs-lookup"><span data-stu-id="48e93-159">environment settings for your application</span></span>
* <span data-ttu-id="48e93-160">transmisión de registro</span><span class="sxs-lookup"><span data-stu-id="48e93-160">log stream</span></span>
* <span data-ttu-id="48e93-161">Volcado de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="48e93-161">diagnostic dump</span></span>
* <span data-ttu-id="48e93-162">Depuración de la consola en la que puede ejecutar cmdlets de Powershell y comandos básicos de DOS.</span><span class="sxs-lookup"><span data-stu-id="48e93-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="48e93-163">Otra característica útil de Kudu es que, en caso de que la aplicación es producir excepciones de primera oportunidad, puede usar Kudu y volcados de memoria de hello SysInternals herramienta Procdump toocreate.</span><span class="sxs-lookup"><span data-stu-id="48e93-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="48e93-164">Estos archivos de volcado de memoria son instantáneas de proceso de Hola y a menudo le permitirá más complicados solucionar problemas relacionados con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="48e93-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="48e93-165">Para obtener más información sobre las características disponibles en Kudu, consulte [Herramientas en línea de Sitios web de Azure que debe conocer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="48e93-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="48e93-166">3. Mitigar el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="48e93-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="48e93-167">Aplicación web de escala hello</span><span class="sxs-lookup"><span data-stu-id="48e93-167">Scale hello web app</span></span>
<span data-ttu-id="48e93-168">En el servicio de aplicación de Azure, para aumentar el rendimiento y la capacidad, puede ajustar la escala de hello en el que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48e93-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="48e93-169">El escalado de una aplicación web implica dos acciones relacionadas: cambiar la tooa del plan de servicio de aplicaciones más alto nivel de precios y configurar ciertas opciones de configuración una vez que haya cambiado toohello cuanto mayor sea el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="48e93-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="48e93-170">Para obtener más información sobre el escalado, consulte [Escalado de una aplicación web en Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="48e93-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="48e93-171">Además, puede elegir toorun su aplicación en más de una instancia.</span><span class="sxs-lookup"><span data-stu-id="48e93-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="48e93-172">Esto no solo le proporciona una mayor capacidad de procesamiento, sino también algo de tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="48e93-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="48e93-173">Si hello proceso deja de funcionar en una instancia, hello otra instancia todavía seguirá servir solicitudes.</span><span class="sxs-lookup"><span data-stu-id="48e93-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="48e93-174">Puede establecer Hola escalado toobe Manual o automático.</span><span class="sxs-lookup"><span data-stu-id="48e93-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="48e93-175">Uso de AutoHeal</span><span class="sxs-lookup"><span data-stu-id="48e93-175">Use AutoHeal</span></span>
<span data-ttu-id="48e93-176">AutoHeal recicla el proceso de trabajo de hello para la aplicación en función de la configuración que elija (como los cambios de configuración, las solicitudes, límites de memoria o el tiempo de hello es necesario tooexecute una solicitud).</span><span class="sxs-lookup"><span data-stu-id="48e93-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="48e93-177">La mayoría de casos de hello, reciclar el proceso de hello es hello toorecover de manera más rápida de un problema.</span><span class="sxs-lookup"><span data-stu-id="48e93-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="48e93-178">Aunque siempre puede reiniciar una aplicación Hola desde web directamente en hello Portal de Azure, AutoHeal hará automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="48e93-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="48e93-179">Todo lo que necesita toodo es agregar algunos de los desencadenadores en el archivo web.config de la raíz de hello para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="48e93-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="48e93-180">Tenga en cuenta que esta configuración podría funcionar en hello igual manera, incluso si la aplicación no es un .net uno.</span><span class="sxs-lookup"><span data-stu-id="48e93-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="48e93-181">Para obtener más información, consulte [Recuperación automática de Sitios web de Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="48e93-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="48e93-182">Reiniciar la aplicación web de Hola</span><span class="sxs-lookup"><span data-stu-id="48e93-182">Restart hello web app</span></span>
<span data-ttu-id="48e93-183">Por lo general, suele ser hello toorecover de manera más sencilla de problemas puntuales.</span><span class="sxs-lookup"><span data-stu-id="48e93-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="48e93-184">En hello [Portal de Azure](https://portal.azure.com/), en la hoja de la aplicación web, dispone de hello opciones toostop o reiniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48e93-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![Reinicie los errores de aplicación toosolve HTTP 502 gateway erróneo y 503 Servicio no disponible](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="48e93-186">También puede administrar la aplicación web con Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="48e93-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="48e93-187">Para obtener más información, vea [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="48e93-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

