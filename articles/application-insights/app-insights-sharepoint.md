---
title: "Supervisión de un sitio de SharePoint con Application Insights"
description: "Inicio de la supervisión de una nueva aplicación con una nueva clave de instrumentación"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: a3b37674469a131016f46af590e1eee3ba4cdc73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="33642-103">Supervisión de un sitio de SharePoint con Application Insights</span><span class="sxs-lookup"><span data-stu-id="33642-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="33642-104">Azure Application Insights le permite supervisar la disponibilidad, el rendimiento y el uso de sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="33642-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="33642-105">Aquí aprenderá a configurarlo para un sitio de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="33642-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="33642-106">Creación de recursos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="33642-106">Create an Application Insights resource</span></span>
<span data-ttu-id="33642-107">En el [portal de Azure](https://portal.azure.com), cree un nuevo recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="33642-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="33642-108">Elija ASP.NET como el tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="33642-108">Choose ASP.NET as the application type.</span></span>

![Haga clic en Propiedades, seleccione la clave y presione ctrl + C.](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="33642-110">En la hoja que se abre podrá ver los datos de uso y rendimiento sobre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33642-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="33642-111">Para volver a ella la próxima vez que inicie sesión en Azure, encontrará un icono correspondiente en la pantalla de inicio.</span><span class="sxs-lookup"><span data-stu-id="33642-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="33642-112">También puede hacer clic en Examinar para buscarla.</span><span class="sxs-lookup"><span data-stu-id="33642-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="33642-113">Agregar nuestro script a las páginas web</span><span class="sxs-lookup"><span data-stu-id="33642-113">Add our script to your web pages</span></span>
<span data-ttu-id="33642-114">En Inicio rápido, obtenga el script para páginas web:</span><span class="sxs-lookup"><span data-stu-id="33642-114">In Quick Start, get the script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="33642-115">Inserte el script justo antes de la etiqueta &lt;/head&gt; de cada página que desea seguir. Si su sitio web tiene una página maestra, puede colocar el script allí.</span><span class="sxs-lookup"><span data-stu-id="33642-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="33642-116">Por ejemplo, en un proyecto de ASP.NET MVC, lo colocaría en View\Shared\\_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="33642-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="33642-117">El script contiene la clave de instrumentación que dirige los datos de telemetría al recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="33642-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="33642-118">Agregar el código a las páginas del sitio</span><span class="sxs-lookup"><span data-stu-id="33642-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="33642-119">En la página maestra</span><span class="sxs-lookup"><span data-stu-id="33642-119">On the master page</span></span>
<span data-ttu-id="33642-120">Si se puede editar la página maestra del sitio, dispondrá de supervisión para cada página del sitio.</span><span class="sxs-lookup"><span data-stu-id="33642-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="33642-121">Desproteja y edite la página maestra mediante SharePoint Designer o cualquier otro editor.</span><span class="sxs-lookup"><span data-stu-id="33642-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="33642-122">Agregue el código justo antes de la etiqueta </head> .</span><span class="sxs-lookup"><span data-stu-id="33642-122">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="33642-123">O, en páginas individuales</span><span class="sxs-lookup"><span data-stu-id="33642-123">Or on individual pages</span></span>
<span data-ttu-id="33642-124">Para supervisar un conjunto limitado de páginas, agregue el script por separado a cada página.</span><span class="sxs-lookup"><span data-stu-id="33642-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="33642-125">Inserte un elemento web e incruste el fragmento de código en él.</span><span class="sxs-lookup"><span data-stu-id="33642-125">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="33642-126">Visualización de los datos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="33642-126">View data about your app</span></span>
<span data-ttu-id="33642-127">Vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33642-127">Redeploy your app.</span></span>

<span data-ttu-id="33642-128">Vuelva a la hoja de la aplicación en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33642-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="33642-129">Los primeros eventos aparecerán en Búsqueda.</span><span class="sxs-lookup"><span data-stu-id="33642-129">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="33642-130">Si espera más datos, haga clic en Actualizar después de unos segundos.</span><span class="sxs-lookup"><span data-stu-id="33642-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="33642-131">En la hoja de introducción, haga clic en **Análisis de uso** para ver a los gráficos de los usuarios, sesiones y vistas de páginas:</span><span class="sxs-lookup"><span data-stu-id="33642-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="33642-132">Haga clic en cualquier gráfico para ver más detalles: por ejemplo, Vistas de página:</span><span class="sxs-lookup"><span data-stu-id="33642-132">Click any chart to see more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="33642-133">O Usuarios:</span><span class="sxs-lookup"><span data-stu-id="33642-133">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="33642-134">Captura del identificador de usuario</span><span class="sxs-lookup"><span data-stu-id="33642-134">Capturing User Id</span></span>
<span data-ttu-id="33642-135">El fragmento de código de una página web estándar no captura el identificador de usuario de SharePoint, pero una pequeña modificación le permitirá hacerlo.</span><span class="sxs-lookup"><span data-stu-id="33642-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="33642-136">Copie la clave de instrumentación de la aplicación de la lista desplegable Essentials en Application Insights .</span><span class="sxs-lookup"><span data-stu-id="33642-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="33642-137">En el siguiente fragmento, sustituya la clave de instrumentación por "XXXX".</span><span class="sxs-lookup"><span data-stu-id="33642-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="33642-138">Inserte el script en la aplicación de SharePoint en lugar del fragmento de código que obtenga desde el portal.</span><span class="sxs-lookup"><span data-stu-id="33642-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="33642-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33642-139">Next Steps</span></span>
* <span data-ttu-id="33642-140">[Pruebas web](app-insights-monitor-web-app-availability.md) para supervisar la disponibilidad de su sitio.</span><span class="sxs-lookup"><span data-stu-id="33642-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="33642-141">[Application Insights](app-insights-overview.md) para otros tipos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="33642-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


