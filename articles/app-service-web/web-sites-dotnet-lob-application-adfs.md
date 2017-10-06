---
title: "una aplicación de Azure de línea de negocio con autenticación de AD FS aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo una aplicación de línea de negocio en el servicio de aplicaciones de Azure que se autentica con toocreate local a STS. Este tutorial dirige a AD FS como Hola a STS local."
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
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="6ae68-104">Creación de una aplicación de Azure de línea de negocio con autenticación de AD FS</span><span class="sxs-lookup"><span data-stu-id="6ae68-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="6ae68-105">Este artículo muestra cómo toocreate un ASP.NET MVC de línea de negocio de aplicación en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) mediante una implementación local [los servicios de federación de Active Directory](http://technet.microsoft.com/library/hh831502.aspx) como proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="6ae68-106">Este escenario puede trabajar cuando desea que las aplicaciones de línea de negocio de toocreate en el servicio de aplicación de Azure, pero su organización requiere toobe de datos de directorio almacenado en el sitio.</span><span class="sxs-lookup"><span data-stu-id="6ae68-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="6ae68-107">Para obtener información general de opciones de autenticación y autorización de empresa diferente de hello para el servicio de aplicaciones de Azure, consulte [autenticar con local de Active Directory en la aplicación de Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="6ae68-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="6ae68-108">Lo que va a crear</span><span class="sxs-lookup"><span data-stu-id="6ae68-108">What you will build</span></span>
<span data-ttu-id="6ae68-109">Va a compilar una aplicación ASP.NET básica en aplicaciones de Web del servicio de aplicación de Azure con hello siguientes características:</span><span class="sxs-lookup"><span data-stu-id="6ae68-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="6ae68-110">Autentica a los usuarios con AD FS</span><span class="sxs-lookup"><span data-stu-id="6ae68-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="6ae68-111">Usa `[Authorize]` tooauthorize a los usuarios para distintas acciones</span><span class="sxs-lookup"><span data-stu-id="6ae68-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="6ae68-112">Configuración estática para depurar en Visual Studio y para publicar aplicaciones Web del servicio tooApp (configurar una sola vez, depurar y publicar en cualquier momento)</span><span class="sxs-lookup"><span data-stu-id="6ae68-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="6ae68-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="6ae68-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="6ae68-114">Necesita Hola siguientes toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="6ae68-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="6ae68-115">Una implementación local implementación de AD FS (para ver un tutorial to-end Hola del laboratorio de pruebas utilizado en este tutorial, vea [laboratorio de pruebas: STS independiente con AD FS en máquinas virtuales de Azure (para solo prueba)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="6ae68-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="6ae68-116">Usuario de confianza de permisos toocreate confía en administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="6ae68-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="6ae68-117">Visual Studio 2013, actualización 4 o posterior</span><span class="sxs-lookup"><span data-stu-id="6ae68-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="6ae68-118">[SDK de Azure 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o posterior.</span><span class="sxs-lookup"><span data-stu-id="6ae68-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="6ae68-119">Usar la aplicación de ejemplo para la plantilla de línea de negocio</span><span class="sxs-lookup"><span data-stu-id="6ae68-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="6ae68-120">Hola la aplicación de ejemplo en este tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), creado por el equipo de Azure Active Directory Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="6ae68-121">Dado que AD FS admite WS-Federation, puede usar como una aplicación de línea de negocio de plantilla toocreate con facilidad.</span><span class="sxs-lookup"><span data-stu-id="6ae68-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="6ae68-122">Tiene Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="6ae68-122">It has hello following features:</span></span>

* <span data-ttu-id="6ae68-123">Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate con una implementación local implementación de AD FS</span><span class="sxs-lookup"><span data-stu-id="6ae68-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="6ae68-124">Funcionalidad de inicio y de cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="6ae68-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="6ae68-125">Usa [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (en lugar de Windows Identity Foundation), que es Hola futuras de ASP.NET y mucho más fácil tooset hacia arriba para autenticación y autorización que WIF</span><span class="sxs-lookup"><span data-stu-id="6ae68-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="6ae68-126">Configurar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="6ae68-126">Set up hello sample application</span></span>
1. <span data-ttu-id="6ae68-127">Clonar o descargar la solución de ejemplo de Hola en [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour de directorio local.</span><span class="sxs-lookup"><span data-stu-id="6ae68-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6ae68-128">Hola instrucciones de [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) mostrarle cómo tooset una aplicación hello con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6ae68-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="6ae68-129">Pero en este tutorial, se configura con AD FS, siga estos pasos de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="6ae68-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="6ae68-130">Abrir solución hello y, a continuación, abra Controllers\AccountController.cs en hello **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="6ae68-131">Verá que el código de hello simplemente emite un usuario de hello tooauthenticate de desafío de autenticación mediante WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="6ae68-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="6ae68-132">Toda la autenticación se configura en App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="6ae68-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="6ae68-133">Abra App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="6ae68-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="6ae68-134">Hola  `ConfigureAuth` /método siguiente, tenga en cuenta Hola línea:</span><span class="sxs-lookup"><span data-stu-id="6ae68-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="6ae68-135">Este fragmento de código de Hola a todos OWIN, es en realidad Hola reconstrucción que mínimo necesita autenticación de WS-Federation tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6ae68-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="6ae68-136">Es mucho más sencillo y más elegante de WIF, donde se inyecta Web.config con XML todo lugar Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="6ae68-137">Hola solo información que necesita es Hola del usuario de confianza (RP) hello y el identificador de dirección URL del archivo de metadatos de su servicio de AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="6ae68-138">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6ae68-138">Here's an example:</span></span>
   
   * <span data-ttu-id="6ae68-139">Identificador del usuario de confianza: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="6ae68-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="6ae68-140">Dirección de metadatos: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="6ae68-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="6ae68-141">En App_Start\Startup.Auth.cs, cambie Hola siguiendo las definiciones de cadena estática:</span><span class="sxs-lookup"><span data-stu-id="6ae68-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="6ae68-142">Ahora, realizar los cambios correspondientes de hello en el archivo Web.config. Abra Web.config hello y modificar Hola después de la configuración de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="6ae68-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="6ae68-143">Rellene los valores de clave de hello en función del entorno respectivo.</span><span class="sxs-lookup"><span data-stu-id="6ae68-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="6ae68-144">Hola toomake de aplicación que no hay ningún error de compilación.</span><span class="sxs-lookup"><span data-stu-id="6ae68-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="6ae68-145">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="6ae68-145">That's it.</span></span> <span data-ttu-id="6ae68-146">Ahora la aplicación de ejemplo de Hola es toowork listo con AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="6ae68-147">Todavía necesita tooconfigure una confianza RP con esta aplicación en AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="6ae68-148">Implementar tooAzure de aplicación de ejemplo de Hola aplicación del servicio de aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="6ae68-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="6ae68-149">En este caso, publicar Hola aplicación tooa web app en aplicaciones Web de servicio de aplicación mientras conserva el entorno de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="6ae68-150">Tenga en cuenta que se vayan aplicación hello de toopublish antes de tener una confianza RP con AD FS, por lo que la autenticación sigue sin funciona aún.</span><span class="sxs-lookup"><span data-stu-id="6ae68-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="6ae68-151">Sin embargo, si lo hace, ahora puede tener Hola URL de aplicación web que puede usar confianza RP de hello tooconfigure más tarde.</span><span class="sxs-lookup"><span data-stu-id="6ae68-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="6ae68-152">Haga clic con el botón derecho en el proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="6ae68-153">Seleccione **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="6ae68-154">Si no está registrado en tooAzure, haga clic en **inicio de sesión** y utilizar cuenta de Microsoft de Hola para su toosign de suscripción de Azure en.</span><span class="sxs-lookup"><span data-stu-id="6ae68-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="6ae68-155">Una vez iniciado sesión, haga clic en **New** toocreate una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6ae68-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="6ae68-156">Rellene todos los campos obligatorios.</span><span class="sxs-lookup"><span data-stu-id="6ae68-156">Fill in all required fields.</span></span> <span data-ttu-id="6ae68-157">Va datos tooon local de tooconnect más adelante, por lo que no cree una base de datos de esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6ae68-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="6ae68-158">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-158">Click **Create**.</span></span> <span data-ttu-id="6ae68-159">Una vez creada la aplicación web de hello, se abre el cuadro de diálogo de publicación Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="6ae68-160">En **dirección URL de destino**, cambiar **http** demasiado**https**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="6ae68-161">Copie Hola todo URL tooa editor de texto para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="6ae68-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="6ae68-162">A continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="6ae68-163">En Visual Studio, abra **Web.Release.config** en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6ae68-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="6ae68-164">Insertar Hola continuación de XML en hello `<configuration>` etiqueta y reemplace el valor de clave de Hola con la dirección URL de la aplicación web publicar.</span><span class="sxs-lookup"><span data-stu-id="6ae68-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="6ae68-165">Cuando haya terminado, tendrá dos identificadores RP configurados en su proyecto, uno para el entorno de depuración en Visual Studio, y uno para hello publica la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="6ae68-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="6ae68-166">Configurará una confianza RP para cada uno de los dos entornos de hello en AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="6ae68-167">Durante la depuración, configuración de aplicaciones de hello en el archivo Web.config está toomake usa su **depurar** trabajo de configuración con AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="6ae68-168">Cuando se publica (de forma predeterminada, Hola **versión** se publica la configuración), se carga un archivo Web.config transformado que incorpora cambios de configuración de aplicación hello en Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="6ae68-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="6ae68-169">Si desea tooattach hello web publicado aplicación en Azure toohello depurador (es decir, debe cargar símbolos de depuración del código de aplicación web publicada de hello), puede crear un clon del programa Hola a depurar la configuración de depuración de Azure, pero con su propio archivo Web.config personalizado transformar) Por ejemplo, Web.AzureDebug.config) que usa la configuración de la aplicación hello desde Web.Release.config. Esto le permite toomaintain una configuración estática entre diferentes entornos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="6ae68-170">Configurar las relaciones de confianza para usuarios autenticados en la administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="6ae68-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="6ae68-171">Ahora debe tooconfigure una confianza RP en administración de AD FS para poder usar la aplicación de ejemplo y autenticarse con AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="6ae68-172">Necesitará tooset dos relaciones de confianza de RP independientes, uno para el entorno de depuración y otro para la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="6ae68-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="6ae68-173">Asegúrese de que repita Hola siguiendo los pasos para ambos de sus entornos.</span><span class="sxs-lookup"><span data-stu-id="6ae68-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="6ae68-174">En el servidor de AD FS, inicie sesión con las credenciales que tienen derechos de administración tooAD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="6ae68-175">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-175">Open AD FS Management.</span></span> <span data-ttu-id="6ae68-176">Haga clic con el botón derecho en **AD FS\Trusted Relationships\Relying Party Trusts** y seleccione **Agregar relación de confianza para usuario de confianza**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="6ae68-177">Hola **Seleccionar origen de datos** , seleccione **escribir manualmente los datos sobre el usuario de confianza de hello**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="6ae68-178">Hola **especificar nombre para mostrar** página, escriba un nombre para mostrar para la aplicación hello y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="6ae68-179">Hola **elegir protocolo** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="6ae68-180">Hola **configurar certificado** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6ae68-181">Puesto que ya debería estar usando HTTPS, los tokens cifrados son opcionales.</span><span class="sxs-lookup"><span data-stu-id="6ae68-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="6ae68-182">Si realmente desea tooencrypt tokens de AD FS en esta página, también debe agregar lógica de descifrado de token en el código.</span><span class="sxs-lookup"><span data-stu-id="6ae68-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="6ae68-183">Para obtener más información, consulte [Configurar manualmente middleware de WS-Federation de OWIN y aceptar tokens cifrados](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ae68-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="6ae68-184">Antes de pasar al paso siguiente de hello, necesita una parte de la información de su proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ae68-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="6ae68-185">En Propiedades del proyecto hello, tenga en cuenta hello **dirección URL de SSL** de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6ae68-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="6ae68-186">En administración de AD FS, en hello **configurar dirección URL** página de hello **entidad confiar en Asistente para agregar**, seleccione **habilitar la compatibilidad de protocolo WS-Federation Passive hello** y Escriba Hola dirección URL de SSL de su proyecto de Visual Studio que anotó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="6ae68-187">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="6ae68-188">Dirección URL especifica donde el cliente de hello toosend tras la autenticación se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="6ae68-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="6ae68-189">Para el entorno de depuración de hello, debe ser <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="6ae68-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="6ae68-190">Para la aplicación web publicada de hello, debe ser URL de la aplicación hello web.</span><span class="sxs-lookup"><span data-stu-id="6ae68-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="6ae68-191">Hola **configurar identificadores** página, compruebe que la dirección URL de SSL de proyecto ya aparece y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="6ae68-192">Haga clic en **siguiente** todos Hola final de manera toohello del Asistente para hello con selecciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="6ae68-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6ae68-193">En App_Start\Startup.Auth.cs de su proyecto de Visual Studio, este identificador se compara con valor de Hola de <code>WsFederationAuthenticationOptions.Wtrealm</code> durante la autenticación federada.</span><span class="sxs-lookup"><span data-stu-id="6ae68-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="6ae68-194">De forma predeterminada, la dirección URL de la aplicación hello del paso anterior Hola se agrega como un identificador RP.</span><span class="sxs-lookup"><span data-stu-id="6ae68-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="6ae68-195">Ahora haya terminado de configurar Hola aplicación RP para el proyecto en AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="6ae68-196">A continuación, configure este toosend aplicación Hola notificaciones necesarios para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ae68-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="6ae68-197">Hola **editar reglas de notificación** cuadro de diálogo se abre de forma predeterminada para al final de hello del Asistente de Hola para que pueda empezar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="6ae68-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="6ae68-198">Vamos a configurar al menos Hola siguientes notificaciones (con esquemas entre paréntesis):</span><span class="sxs-lookup"><span data-stu-id="6ae68-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="6ae68-199">Nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - utilizado por ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="6ae68-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="6ae68-200">Usuario nombre de entidad de seguridad (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - usado toouniquely identificar a los usuarios en la organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="6ae68-201">Pertenencia a grupos como roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - puede utilizarse con `[Authorize(Roles="role1, role2,...")]` decoración tooauthorize controladores o acciones.</span><span class="sxs-lookup"><span data-stu-id="6ae68-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="6ae68-202">En realidad, este enfoque puede no ser Hola que ofrece mayor rendimiento para la autorización de rol.</span><span class="sxs-lookup"><span data-stu-id="6ae68-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="6ae68-203">Si los usuarios de AD pertenecen toohundreds de grupos de seguridad, se convierten en cientos de notificaciones de rol en el token SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="6ae68-204">Un enfoque alternativo es toosend una única función de notificación condicionalmente según la pertenencia del usuario de hello en un grupo determinado.</span><span class="sxs-lookup"><span data-stu-id="6ae68-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="6ae68-205">Sin embargo, lo mantendremos sencillo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6ae68-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="6ae68-206">Identificador de nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier): se puede usar para la validación de antifalsificación.</span><span class="sxs-lookup"><span data-stu-id="6ae68-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="6ae68-207">Para obtener más información sobre cómo toomake funciona con validación antifalsificación, vea hello **agregar funcionalidad de línea de negocio** sección de [crear una aplicación de Azure de línea de negocio con la autenticación de Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="6ae68-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="6ae68-208">Hello notificación tipos que se necesita tooconfigure la aplicación se determina mediante las necesidades de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ae68-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="6ae68-209">Lista de Hola de notificaciones admitidos por las aplicaciones de Azure Active Directory (es decir, las confianzas RP), por ejemplo, vea [admite tokens y los tipos de notificación](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ae68-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="6ae68-210">En el cuadro de diálogo de hello editar reglas de notificación, haga clic en **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="6ae68-211">Configurar notificaciones de rol, UPN y nombre de hello tal y como se muestra en la captura de pantalla de Hola y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="6ae68-212">A continuación, cree un nombre temporal Id. de notificación mediante Hola pasos mostrados en [identificadores de nombre en las aserciones de SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ae68-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="6ae68-213">Haga clic en **Agregar regla** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6ae68-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="6ae68-214">Seleccione **Enviar notificaciones con una regla personalizada** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="6ae68-215">Siguiente de hello pegar regla lenguaje en hello **regla personalizada** cuadro, nombre de regla de hello **por el identificador de sesión** y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="6ae68-216">Su regla personalizada debe tener un aspecto similar a esta captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="6ae68-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="6ae68-217">Haga clic en **Agregar regla** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6ae68-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="6ae68-218">Seleccione **Transformar una notificación entrante** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="6ae68-219">Configurar regla de hello tal y como se muestra en la captura de pantalla de hello (mediante el tipo de notificación de Hola que creó en la regla personalizada hello) y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="6ae68-220">Para obtener información detallada sobre los pasos de Hola para notificación de Id. de nombre transitorio hello, consulte [identificadores de nombre en las aserciones de SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ae68-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="6ae68-221">Haga clic en **aplicar** en hello **editar reglas de notificación** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ae68-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="6ae68-222">Ahora debería ser similar Hola siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="6ae68-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="6ae68-223">Nuevamente, asegúrese de repetir estos pasos tanto para el entorno de depuración como para la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="6ae68-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="6ae68-224">Probar la autenticación federada para la aplicación</span><span class="sxs-lookup"><span data-stu-id="6ae68-224">Test federated authentication for your application</span></span>
<span data-ttu-id="6ae68-225">Se está tootest listo lógica de autenticación de la aplicación en AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="6ae68-226">En el entorno de laboratorio de AD FS, tengo un usuario de prueba que pertenece el grupo de prueba de tooa en Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="6ae68-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="6ae68-227">autenticación de tootest en el depurador hello, todo lo que necesita toodo ahora es de tipo `F5`.</span><span class="sxs-lookup"><span data-stu-id="6ae68-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="6ae68-228">Si desea que la autenticación tootest en aplicación web publicada de hello, Explorar dirección URL de toohello.</span><span class="sxs-lookup"><span data-stu-id="6ae68-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="6ae68-229">Una vez cargada la aplicación web de hello, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="6ae68-230">Ahora deberá obtener cualquier un inicio de sesión Hola o cuadro de diálogo Inicio de sesión página atendida por AD FS, según el método de autenticación de hello elegido por AD FS.</span><span class="sxs-lookup"><span data-stu-id="6ae68-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="6ae68-231">Esto es lo que aparece en Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="6ae68-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="6ae68-232">Una vez que inicie sesión con un usuario de dominio de AD de Hola de implementación de hello AD FS, ahora debería ver la página principal de hello nuevo con **Hola, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="6ae68-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="6ae68-233">en la esquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-233">in hello corner.</span></span> <span data-ttu-id="6ae68-234">Esto es lo que vemos.</span><span class="sxs-lookup"><span data-stu-id="6ae68-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="6ae68-235">Hasta ahora, ha logrado Hola siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="6ae68-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="6ae68-236">La aplicación ha alcanzado correctamente AD FS y un identificador RP coincidente se encuentra en hello base de datos de AD FS</span><span class="sxs-lookup"><span data-stu-id="6ae68-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="6ae68-237">AD FS haya autenticado correctamente una redirección de realizar la copia de la página de inicio de la aplicación toohello y usuarios de AD</span><span class="sxs-lookup"><span data-stu-id="6ae68-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="6ae68-238">AD FS como nombre de hello enviado correctamente de notificación (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour aplicación, como se indica por el hecho de hello ese usuario Hola nombre se muestra en la esquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="6ae68-239">Si falta la notificación de nombre de hello, habría visto **Hola!**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="6ae68-240">Si observa Views\Shared\_LoginPartial.cshtml, encontrará que usa `User.Identity.Name` nombre de usuario de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="6ae68-241">Como se mencionó anteriormente, si nombre Hola de notificación de hello autenticado de usuario está disponible en el token SAML de hello, ASP.NET hydrates esta propiedad con él.</span><span class="sxs-lookup"><span data-stu-id="6ae68-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="6ae68-242">toosee que Hola a todos de notificaciones que se envían por AD FS, coloque un punto de interrupción en controllers\homecontroller. cs, Hola método de acción de índice.</span><span class="sxs-lookup"><span data-stu-id="6ae68-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="6ae68-243">Una vez autenticado el usuario hello, inspeccionar hello `System.Security.Claims.Current.Claims` colección.</span><span class="sxs-lookup"><span data-stu-id="6ae68-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="6ae68-244">Autorizar a los usuarios para acciones o controladores concretos</span><span class="sxs-lookup"><span data-stu-id="6ae68-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="6ae68-245">Puesto que ha incluido las pertenencias a grupos como notificaciones de rol en la configuración de confianza RP, ahora puede usar ellos directamente en hello `[Authorize(Roles="...")]` decoración para controladores y acciones.</span><span class="sxs-lookup"><span data-stu-id="6ae68-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="6ae68-246">En una aplicación de línea de negocio con patrón de hello crear-lectura-actualización y eliminación (CRUD), puede autorizar a roles específicos tooaccess cada acción.</span><span class="sxs-lookup"><span data-stu-id="6ae68-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="6ae68-247">Por ahora, simplemente intentará el uso de esta característica en el controlador principal existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="6ae68-248">Abra Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="6ae68-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="6ae68-249">Decorar hello `About` y `Contact` toohello similar de acción métodos siguiente código, el uso de miembros de grupos de seguridad que el usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="6ae68-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="6ae68-250">Puesto que se ha agregado **usuario de prueba** demasiado**grupo de prueba** en mi entorno de laboratorio de AD FS, podrá usar autorización de grupo de prueba tootest en `About`.</span><span class="sxs-lookup"><span data-stu-id="6ae68-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="6ae68-251">Para `Contact`, probará caso negativo de Hola de **Admins. del dominio**, toowhich **usuario probar** no pertenece.</span><span class="sxs-lookup"><span data-stu-id="6ae68-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="6ae68-252">Iniciar el depurador de hello escribiendo `F5` e iniciar sesión, a continuación, haga clic en **sobre**.</span><span class="sxs-lookup"><span data-stu-id="6ae68-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="6ae68-253">Se debería ver ahora hello `~/About/Index` página correctamente, si el usuario autenticado tiene autorización para esa acción.</span><span class="sxs-lookup"><span data-stu-id="6ae68-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="6ae68-254">Ahora haga clic en **póngase en contacto con**, que en mi caso debe autorizar no **usuario de prueba** para la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ae68-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="6ae68-255">Sin embargo, Explorador de hello es redirigido tooAD FS, que finalmente se muestra este mensaje:</span><span class="sxs-lookup"><span data-stu-id="6ae68-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="6ae68-256">Si investigar este error en el Visor de eventos en el servidor de AD FS de hello, verá este mensaje de excepción:</span><span class="sxs-lookup"><span data-stu-id="6ae68-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="6ae68-257">motivo de Hola de este error es que de forma predeterminada, MVC devuelve un 401 no autorizado cuando roles de usuario no están autorizados.</span><span class="sxs-lookup"><span data-stu-id="6ae68-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="6ae68-258">Esto desencadena un proveedor de identidad de la reautenticación solicitud tooyour (AD FS).</span><span class="sxs-lookup"><span data-stu-id="6ae68-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="6ae68-259">Puesto que ya está autenticado el usuario Hola, AD FS devuelve toohello sintonía, que, a continuación, emite otra 401, crear un bucle de redirección.</span><span class="sxs-lookup"><span data-stu-id="6ae68-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="6ae68-260">Deberá reemplazar de AuthorizeAttribute `HandleUnauthorizedRequest` método con una lógica sencilla tooshow algo que tiene sentido en lugar de bucle de redirección de hello continuando.</span><span class="sxs-lookup"><span data-stu-id="6ae68-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="6ae68-261">Cree un archivo de proyecto de hello denominado AuthorizeAttribute.cs y Hola pegar siguiente código en él.</span><span class="sxs-lookup"><span data-stu-id="6ae68-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
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
   
    <span data-ttu-id="6ae68-262">Hola invalidar envía un HTTP 403 (prohibido) de código en lugar de HTTP 401 (no autorizado) en los casos autenticados pero no autorizados.</span><span class="sxs-lookup"><span data-stu-id="6ae68-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="6ae68-263">Ejecutar el depurador de hello nuevo con `F5`.</span><span class="sxs-lookup"><span data-stu-id="6ae68-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="6ae68-264">Si se hace clic en **Contacto** aparece ahora un mensaje de error más informativo (aunque poco atractivo):</span><span class="sxs-lookup"><span data-stu-id="6ae68-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="6ae68-265">Vuelva a publicar Hola aplicación tooAzure aplicación del servicio de aplicaciones Web y probar el comportamiento de Hola de aplicación de hello en vivo.</span><span class="sxs-lookup"><span data-stu-id="6ae68-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="6ae68-266">Conectar datos tooon locales</span><span class="sxs-lookup"><span data-stu-id="6ae68-266">Connect tooon-premises data</span></span>
<span data-ttu-id="6ae68-267">Un motivo que desearía tooimplement la aplicación de línea de negocio con AD FS en lugar de Azure Active Directory es problemas de compatibilidad con la actualización de la organización datos local y remota.</span><span class="sxs-lookup"><span data-stu-id="6ae68-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="6ae68-268">Esto también puede significar que la aplicación web en Azure debe tener acceso a las bases de datos local, ya que no se permiten toouse [base de datos SQL](/services/sql-database/) como capa de datos de Hola para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="6ae68-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="6ae68-269">Azure App Service Web Apps admite el acceso a bases de datos locales con dos enfoques: [Conexiones híbridas](../biztalk-services/integration-hybrid-connection-overview.md) y [Redes virtuales](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="6ae68-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="6ae68-270">Para obtener más información, consulte [Uso de integración VNET y conexiones híbridas con Aplicaciones web del Servicio de aplicaciones de Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="6ae68-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="6ae68-271">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6ae68-271">Further resources</span></span>
* [<span data-ttu-id="6ae68-272">Autenticación con Active Directory local en aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="6ae68-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="6ae68-273">Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ae68-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="6ae68-274">Usar hello local organizativa autenticación opción (ADFS) con ASP.NET en Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6ae68-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="6ae68-275">Migrar un proyecto de VS2013 Web de WIF tooKatana</span><span class="sxs-lookup"><span data-stu-id="6ae68-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="6ae68-276">Información general de Servicios de federación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ae68-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="6ae68-277">Especificación de WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="6ae68-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

