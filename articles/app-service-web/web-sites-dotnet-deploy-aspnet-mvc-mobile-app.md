---
title: "aplicación web móvil de aaaDeploy un MVC de ASP.NET 5 en el servicio de aplicación de Azure"
description: "Un tutorial que le enseña cómo toodeploy una tooAzure de aplicación web servicio de aplicaciones con móviles características en ASP.NET MVC de aplicación web 5."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="237d5-103">Implementar una aplicación web móvil de ASP.NET MVC 5 en el servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="237d5-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="237d5-104">Este tutorial le mostrará también Hola conceptos básicos de cómo toobuild un 5 de MVC de ASP.NET web aplicación que está preparado para dispositivos móviles e implementarlo tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="237d5-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="237d5-105">Para este tutorial, necesita [Visual Studio Express 2013 para Web] [ Visual Studio Express 2013] Hola edición o professional de Visual Studio si ya tienes que.</span><span class="sxs-lookup"><span data-stu-id="237d5-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="237d5-106">Puede usar [Visual Studio 2015] pero capturas de pantalla de hello serán diferentes y se deben utilizar plantillas de hello ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="237d5-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="237d5-107">Lo que creará</span><span class="sxs-lookup"><span data-stu-id="237d5-107">What You'll Build</span></span>
<span data-ttu-id="237d5-108">Para este tutorial, agregará características para móviles toohello conferencia lista aplicación simple que se proporciona en hello [proyecto inicial][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="237d5-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="237d5-109">Hello captura de pantalla siguiente muestra las sesiones ASP.NET de hello en aplicación Hola completado, tal como se muestra en el emulador de explorador hello en herramientas de desarrollo F12 de Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="237d5-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="237d5-110">Puede usar herramientas de desarrollo F12 de Internet Explorer 11 Hola y Hola [herramienta Fiddler] [ Fiddler] toohelp depurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="237d5-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="237d5-111">Habilidades que aprenderá</span><span class="sxs-lookup"><span data-stu-id="237d5-111">Skills You'll Learn</span></span>
<span data-ttu-id="237d5-112">Aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="237d5-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="237d5-113">¿Cómo toouse Visual Studio 2013 toopublish su aplicación web directamente tooa aplicación web en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="237d5-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="237d5-114">Cómo plantillas Hola ASP.NET MVC 5 usar framework de arranque de CSS de Hola para mejorar la visualización en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="237d5-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="237d5-115">¿Cómo toocreate específica para equipos móviles vistas exploradores móviles específico tootarget, como Hola iPhone y Android</span><span class="sxs-lookup"><span data-stu-id="237d5-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="237d5-116">¿Cómo toocreate respondiendo vistas (vistas que respondan toodifferent exploradores en todos los dispositivos)</span><span class="sxs-lookup"><span data-stu-id="237d5-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="237d5-117">Configurar el entorno de desarrollo de Hola</span><span class="sxs-lookup"><span data-stu-id="237d5-117">Set up hello development environment</span></span>
<span data-ttu-id="237d5-118">Configurar el entorno de desarrollo instalando hello Azure SDK para .NET 2.5.1 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="237d5-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="237d5-119">tooinstall hello Azure SDK para. NET, haga clic en el siguiente vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="237d5-120">Si no tiene Visual Studio 2013 instalado todavía, se instalará por el vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="237d5-121">Este tutorial requiere Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="237d5-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="237d5-122">[Azure SDK para Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="237d5-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="237d5-123">En la ventana del instalador de plataforma Web de hello, haga clic en **instalar** y continuar con la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="237d5-124">También necesitará un emulador de explorador móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="237d5-125">Ninguno de los siguientes Hola funcionará:</span><span class="sxs-lookup"><span data-stu-id="237d5-125">Any of hello following will work:</span></span>

* <span data-ttu-id="237d5-126">Emulador de explorador en las herramientas para desarrolladores de [Internet Explorer 11 F12][EmulatorIE11] (se usan en todas las capturas de pantalla de explorador móvil).</span><span class="sxs-lookup"><span data-stu-id="237d5-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="237d5-127">Cuenta con los calores predefinidos de cadena de agente de usuario para Windows Phone 8, Windows Phone 7 y Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="237d5-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="237d5-128">Emulador de explorador en [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="237d5-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="237d5-129">Contiene valores predefinidos para varios dispositivos Android, así como Apple iPhone, Apple iPad y Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="237d5-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="237d5-130">También emula eventos táctiles.</span><span class="sxs-lookup"><span data-stu-id="237d5-130">It also emulates touch events.</span></span>
* <span data-ttu-id="237d5-131">[Emulador de Opera Mobile][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="237d5-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="237d5-132">Proyectos de Visual Studio con C\# código fuente está tooaccompany disponible en este tema:</span><span class="sxs-lookup"><span data-stu-id="237d5-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="237d5-133">[Descarga del proyecto inicial][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="237d5-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="237d5-134">[Descarga del proyecto completado][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="237d5-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="237d5-135"><a name="bkmk_DeployStarterProject"></a>Implementar la aplicación web de Azure de hello starter proyecto tooan</span><span class="sxs-lookup"><span data-stu-id="237d5-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="237d5-136">Descargar la aplicación de lista de la conferencia de hello [proyecto inicial][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="237d5-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="237d5-137">A continuación, en el Explorador de Windows, haga clic en archivo ZIP de descarga de Hola y elija *propiedades*.</span><span class="sxs-lookup"><span data-stu-id="237d5-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="237d5-138">Hola **propiedades** diálogo cuadro, elija hello **Unblock** botón.</span><span class="sxs-lookup"><span data-stu-id="237d5-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="237d5-139">(Desbloqueo impide que una advertencia de seguridad que se produce cuando intenta toouse un *.zip* archivo que descargó desde web Hola.)</span><span class="sxs-lookup"><span data-stu-id="237d5-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="237d5-140">Haga clic en archivo ZIP de Hola y seleccione **extraer todo** para descomprimir el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="237d5-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="237d5-141">En Visual Studio, abra hello *C#\Mvc5Mobile.sln* archivo.</span><span class="sxs-lookup"><span data-stu-id="237d5-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="237d5-142">En el Explorador de soluciones, haga clic en proyecto de Hola y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="237d5-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="237d5-143">En Publicación web, haga clic en **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="237d5-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="237d5-144">Si aún no inició sesión en Azure, haga clic en **Agregar una cuenta**.</span><span class="sxs-lookup"><span data-stu-id="237d5-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="237d5-145">Siga toolog de mensajes de Hola en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="237d5-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="237d5-146">Hola, cuadro de diálogo de servicio de aplicaciones debería aparecer ahora como iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="237d5-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="237d5-147">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="237d5-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="237d5-148">Hola **nombre de la aplicación Web** , a continuación, especifique un prefijo de nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="237d5-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="237d5-149">El nombre completo del sitio será *&lt;prefijo>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="237d5-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="237d5-150">Además, seleccione o especifique un nuevo nombre de grupo de recursos en **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="237d5-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="237d5-151">A continuación, haga clic en **New** toocreate un nuevo plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="237d5-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="237d5-152">Configurar Hola nuevo plan de servicio de aplicaciones y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="237d5-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="237d5-153">En cuadro de diálogo de hello crear servicio en la aplicación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="237d5-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="237d5-154">Después de hello recursos de Azure se crean, cuadro de diálogo de publicación Web de Hola se rellenará con valores de hello para la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="237d5-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="237d5-155">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="237d5-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="237d5-156">Una vez que Visual Studio finaliza la aplicación web de Azure starter proyecto toohello de publicación hello, Explorador de escritorio de hello abre la aplicación web en directo de toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="237d5-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="237d5-157">Inicie el emulador de explorador móvil, copie la dirección URL de hello para la aplicación de la conferencia de hello (*<prefix>*. azurewebsites.net) en el emulador de Windows hello y, a continuación, haga clic en el botón de la parte superior derecha y seleccione **Examinar por etiqueta**.</span><span class="sxs-lookup"><span data-stu-id="237d5-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="237d5-158">Si usa Internet Explorer 11 como explorador predeterminado de hello, solo deberá tootype `F12`, a continuación, `Ctrl+8`y, a continuación, cambiar perfil de explorador Hola demasiado**de Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="237d5-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="237d5-159">La imagen siguiente muestra hello *AllTags* vista en modo vertical (de la elección de **Examinar por etiqueta**).</span><span class="sxs-lookup"><span data-stu-id="237d5-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="237d5-160">Aunque puede depurar su aplicación de MVC 5 desde dentro de Visual Studio, puede publicar su tooAzure de aplicación web nuevo tooverify hello en vivo aplicación web directamente desde el explorador móvil o un emulador de explorador.</span><span class="sxs-lookup"><span data-stu-id="237d5-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="237d5-161">Visualización de Hello es muy legible en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="237d5-162">También puede ver algunos efectos visuales de hello aplicados por el marco de trabajo de hello Bootstrap CSS.</span><span class="sxs-lookup"><span data-stu-id="237d5-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="237d5-163">Haga clic en hello **ASP.NET** vínculo.</span><span class="sxs-lookup"><span data-stu-id="237d5-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="237d5-164">Hola vista de etiqueta ASP.NET es pantalla toohello ajusta el zoom, que arranque realiza automáticamente de forma automática.</span><span class="sxs-lookup"><span data-stu-id="237d5-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="237d5-165">Sin embargo, puede mejorar este explorador móvil vista toobetter palo Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="237d5-166">Por ejemplo, hello **fecha** columna es difícil de leer.</span><span class="sxs-lookup"><span data-stu-id="237d5-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="237d5-167">Más adelante en el tutorial Hola cambiará hello *AllTags* ver toomake, preparadas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="237d5-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="237d5-168"><a name="bkmk_bootstrap"></a> Marco Bootstrap CSS</span><span class="sxs-lookup"><span data-stu-id="237d5-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="237d5-169">Nuevo en hello MVC 5 plantilla es la compatibilidad integrada de arranque.</span><span class="sxs-lookup"><span data-stu-id="237d5-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="237d5-170">Ya hemos visto cómo mejora inmediatamente vistas diferentes de hello en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="237d5-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="237d5-171">Por ejemplo, barra de navegación superior de Hola Hola es contraíble automáticamente al ancho del explorador de hello es pequeño.</span><span class="sxs-lookup"><span data-stu-id="237d5-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="237d5-172">En el Explorador de escritorio de hello, intente cambiar el tamaño de la ventana del explorador de Hola y ver cómo la barra de navegación de hello cambia su apariencia y funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="237d5-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="237d5-173">Se trata de diseño de web con capacidad de respuesta de Hola que está integrado en el arranque.</span><span class="sxs-lookup"><span data-stu-id="237d5-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="237d5-174">toosee cómo la aplicación Web de hello sería sin arranque, abra *aplicación\_iniciar\\BundleConfig.cs* y marque como comentario las líneas de Hola que contengan *bootstrap.js* y *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="237d5-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="237d5-175">Hello código siguiente muestra hello las dos últimas instrucciones de hello `RegisterBundles` método después de cambiar de hello:</span><span class="sxs-lookup"><span data-stu-id="237d5-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="237d5-176">Presione `Ctrl+F5` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="237d5-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="237d5-177">Observe que esa barra de navegación contraíble Hola ahora es simplemente una lista sin ordenar normal.</span><span class="sxs-lookup"><span data-stu-id="237d5-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="237d5-178">Haga nuevamente clic en **Explorar por etiqueta** y luego haga clic en **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="237d5-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="237d5-179">En la vista del emulador de dispositivos móviles de hello, verá ahora que ya no es pantalla toohello ajusta el zoom y debe desplazar hacia un lado en orden toosee Hola derecha de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="237d5-180">Deshacer los cambios y actualizar Hola explorador móvil tooverify que se ha restaurado la presentación de hello preparadas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="237d5-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="237d5-181">Bootstrap no es específico tooASP.NET MVC 5, y puede aprovechar estas características en cualquier aplicación web.</span><span class="sxs-lookup"><span data-stu-id="237d5-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="237d5-182">Sin embargo, ahora está integrado en la plantilla de proyecto de ASP.NET MVC 5, por lo que su aplicación web MVC 5 puede sacar provecho de Bootstrap de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="237d5-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="237d5-183">Para obtener más información acerca de arranque, consulte toothe [arranque] [ BootstrapSite] sitio.</span><span class="sxs-lookup"><span data-stu-id="237d5-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="237d5-184">En la sección siguiente Hola verá cómo vistas específicas de tooprovide explorador móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="237d5-185"><a name="bkmk_overrideviews"></a>Reemplazar Hola vistas, diseños y las vistas parciales</span><span class="sxs-lookup"><span data-stu-id="237d5-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="237d5-186">Puede reemplazar cualquier vista (incluidos los diseños y las vistas parciales) para exploradores móviles en general, para un explorador móvil individual o para cualquier explorador específico.</span><span class="sxs-lookup"><span data-stu-id="237d5-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="237d5-187">ver de un determinado mobile tooprovide, puede copiar un archivo de vista y agregar *. Mobile* toohello nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="237d5-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="237d5-188">Toocreate por ejemplo, un teléfono móvil *índice* vista, puede copiar *vistas\\inicio\\Index.cshtml* a *vistas\\inicio\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="237d5-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="237d5-189">En esta sección, creará un archivo de diseño específico para móviles.</span><span class="sxs-lookup"><span data-stu-id="237d5-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="237d5-190">toostart, copia *vistas\\Shared\\\_Layout.cshtml* a *vistas\\Shared\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="237d5-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="237d5-191">Abra  *\_Layout.Mobile.cshtml* y cambie el título de Hola de **MVC5 aplicación** demasiado**MVC5 aplicación (móvil)**.</span><span class="sxs-lookup"><span data-stu-id="237d5-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="237d5-192">En cada uno de ellos `Html.ActionLink` prevén la barra de navegación de hello, quite "Buscar por" en cada vínculo *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="237d5-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="237d5-193">Hello código siguiente muestra hello completado `<ul class="nav navbar-nav">` etiqueta del archivo de diseño móviles Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="237d5-194">Hola copia *vistas\\inicio\\AllTags.cshtml* del archivo a *vistas\\inicio\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="237d5-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="237d5-195">Abra el archivo nuevo de hello y cambie el `<h2>` elemento de "Etiquetas" demasiado "etiquetas (M)":</span><span class="sxs-lookup"><span data-stu-id="237d5-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="237d5-196">Examinar toohello etiquetas página utilizando un explorador de escritorio y el emulador de explorador móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="237d5-197">emulador de explorador móvil Hello muestra hello dos cambios realizados (Hola título de  *\_Layout.Mobile.cshtml* y el título de Hola de *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="237d5-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="237d5-198">En cambio, no ha cambiado la visualización de escritorio de hello (con títulos de  *\_Layout.cshtml* y *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="237d5-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="237d5-199"><a name="bkmk_browserviews"></a> Creación de vistas específicas de explorador</span><span class="sxs-lookup"><span data-stu-id="237d5-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="237d5-200">Además vistas específicas de escritorio y toomobile, puede crear vistas para un explorador individual.</span><span class="sxs-lookup"><span data-stu-id="237d5-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="237d5-201">Por ejemplo, puede crear vistas que son específicos para iPhone de Hola o explorador Android Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="237d5-202">En esta sección, creará un diseño para una versión de iPhone de Hola y de explorador de iPhone de hello *AllTags* vista.</span><span class="sxs-lookup"><span data-stu-id="237d5-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="237d5-203">Abra hello *Global.asax* de archivos y agregar Hola después de la parte inferior de toohello de código de la `Application_Start` método.</span><span class="sxs-lookup"><span data-stu-id="237d5-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="237d5-204">Este código define un nuevo modo de visualización llamado "iPhone" que se comparará con cada solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="237d5-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="237d5-205">Si la solicitud entrante de hello coincide con la condición definida (es decir, si el agente de usuario de hello contiene la cadena hello "iPhone"), ASP.NET MVC buscará vistas cuyo nombre contiene el sufijo "iPhone".</span><span class="sxs-lookup"><span data-stu-id="237d5-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="237d5-206">Al agregar específicas del explorador móvil modos de presentación, como para iPhone y Android, ser seguro tooset Hola primeros argumentos demasiado`0` (inserción en la parte superior de Hola de lista de Hola) toomake seguro de que el modo de explorador específico hello tiene prioridad sobre la plantilla móvil Hola (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="237d5-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="237d5-207">Si Hola móviles plantilla princip Hola de lista de hello en su lugar, se seleccionará en el modo de presentación deseado (Hola wins primera coincidencia y plantilla móvil Hola coincide con todos los exploradores móviles).</span><span class="sxs-lookup"><span data-stu-id="237d5-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="237d5-208">En el código de hello, haga clic en `DefaultDisplayMode`, elija **resolver**y, a continuación, elija `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="237d5-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="237d5-209">Esto agrega una referencia toothe `System.Web.WebPages` espacio de nombres, que es donde el `DisplayModeProvider` y `DefaultDisplayMode` se definen los tipos.</span><span class="sxs-lookup"><span data-stu-id="237d5-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="237d5-210">Como alternativa, puede agregar simplemente manualmente Hola después línea toothe `using` sección del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="237d5-211">Guarde los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-211">Save hello changes.</span></span> <span data-ttu-id="237d5-212">Copie el archivo *Views\\Shared\\\_Layout.Mobile.cshtml* a *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="237d5-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="237d5-213">Abra Hola nuevo archivo y, a continuación, Cambiar título Hola de `MVC5 Application (Mobile)` a `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="237d5-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="237d5-214">Hola copia *vistas\\inicio\\AllTags.Mobile.cshtml* del archivo a *vistas\\inicio\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="237d5-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="237d5-215">En el nuevo archivo hello, cambie hello `<h2>` elemento de "etiquetas (M)" demasiadas "etiquetas (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="237d5-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="237d5-216">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="237d5-216">Run hello application.</span></span> <span data-ttu-id="237d5-217">Ejecutar un emulador de explorador móvil, asegúrese de que el agente de usuario se establece demasiado "iPhone" y examinar toohello *AllTags* vista.</span><span class="sxs-lookup"><span data-stu-id="237d5-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="237d5-218">Si usas emulador hello en herramientas de desarrollo F12 de Internet Explorer 11, configure siguiente de toohello de emulación:</span><span class="sxs-lookup"><span data-stu-id="237d5-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="237d5-219">Perfil de explorador = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="237d5-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="237d5-220">Cadena de agente de usuario = **Custom**</span><span class="sxs-lookup"><span data-stu-id="237d5-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="237d5-221">Cadena personalizada = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="237d5-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="237d5-222">captura de pantalla siguiente Hello muestra hello *AllTags* vista representada en el emulador en herramientas de desarrollo F12 de Internet Explorer 11 con la cadena de agente de usuario personalizado de hello (Esto es una cadena de agente de usuario de iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="237d5-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="237d5-223">En el explorador móvil de hello, seleccione hello **altavoces** vínculo.</span><span class="sxs-lookup"><span data-stu-id="237d5-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="237d5-224">Porque no hay una vista móvil (*AllSpeakers.Mobile.cshtml*), ver los altavoces de hello predeterminado (*AllSpeakers.cshtml*) se representa mediante la vista de diseño de móviles hello ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="237d5-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="237d5-225">Tal y como se muestra a continuación, el título de hello **MVC5 aplicación (móvil)** se define en  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="237d5-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="237d5-226">Global puede deshabilitar una vista de (no son móviles) predeterminado de representación dentro de un diseño móvil estableciendo `RequireConsistentDisplayMode` a `true` en hello *vistas\\\_ViewStart.cshtml* archivo, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="237d5-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="237d5-227">Cuando `RequireConsistentDisplayMode` se establece demasiado`true`, diseño móviles hello (*\_Layout.Mobile.cshtml*) se utiliza únicamente para las vistas móviles (es decir, cuando es el archivo de vista de formulario de hello  ***ViewName** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="237d5-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="237d5-228">Es recomendable tooset `RequireConsistentDisplayMode` demasiado`true` si su diseño móvil no funciona bien con las vistas no son móviles.</span><span class="sxs-lookup"><span data-stu-id="237d5-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="237d5-229">Hello captura de pantalla siguiente muestra cómo Hola *altavoces* la página presenta cuando `RequireConsistentDisplayMode` se establece demasiado`true` (sin cadena de hello "(móvil)" en la navegación de la barra en la parte superior de Hola Hola).</span><span class="sxs-lookup"><span data-stu-id="237d5-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="237d5-230">Puede deshabilitar el modo de presentación coherente en una vista específica estableciendo `RequireConsistentDisplayMode` demasiado`false` en archivo de vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="237d5-231">El siguiente marcado en hello *vistas\\inicio\\AllSpeakers.cshtml* archivo establece `RequireConsistentDisplayMode` demasiado`false`:</span><span class="sxs-lookup"><span data-stu-id="237d5-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="237d5-232">En esta sección que hemos visto cómo toocreate móviles diseños, vistas y cómo toocreate diseños y las vistas para dispositivos específicos como Hola iPhone.</span><span class="sxs-lookup"><span data-stu-id="237d5-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="237d5-233">Sin embargo, Hola principal ventaja del marco de trabajo de Bootstrap CSS hello es el diseño dinámico, lo que significa que una sola hoja de estilos puede aplicarse a través de escritorio y teléfono, tableta exploradores toocreate una apariencia coherente.</span><span class="sxs-lookup"><span data-stu-id="237d5-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="237d5-234">En la sección siguiente Hola verá cómo tooleverage arrancar toocreate preparadas para dispositivos móviles vistas.</span><span class="sxs-lookup"><span data-stu-id="237d5-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="237d5-235"><a name="bkmk_Improvespeakerslist"></a>Mejorar Hola altavoces lista</span><span class="sxs-lookup"><span data-stu-id="237d5-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="237d5-236">Como ha visto, Hola *altavoces* vista es legible, pero Hola vínculos son pequeños y son difíciles de tootap en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="237d5-237">En esta sección, hará hello *AllSpeakers* preparadas para dispositivos móviles, la vista que muestra vínculos grandes y fácil de tap y contiene un tooquickly del cuadro de búsqueda encontró altavoces.</span><span class="sxs-lookup"><span data-stu-id="237d5-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="237d5-238">Puede usar hello Bootstrap [grupo de la lista vinculada] [ linked list group] estilos para mejorar hello *altavoces* vista.</span><span class="sxs-lookup"><span data-stu-id="237d5-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="237d5-239">En *vistas\\inicio\\AllSpeakers.cshtml*, reemplace el contenido de hello del archivo de Razor Hola con código de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="237d5-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="237d5-240">Hola `class="list-group"` atributo Hola `<div>` etiqueta aplica el estilo de lista de arranque, hello y `class="input-group-item"` vínculo de tooeach de estilo de elementos de lista de arranque aplica el atributo.</span><span class="sxs-lookup"><span data-stu-id="237d5-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="237d5-241">Actualice el explorador móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="237d5-242">Hola actualiza vista es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="237d5-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="237d5-243">Hola Bootstrap [grupo de la lista vinculada] [ linked list group] estilo hace Hola un cuadro completo para cada vínculo interactivo, que es una experiencia de usuario mucho mejor.</span><span class="sxs-lookup"><span data-stu-id="237d5-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="237d5-244">Cambiar la vista de escritorio toothe y observe la apariencia y funcionamiento coherente Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="237d5-245">Aunque se mejoró la vista de explorador móvil hello, es difícil la navegación lista larga de Hola de altavoces.</span><span class="sxs-lookup"><span data-stu-id="237d5-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="237d5-246">Bootstrap no proporciona una funcionalidad de filtro de búsqueda de forma predeterminada, pero puede agregarla con unas pocas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="237d5-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="237d5-247">En primer lugar se agregará una vista de toohello del cuadro de búsqueda, a continuación, enlazar con el código de JavaScript para la función de filtro de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="237d5-248">En *vistas\\inicio\\AllSpeakers.cshtml*, agregue un \<formulario\> etiqueta justo después de hello \<h2\> etiqueta, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="237d5-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="237d5-249">Tenga en cuenta que hello `<form>` y `<input>` etiquetas ambos tienen Hola arranque estilos aplicados toothem.</span><span class="sxs-lookup"><span data-stu-id="237d5-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="237d5-250">Hola `<span>` elemento agrega un arranque [glyphicon] [ glyphicon] toothe cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="237d5-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="237d5-251">Hola *Scripts* carpeta, agregue un archivo JavaScript denominado *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="237d5-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="237d5-252">Abra el archivo hello y pegue Hola siguiente código en él:</span><span class="sxs-lookup"><span data-stu-id="237d5-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="237d5-253">También necesita tooinclude filter.js en sus agrupaciones registradas.</span><span class="sxs-lookup"><span data-stu-id="237d5-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="237d5-254">Abra *aplicación\_iniciar\\BundleConfig.cs* y cambiar paquetes primera Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="237d5-255">Cambiar la primera `bundles.Add` instrucción (para hello **jquery** agrupación) tooinclude *Scripts\\filter.js*, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="237d5-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="237d5-256">Hola **jquery** agrupación ya se representa de forma predeterminada de hello  *\_diseño* vista.</span><span class="sxs-lookup"><span data-stu-id="237d5-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="237d5-257">Más adelante, puede utilizar Hola JavaScript mismo código tooapply las vistas de lista de tooother de funcionalidad de filtro.</span><span class="sxs-lookup"><span data-stu-id="237d5-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="237d5-258">Actualice el explorador móvil hello y vaya toohello *AllSpeakers* vista.</span><span class="sxs-lookup"><span data-stu-id="237d5-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="237d5-259">En el cuadro de búsqueda, escriba "sc".</span><span class="sxs-lookup"><span data-stu-id="237d5-259">In the search box, type "sc".</span></span> <span data-ttu-id="237d5-260">Ahora se debe filtrar lista de altavoces Hola según la cadena de búsqueda de tooyour.</span><span class="sxs-lookup"><span data-stu-id="237d5-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="237d5-261"><a name="bkmk_improvetags"></a>Mejorar Hola lista etiquetas</span><span class="sxs-lookup"><span data-stu-id="237d5-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="237d5-262">Al igual que hello *altavoces* ver, hello *etiquetas* vista es legible, pero los vínculos de hello son pequeño y difícil de tootap en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="237d5-263">Puede corregir hello *etiquetas* vista Hola igual manera de corregir hello *altavoces* ver, si utiliza los cambios de código de hello descritos anteriormente, pero con la siguiente hello `Html.ActionLink` sintaxis de método en  *Vistas\\inicio\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="237d5-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="237d5-264">Hola actualiza Explorador de escritorio aparece como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="237d5-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="237d5-265">Y Hola actualiza explorador móvil aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="237d5-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="237d5-266">Si observa ese formato de la lista original de hello sigue estando allí en Hola explorador móvil y se pregunte qué aplicación de estilos de arranque "nice" de tooyour problema, se trata de un artefacto de las anterior acción toocreate móviles vistas específicas.</span><span class="sxs-lookup"><span data-stu-id="237d5-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="237d5-267">Sin embargo, ahora que utilizas Hola Bootstrap CSS framework toocreate un diseño web con capacidad de respuesta, avanzar y quitar estas vistas específicas de mobile y vistas de diseño específicos de mobile Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="237d5-268">Una vez que lo ha hecho, explorador móvil actualizado de hello mostrará un estilo de arranque de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="237d5-269"><a name="bkmk_improvedates"></a>Mejorar Hola lista de fechas</span><span class="sxs-lookup"><span data-stu-id="237d5-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="237d5-270">Puede mejorar hello *fechas* ver como mejorado hello *altavoces* y *etiquetas* vistas si usas Hola cambios en el código se describe anteriormente, pero con hello después `Html.ActionLink` sintaxis de método en *vistas\\inicio\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="237d5-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="237d5-271">Obtendrá una vista de explorador móvil actualizada con el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="237d5-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="237d5-272">Puede mejorar aún más hello *fechas* vista de organizar los valores de fecha y hora de Hola por fecha.</span><span class="sxs-lookup"><span data-stu-id="237d5-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="237d5-273">Esto puede hacerse con hello Bootstrap [paneles] [ panels] aplicación de estilos.</span><span class="sxs-lookup"><span data-stu-id="237d5-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="237d5-274">Reemplazar contenido Hola de hello *vistas\\inicio\\AllDates.cshtml* archivo con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="237d5-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="237d5-275">Este código crea otro `<div class="panel panel-primary">` etiqueta para cada fecha en la lista de Hola y Hola usa distinto [grupo de la lista vinculada] [ linked list group] para los respectivos vincula como antes.</span><span class="sxs-lookup"><span data-stu-id="237d5-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="237d5-276">Este es el explorador móvil Hola aspecto cuando se ejecuta este código:</span><span class="sxs-lookup"><span data-stu-id="237d5-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="237d5-277">Explorador de escritorio toohello de conmutador.</span><span class="sxs-lookup"><span data-stu-id="237d5-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="237d5-278">De nuevo, tenga en cuenta Hola apariencia coherente.</span><span class="sxs-lookup"><span data-stu-id="237d5-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="237d5-279"><a name="bkmk_improvesessionstable"></a>Mejorar hello SessionsTable vista</span><span class="sxs-lookup"><span data-stu-id="237d5-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="237d5-280">En esta sección, hará hello *SessionsTable* ver más preparado para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="237d5-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="237d5-281">Este cambio es más amplias cambios anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="237d5-282">En el explorador móvil de hello, puntee en hello **etiqueta** , a continuación, escriba `asp` en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="237d5-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="237d5-283">Pulse hello **ASP.NET** vínculo.</span><span class="sxs-lookup"><span data-stu-id="237d5-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="237d5-284">Como puede ver, mostrar hello se formatea como una tabla, que está diseñado actualmente toobe ver en el Explorador de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="237d5-285">Sin embargo, es un poco difícil tooread en un explorador móvil.</span><span class="sxs-lookup"><span data-stu-id="237d5-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="237d5-286">toofix, abra *vistas\\inicio\\SessionsTable.cshtml* y, a continuación, reemplace el contenido de hello del archivo con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="237d5-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="237d5-287">código de Hello hace 3 cosas:</span><span class="sxs-lookup"><span data-stu-id="237d5-287">hello code does 3 things:</span></span>

* <span data-ttu-id="237d5-288">usa Hola Bootstrap [grupo personalizado de lista vinculada] [ custom linked list group] tooformat Hola verticalmente, información de la sesión para que toda esta información es legible en un explorador móvil (mediante clases como lista grupo-elemento de texto)</span><span class="sxs-lookup"><span data-stu-id="237d5-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="237d5-289">se aplica hello [sistema cuadrícula] [ grid system] toothe diseño, por lo que esa sesión Hola elementos de flujo horizontal en el Explorador de escritorio de Hola y verticalmente en explorador móvil hello (mediante la clase de hello col-md-4)</span><span class="sxs-lookup"><span data-stu-id="237d5-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="237d5-290">hello usa [utilidades respondiendo] [ responsive utilities] para ocultar las etiquetas de sesión de hello cuando se ve en el explorador móvil hello (mediante la clase de hello extra oculto)</span><span class="sxs-lookup"><span data-stu-id="237d5-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="237d5-291">También puede puntear en una sesión título vínculo toogo toohello respectivos.</span><span class="sxs-lookup"><span data-stu-id="237d5-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="237d5-292">imagen de Hello siguiente refleja los cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="237d5-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="237d5-293">sistema de arranque cuadrícula Hola que aplican automáticamente Organiza las sesiones verticalmente en explorador móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="237d5-294">Además, tenga en cuenta que no se muestran las etiquetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="237d5-295">Explorador de escritorio toohello de conmutador.</span><span class="sxs-lookup"><span data-stu-id="237d5-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="237d5-296">En el Explorador de escritorio de hello, tenga en cuenta que ahora se muestran las etiquetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="237d5-297">Además, puede ver que sistema de arranque cuadrícula Hola aplicados organiza los elementos de la sesión de hello en dos columnas.</span><span class="sxs-lookup"><span data-stu-id="237d5-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="237d5-298">Si amplía el explorador, verá que los cambios de organización de hello toothree columnas.</span><span class="sxs-lookup"><span data-stu-id="237d5-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="237d5-299"><a name="bkmk_improvesessionbycode"></a>Mejorar hello SessionByCode vista</span><span class="sxs-lookup"><span data-stu-id="237d5-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="237d5-300">Por último, va a corregir hello *SessionByCode* ver toomake, preparadas para dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="237d5-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="237d5-301">En el explorador móvil de hello, puntee en hello **etiqueta** , a continuación, escriba `asp` en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="237d5-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="237d5-302">Pulse hello **ASP.NET** vínculo.</span><span class="sxs-lookup"><span data-stu-id="237d5-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="237d5-303">Se mostrarán las sesiones de etiqueta ASP.NET de Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="237d5-304">Elija hello **crear una aplicación de página única con ASP.NET y AngularJS** vínculo.</span><span class="sxs-lookup"><span data-stu-id="237d5-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="237d5-305">vista de escritorio de Hello predeterminada es correcto, pero puede mejorar el aspecto de hello fácilmente mediante el uso de algunos componentes de GUI de arranque.</span><span class="sxs-lookup"><span data-stu-id="237d5-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="237d5-306">Abra *vistas\\inicio\\SessionByCode.cshtml* y reemplace el contenido de hello con hello sigue marcado:</span><span class="sxs-lookup"><span data-stu-id="237d5-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="237d5-307">nueva marca de Hello usa arranque paneles vista móvil de tooimprove Hola de aplicación de estilos.</span><span class="sxs-lookup"><span data-stu-id="237d5-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="237d5-308">Actualice el explorador móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="237d5-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="237d5-309">Hello imagen siguiente refleja los cambios de código de hello que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="237d5-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="237d5-310">Resumen y revisión</span><span class="sxs-lookup"><span data-stu-id="237d5-310">Wrap Up and Review</span></span>
<span data-ttu-id="237d5-311">Este tutorial le ha mostrado cómo las aplicaciones Web de ASP.NET MVC 5 toodevelop preparadas para dispositivos móviles toouse.</span><span class="sxs-lookup"><span data-stu-id="237d5-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="237d5-312">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="237d5-312">These include:</span></span>

* <span data-ttu-id="237d5-313">Implementar un tooan de aplicación de ASP.NET MVC 5 aplicación de servicio de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="237d5-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="237d5-314">Usar el diseño de capacidad de respuesta web de arranque toocreate en la aplicación de MVC 5</span><span class="sxs-lookup"><span data-stu-id="237d5-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="237d5-315">Invalidación del diseño, las vistas y las vistas parciales, tanto de manera global como para una vista individual</span><span class="sxs-lookup"><span data-stu-id="237d5-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="237d5-316">Control del diseño y aplicación de la invalidación parcial mediante la propiedad `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="237d5-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="237d5-317">Crear vistas que tienen como destino exploradores específicos, como el Explorador de iPhone Hola</span><span class="sxs-lookup"><span data-stu-id="237d5-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="237d5-318">Aplicación del estilo de Bootstrap en el código de Razor</span><span class="sxs-lookup"><span data-stu-id="237d5-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="237d5-319">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="237d5-319">See Also</span></span>
* [<span data-ttu-id="237d5-320">Nueve principios básicos del diseño web con respuesta</span><span class="sxs-lookup"><span data-stu-id="237d5-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="237d5-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="237d5-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="237d5-322">[Blog oficial de Bootstrap][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="237d5-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="237d5-323">[Tutorial de Twitter Bootstrap de Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="237d5-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="237d5-324">[Hola Bootstrap Playground][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="237d5-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="237d5-325">[Prácticas recomendadas y recomendaciones de W3C para aplicaciones web móviles][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="237d5-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="237d5-326">[Recomendación de candidatos de W3C para consultas multimedia][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="237d5-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="237d5-327">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="237d5-327">What's changed</span></span>
* <span data-ttu-id="237d5-328">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="237d5-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

