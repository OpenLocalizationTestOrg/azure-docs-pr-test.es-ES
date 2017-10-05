---
title: "Solución de los errores 502 Puerta de enlace no válida y 503 Servicio no disponible | Microsoft Docs"
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
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="bfc05-104">Solucionar los errores HTTP de "502 Puerta de enlace no válida" y "503 Servicio no disponible" en las aplicaciones web de Azure</span><span class="sxs-lookup"><span data-stu-id="bfc05-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="bfc05-105">"502 Puerta de enlace no válida" y "503 Servicio no disponible" son errores comunes de su aplicación web hospedada en [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="bfc05-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="bfc05-106">Este artículo le ayuda a solucionar estos errores.</span><span class="sxs-lookup"><span data-stu-id="bfc05-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="bfc05-107">Si necesita más ayuda en cualquier momento con este artículo, puede ponerse en contacto con los expertos de Azure en [los foros de MSDN Azure y de desbordamiento de pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="bfc05-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="bfc05-108">Como alternativa, también puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfc05-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="bfc05-109">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Obtener soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="bfc05-110">Síntoma</span><span class="sxs-lookup"><span data-stu-id="bfc05-110">Symptom</span></span>
<span data-ttu-id="bfc05-111">Cuando se dirige a la aplicación web, se devuelve un error HTTP "502 Puerta de enlace no válida" o un error HTTP "503 Servicio no disponible".</span><span class="sxs-lookup"><span data-stu-id="bfc05-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="bfc05-112">Causa</span><span class="sxs-lookup"><span data-stu-id="bfc05-112">Cause</span></span>
<span data-ttu-id="bfc05-113">Con frecuencia este problema se debe a problemas en el nivel de la aplicación, como, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bfc05-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="bfc05-114">Solicitudes que tardan mucho tiempo</span><span class="sxs-lookup"><span data-stu-id="bfc05-114">requests taking a long time</span></span>
* <span data-ttu-id="bfc05-115">Aplicaciones que hacen un uso elevado de memoria y CPU</span><span class="sxs-lookup"><span data-stu-id="bfc05-115">application using high memory/CPU</span></span>
* <span data-ttu-id="bfc05-116">Aplicaciones que se bloquean debido a una excepción.</span><span class="sxs-lookup"><span data-stu-id="bfc05-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="bfc05-117">Pasos de solución de problemas para resolver los errores "502 Puerta de enlace no válida" y "503 Servicio no disponible"</span><span class="sxs-lookup"><span data-stu-id="bfc05-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="bfc05-118">El procedimiento de solución de problemas se puede dividir en tres tareas distintas, en orden secuencial:</span><span class="sxs-lookup"><span data-stu-id="bfc05-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="bfc05-119">Observación y supervisión del comportamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bfc05-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="bfc05-120">Recopilación de datos</span><span class="sxs-lookup"><span data-stu-id="bfc05-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="bfc05-121">Mitigación del problema</span><span class="sxs-lookup"><span data-stu-id="bfc05-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="bfc05-122">[Azure App Service Web Apps](/services/app-service/web/) ofrece diversas opciones en cada paso.</span><span class="sxs-lookup"><span data-stu-id="bfc05-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="bfc05-123">1. Observación y supervisión del comportamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bfc05-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="bfc05-124">Seguimiento del estado del servicio</span><span class="sxs-lookup"><span data-stu-id="bfc05-124">Track Service health</span></span>
<span data-ttu-id="bfc05-125">Cada vez que hay una interrupción del servicio o una degradación del rendimiento, Microsoft Azure lo anuncia.</span><span class="sxs-lookup"><span data-stu-id="bfc05-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="bfc05-126">Puede realizar un seguimiento del estado del servicio en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bfc05-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="bfc05-127">Para más información, consulte [Track service health](../monitoring-and-diagnostics/insights-service-health.md) (Seguimiento del estado del servicio).</span><span class="sxs-lookup"><span data-stu-id="bfc05-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="bfc05-128">Supervisión de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bfc05-128">Monitor your web app</span></span>
<span data-ttu-id="bfc05-129">Esta opción le permite averiguar si la aplicación tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="bfc05-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="bfc05-130">En la hoja de la aplicación web, haga clic en el icono **Solicitudes y errores** .</span><span class="sxs-lookup"><span data-stu-id="bfc05-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="bfc05-131">La hoja **Métrica** mostrará todas las métricas que puede agregar.</span><span class="sxs-lookup"><span data-stu-id="bfc05-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="bfc05-132">Algunas de las métricas que podría querer supervisar para su aplicación web son:</span><span class="sxs-lookup"><span data-stu-id="bfc05-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="bfc05-133">Espacio de trabajo de memoria promedio</span><span class="sxs-lookup"><span data-stu-id="bfc05-133">Average memory working set</span></span>
* <span data-ttu-id="bfc05-134">Tiempo medio de respuesta</span><span class="sxs-lookup"><span data-stu-id="bfc05-134">Average response time</span></span>
* <span data-ttu-id="bfc05-135">Tiempo de CPU</span><span class="sxs-lookup"><span data-stu-id="bfc05-135">CPU time</span></span>
* <span data-ttu-id="bfc05-136">Espacio de trabajo de memoria</span><span class="sxs-lookup"><span data-stu-id="bfc05-136">Memory working set</span></span>
* <span data-ttu-id="bfc05-137">Solicitudes</span><span class="sxs-lookup"><span data-stu-id="bfc05-137">Requests</span></span>

![supervisar la aplicación web para solucionar los errores HTTP de 502 Puerta de enlace no válida y 503 Servicio no disponible](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="bfc05-139">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="bfc05-139">For more information, see:</span></span>

* [<span data-ttu-id="bfc05-140">Supervisión de aplicaciones web en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bfc05-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="bfc05-141">Recibir notificaciones de alerta</span><span class="sxs-lookup"><span data-stu-id="bfc05-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="bfc05-142">2. Recopilación de datos</span><span class="sxs-lookup"><span data-stu-id="bfc05-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="bfc05-143">Uso del Portal de soporte técnico del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="bfc05-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="bfc05-144">El servicio Aplicaciones web ofrece la posibilidad de solucionar los problemas relacionados con su aplicación web con solo examinar los registros HTTP, los registros de eventos, los volcados de proceso, etc.</span><span class="sxs-lookup"><span data-stu-id="bfc05-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="bfc05-145">Puede tener acceso a toda esta información con nuestro Portal de soporte técnico en **http://&lt;Nombre de la aplicación>.scm.azurewebsites.net/Support**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="bfc05-146">El Portal de soporte técnico del Servicio de aplicaciones de Azure le proporciona tres pestañas distintas correspondientes a los tres pasos de un escenario común de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="bfc05-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="bfc05-147">Observación del comportamiento actual</span><span class="sxs-lookup"><span data-stu-id="bfc05-147">Observe current behavior</span></span>
2. <span data-ttu-id="bfc05-148">Análisis mediante la recopilación de información de diagnóstico y la ejecución de los analizadores integrados</span><span class="sxs-lookup"><span data-stu-id="bfc05-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="bfc05-149">Mitigación</span><span class="sxs-lookup"><span data-stu-id="bfc05-149">Mitigate</span></span>

<span data-ttu-id="bfc05-150">Si el problema está sucediendo justo ahora, haga clic en **Analizar** > **Diagnósticos** > **Diagnosticar ahora** para crear una sesión de diagnóstico, que recopilará registros HTTP, registros del visor de eventos, volcados de memoria, registros de errores PHP e informes de procesos PHP.</span><span class="sxs-lookup"><span data-stu-id="bfc05-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="bfc05-151">Después de la recopilación de los datos, también se ejecuta un análisis de ellos y se proporciona un informe HTML.</span><span class="sxs-lookup"><span data-stu-id="bfc05-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="bfc05-152">En caso de que quiera descargar los datos, de forma predeterminada se almacenarían en la carpeta D:\home\data\DaaS.</span><span class="sxs-lookup"><span data-stu-id="bfc05-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="bfc05-153">Para obtener más información sobre el Portal de soporte técnico del Servicio de aplicaciones de Azure, consulte [Nuevas actualizaciones de la extensión de sitios de soporte técnico para Sitios web de Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="bfc05-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="bfc05-154">Uso de la consola de depuración Kudu</span><span class="sxs-lookup"><span data-stu-id="bfc05-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="bfc05-155">El servicio Aplicaciones web incluye una consola de depuración que puede usar para depurar, explorar o cargar archivos, e incluye también puntos de conexión JSON para obtener información sobre su entorno.</span><span class="sxs-lookup"><span data-stu-id="bfc05-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="bfc05-156">A esto se le denomina *Consola Kudu* o *Panel SCM* para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bfc05-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="bfc05-157">Puede tener acceso a este panel en el vínculo **https://&lt;Nombre de la aplicación>.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="bfc05-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="bfc05-158">Algunas de las cosas que proporciona Kudu son:</span><span class="sxs-lookup"><span data-stu-id="bfc05-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="bfc05-159">Configuración del entorno de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bfc05-159">environment settings for your application</span></span>
* <span data-ttu-id="bfc05-160">transmisión de registro</span><span class="sxs-lookup"><span data-stu-id="bfc05-160">log stream</span></span>
* <span data-ttu-id="bfc05-161">Volcado de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="bfc05-161">diagnostic dump</span></span>
* <span data-ttu-id="bfc05-162">Depuración de la consola en la que puede ejecutar cmdlets de Powershell y comandos básicos de DOS.</span><span class="sxs-lookup"><span data-stu-id="bfc05-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="bfc05-163">Otra característica útil de Kudu es que, en caso de que la aplicación inicie excepciones de primera oportunidad, puede usar Kudu y la herramienta Procdump de SysInternals para crear volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="bfc05-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="bfc05-164">Estos volcados de memoria son instantáneas del proceso y a menudo pueden ayudarle solucionar problemas más complicados de su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bfc05-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="bfc05-165">Para obtener más información sobre las características disponibles en Kudu, consulte [Herramientas en línea de Sitios web de Azure que debe conocer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="bfc05-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="bfc05-166">3. Mitigación del problema</span><span class="sxs-lookup"><span data-stu-id="bfc05-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="bfc05-167">Escalado de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bfc05-167">Scale the web app</span></span>
<span data-ttu-id="bfc05-168">En Azure App Service, puede ajustar la escala en la que se ejecuta la aplicación para aumentar el rendimiento y la capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="bfc05-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="bfc05-169">El escalado vertical de una aplicación web implica dos acciones relacionadas: cambiar el plan de App Service por un plan de tarifa más alto y configurar determinados valores después de haber cambiado a ese plan de tarifa más alto.</span><span class="sxs-lookup"><span data-stu-id="bfc05-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="bfc05-170">Para obtener más información sobre el escalado, consulte [Escalado de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="bfc05-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="bfc05-171">Además, puede elegir ejecutar la aplicación en más de una instancia.</span><span class="sxs-lookup"><span data-stu-id="bfc05-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="bfc05-172">Esto no solo le proporciona una mayor capacidad de procesamiento, sino también algo de tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="bfc05-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="bfc05-173">Si el proceso se interrumpe en una instancia, la otra instancia seguirá atendiendo las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="bfc05-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="bfc05-174">Puede establecer el escalado en Manual o Automático.</span><span class="sxs-lookup"><span data-stu-id="bfc05-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="bfc05-175">Uso de AutoHeal</span><span class="sxs-lookup"><span data-stu-id="bfc05-175">Use AutoHeal</span></span>
<span data-ttu-id="bfc05-176">AutoHeal recicla el proceso de trabajo para su aplicación en función de la configuración que elija (como cambios de configuración, solicitudes, límites de memoria o el tiempo necesario para ejecutar una solicitud).</span><span class="sxs-lookup"><span data-stu-id="bfc05-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="bfc05-177">Casi siempre, el proceso de reciclaje es la forma más rápida de recuperarse de un problema.</span><span class="sxs-lookup"><span data-stu-id="bfc05-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="bfc05-178">Aunque siempre puede reiniciar la aplicación web directamente en el Portal de Azure, AutoHeal lo hará automáticamente por usted.</span><span class="sxs-lookup"><span data-stu-id="bfc05-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="bfc05-179">Todo lo que debe hacer es agregar algunos desencadenadores en web.config raíz de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bfc05-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="bfc05-180">Tenga en cuenta que esta configuración funcionaría igual incluso si la aplicación no fuera .Net.</span><span class="sxs-lookup"><span data-stu-id="bfc05-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="bfc05-181">Para obtener más información, consulte [Recuperación automática de Sitios web de Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="bfc05-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="bfc05-182">Reinicio de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bfc05-182">Restart the web app</span></span>
<span data-ttu-id="bfc05-183">Suele ser la manera más sencilla de recuperarse de problemas que solo tienen lugar una vez.</span><span class="sxs-lookup"><span data-stu-id="bfc05-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="bfc05-184">En el [Portal de Azure](https://portal.azure.com/), en la hoja de la aplicación web, tiene las opciones para detener o reiniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bfc05-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![reiniciar la aplicación para solucionar los errores HTTP de 502 Puerta de enlace no válida y 503 Servicio no disponible](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="bfc05-186">También puede administrar la aplicación web con Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="bfc05-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="bfc05-187">Para obtener más información, vea [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bfc05-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

