---
title: "aaaHow toowork con el servidor back-end de .NET Hola SDK para aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toowork con Hola servidor back-end de .NET SDK para aplicaciones de Mobile de servicio de aplicación de Azure."
keywords: "servicio de aplicaciones, servicio de aplicaciones de azure, aplicación móvil, servicio móvil, escala, escalable, implementación de aplicaciones, implementación de aplicaciones de azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="eb396-104">Trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="eb396-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="eb396-105">Este tema muestra cómo toouse Hola servidor de back-end de .NET SDK en escenarios de aplicaciones móviles de Azure aplicación servicio clave.</span><span class="sxs-lookup"><span data-stu-id="eb396-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="eb396-106">Hola SDK de aplicaciones móviles de Azure le ayuda a trabajar con clientes móviles desde la aplicación de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="eb396-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="eb396-107">Hola [servidor .NET SDK para aplicaciones móviles de Azure] [ 2] es código abierto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="eb396-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="eb396-108">repositorio de Hello contiene todo el código fuente como conjunto de pruebas de unidad SDK de todo el servidor de Hola y algunos proyectos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="eb396-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="eb396-109">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="eb396-109">Reference documentation</span></span>
<span data-ttu-id="eb396-110">documentación de referencia de Hello para el servidor de hello SDK se encuentra aquí: [referencia de .NET de aplicaciones de Azure Mobile][1].</span><span class="sxs-lookup"><span data-stu-id="eb396-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="eb396-111"><a name="create-app"></a>Creación de un back-end de aplicación móvil .NET</span><span class="sxs-lookup"><span data-stu-id="eb396-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="eb396-112">Si está iniciando un nuevo proyecto, puede crear una aplicación de servicio de aplicaciones con cualquier hello [portal de Azure] o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb396-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="eb396-113">Puede ejecutar localmente Hola aplicación de servicio de aplicaciones o publicar el proyecto tooyour en la nube servicio de aplicaciones móvil aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eb396-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="eb396-114">Si va a Agregar proyecto existente de capacidades móviles tooan, vea hello [descargar e inicializar Hola SDK](#install-sdk) sección.</span><span class="sxs-lookup"><span data-stu-id="eb396-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="eb396-115">Crear un back-end de .NET mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="eb396-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="eb396-116">toocreate un back-end de servicio de aplicaciones móvil, ya sea siga hello [tutorial rápido] [ 3] o siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="eb396-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="eb396-117">En hello *Introducción* hoja, en **crear una tabla API**, elija **C#** como su **idioma de back-end**.</span><span class="sxs-lookup"><span data-stu-id="eb396-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="eb396-118">Haga clic en **descargar**, extraer el equipo de proyecto comprimido archivos tooyour local y abra la solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb396-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="eb396-119">Creación de un back-end .NET con Visual Studio 2013 y Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="eb396-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="eb396-120">Instalar hello [Azure SDK para .NET] [ 4] (versión 2.9.0 o posterior) toocreate un proyecto de aplicaciones móviles de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb396-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="eb396-121">Una vez haya instalado el SDK de hello, crear una aplicación de ASP.NET con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="eb396-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="eb396-122">Abra hello **nuevo proyecto** diálogo (desde *archivo* > **New** > **proyecto...** ).</span><span class="sxs-lookup"><span data-stu-id="eb396-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="eb396-123">Expanda **Plantillas** > **Visual C#** y seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="eb396-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="eb396-124">Seleccione **Aplicación web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="eb396-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="eb396-125">Rellene el nombre del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-125">Fill in hello project name.</span></span> <span data-ttu-id="eb396-126">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-126">Then click **OK**.</span></span>
5. <span data-ttu-id="eb396-127">En *Plantillas de ASP.NET 4.5.2*, seleccione **Aplicación móvil de Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb396-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="eb396-128">Comprobar **Host en la nube de hello** toocreate un back-end móvil Hola toowhich puede publicar este proyecto en la nube.</span><span class="sxs-lookup"><span data-stu-id="eb396-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="eb396-129">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-129">Click **OK**.</span></span>

## <span data-ttu-id="eb396-130"><a name="install-sdk"></a>Cómo: descargar e inicializar Hola SDK</span><span class="sxs-lookup"><span data-stu-id="eb396-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="eb396-131">Hello SDK está disponible en [NuGet.org]. Este paquete incluye Hola funcionalidad base necesaria tooget iniciado mediante Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="eb396-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="eb396-132">tooinitialize Hola SDK, deberá tooperform acciones en hello **HttpConfiguration** objeto.</span><span class="sxs-lookup"><span data-stu-id="eb396-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="eb396-133">Instalar SDK de Hola</span><span class="sxs-lookup"><span data-stu-id="eb396-133">Install hello SDK</span></span>
<span data-ttu-id="eb396-134">Hola tooinstall SDK, el botón secundario en el proyecto de servidor de hello en Visual Studio, seleccione **administrar paquetes de NuGet**, busque hello [Microsoft.Azure.Mobile.Server] del paquete, a continuación, haga clic en  **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="eb396-135"><a name="server-project-setup"></a>Inicializar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="eb396-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="eb396-136">Un proyecto de servidor de back-end de .NET es inicializado similar tooother los proyectos ASP.NET, mediante la inclusión de una clase de inicio OWIN.</span><span class="sxs-lookup"><span data-stu-id="eb396-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="eb396-137">Asegúrese de que se ha hecho referencia paquete de NuGet hello `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="eb396-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="eb396-138">tooadd esta clase en Visual Studio, haga clic en el proyecto de servidor y seleccione **agregar** >
**nuevo elemento**, a continuación, **Web**  >  ** General** > **clase de inicio de OWIN**.</span><span class="sxs-lookup"><span data-stu-id="eb396-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="eb396-139">Se genera una clase con hello siguiente atributo:</span><span class="sxs-lookup"><span data-stu-id="eb396-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="eb396-140">Hola `Configuration()` método de la clase de inicio OWIN, use un **HttpConfiguration** entorno de aplicaciones móviles de Azure de objetos tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="eb396-141">Hola siguiente ejemplo inicializa el proyecto de servidor de hello con ninguna característica agregada:</span><span class="sxs-lookup"><span data-stu-id="eb396-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="eb396-142">tooenable características individuales, deben llamar a métodos de extensión en hello **MobileAppConfiguration** objeto antes de llamar a **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="eb396-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="eb396-143">Por ejemplo, hello siguiente código agrega predeterminado Hola enruta controladores tooall API que tienen el atributo de hello `[MobileAppController]` durante la inicialización:</span><span class="sxs-lookup"><span data-stu-id="eb396-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="eb396-144">Inicio rápido de servidor Hello de Hola llamadas portales Azure **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="eb396-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="eb396-145">Este toohello equivalente después de la instalación:</span><span class="sxs-lookup"><span data-stu-id="eb396-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="eb396-146">métodos de extensión de Hello usados son:</span><span class="sxs-lookup"><span data-stu-id="eb396-146">hello extension methods used are:</span></span>

* <span data-ttu-id="eb396-147">`AddMobileAppHomeController()`proporciona la página de inicio de aplicaciones móviles de Azure de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="eb396-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="eb396-148">`MapApiControllers()`proporciona capacidades de API personalizadas para los controladores de WebAPI decorados con hello `[MobileAppController]` atributo.</span><span class="sxs-lookup"><span data-stu-id="eb396-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="eb396-149">`AddTables()`Proporciona una asignación de hello `/tables` controladores tootable de puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="eb396-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="eb396-150">`AddTablesWithEntityFramework()`es un abreviada para hello asignación `/tables` controladores basados en los extremos que usan Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="eb396-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="eb396-151">`AddPushNotifications()` proporciona un método sencillo de registrar los dispositivos para Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="eb396-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="eb396-152">`MapLegacyCrossDomainController()` proporciona los encabezados de CORS estándar para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="eb396-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="eb396-153">Extensiones de SDK</span><span class="sxs-lookup"><span data-stu-id="eb396-153">SDK extensions</span></span>
<span data-ttu-id="eb396-154">Hola siguientes paquetes de NuGet-based extensión proporciona diversas características de dispositivos móviles que se pueden usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb396-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="eb396-155">Habilitar extensiones durante la inicialización mediante hello **MobileAppConfiguration** objeto.</span><span class="sxs-lookup"><span data-stu-id="eb396-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="eb396-156">[Microsoft.Azure.Mobile.Server.Quickstart] admite Hola configuración básica de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="eb396-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="eb396-157">La configuración agregada toohello Hola que realiza la llamada **UseDefaultConfiguration** método de extensión durante la inicialización.</span><span class="sxs-lookup"><span data-stu-id="eb396-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="eb396-158">Esta extensión incluye las siguientes extensiones: paquetes de notificaciones, autenticación, entidad, tablas, entre dominios y principal.</span><span class="sxs-lookup"><span data-stu-id="eb396-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="eb396-159">Inicio rápido de aplicaciones móviles disponibles en el portal de Azure Hola Hola utiliza este paquete.</span><span class="sxs-lookup"><span data-stu-id="eb396-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="eb396-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa de forma predeterminada hello *esta aplicación móvil esté en funcionamiento página* para la raíz del sitio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="eb396-161">Agregar configuración toohello mediante una llamada a la **AddMobileAppHomeController** método de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="eb396-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) incluye clases para trabajar con conjuntos de datos y de canalización de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="eb396-163">Agregar configuración toohello Hola llamada **AddTables** método de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="eb396-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permite que los datos de tooaccess de Entity Framework Hola Hola base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="eb396-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="eb396-165">Agregar configuración toohello Hola llamada **AddTablesWithEntityFramework** método de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="eb396-166">[Microsoft.Azure.Mobile.Server.Authentication] middleware de OWIN de Hola de autenticación y conjuntos de seguridad permite usa toovalidate símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="eb396-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="eb396-167">Agregar configuración toohello Hola llamada **AddAppServiceAuthentication** y **IAppBuilder**. **UseAppServiceAuthentication** métodos de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="eb396-168">[Microsoft.Azure.Mobile.Server.Notifications] habilita las notificaciones push y define un punto de conexión de registro de inserción.</span><span class="sxs-lookup"><span data-stu-id="eb396-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="eb396-169">Agregar configuración toohello Hola llamada **AddPushNotifications** método de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="eb396-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) crea un controlador que sirve datos toolegacy exploradores web desde su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="eb396-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="eb396-171">Agregar configuración toohello mediante una llamada a la **MapLegacyCrossDomainController** método de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="eb396-172">[Microsoft.Azure.Mobile.Server.Login] proporciona hello AppServiceLoginHandler.CreateToken() método, que es un método estático que se usa en escenarios de autenticación personalizado de.</span><span class="sxs-lookup"><span data-stu-id="eb396-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="eb396-173"><a name="publish-server-project"></a>Cómo: Publicar proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="eb396-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="eb396-174">Esta sección muestra cómo toopublish el back-end de .NET proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb396-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="eb396-175">También puede implementar el proyecto de back-end con Git o cualquiera de Hola otros métodos que se tratan en hello [documentación de implementación de servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="eb396-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="eb396-176">En Visual Studio, vuelva a generar paquetes de NuGet de hello proyecto toorestore.</span><span class="sxs-lookup"><span data-stu-id="eb396-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="eb396-177">En el Explorador de soluciones, proyectos de Hola de menú contextual, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="eb396-178">Hello primera vez que publique, deberá toodefine un perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="eb396-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="eb396-179">Si ya tiene un perfil definido, puede seleccionarlo y hacer clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="eb396-180">Si se le solicita tooselect un destino de publicación, haga clic en **servicio de aplicaciones de Microsoft Azure** > **siguiente**, a continuación, (si es necesario) iniciar sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb396-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="eb396-181">Visual Studio descarga y almacena la configuración de publicación directamente desde Azure.</span><span class="sxs-lookup"><span data-stu-id="eb396-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="eb396-182">Elija su suscripción en **Suscripción**, seleccione **Tipo de recurso** en **Vista**, expanda **Aplicación móvil** y haga clic en el back-end de aplicación móvil y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="eb396-183">Comprobar Hola publicar información del perfil y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="eb396-184">Cuando el back-end de la aplicación móvil se haya publicado correctamente, verá una página de aterrizaje que indica el éxito.</span><span class="sxs-lookup"><span data-stu-id="eb396-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="eb396-185"><a name="define-table-controller"></a> Definición de un controlador de tabla</span><span class="sxs-lookup"><span data-stu-id="eb396-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="eb396-186">Definir un controlador de tabla tooexpose los clientes un toomobile de tabla SQL.</span><span class="sxs-lookup"><span data-stu-id="eb396-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="eb396-187">La configuración de un controlador de tabla requiere tres pasos:</span><span class="sxs-lookup"><span data-stu-id="eb396-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="eb396-188">Creación de una clase Data Transfer Object (DTO).</span><span class="sxs-lookup"><span data-stu-id="eb396-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="eb396-189">Configurar una referencia de tabla en hello clase DbContext Mobile.</span><span class="sxs-lookup"><span data-stu-id="eb396-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="eb396-190">Creación de un controlador de tabla.</span><span class="sxs-lookup"><span data-stu-id="eb396-190">Create a table controller.</span></span>

<span data-ttu-id="eb396-191">Un objeto de transferencia de datos (DTO) es un objeto de C# simple heredado de `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="eb396-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="eb396-192">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eb396-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="eb396-193">Hola DTO es tabla de hello toodefine utilizados dentro de la base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="eb396-194">Hola toocreate entrada de la base de datos, agregue un `DbSet<>` propiedad a saludos DbContext utilizas.</span><span class="sxs-lookup"><span data-stu-id="eb396-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="eb396-195">En la plantilla de proyecto de hello predeterminada para las aplicaciones móviles de Azure, hello DbContext se denomina `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="eb396-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="eb396-196">Si tiene instalado el SDK de Azure de Hola, ahora puede crear un controlador de tabla de plantilla como sigue:</span><span class="sxs-lookup"><span data-stu-id="eb396-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="eb396-197">Haga doble clic en la carpeta de controladores de Hola y seleccione **agregar** > **controlador...** .</span><span class="sxs-lookup"><span data-stu-id="eb396-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="eb396-198">Seleccione hello **controlador de tabla de aplicaciones de Azure Mobile** opción, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="eb396-199">Hola **Agregar controlador** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="eb396-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="eb396-200">Hola **clase modelo** de lista desplegable, seleccione el nuevo DTO.</span><span class="sxs-lookup"><span data-stu-id="eb396-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="eb396-201">Hola **DbContext** lista desplegable, clase de DbContext del servicio móvil de hello select.</span><span class="sxs-lookup"><span data-stu-id="eb396-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="eb396-202">nombre del controlador de Hola se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="eb396-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="eb396-203">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-203">Click **Add**.</span></span>

<span data-ttu-id="eb396-204">proyecto de servidor de inicio rápido de Hello contiene un ejemplo de un sencillo **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="eb396-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="eb396-205"><a name="adjust-pagesize"></a>Cómo: ajustar el tamaño de paginación de tabla Hola</span><span class="sxs-lookup"><span data-stu-id="eb396-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="eb396-206">De forma predeterminada, Aplicaciones móviles de Azure devuelve 50 registros por solicitud.</span><span class="sxs-lookup"><span data-stu-id="eb396-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="eb396-207">Paginación se asegura de que el cliente hello no atar su servidor de hello ni de subproceso de interfaz de usuario durante demasiado tiempo, garantizar una buena experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="eb396-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="eb396-208">tamaño de paginación de la tabla de hello toochange, lado del servidor aumento Hola "tamaño de consulta permitido" y hello página del lado cliente tamaño Hola servidor "tamaño de consulta permitido" se ajusta con hello `EnableQuery` atributo:</span><span class="sxs-lookup"><span data-stu-id="eb396-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="eb396-209">Asegúrese de hello PageSize es hello mismo o mayor que el tamaño de hello solicitada por el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="eb396-210">Consulte la documentación de cómo de cliente específico de toohello para obtener más información acerca de cómo cambiar el tamaño de página de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="eb396-211">Cómo definir un controlador de API personalizada</span><span class="sxs-lookup"><span data-stu-id="eb396-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="eb396-212">controlador de API personalizada Hello proporciona hello más básico funcionalidad tooyour aplicación móvil back-end mediante la exposición de un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="eb396-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="eb396-213">Puede registrar un controlador de API de mobile específica mediante el atributo Hola [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="eb396-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="eb396-214">Hola `MobileAppController` atributo registra ruta hello, configura el serializador de JSON de aplicaciones móviles de Hola y activará [comprobación de la versión de cliente](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="eb396-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="eb396-215">En Visual Studio, la carpeta de controladores de menú contextual hello, a continuación, haga clic en **agregar** > **controlador**, seleccione **controlador de Web API 2&mdash;vacía** y Haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="eb396-216">Proporcione un valor de **Nombre de controlador**, como `CustomController`, y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="eb396-217">En el archivo de clase de controlador nuevo hello, agregue el siguiente de hello instrucción using:</span><span class="sxs-lookup"><span data-stu-id="eb396-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="eb396-218">Aplicar hello **[MobileAppController]** definición de clase de controlador toohello API, como en el siguiente ejemplo de Hola de atributo:</span><span class="sxs-lookup"><span data-stu-id="eb396-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="eb396-219">En el archivo de App_Start/Startup.MobileApp.cs, agregue una llamada toohello **MapApiControllers** método de extensión, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="eb396-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="eb396-220">También puede usar hello `UseDefaultConfiguration()` en lugar del método de extensión `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="eb396-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="eb396-221">Los clientes pueden tener acceso a un controlador aunque este no tenga un elemento **MobileAppControllerAttribute** aplicado, pero puede que no lo consuman correctamente si usan un SDK de cliente de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="eb396-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="eb396-222">Procedimiento: Autenticación</span><span class="sxs-lookup"><span data-stu-id="eb396-222">How to: Work with authentication</span></span>
<span data-ttu-id="eb396-223">Aplicaciones móviles de Azure usa la aplicación de servicio de autenticación / autorización toosecure el back-end de dispositivos móvil.</span><span class="sxs-lookup"><span data-stu-id="eb396-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="eb396-224">Esta sección muestra cómo hello tooperform siguientes tareas relacionadas con la autenticación en el proyecto de servidor de back-end. NET:</span><span class="sxs-lookup"><span data-stu-id="eb396-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="eb396-225">Cómo: Agregar proyecto de servidor de autenticación tooa</span><span class="sxs-lookup"><span data-stu-id="eb396-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="eb396-226">Procedimiento: Uso de autenticación personalizada en la aplicación</span><span class="sxs-lookup"><span data-stu-id="eb396-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="eb396-227">Procedimiento: Recuperación de la información de usuario de autenticado</span><span class="sxs-lookup"><span data-stu-id="eb396-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="eb396-228">Cómo restringir el acceso a datos para los usuarios autorizados</span><span class="sxs-lookup"><span data-stu-id="eb396-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="eb396-229"><a name="add-auth"></a>Cómo: Agregar proyecto de servidor de autenticación tooa</span><span class="sxs-lookup"><span data-stu-id="eb396-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="eb396-230">Puede agregar el proyecto de servidor de autenticación tooyour extendiendo hello **MobileAppConfiguration** objeto y la configuración de middleware de OWIN.</span><span class="sxs-lookup"><span data-stu-id="eb396-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="eb396-231">Cuando instala hello [Microsoft.Azure.Mobile.Server.Quickstart] Hola de paquete y llame al método **UseDefaultConfiguration** método de extensión, puede omitir toostep 3.</span><span class="sxs-lookup"><span data-stu-id="eb396-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="eb396-232">En Visual Studio, instale hello [Microsoft.Azure.Mobile.Server.Authentication] paquete.</span><span class="sxs-lookup"><span data-stu-id="eb396-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="eb396-233">En el archivo de proyecto de hello Startup.cs, agregar Hola después de la línea de código al principio de Hola de hello **configuración** método:</span><span class="sxs-lookup"><span data-stu-id="eb396-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="eb396-234">Este componente de middleware OWIN valida tokens emitidos por la puerta de enlace de servicio de aplicaciones de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="eb396-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="eb396-235">Agregar hello `[Authorize]` controlador tooany de atributo o un método que requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="eb396-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="eb396-236">toolearn acerca de cómo los clientes de tooauthenticate tooyour back-end de aplicaciones móviles, consulte [agregar autenticación tooyour aplicación](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="eb396-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="eb396-237"><a name="custom-auth"></a>Procedimiento: Uso de autenticación personalizada en la aplicación</span><span class="sxs-lookup"><span data-stu-id="eb396-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="eb396-238">Si no desea toouse uno de los proveedores de autenticación/autorización del servicio de aplicación Hola, puede implementar su propio sistema de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="eb396-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="eb396-239">Instalar hello [Microsoft.Azure.Mobile.Server.Login] tooassist con generación de tokens de autenticación del paquete.</span><span class="sxs-lookup"><span data-stu-id="eb396-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="eb396-240">Proporcione su propio código para validar las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="eb396-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="eb396-241">Por ejemplo, podría comprobar las contraseñas con sal y hash de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="eb396-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="eb396-242">En el siguiente ejemplo de Hola, Hola `isValidAssertion()` método (definido en otro lugar) es responsable de estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="eb396-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="eb396-243">autenticación personalizada Hello se expone mediante la creación de un ApiController y exponer `register` y `login` acciones.</span><span class="sxs-lookup"><span data-stu-id="eb396-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="eb396-244">cliente de Hello debería utilizar una información de hello toocollect de interfaz de usuario personalizada de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="eb396-245">información de Hello es llamar a la API de toohello enviado con un estándar HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="eb396-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="eb396-246">Una vez que el servidor hello valida aserción hello, se emite un token con hello `AppServiceLoginHandler.CreateToken()` método.</span><span class="sxs-lookup"><span data-stu-id="eb396-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="eb396-247">Hola ApiController **no debería** usar hello `[MobileAppController]` atributo.</span><span class="sxs-lookup"><span data-stu-id="eb396-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="eb396-248">Ejemplo de la acción `login` :</span><span class="sxs-lookup"><span data-stu-id="eb396-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="eb396-249">En el anterior ejemplo de Hola, LoginResult y LoginResultUser son objetos serializables exponer propiedades necesarias.</span><span class="sxs-lookup"><span data-stu-id="eb396-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="eb396-250">cliente de Hello espera toobe de respuestas de inicio de sesión devuelven como objetos JSON del formulario de hello:</span><span class="sxs-lookup"><span data-stu-id="eb396-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="eb396-251">Hola `AppServiceLoginHandler.CreateToken()` método incluye un *audiencia* y *emisor* parámetro.</span><span class="sxs-lookup"><span data-stu-id="eb396-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="eb396-252">Ambos parámetros se establecen toohello URL de la raíz de la aplicación, con esquema HTTPS de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="eb396-253">Del mismo modo debe establecer *secretKey* toobe valor de saludo de la aplicación de la clave de firma.</span><span class="sxs-lookup"><span data-stu-id="eb396-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="eb396-254">No distribuya Hola firma clave en un cliente puede ser toomint usa claves y suplantar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="eb396-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="eb396-255">Puede obtener Hola firma clave mientras hospedada en el servicio de aplicaciones haciendo referencia a hello *sitio Web\_AUTH\_firma\_clave* variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="eb396-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="eb396-256">Si es necesario en un contexto de depuración local, siga las instrucciones de Hola Hola [depuración Local con autenticación](#local-debug) sección tooretrieve clave de Hola y almacenar como una configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb396-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="eb396-257">También puede incluir el token emitido de Hello el resto de reclamaciones y una fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="eb396-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="eb396-258">Como mínimo, símbolo (token) de hello emitido debe incluir un asunto (**sub**) de notificación.</span><span class="sxs-lookup"><span data-stu-id="eb396-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="eb396-259">Puede admitir cliente estándar hello `loginAsync()` método mediante la sobrecarga de la ruta de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="eb396-260">Si llama a cliente hello `client.loginAsync('custom');` toolog en, la ruta debe ser `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="eb396-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="eb396-261">Puede establecer la ruta de hello para el uso de controlador de autenticación personalizada hello `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="eb396-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="eb396-262">Con hello `loginAsync()` enfoque garantiza que se adjunta ese token de autenticación de hello tooevery llamada subsiguiente toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="eb396-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="eb396-263"><a name="user-info"></a>Procedimiento: Recuperación de la información de usuario de autenticado</span><span class="sxs-lookup"><span data-stu-id="eb396-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="eb396-264">Cuando un usuario se autentica por el servicio de aplicaciones, puede tener acceso a Hola asignado el Id. de usuario y otra información en el código de back-end. NET.</span><span class="sxs-lookup"><span data-stu-id="eb396-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="eb396-265">información de usuario de Hello puede usarse para tomar las decisiones de autorización Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="eb396-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="eb396-266">Hello código siguiente obtiene Hola Id. de usuario asociada a una solicitud:</span><span class="sxs-lookup"><span data-stu-id="eb396-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="eb396-267">Hola SID se deriva de Id. de usuario específica del proveedor de Hola y es estático para un usuario determinado y un proveedor de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="eb396-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="eb396-268">Hola SID es null para los tokens de autenticación no válida.</span><span class="sxs-lookup"><span data-stu-id="eb396-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="eb396-269">El Servicio de aplicaciones también le permite solicitar notificaciones específicas de su proveedor de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="eb396-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="eb396-270">Cada proveedor de identidades puede proporcionar más información mediante el SDK del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="eb396-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="eb396-271">Por ejemplo, puede usar hello Graph API de Facebook para obtener información de amigos.</span><span class="sxs-lookup"><span data-stu-id="eb396-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="eb396-272">Puede especificar demandas solicitadas en la hoja de proveedor de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb396-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="eb396-273">Algunas notificaciones requieren configuración adicional con el proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="eb396-274">Hola de llamadas de código siguiente Hello **GetAppServiceIdentityAsync** extensión método tooget Hola credenciales inicio de sesión, que incluyen las solicitudes de token toomake necesarios de hello acceso contra Hola Graph API de Facebook:</span><span class="sxs-lookup"><span data-stu-id="eb396-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="eb396-275">Agregue un mediante declaración para `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** método de extensión.</span><span class="sxs-lookup"><span data-stu-id="eb396-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="eb396-276"><a name="authorize"></a>Cómo restringir el acceso a datos para los usuarios autorizados</span><span class="sxs-lookup"><span data-stu-id="eb396-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="eb396-277">En la sección anterior de hello, mostramos cómo tooretrieve Hola Id. de usuario de un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="eb396-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="eb396-278">Puede restringir el acceso toodata y otros recursos en función de este valor.</span><span class="sxs-lookup"><span data-stu-id="eb396-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="eb396-279">Por ejemplo, agregar un tootables de la columna de identificador de usuario y filtrar resultados de la consulta de Hola por Id. de usuario de hello son un toolimit de manera sencilla devuelve solo los usuarios tooauthorized datos.</span><span class="sxs-lookup"><span data-stu-id="eb396-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="eb396-280">Hello código siguiente devuelve filas de datos solo cuando Hola SID coincide con el valor de columna de identificador de usuario de hello en la tabla TodoItem de hello:</span><span class="sxs-lookup"><span data-stu-id="eb396-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="eb396-281">Hola `Query()` método devuelve un `IQueryable` que se pueden manipular mediante el filtrado de toohandle LINQ.</span><span class="sxs-lookup"><span data-stu-id="eb396-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="eb396-282">Cómo: Agregar proyecto de servidor de tooa de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="eb396-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="eb396-283">Agregar proyecto de servidor de tooyour de notificaciones de inserción mediante la extensión de hello **MobileAppConfiguration** objeto y la creación de un cliente de los centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="eb396-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="eb396-284">En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**, busque `Microsoft.Azure.Mobile.Server.Notifications`, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="eb396-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="eb396-285">Repita este Hola de tooinstall paso `Microsoft.Azure.NotificationHubs` paquete, que incluye la biblioteca de cliente de hello centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="eb396-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="eb396-286">En App_Start/Startup.MobileApp.cs y agregue una llamada toohello **AddPushNotifications()** método de extensión durante la inicialización:</span><span class="sxs-lookup"><span data-stu-id="eb396-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="eb396-287">Agregue Hola después el código que crea a un cliente de los centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="eb396-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="eb396-288">Ahora puede usar Hola centros de notificaciones toosend inserción notificaciones tooregistered los dispositivos cliente.</span><span class="sxs-lookup"><span data-stu-id="eb396-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="eb396-289">Para obtener más información, consulte [aplicación de tooyour de notificaciones de inserción de agregar](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="eb396-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="eb396-290">toolearn más información acerca de los centros de notificaciones, consulte [información general de los centros de notificación](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eb396-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="eb396-291"><a name="tags"></a>Habilitación de la inserción de destino mediante etiquetas</span><span class="sxs-lookup"><span data-stu-id="eb396-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="eb396-292">Los centros de notificaciones le permite enviar notificaciones de destino toospecific registros mediante el uso de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="eb396-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="eb396-293">Se crean varias etiquetas automáticamente:</span><span class="sxs-lookup"><span data-stu-id="eb396-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="eb396-294">Hola identificador de instalación identifica un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="eb396-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="eb396-295">Hello Id. de usuario basado en hello autenticado SID identifica a un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="eb396-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="eb396-296">Hola instalación identificador puede tener acceso desde hello **installationId** propiedad hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="eb396-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="eb396-297">Hello en el ejemplo siguiente se muestra cómo utilizar un tooadd de Id. de instalación específicas de instalación de tooa etiqueta en los centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="eb396-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="eb396-298">Hola back-end omite las etiquetas proporcionadas por el cliente de Hola durante el registro de notificaciones de inserción cuando se crea la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="eb396-299">tooenable un tooadd cliente etiquetas toohello instalación, debe crear una API personalizada que agrega etiquetas mediante Hola anterior patrón.</span><span class="sxs-lookup"><span data-stu-id="eb396-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="eb396-300">Vea [etiquetas de notificación de inserción de cliente agregado] [ 5] en el ejemplo de tutorial rápido completada de aplicación del servicio de aplicaciones móviles de Hola para obtener un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="eb396-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="eb396-301"><a name="push-user"></a>Cómo: tooan de notificaciones de inserción de envío autentica el usuario</span><span class="sxs-lookup"><span data-stu-id="eb396-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="eb396-302">Cuando un usuario autenticado se registra para las notificaciones de inserción, una etiqueta de Id. de usuario se agrega automáticamente el registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="eb396-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="eb396-303">Mediante el uso de esta etiqueta, puede enviar inserción dispositivos de tooall notificaciones registrados por esa persona.</span><span class="sxs-lookup"><span data-stu-id="eb396-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="eb396-304">Hello código siguiente obtiene Hola SID del usuario que realiza la solicitud y envía un registro de dispositivos plantilla tooevery de notificación de inserción para esa persona:</span><span class="sxs-lookup"><span data-stu-id="eb396-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="eb396-305">Cuando se registre para notificaciones push desde un cliente autenticado, asegúrese de que la autenticación se ha completado antes de intentar el registro.</span><span class="sxs-lookup"><span data-stu-id="eb396-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="eb396-306">Para obtener más información, consulte [Push toousers] [ 6] de ejemplo de tutorial rápido completada de aplicación del servicio de aplicaciones móviles de Hola de back-end. NET.</span><span class="sxs-lookup"><span data-stu-id="eb396-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="eb396-307">Cómo: depurar y solucionar problemas de hello .NET SDK de servidor</span><span class="sxs-lookup"><span data-stu-id="eb396-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="eb396-308">El Servicio de aplicaciones de Azure proporciona varias técnicas de depuración y solución de problemas para las aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="eb396-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="eb396-309">Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="eb396-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="eb396-310">Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="eb396-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="eb396-311">Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eb396-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="eb396-312">Registro</span><span class="sxs-lookup"><span data-stu-id="eb396-312">Logging</span></span>
<span data-ttu-id="eb396-313">Puede escribir tooApp registros de diagnóstico de servicio mediante el uso de escritura de seguimiento ASP.NET estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="eb396-314">Antes de poder escribir toohello registros, debe habilitar los diagnósticos en su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="eb396-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="eb396-315">registros de toohello de escritura y diagnóstico tooenable:</span><span class="sxs-lookup"><span data-stu-id="eb396-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="eb396-316">Siga los pasos de hello en [cómo diagnósticos tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="eb396-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="eb396-317">Agregue los siguiente hello mediante declaración en el archivo de código:</span><span class="sxs-lookup"><span data-stu-id="eb396-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="eb396-318">Crear un toowrite de escritor de seguimiento de hello .NET back-end toohello registros de diagnóstico, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="eb396-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="eb396-319">Volver a publicar el proyecto de servidor y ruta de código de hello tooexecute back-end de aplicación móvil Hola con el registro de hello de acceso.</span><span class="sxs-lookup"><span data-stu-id="eb396-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="eb396-320">Descargue y evalúe los registros de hello, como se describe en [Cómo: descargar registros](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="eb396-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="eb396-321"><a name="local-debug"></a>Depuración local con autenticación</span><span class="sxs-lookup"><span data-stu-id="eb396-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="eb396-322">Puede ejecutar la aplicación localmente tootest cambia antes de publicarlos en la nube toohello.</span><span class="sxs-lookup"><span data-stu-id="eb396-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="eb396-323">Para la mayoría de los servidores back-end de Azure Mobile Apps, presione *F5* mientras está en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb396-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="eb396-324">Sin embargo, hay algunas consideraciones adicionales cuando se usa la autenticación.</span><span class="sxs-lookup"><span data-stu-id="eb396-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="eb396-325">Debe tener una aplicación móvil en la nube con aplicación de servicio de autenticación/autorización configurado, y el cliente debe tener el extremo de nube Hola especificado como host de inicio de sesión alternativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb396-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="eb396-326">Consulte la documentación de hello para la plataforma de cliente para obtener pasos específicos Hola necesarios.</span><span class="sxs-lookup"><span data-stu-id="eb396-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="eb396-327">Asegúrese de que el back-end tenga instalado [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="eb396-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="eb396-328">A continuación, en la clase de inicio de la aplicación OWIN, agregue siguiente hello, después de `MobileAppConfiguration` se ha aplicado tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="eb396-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="eb396-329">En el anterior ejemplo de Hola, debe configurar hello *authAudience* y *authIssuer* aplicación en el archivo Web.config del archivo de configuración tooeach sea la dirección URL de la raíz de la aplicación, con hello HTTPS esquema.</span><span class="sxs-lookup"><span data-stu-id="eb396-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="eb396-330">Del mismo modo debe establecer *authSigningKey* toobe valor de saludo de la aplicación de la clave de firma.</span><span class="sxs-lookup"><span data-stu-id="eb396-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="eb396-331">clave de firma de Hola tooobtain:</span><span class="sxs-lookup"><span data-stu-id="eb396-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="eb396-332">Navegar por la aplicación tooyour en hello [portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="eb396-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="eb396-333">Haga clic en **Herramientas**, **Kudu**, **Ir**.</span><span class="sxs-lookup"><span data-stu-id="eb396-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="eb396-334">En el sitio de administración de Kudu hello, haga clic en **entorno**.</span><span class="sxs-lookup"><span data-stu-id="eb396-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="eb396-335">Buscar valor Hola para *sitio Web\_AUTH\_firma\_clave*.</span><span class="sxs-lookup"><span data-stu-id="eb396-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="eb396-336">Hola de uso clave para hello firma *authSigningKey* parámetro en la configuración de la aplicación local.  El back-end móvil ya está equipado toovalidate tokens cuando se ejecuta localmente, qué cliente hello Obtiene el token de Hola desde el punto de conexión de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="eb396-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portal de Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
