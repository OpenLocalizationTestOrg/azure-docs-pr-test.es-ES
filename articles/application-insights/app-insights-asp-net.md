---
title: "Configuración del análisis de aplicaciones web para ASP.NET con Azure Application Insights | Microsoft Docs"
description: "Configure el análisis del rendimiento, la disponibilidad y el uso de un sitio web de ASP.NET, hospedado localmente o en Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: cb247ee68da88265f7c51258644064463d44f8b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="295b8-103">Configuración de Application Insights para un sitio web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="295b8-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="295b8-104">Este procedimiento configura una aplicación web de ASP.NET para que envíe datos de telemetría al servicio [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="295b8-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="295b8-105">Funciona en las aplicaciones ASP.NET que se hospedan en su propio servidor IIS o en la nube.</span><span class="sxs-lookup"><span data-stu-id="295b8-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="295b8-106">Obtenga gráficos y un eficaz lenguaje de consulta que le ayudarán a conocer el rendimiento de la aplicación y cómo la usan las personas, más alertas automáticas cuando aparezcan errores o haya problemas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="295b8-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="295b8-107">Muchos desarrolladores consideran que estas características son excelentes tal y como están, pero si necesita ampliar y personalizar la telemetría, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="295b8-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="295b8-108">Su instalación se realiza desde Visual Studio con unos pocos clics.</span><span class="sxs-lookup"><span data-stu-id="295b8-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="295b8-109">Tiene la opción para evitar cargos. Para ello, solo debe limitar el volumen de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="295b8-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="295b8-110">Esto le permite probar y depurar un sitio con no muchos usuarios, o incluso supervisarlo.</span><span class="sxs-lookup"><span data-stu-id="295b8-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="295b8-111">Si decide que desea supervisar su sitio de producción, no le costará trabajo aumentar el límite más adelante.</span><span class="sxs-lookup"><span data-stu-id="295b8-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="295b8-112">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="295b8-112">Before you start</span></span>
<span data-ttu-id="295b8-113">Necesita:</span><span class="sxs-lookup"><span data-stu-id="295b8-113">You need:</span></span>

* <span data-ttu-id="295b8-114">Visual Studio 2013, actualización 3 o superior.</span><span class="sxs-lookup"><span data-stu-id="295b8-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="295b8-115">Es mejor que sea superior.</span><span class="sxs-lookup"><span data-stu-id="295b8-115">Later is better.</span></span>
* <span data-ttu-id="295b8-116">Una suscripción a [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="295b8-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="295b8-117">Si su equipo u organización tiene una suscripción a Azure, el propietario puede agregarla a ella con su [cuenta Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="295b8-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="295b8-118">Si está interesado, puede examinar otros temas:</span><span class="sxs-lookup"><span data-stu-id="295b8-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="295b8-119">Instrumentación de aplicaciones web en tiempo de ejecución con Application Insights</span><span class="sxs-lookup"><span data-stu-id="295b8-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="295b8-120">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="295b8-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="295b8-121"><a name="ide"></a>Paso 1: Agregue el SDK de Application Insights</span><span class="sxs-lookup"><span data-stu-id="295b8-121"><a name="ide"></a> Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="295b8-122">Haga clic con el botón derecho en su proyecto de aplicación web en el Explorador de soluciones y elija **Agregar** > **Telemetría de Application Insights...**  o **Configurar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="295b8-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Captura de pantalla del Explorador de soluciones, con Agregar telemetría de Application Insights resaltado](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="295b8-124">(En Visual Studio 2015, también hay una opción para agregar Application Insights en el cuadro de diálogo Nuevo proyecto.)</span><span class="sxs-lookup"><span data-stu-id="295b8-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="295b8-125">Vaya a la página de configuración de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="295b8-125">Continue to the Application Insights configuration page:</span></span>

![Captura de pantalla de la página Registre la aplicación en Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="295b8-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="295b8-127">**a.**</span></span> <span data-ttu-id="295b8-128">Seleccione la cuenta y la suscripción que usa para acceder a Azure.</span><span class="sxs-lookup"><span data-stu-id="295b8-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="295b8-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="295b8-129">**b.**</span></span> <span data-ttu-id="295b8-130">Seleccione el recurso de Azure en el que desea ver los datos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="295b8-131">Por lo general:</span><span class="sxs-lookup"><span data-stu-id="295b8-131">Usually:</span></span>

* <span data-ttu-id="295b8-132">Use un [único recurso para diferentes componentes](app-insights-monitor-multi-role-apps.md) de una sola aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="295b8-133">Cree recursos independientes para las aplicaciones no relacionadas.</span><span class="sxs-lookup"><span data-stu-id="295b8-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="295b8-134">Si desea establecer el grupo de recursos o la ubicación en que se almacenan los datos, haga clic en **Parámetros de configuración**.</span><span class="sxs-lookup"><span data-stu-id="295b8-134">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="295b8-135">Los grupos de recursos se utilizan para controlar el acceso a los datos.</span><span class="sxs-lookup"><span data-stu-id="295b8-135">Resource groups are used to control access to data.</span></span> <span data-ttu-id="295b8-136">Por ejemplo, si tiene varias aplicaciones que forman parte del mismo sistema, puede poner sus datos de Application Insights en el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="295b8-136">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="295b8-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="295b8-137">**c.**</span></span> <span data-ttu-id="295b8-138">Para evitar cargos, ponga un tope en el límite de volumen de datos gratuito.</span><span class="sxs-lookup"><span data-stu-id="295b8-138">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="295b8-139">Application Insights es gratuito hasta un volumen de telemetría determinado.</span><span class="sxs-lookup"><span data-stu-id="295b8-139">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="295b8-140">Una vez que se crea el recurso, puede cambiar la opción seleccionadas en el portal. Para ello, es preciso abrir **Características y precios** >  **Administración de datos** > **Límite de volumen diario**.</span><span class="sxs-lookup"><span data-stu-id="295b8-140">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="295b8-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="295b8-141">**d.**</span></span> <span data-ttu-id="295b8-142">Haga clic en **Registrar** para avanzar y configurar Application Insights para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="295b8-142">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="295b8-143">La telemetría se enviará a [Azure Portal](https://portal.azure.com), durante la depuración y después de que se haya publicado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-143">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="295b8-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="295b8-144">**e.**</span></span> <span data-ttu-id="295b8-145">Si no desea enviar datos de telemetría al portal mientras se lleva a cabo una depuración, agregue el SDK de Application Insights a la aplicación, pero no configure ningún recurso en el portal.</span><span class="sxs-lookup"><span data-stu-id="295b8-145">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="295b8-146">Durante la depuración podrá ver la telemetría en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="295b8-146">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="295b8-147">Posteriormente, puede volver a esta página de configuración, o bien puede esperar hasta que haya implementado la aplicación y [activar la telemetría en tiempo de ejecución](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="295b8-147">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="295b8-148"><a name="run"></a>Paso 2: Ejecute la aplicación</span><span class="sxs-lookup"><span data-stu-id="295b8-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="295b8-149">Ejecute la aplicación con F5.</span><span class="sxs-lookup"><span data-stu-id="295b8-149">Run your app with F5.</span></span> <span data-ttu-id="295b8-150">Abra distintas páginas para generar telemetría.</span><span class="sxs-lookup"><span data-stu-id="295b8-150">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="295b8-151">En Visual Studio, aparece un recuento de los eventos que se han registrado.</span><span class="sxs-lookup"><span data-stu-id="295b8-151">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Captura de pantalla de Visual Studio.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="295b8-154">Paso 3: Vea su telemetría</span><span class="sxs-lookup"><span data-stu-id="295b8-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="295b8-155">La telemetría se puede ver en Visual Studio o en el portal web de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="295b8-155">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="295b8-156">Busque telemetría en Visual Studio, ya que le ayudará a depurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-156">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="295b8-157">Supervise el rendimiento y uso en el portal web cuando el sistema esté activo.</span><span class="sxs-lookup"><span data-stu-id="295b8-157">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="295b8-158">Visualización de datos de telemetría en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="295b8-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="295b8-159">En Visual Studio, abra la ventana de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="295b8-159">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="295b8-160">Haga clic en el botón **Application Insights** o haga clic con el botón derecho en el Explorador de soluciones, seleccione **Application Insights** y, después, haga clic en el proyecto en **Buscar telemetría activa**.</span><span class="sxs-lookup"><span data-stu-id="295b8-160">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="295b8-161">En la ventana de búsqueda de Application Insights de Visual Studio, en la vista de **datos de la sesión de depuración** encontrará la telemetría generada en el lado del servidor de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-161">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="295b8-162">Experimente con los filtros y haga clic en cualquier evento para ver más información al respecto.</span><span class="sxs-lookup"><span data-stu-id="295b8-162">Experiment with the filters, and click any event to see more detail.</span></span>

![Captura de pantalla de la vista de datos de la sesión de depuración en la ventana de Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="295b8-164">Si no ve datos, asegúrese de que el intervalo de tiempo es correcto y haga clic en el icono de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="295b8-164">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="295b8-165">[Más información acerca de las herramientas de Application Insights en Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="295b8-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="295b8-166">Visualización de datos de telemetría en el portal web</span><span class="sxs-lookup"><span data-stu-id="295b8-166">See telemetry in web portal</span></span>

<span data-ttu-id="295b8-167">La telemetría también se puede ver en el portal web de Application Insights (salvo que se elija instalar solo el SDK).</span><span class="sxs-lookup"><span data-stu-id="295b8-167">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="295b8-168">El portal tiene más gráficos, herramientas de análisis y vistas de componentes que Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="295b8-168">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="295b8-169">El portal también ofrece alertas.</span><span class="sxs-lookup"><span data-stu-id="295b8-169">The portal also provides alerts.</span></span>

<span data-ttu-id="295b8-170">Abra el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="295b8-170">Open your Application Insights resource.</span></span> <span data-ttu-id="295b8-171">Inicie sesión en [Azure Portal](https://portal.azure.com/) y búsquelo allí, o haga clic en el proyecto en Visual Studio y deje que lo lleve allí.</span><span class="sxs-lookup"><span data-stu-id="295b8-171">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Captura de pantalla de Visual Studio, en la que se muestra cómo abrir el portal de Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="295b8-173">Si recibe un error de acceso, es posible que tenga más de un conjunto de credenciales de Microsoft y que haya iniciado sesión con el erróneo.</span><span class="sxs-lookup"><span data-stu-id="295b8-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="295b8-174">En el portal, cierre la sesión y vuelva a iniciarla.</span><span class="sxs-lookup"><span data-stu-id="295b8-174">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="295b8-175">El portal se abrirá en una vista de los datos de telemetría de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-175">The portal opens on a view of the telemetry from your app.</span></span>

![Captura de pantalla de la página de información general de Application Insights](./media/app-insights-asp-net/66.png)

<span data-ttu-id="295b8-177">En el portal, haga clic en cualquier icono para ver su contenido con mayor detalle.</span><span class="sxs-lookup"><span data-stu-id="295b8-177">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="295b8-178">[Más información acerca del uso de Application Insights en Azure Portal](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="295b8-178">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="295b8-179">Paso 4: Publique la aplicación</span><span class="sxs-lookup"><span data-stu-id="295b8-179">Step 4: Publish your app</span></span>
<span data-ttu-id="295b8-180">Publique su aplicación en el servidor IIS o en Azure.</span><span class="sxs-lookup"><span data-stu-id="295b8-180">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="295b8-181">Consulte [Secuencia de métricas en directo](app-insights-metrics-explorer.md#live-metrics-stream) para asegurarse de que todo está ejecutándose sin problemas.</span><span class="sxs-lookup"><span data-stu-id="295b8-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="295b8-182">La telemetría se crea en el portal de Application Insights, donde puede supervisar las métricas, buscar en la telemetría y configurar los [paneles](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="295b8-182">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="295b8-183">También puede usar el eficaz [lenguaje de consulta de Log Analytics](https://docs.loganalytics.io/) para analizar el uso y el rendimiento o para buscar eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="295b8-183">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="295b8-184">También puede seguir analizando la telemetría en [Visual Studio](app-insights-visual-studio.md) con herramientas como búsqueda de diagnóstico y las [tendencias](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="295b8-184">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="295b8-185">Si la aplicación envía suficiente telemetría que se acerque a las [limitaciones de peticiones](app-insights-pricing.md#limits-summary), se activará el [muestreo](app-insights-sampling.md) automático.</span><span class="sxs-lookup"><span data-stu-id="295b8-185">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="295b8-186">El muestreo reduce la cantidad de datos de telemetría enviados desde su aplicación, a la vez que conserva los datos correlacionados para fines de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="295b8-186">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="295b8-187"><a name="land"></a>Ya está listo</span><span class="sxs-lookup"><span data-stu-id="295b8-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="295b8-188">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="295b8-188">Congratulations!</span></span> <span data-ttu-id="295b8-189">Ha instalado el paquete de Application Insights en la aplicación y lo ha configurado para que envíe telemetría al servicio Application Insights en Azure.</span><span class="sxs-lookup"><span data-stu-id="295b8-189">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Diagrama del movimiento de la telemetría](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="295b8-191">El recurso de Azure que recibe la telemetría de la aplicación se identifica mediante una *clave de instrumentación*,</span><span class="sxs-lookup"><span data-stu-id="295b8-191">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="295b8-192">que se encuentra en el archivo ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="295b8-192">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="295b8-193">Actualización a futuras versiones del SDK</span><span class="sxs-lookup"><span data-stu-id="295b8-193">Upgrade to future SDK versions</span></span>
<span data-ttu-id="295b8-194">Para actualizar a una [nueva versión del SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), vuelva a abrir el **Administrador de paquetes NuGet** y filtre por los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="295b8-194">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="295b8-195">Seleccione **Microsoft.ApplicationInsights.Web** y elija **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="295b8-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="295b8-196">Si ha hecho alguna personalización en ApplicationInsights.config, guarde una copia del mismo antes de realizar la actualización.</span><span class="sxs-lookup"><span data-stu-id="295b8-196">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="295b8-197">Luego, combine los cambios en la nueva versión.</span><span class="sxs-lookup"><span data-stu-id="295b8-197">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="295b8-198">Vídeo</span><span class="sxs-lookup"><span data-stu-id="295b8-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="295b8-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="295b8-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="295b8-200">Más telemetría</span><span class="sxs-lookup"><span data-stu-id="295b8-200">More telemetry</span></span>

* <span data-ttu-id="295b8-201">**[Datos de carga de página y explorador](app-insights-javascript.md)**: inserte un fragmento de código en las páginas web.</span><span class="sxs-lookup"><span data-stu-id="295b8-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="295b8-202">**[Obtenga una supervisión más detallada de las dependencias y excepciones](app-insights-monitor-performance-live-website-now.md)**: instale el Monitor de estado en el servidor.</span><span class="sxs-lookup"><span data-stu-id="295b8-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="295b8-203">**[Codifique eventos personalizados](app-insights-api-custom-events-metrics.md)** para contar, cronometrar y medir las acciones de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="295b8-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="295b8-204">**[Obtenga datos del registro](app-insights-asp-net-trace-logs.md)**: ponga en correlación los datos del registro con la telemetría.</span><span class="sxs-lookup"><span data-stu-id="295b8-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="295b8-205">Análisis</span><span class="sxs-lookup"><span data-stu-id="295b8-205">Analysis</span></span>

* <span data-ttu-id="295b8-206">**[Trabajo con Application Insights en Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="295b8-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="295b8-207">Incluye información acerca de la depuración con telemetría, la búsqueda de diagnóstico y la profundización en el código.</span><span class="sxs-lookup"><span data-stu-id="295b8-207">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="295b8-208">**[Trabajo con el portal de Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="295b8-208">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="295b8-209">Incluye información acerca de los paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y exportación de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="295b8-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="295b8-210">**[Analytics](app-insights-analytics-tour.md)**: eficaz lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="295b8-210">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="295b8-211">Alertas</span><span class="sxs-lookup"><span data-stu-id="295b8-211">Alerts</span></span>

* <span data-ttu-id="295b8-212">[Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md): cree estas pruebas para asegurarse de que el sitio se ve en la web.</span><span class="sxs-lookup"><span data-stu-id="295b8-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="295b8-213">[Diagnósticos inteligentes](app-insights-proactive-diagnostics.md): estas pruebas se realizan automáticamente, por lo que no es preciso hacer nada para configurarlas.</span><span class="sxs-lookup"><span data-stu-id="295b8-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="295b8-214">Le indican si la aplicación tiene una tasa de solicitudes con error inusual.</span><span class="sxs-lookup"><span data-stu-id="295b8-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="295b8-215">[Alertas de métricas](app-insights-alerts.md): establézcalas para que le adviertan si una métrica supera un umbral.</span><span class="sxs-lookup"><span data-stu-id="295b8-215">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="295b8-216">Puede establecerlas en las métricas personalizadas que codifique en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="295b8-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="295b8-217">Automation</span><span class="sxs-lookup"><span data-stu-id="295b8-217">Automation</span></span>

* [<span data-ttu-id="295b8-218">Creación de recursos de Application Insights mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="295b8-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
