---
title: aaaMonitor un sitio de SharePoint con Application Insights
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
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="8d85a-103">Supervisión de un sitio de SharePoint con Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d85a-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="8d85a-104">Azure Hola supervisa la disponibilidad, rendimiento y uso de las aplicaciones de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d85a-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="8d85a-105">Aquí aprenderá cómo tooset que en un sitio de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8d85a-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="8d85a-106">Creación de recursos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d85a-106">Create an Application Insights resource</span></span>
<span data-ttu-id="8d85a-107">Hola [portal de Azure](https://portal.azure.com), cree un nuevo recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d85a-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="8d85a-108">Elija ASP.NET como tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="8d85a-108">Choose ASP.NET as hello application type.</span></span>

![Haga clic en Propiedades, seleccione la clave de hello y presione ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="8d85a-110">hoja de Hola que se abre es lugar de Hola donde podrá ver datos de rendimiento y uso sobre su aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d85a-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="8d85a-111">tooget atrás tooit próxima vez que inicie sesión tooAzure, debería encontrar un icono para él en la pantalla de inicio de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="8d85a-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="8d85a-112">O bien haga clic en Examinar toofind lo.</span><span class="sxs-lookup"><span data-stu-id="8d85a-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="8d85a-113">Agregar nuestras páginas web de tooyour de secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="8d85a-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="8d85a-114">En Inicio rápido, obtener script de Hola para páginas web:</span><span class="sxs-lookup"><span data-stu-id="8d85a-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="8d85a-115">Insertar el script de Hola justo antes de hello &lt;/head&gt; etiqueta de cada página que desee tootrack.</span><span class="sxs-lookup"><span data-stu-id="8d85a-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="8d85a-116">Si su sitio Web tiene una página maestra, puede colocar el script de Hola no existe.</span><span class="sxs-lookup"><span data-stu-id="8d85a-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="8d85a-117">Por ejemplo, en un proyecto de ASP.NET MVC, lo colocaría en View\Shared\\_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="8d85a-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="8d85a-118">script de Hola contiene la clave de instrumentación de Hola que dirige el recurso de Application Insights de hello telemetría tooyour.</span><span class="sxs-lookup"><span data-stu-id="8d85a-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="8d85a-119">Agregar código de hello tooyour páginas de sitio</span><span class="sxs-lookup"><span data-stu-id="8d85a-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="8d85a-120">En la página maestra Hola</span><span class="sxs-lookup"><span data-stu-id="8d85a-120">On hello master page</span></span>
<span data-ttu-id="8d85a-121">Si se puede editar la página principal del sitio de hello, que proporcionarán supervisión para todas las páginas en el sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d85a-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="8d85a-122">Visite la página principal de Hola y modificarlo con SharePoint Designer o cualquier otro editor.</span><span class="sxs-lookup"><span data-stu-id="8d85a-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="8d85a-123">Agregar código de hello justo antes de hello </head> etiqueta.</span><span class="sxs-lookup"><span data-stu-id="8d85a-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="8d85a-124">O, en páginas individuales</span><span class="sxs-lookup"><span data-stu-id="8d85a-124">Or on individual pages</span></span>
<span data-ttu-id="8d85a-125">toomonitor un conjunto limitado de páginas, agregue el script de Hola por separado tooeach página.</span><span class="sxs-lookup"><span data-stu-id="8d85a-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="8d85a-126">Insertar un elemento web e insertar el fragmento de código de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="8d85a-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="8d85a-127">Visualización de los datos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8d85a-127">View data about your app</span></span>
<span data-ttu-id="8d85a-128">Vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d85a-128">Redeploy your app.</span></span>

<span data-ttu-id="8d85a-129">Hoja de aplicaciones tooyour devuelto en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d85a-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8d85a-130">eventos primera Hola se definirán en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8d85a-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="8d85a-131">Si espera más datos, haga clic en Actualizar después de unos segundos.</span><span class="sxs-lookup"><span data-stu-id="8d85a-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="8d85a-132">En la hoja de información general de hello, haga clic en **análisis de uso** toosee toocharts de usuarios, sesiones y vistas de página:</span><span class="sxs-lookup"><span data-stu-id="8d85a-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="8d85a-133">Haga clic en cualquier toosee gráfico más detalles: por ejemplo vistas de página:</span><span class="sxs-lookup"><span data-stu-id="8d85a-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="8d85a-134">O Usuarios:</span><span class="sxs-lookup"><span data-stu-id="8d85a-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="8d85a-135">Captura del identificador de usuario</span><span class="sxs-lookup"><span data-stu-id="8d85a-135">Capturing User Id</span></span>
<span data-ttu-id="8d85a-136">fragmento de código de página web estándar de Hello no captura el Id. de usuario de Hola desde SharePoint, pero puede hacerlo con una pequeña modificación.</span><span class="sxs-lookup"><span data-stu-id="8d85a-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="8d85a-137">Copie la clave de instrumentación de la aplicación de hello Essentials desplegable en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d85a-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="8d85a-138">Sustituya la clave de instrumentación de Hola para "XXXX" en el siguiente fragmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d85a-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="8d85a-139">Incruste scripts de hello en la aplicación de SharePoint en lugar de fragmento de código de hello que obtener del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d85a-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="8d85a-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8d85a-140">Next Steps</span></span>
* <span data-ttu-id="8d85a-141">[Pruebas Web](app-insights-monitor-web-app-availability.md) toomonitor disponibilidad de Hola de su sitio.</span><span class="sxs-lookup"><span data-stu-id="8d85a-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="8d85a-142">[Application Insights](app-insights-overview.md) para otros tipos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d85a-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


