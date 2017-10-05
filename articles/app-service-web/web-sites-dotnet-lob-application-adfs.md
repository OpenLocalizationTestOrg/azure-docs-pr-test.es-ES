---
title: "Creación de una aplicación de Azure de línea de negocio con autenticación de AD FS | Microsoft Docs"
description: "Aprenda a crear una aplicación de línea de negocio en Azure App Service que se autentica con STS local. En este tutorial se dirige a AD FS como STS local."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="27153-104">Creación de una aplicación de Azure de línea de negocio con autenticación de AD FS</span><span class="sxs-lookup"><span data-stu-id="27153-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="27153-105">En este artículo se muestra cómo crear una aplicación de línea de negocio ASP.NET MVC en [Azure App Service](../app-service/app-service-value-prop-what-is.md) mediante el uso de [Servicios de federación de Active Directory](http://technet.microsoft.com/library/hh831502.aspx) locales como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="27153-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="27153-106">Este escenario puede funcionar cuando desea crear aplicaciones de línea de negocio en el Servicio de aplicaciones de Azure, pero su organización requiere que los datos de directorio se almacenen en el sitio.</span><span class="sxs-lookup"><span data-stu-id="27153-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="27153-107">Para información general de las distintas opciones de autorización y autenticación empresarial para Servicio de aplicaciones de Azure, consulte [Autenticación con Active Directory local en aplicaciones de Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="27153-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="27153-108">Lo que va a crear</span><span class="sxs-lookup"><span data-stu-id="27153-108">What you will build</span></span>
<span data-ttu-id="27153-109">Creará una aplicación ASP.NET básica en Aplicaciones web del Servicio de aplicaciones de Azure con las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="27153-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="27153-110">Autentica a los usuarios con AD FS</span><span class="sxs-lookup"><span data-stu-id="27153-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="27153-111">Usa `[Authorize]` para autorizar a los usuarios para distintas acciones</span><span class="sxs-lookup"><span data-stu-id="27153-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="27153-112">Configuración estática tanto para depurar en Visual Studio como para publicar en Aplicaciones web del Servicio de aplicaciones (configurar una vez, depurar y publicar en cualquier momento)</span><span class="sxs-lookup"><span data-stu-id="27153-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="27153-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="27153-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="27153-114">Necesita lo siguiente para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="27153-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="27153-115">Una implementación de AD FS local (para obtener un tutorial de un extremo a otro del laboratorio de pruebas que se usa en este tutorial, consulte [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/)) [Laboratorio de pruebas: STS independiente con AD FS en VM de Azure (solo para prueba)].</span><span class="sxs-lookup"><span data-stu-id="27153-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="27153-116">Permisos para crear relaciones de confianza para usuarios autenticados en la administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="27153-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="27153-117">Visual Studio 2013, actualización 4 o posterior</span><span class="sxs-lookup"><span data-stu-id="27153-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="27153-118">[SDK de Azure 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o posterior.</span><span class="sxs-lookup"><span data-stu-id="27153-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="27153-119">Usar la aplicación de ejemplo para la plantilla de línea de negocio</span><span class="sxs-lookup"><span data-stu-id="27153-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="27153-120">La aplicación de muestra de este tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), la crea el equipo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27153-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="27153-121">Debido a que AD FS es compatible con WS-Federation, puede usarla como una plantilla para crear aplicaciones de línea de negocio con facilidad.</span><span class="sxs-lookup"><span data-stu-id="27153-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="27153-122">Tiene las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="27153-122">It has the following features:</span></span>

* <span data-ttu-id="27153-123">Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) para autenticar con una implementación de AD FS local</span><span class="sxs-lookup"><span data-stu-id="27153-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="27153-124">Funcionalidad de inicio y de cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="27153-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="27153-125">Usa [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (en lugar de Windows Identity Foundation), que es el futuro de ASP.NET y mucho más sencillo de configurar que WIF para la autenticación y autorización</span><span class="sxs-lookup"><span data-stu-id="27153-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="27153-126">Configurar la aplicación de muestra</span><span class="sxs-lookup"><span data-stu-id="27153-126">Set up the sample application</span></span>
1. <span data-ttu-id="27153-127">Clone o descargue la solución de muestra de [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) en su directorio local.</span><span class="sxs-lookup"><span data-stu-id="27153-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27153-128">Las instrucciones de [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) le muestran cómo configurar la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27153-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="27153-129">No obstante, en este tutorial, la va a configurar con AD FS, por lo que tiene que seguir los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="27153-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="27153-130">Abra la solución y, a continuación, Controllers\AccountController.cs en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="27153-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="27153-131">Verá que el código simplemente emite un desafío de autenticación para autenticar al usuario con WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="27153-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="27153-132">Toda la autenticación se configura en App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="27153-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="27153-133">Abra App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="27153-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="27153-134">En el método `ConfigureAuth`, observe la línea:</span><span class="sxs-lookup"><span data-stu-id="27153-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="27153-135">En el mundo de OWIN, este snippet es realmente lo mínimo que se necesita para configurar la autenticación de WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="27153-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="27153-136">Es mucho más sencillo y elegante que WIF, donde Web.config se inserta con XML por todas partes.</span><span class="sxs-lookup"><span data-stu-id="27153-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="27153-137">La única información que necesita es el identificador del usuario de confianza y la dirección URL del archivo de metadatos del servicio AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="27153-138">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="27153-138">Here's an example:</span></span>
   
   * <span data-ttu-id="27153-139">Identificador del usuario de confianza: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="27153-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="27153-140">Dirección de metadatos: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="27153-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="27153-141">En App_Start\Startup.Auth.cs, cambie las siguientes definiciones de cadena estática:</span><span class="sxs-lookup"><span data-stu-id="27153-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="27153-142">Ahora haga los cambios correspondientes en Web.config.</span><span class="sxs-lookup"><span data-stu-id="27153-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="27153-143">Abra Web.config y modifique la siguiente configuración de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="27153-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="27153-144">Rellene los valores de clave en función de su entorno respectivo.</span><span class="sxs-lookup"><span data-stu-id="27153-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="27153-145">Compile la aplicación para asegurarse de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="27153-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="27153-146">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="27153-146">That's it.</span></span> <span data-ttu-id="27153-147">Ahora la aplicación de muestra está lista para trabajar con AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="27153-148">Todavía tiene que configurar una relación de confianza para usuario autenticado con esta aplicación en AD FS posteriormente.</span><span class="sxs-lookup"><span data-stu-id="27153-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="27153-149">Implemente la aplicación de muestra en Aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="27153-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="27153-150">Aquí publica la aplicación en una aplicación web en Aplicaciones web del Servicio de aplicaciones, a la vez que conserva el entorno de depuración.</span><span class="sxs-lookup"><span data-stu-id="27153-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="27153-151">Tenga en cuenta que va a publicar la aplicación antes de que tenga una relación de confianza para usuario autenticado con AD FS, por lo que la autenticación no funciona todavía.</span><span class="sxs-lookup"><span data-stu-id="27153-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="27153-152">Sin embargo, si lo hace ahora puede tener la dirección URL de la aplicación web que puede usar para configurar una relación de confianza para usuario autenticado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="27153-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="27153-153">Haga clic con el botón derecho en el proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="27153-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="27153-154">Seleccione **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="27153-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="27153-155">Si no ha iniciado sesión en Azure, haga clic en **Iniciar sesión** y use la cuenta de Microsoft de su suscripción de Azure para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="27153-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="27153-156">Cuando haya iniciado sesión, haga clic en **Nuevo** para crear una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="27153-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="27153-157">Rellene todos los campos obligatorios.</span><span class="sxs-lookup"><span data-stu-id="27153-157">Fill in all required fields.</span></span> <span data-ttu-id="27153-158">Se va a conectar a datos locales posteriormente, así que no cree ninguna base de datos para esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="27153-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="27153-159">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="27153-159">Click **Create**.</span></span> <span data-ttu-id="27153-160">Una vez que se haya creado la aplicación web, se abrirá el cuadro de diálogo Publicación web.</span><span class="sxs-lookup"><span data-stu-id="27153-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="27153-161">En **Dirección URL de destino**, cambie **http** a **https**.</span><span class="sxs-lookup"><span data-stu-id="27153-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="27153-162">Copie toda la dirección URL en un editor de texto para poder utilizarla posteriormente.</span><span class="sxs-lookup"><span data-stu-id="27153-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="27153-163">A continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="27153-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="27153-164">En Visual Studio, abra **Web.Release.config** en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="27153-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="27153-165">Introduzca el siguiente código XML en la etiqueta `<configuration>` y reemplace el valor de la clave por la dirección URL de la aplicación web de publicación.</span><span class="sxs-lookup"><span data-stu-id="27153-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="27153-166">Cuando haya terminado, tendrá dos identificadores de usuario de confianza configurados en el proyecto, uno para el entorno de depuración en Visual Studio y otro para el sitio web publicado en Azure.</span><span class="sxs-lookup"><span data-stu-id="27153-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="27153-167">Configurará una relación de confianza para usuario autenticado para cada uno de los dos entornos de AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="27153-168">Durante la depuración, la configuración de la aplicación en Web.config se usa para que su configuración de **Debug** funcione con AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="27153-169">Cuando se publique (de forma predeterminada, se publica la configuración de **Release** ), se carga un archivo Web.config transformado que incorpora los cambios de configuración de la aplicación en Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="27153-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="27153-170">Si desea asociar la aplicación web publicada en Azure al depurador (es decir, debe cargar los símbolos de depuración del código en el sitio web publicado), puede crear un clon de la configuración de depuración para la depuración de Azure, pero con su propia transformación de Web.config personalizada (por ejemplo, Web.AzureDebug.config) que usa la configuración de la aplicación de aplicación de Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="27153-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="27153-171">Esto le permite mantener una configuración estática en los distintos entornos.</span><span class="sxs-lookup"><span data-stu-id="27153-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="27153-172">Configurar las relaciones de confianza para usuarios autenticados en la administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="27153-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="27153-173">Ahora debe configurar una relación de confianza para usuario autenticado en Administración de AD FS para poder usar su aplicación de muestra y que se pueda autenticar realmente con AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="27153-174">Deberá configurar dos relaciones de confianza para usuarios autenticados independientes, una para su entorno de depuración y otra para su aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="27153-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="27153-175">Asegúrese de repetir los pasos siguientes para ambos entornos.</span><span class="sxs-lookup"><span data-stu-id="27153-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="27153-176">En su servidor de AD FS, inicie sesión con credenciales que tengan derechos de administración para AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="27153-177">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-177">Open AD FS Management.</span></span> <span data-ttu-id="27153-178">Haga clic con el botón derecho en **AD FS\Trusted Relationships\Relying Party Trusts** y seleccione **Agregar relación de confianza para usuario de confianza**.</span><span class="sxs-lookup"><span data-stu-id="27153-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="27153-179">En la página **Seleccionar origen de datos**, seleccione **Especificar datos acerca del usuario de confianza manualmente**.</span><span class="sxs-lookup"><span data-stu-id="27153-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="27153-180">En la página **Especificar nombre para mostrar**, escriba un nombre para mostrar para la aplicación y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="27153-181">En la página **Elegir protocolo**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="27153-182">En la página **Configurar certificado**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27153-183">Puesto que ya debería estar usando HTTPS, los tokens cifrados son opcionales.</span><span class="sxs-lookup"><span data-stu-id="27153-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="27153-184">Si desea realmente cifrar tokens desde AD FS en este página, debe agregar también lógica de descifrado de tokens en su código.</span><span class="sxs-lookup"><span data-stu-id="27153-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="27153-185">Para obtener más información, consulte [Configurar manualmente middleware de WS-Federation de OWIN y aceptar tokens cifrados](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="27153-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="27153-186">Antes de pasar al siguiente paso, necesita algo de información de su proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27153-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="27153-187">En las propiedades del proyecto, observe la **Dirección URL de SSL** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="27153-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="27153-188">De nuevo en la administración de AD FS, en la página **Configurar dirección URL** del **Asistente para agregar relación de confianza para usuario de confianza**, seleccione **Habilitar la compatibilidad para el protocolo WS-Federation Passive** y escriba la dirección URL de SSL del proyecto de Visual Studio que anotó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="27153-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="27153-189">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="27153-190">La dirección URL especifica dónde enviar al cliente después de que la autenticación se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="27153-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="27153-191">Para el entorno de depuración, debe ser <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="27153-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="27153-192">En el caso de la aplicación web publicada, debe ser la dirección URL de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="27153-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="27153-193">En la página **Configurar identificadores**, compruebe que la dirección URL de SSL del proyecto ya aparece en la lista y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="27153-194">Haga clic en **Siguiente** hasta el final del asistente con las selecciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="27153-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27153-195">En App_Start\Startup.Auth.cs de su proyecto de Visual Studio, este identificador se compara con el valor de <code>WsFederationAuthenticationOptions.Wtrealm</code> durante la autenticación federada.</span><span class="sxs-lookup"><span data-stu-id="27153-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="27153-196">De forma predeterminada, se agrega la dirección URL de la aplicación del paso anterior como un identificador de usuario de confianza.</span><span class="sxs-lookup"><span data-stu-id="27153-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="27153-197">Ahora ha terminado de configurar la aplicación de usuario de confianza para su proyecto en AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="27153-198">A continuación, configura esta aplicación para enviar las notificaciones necesarias para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="27153-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="27153-199">El cuadro de diálogo **Editar reglas de notificación** se abre de forma predeterminada al final del Asistente para que pueda empezar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="27153-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="27153-200">Vamos a configurar al menos las siguientes notificaciones (con esquemas entre paréntesis):</span><span class="sxs-lookup"><span data-stu-id="27153-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="27153-201">Nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name): usado por ASP.NET para hacer uso de `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="27153-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="27153-202">Nombre principal de usuario (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn): se usa para identificar de manera única a los usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="27153-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="27153-203">Pertenencias a grupos como roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role): se pueden usar con la representación `[Authorize(Roles="role1, role2,...")]` para autorizar a los controladores/acciones.</span><span class="sxs-lookup"><span data-stu-id="27153-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="27153-204">En realidad, puede que este no sea el enfoque de mayor rendimiento para la autorización de roles.</span><span class="sxs-lookup"><span data-stu-id="27153-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="27153-205">Si sus usuarios de AD pertenecen a cientos de grupos de seguridad, se convierten en cientos de notificaciones de rol en el token de SAML.</span><span class="sxs-lookup"><span data-stu-id="27153-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="27153-206">Un método alternativo consiste en enviar una notificación de rol única condicionalmente en función de la pertenencia del usuario a un grupo concreto.</span><span class="sxs-lookup"><span data-stu-id="27153-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="27153-207">Sin embargo, lo mantendremos sencillo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="27153-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="27153-208">Identificador de nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier): se puede usar para la validación de antifalsificación.</span><span class="sxs-lookup"><span data-stu-id="27153-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="27153-209">Para más información sobre cómo hacer que funcione con validación de antifalsificación, consulte la sección **Agregar funcionalidad de línea de negocio a la aplicación de ejemplo** de [Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="27153-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="27153-210">Los tipos de notificación que necesita configurar para su aplicación dependen de las necesidades de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="27153-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="27153-211">Para ver la lista de notificaciones admitidas por las aplicaciones de Azure Active Directory (es decir, relaciones de confianza para usuarios autenticados), por ejemplo, consulte [Tipos de notificaciones y tokens admitidos](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="27153-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="27153-212">En el cuadro de diálogo Editar reglas de notificación, haga clic en **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="27153-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="27153-213">Configure las notificaciones de nombre, UPN y rol, como se muestra en la captura de pantalla, y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="27153-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="27153-214">A continuación, crea una notificación de identificador de nombre transitorio mediante los pasos que se muestran en [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)(Identificadores de nombres en aserciones de SAML).</span><span class="sxs-lookup"><span data-stu-id="27153-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="27153-215">Haga clic en **Agregar regla** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="27153-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="27153-216">Seleccione **Enviar notificaciones con una regla personalizada** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="27153-217">Pegue el siguiente lenguaje de regla en el cuadro **Regla personalizada**, asigne el nombre **Por identificador de sesión** a la regla y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="27153-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="27153-218">Su regla personalizada debe tener un aspecto similar a esta captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="27153-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="27153-219">Haga clic en **Agregar regla** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="27153-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="27153-220">Seleccione **Transformar una notificación entrante** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27153-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="27153-221">Configure la regla como se muestra en la captura de pantalla (con el tipo de notificación que creó en la regla personalizada) y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="27153-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="27153-222">Para información más detallada sobre los pasos de la notificación de identificador de nombre transitorio, consulte [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)(Identificadores de nombres en aserciones de SAML).</span><span class="sxs-lookup"><span data-stu-id="27153-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="27153-223">Haga clic en **Aplicar** en el cuadro de diálogo **Editar reglas de notificación**.</span><span class="sxs-lookup"><span data-stu-id="27153-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="27153-224">Ahora debería tener un aspecto similar al de la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="27153-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="27153-225">Nuevamente, asegúrese de repetir estos pasos tanto para el entorno de depuración como para la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="27153-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="27153-226">Probar la autenticación federada para la aplicación</span><span class="sxs-lookup"><span data-stu-id="27153-226">Test federated authentication for your application</span></span>
<span data-ttu-id="27153-227">Está preparado para probar la lógica de autenticación de la aplicación con AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="27153-228">En mi entorno de laboratorio de AD FS, tengo un usuario de prueba que pertenece a un grupo de prueba en Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="27153-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="27153-229">Para probar la autenticación en el depurador, todo lo que tiene que hacer ahora es escribir `F5`.</span><span class="sxs-lookup"><span data-stu-id="27153-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="27153-230">Si desea probar la autenticación de prueba en la aplicación web publicada, navegue hasta la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="27153-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="27153-231">Cuando se cargue la aplicación web, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="27153-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="27153-232">Ahora debería obtener un cuadro de diálogo de inicio de sesión o la página de inicio de sesión atendida por AD FS, en función del método de autenticación seleccionado por AD FS.</span><span class="sxs-lookup"><span data-stu-id="27153-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="27153-233">Esto es lo que aparece en Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="27153-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="27153-234">Cuando inicie sesión con un usuario en el dominio de AD de la implementación de AD FS, debería ver la página principal de nuevo con **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="27153-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="27153-235">en la esquina.</span><span class="sxs-lookup"><span data-stu-id="27153-235">in the corner.</span></span> <span data-ttu-id="27153-236">Esto es lo que vemos.</span><span class="sxs-lookup"><span data-stu-id="27153-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="27153-237">Hasta ahora, ha llevado a cabo correctamente lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="27153-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="27153-238">La aplicación ha alcanzado AD FS correctamente y hay un identificador de usuario de confianza coincidente en la base de datos de AD FS</span><span class="sxs-lookup"><span data-stu-id="27153-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="27153-239">AD FS ha autenticado correctamente un usuario de AD y le redirige de nuevo a la página principal de la aplicación</span><span class="sxs-lookup"><span data-stu-id="27153-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="27153-240">AD FS envió correctamente la notificación del nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) a la aplicación, como se indica por el hecho de que el nombre de usuario aparece en la esquina.</span><span class="sxs-lookup"><span data-stu-id="27153-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="27153-241">Si falta la notificación de nombre, habría visto **Hello, !**.</span><span class="sxs-lookup"><span data-stu-id="27153-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="27153-242">Si echa un vistazo a Views\Shared\_LoginPartial.cshtml, ve que usa `User.Identity.Name` para mostrar el nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="27153-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="27153-243">Como se mencionó anteriormente, si la notificación del nombre del usuario autenticado está disponible en el token de SAML, ASP.NET hidrata esta propiedad con ella.</span><span class="sxs-lookup"><span data-stu-id="27153-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="27153-244">Para ver todas las notificaciones que se envían por AD FS, coloque un punto de interrupción en Controllers\HomeController.cs, en el método de acción de índice.</span><span class="sxs-lookup"><span data-stu-id="27153-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="27153-245">Cuando se autentique el usuario, inspeccione la colección `System.Security.Claims.Current.Claims` .</span><span class="sxs-lookup"><span data-stu-id="27153-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="27153-246">Autorizar a los usuarios para acciones o controladores concretos</span><span class="sxs-lookup"><span data-stu-id="27153-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="27153-247">Puesto que ha incluido las pertenencias a grupos como notificaciones de rol en la configuración de relación de confianza para usuario autenticado, ahora puede usarlas directamente en la representación `[Authorize(Roles="...")]` para controladores y acciones.</span><span class="sxs-lookup"><span data-stu-id="27153-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="27153-248">En una aplicación de línea de negocio con el patrón Create-Read-Update-Delete (CRUD), puede autorizar a roles específicos para acceder a cada acción.</span><span class="sxs-lookup"><span data-stu-id="27153-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="27153-249">Por ahora, solo probará esta característica en el controlador principal existente.</span><span class="sxs-lookup"><span data-stu-id="27153-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="27153-250">Abra Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="27153-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="27153-251">Represente los métodos de acción `About` y `Contact` similares al código siguiente, con las pertenencias a grupos de seguridad que su usuario autenticado tiene.</span><span class="sxs-lookup"><span data-stu-id="27153-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="27153-252">Puesto que agregué **Usuario de prueba** a **Grupo de prueba** en mi entorno de laboratorio de AD FS, usaré el grupo de prueba para probar la autorización en `About`.</span><span class="sxs-lookup"><span data-stu-id="27153-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="27153-253">Para `Contact`, probaré el caso negativo de **Admins. del dominio**, al que no pertenece el **Usuario de prueba**.</span><span class="sxs-lookup"><span data-stu-id="27153-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="27153-254">Para iniciar el depurador, escriba `F5` e inicie sesión y, a continuación, haga clic en **Acerca de**.</span><span class="sxs-lookup"><span data-stu-id="27153-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="27153-255">Ahora debería ver la página `~/About/Index` correctamente, si el usuario autenticado tiene autorización para esa acción.</span><span class="sxs-lookup"><span data-stu-id="27153-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="27153-256">Ahora haga clic en **Contacto**, lo que en mi caso no debería autorizar a **Usuario de prueba** para la acción.</span><span class="sxs-lookup"><span data-stu-id="27153-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="27153-257">Sin embargo, el explorador se redirige a AD FS, que finalmente muestra este mensaje:</span><span class="sxs-lookup"><span data-stu-id="27153-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="27153-258">Si investiga este error en el Visor de eventos del servidor de AD FS, verá este mensaje de excepción:</span><span class="sxs-lookup"><span data-stu-id="27153-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="27153-259">El motivo de este error es que, de forma predeterminada, MVC devuelve un mensaje 401 No autorizado cuando los roles de un usuario no están autorizados.</span><span class="sxs-lookup"><span data-stu-id="27153-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="27153-260">Esto desencadena una solicitud de reautenticación para su proveedor de identidades (AD FS).</span><span class="sxs-lookup"><span data-stu-id="27153-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="27153-261">Puesto que el usuario ya está autenticado, AD FS vuelve a la misma página, que a continuación emite otro mensaje 401, creando un bucle de redirección.</span><span class="sxs-lookup"><span data-stu-id="27153-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="27153-262">Ahora reemplazará el método `HandleUnauthorizedRequest` de AuthorizeAttribute con una lógica sencilla para mostrar algo que tenga sentido, en lugar de continuar el bucle de redirección.</span><span class="sxs-lookup"><span data-stu-id="27153-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="27153-263">Cree un archivo en el proyecto llamado AuthorizeAttribute.cs y pegue el código siguiente en él.</span><span class="sxs-lookup"><span data-stu-id="27153-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="27153-264">El código de reemplazo envía un mensaje HTTP 403 (Prohibido) en lugar de HTTP 401 (No autorizado) en los casos autenticados pero no autorizados.</span><span class="sxs-lookup"><span data-stu-id="27153-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="27153-265">Ejecute nuevamente el depurador con `F5`.</span><span class="sxs-lookup"><span data-stu-id="27153-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="27153-266">Si se hace clic en **Contacto** aparece ahora un mensaje de error más informativo (aunque poco atractivo):</span><span class="sxs-lookup"><span data-stu-id="27153-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="27153-267">Publique nuevamente la aplicación en Aplicaciones web del Servicio de aplicaciones de Azure y pruebe el comportamiento de la aplicación activa.</span><span class="sxs-lookup"><span data-stu-id="27153-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="27153-268">Conectarse a datos locales</span><span class="sxs-lookup"><span data-stu-id="27153-268">Connect to on-premises data</span></span>
<span data-ttu-id="27153-269">Un motivo por el que desearía implementar su aplicación de línea de negocio con AD FS en lugar de Azure Active Directory son los problemas de cumplimiento a la hora de mantener los datos de la organización remotos.</span><span class="sxs-lookup"><span data-stu-id="27153-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="27153-270">Esto también puede significar que su aplicación web de Azure deba acceder a bases de datos locales, ya que no se le permite usar [Base de datos SQL](/services/sql-database/) como la capa de datos para sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="27153-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="27153-271">Azure App Service Web Apps admite el acceso a bases de datos locales con dos enfoques: [Conexiones híbridas](../biztalk-services/integration-hybrid-connection-overview.md) y [Redes virtuales](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="27153-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="27153-272">Para obtener más información, consulte [Uso de integración VNET y conexiones híbridas con Aplicaciones web del Servicio de aplicaciones de Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="27153-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="27153-273">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="27153-273">Further resources</span></span>
* [<span data-ttu-id="27153-274">Autenticación con Active Directory local en aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="27153-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="27153-275">Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27153-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="27153-276">Usar la opción de autenticación de organización profesional local (ADFS) con ASP.NET en Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="27153-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="27153-277">Migrar un proyecto web de VS2013 de WIF a Katana</span><span class="sxs-lookup"><span data-stu-id="27153-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="27153-278">Información general de Servicios de federación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="27153-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="27153-279">Especificación de WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="27153-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

