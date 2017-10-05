---
title: Trabajo con el SDK del servidor back-end de .NET para Mobile Apps | Microsoft Docs
description: "Obtenga información sobre cómo trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles del Servicio de aplicaciones de Azure"
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="4d7b9-104">Trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="4d7b9-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="4d7b9-105">En este tema se muestra cómo usar el SDK del servidor back-end de .NET en escenarios clave de Aplicaciones móviles del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="4d7b9-106">El SDK de Aplicaciones móviles de Azure le permite trabajar con clientes móviles de su aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="4d7b9-107">El [SDK de servidor de .NET para Azure Mobile Apps][2] es de código abierto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="4d7b9-108">El repositorio contiene todo el código fuente incluido en el conjunto de pruebas de unidad SDK del servidor completo, así como algunos proyectos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="4d7b9-109">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="4d7b9-109">Reference documentation</span></span>
<span data-ttu-id="4d7b9-110">La documentación de referencia del SDK del servidor se encuentra aquí: [Referencia de .NET de Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="4d7b9-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="4d7b9-111"><a name="create-app"></a>Creación de un back-end de aplicación móvil .NET</span><span class="sxs-lookup"><span data-stu-id="4d7b9-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="4d7b9-112">Si va a iniciar un nuevo proyecto, puede crear una aplicación del Servicio de aplicaciones mediante el [Portal de Azure] o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="4d7b9-113">Puede ejecutar la aplicación de App Service localmente o publicarla en la aplicación móvil de App Service basada en la nube.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="4d7b9-114">Si va a agregar funcionalidades móviles a un proyecto existente, consulte la sección [Descarga e inicialización del SDK](#install-sdk) .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="4d7b9-115">Creación de un back-end .NET mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4d7b9-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="4d7b9-116">Para crear una instancia de App Service de back-end móvil, siga el [tutorial rápido][3] o estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="4d7b9-117">De nuevo en la hoja *Comenzar*, en **Create a table API** (Crear una API de tabla), elija **C#** como el valor de **Backend language** (Lenguaje de back-end).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="4d7b9-118">Haga clic en **Descargar**, extraiga los archivos de proyecto comprimidos en el equipo local y abra la solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="4d7b9-119">Creación de un back-end .NET con Visual Studio 2013 y Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4d7b9-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="4d7b9-120">Para crear un proyecto de Azure Mobile Apps en Visual Studio, instale la versión 2.9.0 o posterior de [Azure SDK para .NET][4].</span><span class="sxs-lookup"><span data-stu-id="4d7b9-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="4d7b9-121">Una vez haya instalado el SDK, cree una aplicación de ASP.NET mediante los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="4d7b9-122">Abra el cuadro de diálogo **Nuevo proyecto** (desde *Archivo* > **Nuevo** > **Proyecto...**).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="4d7b9-123">Expanda **Plantillas** > **Visual C#** y seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="4d7b9-124">Seleccione **Aplicación web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="4d7b9-125">Rellene el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-125">Fill in the project name.</span></span> <span data-ttu-id="4d7b9-126">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-126">Then click **OK**.</span></span>
5. <span data-ttu-id="4d7b9-127">En *Plantillas de ASP.NET 4.5.2*, seleccione **Aplicación móvil de Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="4d7b9-128">Seleccione **Host en la nube** para crear un back-end móvil en la nube, en el que puede publicar este proyecto.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="4d7b9-129">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-129">Click **OK**.</span></span>

## <span data-ttu-id="4d7b9-130"><a name="install-sdk"></a>Descarga e inicialización del SDK</span><span class="sxs-lookup"><span data-stu-id="4d7b9-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="4d7b9-131">El SDK está disponible en [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="4d7b9-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="4d7b9-132">Este paquete incluye la funcionalidad básica necesaria para comenzar a usar el SDK.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="4d7b9-133">Para inicializar el SDK, tendrá que realizar acciones en el objeto **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="4d7b9-134">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="4d7b9-134">Install the SDK</span></span>
<span data-ttu-id="4d7b9-135">Para instalar el SDK, haga clic con el botón derecho en el proyecto de servidor en Visual Studio, seleccione **Administrar paquetes de NuGet**, busque el paquete [Microsoft.Azure.Mobile.Server] y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="4d7b9-136"><a name="server-project-setup"></a> Inicializar el proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="4d7b9-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="4d7b9-137">Un proyecto de servidor backend de .NET se inicializa de manera similar a otros proyectos ASP.NET mediante la inclusión de una clase de inicio OWIN.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="4d7b9-138">Asegúrese de que ha hecho referencia al paquete de NuGet `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="4d7b9-139">Para agregar esta clase en Visual Studio, haga clic con el botón derecho en el proyecto de servidor y seleccione **Agregar** >
**Nuevo elemento**, luego **Web** > **General** > **Clase de inicio OWIN**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="4d7b9-140">Se genera una clase con el atributo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="4d7b9-141">En el método `Configuration()` de la clase de inicio OWIN, use un objeto **HttpConfiguration** para configurar el entorno de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="4d7b9-142">En el ejemplo siguiente se inicializa el proyecto de servidor sin características agregadas:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="4d7b9-143">Para habilitar características individuales, debe llamar a los métodos de extensión del objeto **MobileAppConfiguration** antes de llamar a **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="4d7b9-144">Por ejemplo, el siguiente código agrega las rutas predeterminadas a todos los controladores de API que tengan el atributo `[MobileAppController]` durante la inicialización:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="4d7b9-145">El inicio rápido de servidor desde el Portal de Azure llama a **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="4d7b9-146">Es equivalente a la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="4d7b9-147">Los métodos de extensión utilizados son:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-147">The extension methods used are:</span></span>

* <span data-ttu-id="4d7b9-148">`AddMobileAppHomeController()` proporciona la página principal predeterminada de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="4d7b9-149">`MapApiControllers()` proporciona funcionalidades de API personalizadas para controladores de WebAPI que contienen el atributo `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="4d7b9-150">`AddTables()` proporciona una asignación de los puntos de conexión `/tables` a los controladores de la tabla.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="4d7b9-151">`AddTablesWithEntityFramework()` es un elemento abreviado para la asignación de los puntos de conexión `/tables` mediante controladores basados en Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="4d7b9-152">`AddPushNotifications()` proporciona un método sencillo de registrar los dispositivos para Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="4d7b9-153">`MapLegacyCrossDomainController()` proporciona los encabezados de CORS estándar para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="4d7b9-154">Extensiones de SDK</span><span class="sxs-lookup"><span data-stu-id="4d7b9-154">SDK extensions</span></span>
<span data-ttu-id="4d7b9-155">Los siguientes paquetes de extensión basados en NuGet proporcionan diversas características móviles que puede usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="4d7b9-156">Las extensiones se habilitan durante la inicialización mediante el objeto **MobileAppConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="4d7b9-157">[Microsoft.Azure.Mobile.Server.Quickstart] admite la configuración básica de Aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="4d7b9-158">Se agrega a la configuración mediante una llamada al método de extensión **UseDefaultConfiguration** durante la inicialización.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="4d7b9-159">Esta extensión incluye las siguientes extensiones: paquetes de notificaciones, autenticación, entidad, tablas, entre dominios y principal.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="4d7b9-160">Inicio rápido de Mobile Apps, disponible en Azure Portal, usa este paquete.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="4d7b9-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implementa el valor predeterminado de *esta página de aplicación móvil está funcionando* para la raíz del sitio web.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="4d7b9-162">Se agrega a la configuración mediante una llamada al método de extensión **AddMobileAppHomeController** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="4d7b9-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) incluye clases para trabajar con datos y configura la canalización de datos.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="4d7b9-164">Se agrega a la configuración mediante una llamada al método de extensión **AddTables** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="4d7b9-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permite a Entity Framework obtener acceso a los datos de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="4d7b9-166">Se agrega a la configuración mediante una llamada al método de extensión **AddTablesWithEntityFramework** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="4d7b9-167">[Microsoft.Azure.Mobile.Server.Authentication] habilita la autenticación y configura el middleware OWIN que se usa para validar los tokens.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="4d7b9-168">Se agrega a la configuración mediante una llamada a los métodos de extensión **AddAppServiceAuthentication** e **IAppBuilder**.**UseAppServiceAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="4d7b9-169">[Microsoft.Azure.Mobile.Server.Notifications] habilita las notificaciones push y define un punto de conexión de registro de inserción.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="4d7b9-170">Se agrega a la configuración mediante una llamada al método de extensión **AddPushNotifications** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="4d7b9-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) crea un controlador que sirve datos de la aplicación móvil a los exploradores web heredados.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="4d7b9-172">Se agrega a la configuración mediante una llamada al método de extensión **MapLegacyCrossDomainController** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="4d7b9-173">[Microsoft.Azure.Mobile.Server.Login] proporciona el método AppServiceLoginHandler.CreateToken(), que es un método estático usado en escenarios de autenticación personalizada.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="4d7b9-174"><a name="publish-server-project"></a>Procedimientos: Publicación del proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="4d7b9-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="4d7b9-175">En esta sección se muestra cómo publicar el proyecto de back-end de .NET desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="4d7b9-176">También puede implementar el proyecto de back-end mediante Git o cualquiera de los otros métodos descritos en la [documentación de implementación del Servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="4d7b9-177">En Visual Studio, vuelva a generar el proyecto para restaurar los paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="4d7b9-178">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y luego haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="4d7b9-179">La primera vez que publique, debe definir un perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="4d7b9-180">Si ya tiene un perfil definido, puede seleccionarlo y hacer clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="4d7b9-181">Si se le pide que seleccione un destino de publicación, haga clic en **Microsoft Azure App Service** > **Siguiente** y, luego, (si es necesario), inicie sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="4d7b9-182">Visual Studio descarga y almacena la configuración de publicación directamente desde Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="4d7b9-183">Elija su suscripción en **Suscripción**, seleccione **Tipo de recurso** en **Vista**, expanda **Aplicación móvil** y haga clic en el back-end de aplicación móvil y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="4d7b9-184">Compruebe la información del perfil de publicación y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="4d7b9-185">Cuando el back-end de la aplicación móvil se haya publicado correctamente, verá una página de aterrizaje que indica el éxito.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="4d7b9-186"><a name="define-table-controller"></a> Definición de un controlador de tabla</span><span class="sxs-lookup"><span data-stu-id="4d7b9-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="4d7b9-187">Defina un controlador de tabla para exponer una tabla de SQL para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="4d7b9-188">La configuración de un controlador de tabla requiere tres pasos:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="4d7b9-189">Creación de una clase Data Transfer Object (DTO).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="4d7b9-190">Configuración de una referencia de tabla en la clase Mobile DbContext.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="4d7b9-191">Creación de un controlador de tabla.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-191">Create a table controller.</span></span>

<span data-ttu-id="4d7b9-192">Un objeto de transferencia de datos (DTO) es un objeto de C# simple heredado de `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="4d7b9-193">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="4d7b9-194">El objeto DTO se utiliza para definir la tabla en SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="4d7b9-195">Para crear la entrada de la base de datos, agregue una propiedad `DbSet<>` a la instancia de DbContext que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="4d7b9-196">En la plantilla de proyecto predeterminada para Azure Mobile Apps, la instancia de DbContext se llama `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="4d7b9-197">Si tiene instalado Azure SDK, ahora puede crear un controlador de tabla de la plantilla como sigue:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="4d7b9-198">Haga clic con el botón derecho en la carpeta Controladores y seleccione **Agregar** > **Controlador...**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="4d7b9-199">Seleccione la opción **Controlador de tabla de Azure Mobile Apps** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="4d7b9-200">En el cuadro de diálogo **Agregar controlador** :</span><span class="sxs-lookup"><span data-stu-id="4d7b9-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="4d7b9-201">En la lista desplegable **Clase de modelo** , seleccione el nuevo DTO.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="4d7b9-202">En la lista desplegable **DbContext** , seleccione la clase Mobile Service DbContext.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="4d7b9-203">Se crea el nombre del controlador.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="4d7b9-204">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-204">Click **Add**.</span></span>

<span data-ttu-id="4d7b9-205">El proyecto de servidor de inicio rápido contiene un ejemplo de un controlador **TodoItemController**simple.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="4d7b9-206"><a name="adjust-pagesize"></a>Cómo ajustar el tamaño de paginación de la tabla</span><span class="sxs-lookup"><span data-stu-id="4d7b9-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="4d7b9-207">De forma predeterminada, Aplicaciones móviles de Azure devuelve 50 registros por solicitud.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="4d7b9-208">La paginación garantiza que el cliente no mantenga ocupado su subproceso de interfaz de usuario ni el servidor durante mucho tiempo, con lo que se asegura una buena experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="4d7b9-209">Para cambiar el tamaño de paginación de la tabla, aumente el "tamaño de consulta permitido" del lado del servidor y cambie el tamaño de la página de lado del cliente. El "tamaño de consulta permitido" del lado del servidor se ajusta con el atributo `EnableQuery`:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="4d7b9-210">Asegúrese de que el valor de PageSize sea igual o mayor que el tamaño solicitado por el cliente.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="4d7b9-211">Consulte la documentación de procedimientos para obtener más información sobre cómo cambiar el tamaño de página de cliente.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="4d7b9-212">Cómo definir un controlador de API personalizada</span><span class="sxs-lookup"><span data-stu-id="4d7b9-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="4d7b9-213">El controlador de API personalizada proporciona la funcionalidad más básica al back-end de la aplicación móvil mediante la exposición de un extremo.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="4d7b9-214">Puede registrar un controlador de API específico de dispositivos móviles con el atributo [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="4d7b9-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="4d7b9-215">El atributo `MobileAppController` registra la ruta, configura el serializador JSON de Mobile Apps y activa la [comprobación de la versión del cliente](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="4d7b9-216">En Visual Studio, haga clic con el botón derecho en la carpeta Controladores y, luego, haga clic en **Agregar** > **Controladores**, seleccione **Controlador de Web API 2&mdash;Vacío** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="4d7b9-217">Proporcione un valor de **Nombre de controlador**, como `CustomController`, y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="4d7b9-218">En el archivo de clase de controlador nuevo, agregue la siguiente instrucción Using:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="4d7b9-219">Aplique el atributo **[MobileAppController]** a la definición de clase del controlador de API, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="4d7b9-220">En el archivo App_Start/Startup.MobileApp.cs, agregue una llamada al método de extensión **MapApiControllers**, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="4d7b9-221">También puede utilizar el método de extensión `UseDefaultConfiguration()`, en lugar de `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="4d7b9-222">Los clientes pueden tener acceso a un controlador aunque este no tenga un elemento **MobileAppControllerAttribute** aplicado, pero puede que no lo consuman correctamente si usan un SDK de cliente de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="4d7b9-223">Procedimiento: Autenticación</span><span class="sxs-lookup"><span data-stu-id="4d7b9-223">How to: Work with authentication</span></span>
<span data-ttu-id="4d7b9-224">Azure Mobile Apps usa la autenticación o autorización de App Service para proteger su back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="4d7b9-225">En esta sección se muestra cómo realizar las siguientes tareas relacionadas con la autenticación en el proyecto de servidor back-end. NET:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="4d7b9-226">Cómo agregar autenticación a un proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="4d7b9-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="4d7b9-227">Procedimiento: Uso de autenticación personalizada en la aplicación</span><span class="sxs-lookup"><span data-stu-id="4d7b9-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="4d7b9-228">Procedimiento: Recuperación de la información de usuario de autenticado</span><span class="sxs-lookup"><span data-stu-id="4d7b9-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="4d7b9-229">Cómo restringir el acceso a datos para los usuarios autorizados</span><span class="sxs-lookup"><span data-stu-id="4d7b9-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="4d7b9-230"><a name="add-auth"></a>Cómo agregar autenticación a un proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="4d7b9-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="4d7b9-231">Para agregar autenticación al proyecto de servidor, extienda el objeto **MobileAppConfiguration** y configure el middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="4d7b9-232">Cuando instale el paquete [Microsoft.Azure.Mobile.Server.Quickstart] y llame al método de extensión **UseDefaultConfiguration** , puede continuar desde el paso 3.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="4d7b9-233">En Visual Studio, instale el paquete [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="4d7b9-234">En el archivo de proyecto Startup.cs, agregue la siguiente línea de código al principio del método **Configuration** :</span><span class="sxs-lookup"><span data-stu-id="4d7b9-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="4d7b9-235">Este componente del middleware OWIN valida los tokens emitidos por la puerta de enlace de App Service asociada.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="4d7b9-236">Agregue el atributo `[Authorize]` a cualquier controlador o método que requiera autenticación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="4d7b9-237">Para más información sobre cómo autenticar a los clientes en el back-end de Aplicaciones móviles, consulte [Incorporación de la autenticación a la aplicación](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="4d7b9-238"><a name="custom-auth"></a>Procedimiento: Uso de autenticación personalizada en la aplicación</span><span class="sxs-lookup"><span data-stu-id="4d7b9-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="4d7b9-239">Si no desea usar uno de los proveedores de autenticación y autorización de App Service, puede implementar su propio sistema de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="4d7b9-240">Instale el paquete [Microsoft.Azure.Mobile.Server.Login] para ayudar a la generación de tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="4d7b9-241">Proporcione su propio código para validar las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="4d7b9-242">Por ejemplo, podría comprobar las contraseñas con sal y hash de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="4d7b9-243">En el ejemplo siguiente, el método `isValidAssertion()` (definido en otra parte) es responsable de estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="4d7b9-244">La autenticación personalizada se expone mediante la creación de un controlador ApiController y la exposición de las acciones `register` y `login`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="4d7b9-245">El cliente debe utilizar una interfaz de usuario personalizada para recopilar la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="4d7b9-246">A continuación, la información se envía a la API con una llamada HTTP POST estándar.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="4d7b9-247">Una vez que el servidor valida la aserción, se emite un token con el método `AppServiceLoginHandler.CreateToken()` .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="4d7b9-248">El controlador ApiController **no debería** utilizar el atributo `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="4d7b9-249">Ejemplo de la acción `login` :</span><span class="sxs-lookup"><span data-stu-id="4d7b9-249">An example `login` action:</span></span>

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

<span data-ttu-id="4d7b9-250">En el ejemplo anterior, LoginResult y LoginResultUser son objetos serializables que exponen las propiedades necesarias.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="4d7b9-251">El cliente espera que las repuestas de inicio de sesión se devuelvan como objetos JSON con este formato:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="4d7b9-252">El método `AppServiceLoginHandler.CreateToken()` incluye un parámetro *audience* y un parámetro *issuer*.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="4d7b9-253">Ambos parámetros se establecen en la dirección URL de la raíz de la aplicación, mediante el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="4d7b9-254">De igual modo, debe establecer *secretKey* como el valor de la clave de firma de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="4d7b9-255">No distribuya la clave de firma en un cliente, ya que se puede usar para inventar claves y suplantar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="4d7b9-256">Puede obtener la clave de firma mientras se hospeda en App Service mediante la referencia a la variable de entorno *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="4d7b9-257">Si es necesario en un contexto de depuración local, siga las instrucciones de la sección [Depuración local con autenticación](#local-debug) para recuperar la clave y almacenarla como un valor de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="4d7b9-258">El token emitido también puede incluir otras notificaciones y una fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="4d7b9-259">Como mínimo, el token emitido debe incluir una notificación de asunto (**sub**).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="4d7b9-260">Puede admitir el método `loginAsync()` del cliente estándar mediante la sobrecarga de la ruta de autenticación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="4d7b9-261">Si el cliente llama a `client.loginAsync('custom');` para iniciar sesión, la ruta debe ser `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="4d7b9-262">Puede establecer la ruta para el controlador de autenticación personalizada con `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="4d7b9-263">Con el enfoque `loginAsync()` se garantiza que el token de autenticación se asocia a cada llamada posterior al servicio.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="4d7b9-264"><a name="user-info"></a>Procedimiento: Recuperación de la información de usuario autenticada</span><span class="sxs-lookup"><span data-stu-id="4d7b9-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="4d7b9-265">Cuando un usuario se autentica mediante el Servicio de aplicaciones, se puede tener acceso al id. de usuario asignado y otra información en el código del back-end. NET.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="4d7b9-266">La información de usuario se puede utilizar para tomar decisiones de autorización en el back-end.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="4d7b9-267">El código siguiente obtiene el identificador de usuario asociado a una solicitud:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="4d7b9-268">El SID se deriva del identificador de usuario específico del proveedor y es estático para un usuario y un proveedor de inicio de sesión dados.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="4d7b9-269">El SID es nulo para los tokens de autenticación no válidos.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="4d7b9-270">El Servicio de aplicaciones también le permite solicitar notificaciones específicas de su proveedor de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="4d7b9-271">Cada proveedor de identidades puede proporcionar más información mediante el SDK del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="4d7b9-272">Por ejemplo, puede usar la API Graph de Facebook para la información de los amigos.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="4d7b9-273">Puede especificar notificaciones solicitadas en la hoja del proveedor en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="4d7b9-274">Algunas notificaciones requieren configuración adicional con el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="4d7b9-275">El código siguiente llama al método de extensión **GetAppServiceIdentityAsync** para obtener las credenciales de inicio de sesión, que incluyen el token de acceso necesario para realizar solicitudes en la API Graph de Facebook:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="4d7b9-276">Agregue una instrucción de uso para que `System.Security.Principal` proporcione el método de extensión **GetAppServiceIdentityAsync** .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="4d7b9-277"><a name="authorize"></a>Cómo restringir el acceso a datos para los usuarios autorizados</span><span class="sxs-lookup"><span data-stu-id="4d7b9-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="4d7b9-278">En la sección anterior, hemos mostrado cómo recuperar el identificador de usuario de un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="4d7b9-279">Puede restringir el acceso a datos y otros recursos basándose en este valor.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="4d7b9-280">Por ejemplo, agregar una columna de identificador de usuario (userId) a las tablas y filtrar los resultados de la consulta por el identificador de usuario es una manera sencilla de limitar los datos devueltos únicamente a los usuarios autorizados.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="4d7b9-281">El código siguiente solo devuelve filas de datos cuando el SID coincide con el valor de la columna UserId de la tabla TodoItem:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="4d7b9-282">El método `Query()` devuelve un `IQueryable` que LINQ puede manipular para controlar el filtrado.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="4d7b9-283">Cómo agregar notificaciones push a un proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="4d7b9-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="4d7b9-284">Para agregar notificaciones push al proyecto de servidor, extienda el objeto **MobileAppConfiguration** y cree un cliente de Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="4d7b9-285">En Visual Studio, haga clic con el botón derecho en el proyecto de servidor, haga clic en **Administrar paquetes de NuGet**, busque `Microsoft.Azure.Mobile.Server.Notifications` y, por último, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="4d7b9-286">Repita este paso para instalar el paquete `Microsoft.Azure.NotificationHubs` , que incluye la biblioteca de cliente de Centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="4d7b9-287">En App_Start/Startup.MobileApp.cs, agregue una llamada al método de extensión **AddPushNotifications()** durante la inicialización:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="4d7b9-288">Agregue el siguiente código, que crea un nuevo cliente de Centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="4d7b9-289">Ahora puede usar el cliente de Notification Hubs para enviar notificaciones push a dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="4d7b9-290">Para más información, vea [Incorporación de notificaciones push a la aplicación](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="4d7b9-291">Aprenda más sobre Notification Hubs en la [introducción a Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="4d7b9-292"><a name="tags"></a>Habilitación de la inserción de destino mediante etiquetas</span><span class="sxs-lookup"><span data-stu-id="4d7b9-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="4d7b9-293">Los Centros de notificaciones permite enviar notificaciones dirigidas a registros específicos mediante el uso de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="4d7b9-294">Se crean varias etiquetas automáticamente:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="4d7b9-295">El identificador de instalación identifica un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="4d7b9-296">El identificador de usuario basado en el SID autenticado identifica un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="4d7b9-297">Se puede acceder al identificador de instalación desde la propiedad **installationId** en **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="4d7b9-298">En el ejemplo siguiente se muestra cómo usar un identificador de instalación para agregar una etiqueta a una instalación específica en los Centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="4d7b9-299">Al crear la instalación, el back-end ignora las etiquetas proporcionadas por el cliente durante el registro de notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="4d7b9-300">Para que un cliente pueda agregar etiquetas a la instalación, debe crear una API personalizada que agregue etiquetas mediante el patrón anterior.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="4d7b9-301">Consulte la información sobre las [etiquetas de notificaciones push agregadas por el cliente][5] en el ejemplo de inicio rápido completado de App Service Mobile Apps para ver un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="4d7b9-302"><a name="push-user"></a>Envío de notificaciones push a un usuario autenticado</span><span class="sxs-lookup"><span data-stu-id="4d7b9-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="4d7b9-303">Cuando un usuario autenticado se registra para las notificaciones push, se agrega automáticamente una etiqueta con el identificador de usuario al registro.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="4d7b9-304">Mediante esta etiqueta, puede enviar notificaciones push a todos los dispositivos registrados por ese usuario.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="4d7b9-305">El código siguiente obtiene el SID del usuario que realiza la solicitud y envía una notificación push de plantilla a cada registro de dispositivo para esa persona:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="4d7b9-306">Cuando se registre para notificaciones push desde un cliente autenticado, asegúrese de que la autenticación se ha completado antes de intentar el registro.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="4d7b9-307">Para más información, consulte [Push to users][6] (Notificación push a usuarios) en el ejemplo de inicio rápido de App Service Mobile Apps completado para el back-end de .NET.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="4d7b9-308">Procedimientos: Depuración y solución de problemas del SDK de .NET Server</span><span class="sxs-lookup"><span data-stu-id="4d7b9-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="4d7b9-309">El Servicio de aplicaciones de Azure proporciona varias técnicas de depuración y solución de problemas para las aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="4d7b9-310">Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="4d7b9-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="4d7b9-311">Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="4d7b9-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="4d7b9-312">Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d7b9-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="4d7b9-313">Registro</span><span class="sxs-lookup"><span data-stu-id="4d7b9-313">Logging</span></span>
<span data-ttu-id="4d7b9-314">Puede escribir en registros de diagnóstico del Servicio de aplicaciones mediante la escritura de seguimiento estándar de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="4d7b9-315">Antes de poder escribir en los registros, debe habilitar los diagnósticos en su back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="4d7b9-316">Para habilitar los diagnósticos y escribir en los registros:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="4d7b9-317">Siga los pasos que se indican en [Habilitación de diagnósticos](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="4d7b9-318">Agregue la siguiente instrucción using en el archivo de código:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="4d7b9-319">Cree un escritor de seguimiento para escribir desde el back-end de .NET en los registros de diagnóstico, de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="4d7b9-320">Vuelva a publicar el proyecto de servidor y acceda al back-end de aplicación móvil para ejecutar la ruta de acceso del código con el registro.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="4d7b9-321">Descargue y evalúe los registros, como se describe en [Procedimiento: Descarga de registros](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="4d7b9-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="4d7b9-322"><a name="local-debug"></a>Depuración local con autenticación</span><span class="sxs-lookup"><span data-stu-id="4d7b9-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="4d7b9-323">Puede ejecutar la aplicación localmente para probar los cambios antes de publicarlos en la nube.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="4d7b9-324">Para la mayoría de los servidores back-end de Azure Mobile Apps, presione *F5* mientras está en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="4d7b9-325">Sin embargo, hay algunas consideraciones adicionales cuando se usa la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="4d7b9-326">Debe tener una aplicación móvil basada en la nube que tenga configurada la característica Autenticación/autorización del Servicio de aplicaciones, y su cliente debe haber especificado el punto de conexión de nube como host de inicio de sesión alternativo.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="4d7b9-327">Consulte la documentación de la plataforma cliente para los pasos específicos requeridos.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="4d7b9-328">Asegúrese de que el back-end tenga instalado [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="4d7b9-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="4d7b9-329">Después, en la clase de inicio OWIN de la aplicación, agregue lo siguiente, después de aplicar `MobileAppConfiguration` a `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="4d7b9-330">En el ejemplo anterior, debe configurar los parámetros de la aplicación *authAudience* y *authIssuer* en el archivo Web.config para que cada uno sea la dirección URL de la raíz de la aplicación; para ello, usará el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="4d7b9-331">De igual modo, debe establecer *authSigningKey* como el valor de la clave de firma de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="4d7b9-332">Para obtener la clave de firma:</span><span class="sxs-lookup"><span data-stu-id="4d7b9-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="4d7b9-333">Vaya a la aplicación en [Portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="4d7b9-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="4d7b9-334">Haga clic en **Herramientas**, **Kudu**, **Ir**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="4d7b9-335">En el sitio de administración de Kudu, haga clic en **Entorno**.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="4d7b9-336">Busque el valor de *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="4d7b9-337">Use la clave de firma para el parámetro *authSigningKey* en la configuración de la aplicación local.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="4d7b9-338">Ahora, el back-end móvil está equipado para validar los tokens cuando se ejecuta localmente; el cliente obtiene el token del punto de conexión basado en la nube.</span><span class="sxs-lookup"><span data-stu-id="4d7b9-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="4d7b9-339">[Portal de Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4d7b9-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="4d7b9-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="4d7b9-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="4d7b9-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="4d7b9-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="4d7b9-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="4d7b9-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="4d7b9-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="4d7b9-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="4d7b9-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="4d7b9-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="4d7b9-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="4d7b9-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
