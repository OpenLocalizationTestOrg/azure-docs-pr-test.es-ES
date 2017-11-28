---
title: tooa aaaChanges realizados MVC proyecto cuando se conecta tooAzure AD | Documentos de Microsoft
description: Describe lo que sucede tooyour proyecto MVC cuando se conecta tooAzure AD mediante el uso de servicios de Visual Studio conectado
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="c40b8-103">¿Qué proyecto MVC toomy problema (servicio de Visual Studio Azure Active Directory conectado)?</span><span class="sxs-lookup"><span data-stu-id="c40b8-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c40b8-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="c40b8-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="c40b8-105">¿Qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="c40b8-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="c40b8-106">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="c40b8-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="c40b8-107">Referencias de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="c40b8-107">NuGet package references</span></span>
* <span data-ttu-id="c40b8-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="c40b8-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="c40b8-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="c40b8-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="c40b8-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="c40b8-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="c40b8-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="c40b8-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="c40b8-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="c40b8-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="c40b8-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="c40b8-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="c40b8-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="c40b8-114">**Owin**</span></span>
* <span data-ttu-id="c40b8-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="c40b8-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="c40b8-116">Referencias de .NET</span><span class="sxs-lookup"><span data-stu-id="c40b8-116">.NET references</span></span>
* <span data-ttu-id="c40b8-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="c40b8-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="c40b8-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="c40b8-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="c40b8-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="c40b8-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="c40b8-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="c40b8-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="c40b8-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="c40b8-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="c40b8-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="c40b8-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="c40b8-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="c40b8-123">**Owin**</span></span>
* <span data-ttu-id="c40b8-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="c40b8-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="c40b8-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="c40b8-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="c40b8-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="c40b8-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="c40b8-127">Se ha agregado el código</span><span class="sxs-lookup"><span data-stu-id="c40b8-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="c40b8-128">Archivos de código se agregaron tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="c40b8-128">Code files were added tooyour project</span></span>
<span data-ttu-id="c40b8-129">Una clase de inicio de autenticación, **App_Start/Startup.Auth.cs** agregó proyecto tooyour que contiene la lógica de inicio para la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c40b8-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="c40b8-130">Además, se ha agregado una clase de controlador (Controllers/AccountController.cs) que contiene los métodos **SignIn()** y **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="c40b8-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="c40b8-131">Por último, se ha agregado una vista parcial **Views/Shared/_LoginPartial.cshtml** que contiene un vínculo de acción para SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="c40b8-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="c40b8-132">El código de inicio se agregó tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="c40b8-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="c40b8-133">Si ya tenía una clase de inicio en el proyecto, Hola **configuración** método era tooinclude actualizado una llamada demasiado**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="c40b8-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="c40b8-134">En caso contrario, se agrega una clase de inicio tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="c40b8-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="c40b8-135">Su archivo app.config o web.config tiene nuevos valores de configuración</span><span class="sxs-lookup"><span data-stu-id="c40b8-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="c40b8-136">se han agregado Hola siguiendo las entradas de configuración.</span><span class="sxs-lookup"><span data-stu-id="c40b8-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="c40b8-137">Se ha creado una aplicación de Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="c40b8-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="c40b8-138">Una aplicación de Azure AD se creó en el directorio de Hola que seleccionó en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c40b8-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="c40b8-139">¿Si activa *deshabilitar la autenticación de cuentas de usuario individuales*, los cambios adicionales se aplicaron toomy proyecto?</span><span class="sxs-lookup"><span data-stu-id="c40b8-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="c40b8-140">Se han quitado las referencias al paquete NuGet y se han quitado los archivos y se ha realizado una copia de seguridad de los mismos.</span><span class="sxs-lookup"><span data-stu-id="c40b8-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="c40b8-141">Según el estado de saludo del proyecto, puede tener toomanually quitar referencias adicionales o archivos, o modificar el código según corresponda.</span><span class="sxs-lookup"><span data-stu-id="c40b8-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="c40b8-142">Referencias al paquete NuGet quitadas (si existen)</span><span class="sxs-lookup"><span data-stu-id="c40b8-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="c40b8-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="c40b8-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="c40b8-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="c40b8-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="c40b8-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="c40b8-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="c40b8-146">Se ha realizado una copia de seguridad de los archivos y se han eliminado (si existen)</span><span class="sxs-lookup"><span data-stu-id="c40b8-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="c40b8-147">Cada uno de los siguientes archivos se copia de seguridad y quitará Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="c40b8-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="c40b8-148">Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c40b8-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="c40b8-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="c40b8-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="c40b8-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="c40b8-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="c40b8-153">Copia de seguridad de los archivos de código (si existen)</span><span class="sxs-lookup"><span data-stu-id="c40b8-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="c40b8-154">Se realizó una copia de seguridad de cada uno de los siguientes archivos antes de ser reemplazados.</span><span class="sxs-lookup"><span data-stu-id="c40b8-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="c40b8-155">Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c40b8-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="c40b8-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-156">**Startup.cs**</span></span>
* <span data-ttu-id="c40b8-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="c40b8-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="c40b8-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="c40b8-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="c40b8-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="c40b8-160">¿Si activa *leer datos de directorio*, los cambios adicionales se aplicaron toomy proyecto?</span><span class="sxs-lookup"><span data-stu-id="c40b8-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="c40b8-161">Se han agregado referencias adicionales.</span><span class="sxs-lookup"><span data-stu-id="c40b8-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="c40b8-162">Referencias de paquetes de NuGet adicionales</span><span class="sxs-lookup"><span data-stu-id="c40b8-162">Additional NuGet package references</span></span>
* <span data-ttu-id="c40b8-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="c40b8-163">**EntityFramework**</span></span>
* <span data-ttu-id="c40b8-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="c40b8-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="c40b8-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="c40b8-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="c40b8-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="c40b8-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="c40b8-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="c40b8-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="c40b8-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="c40b8-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="c40b8-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="c40b8-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="c40b8-170">Referencias de .NET adicionales</span><span class="sxs-lookup"><span data-stu-id="c40b8-170">Additional .NET references</span></span>
* <span data-ttu-id="c40b8-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="c40b8-171">**EntityFramework**</span></span>
* <span data-ttu-id="c40b8-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="c40b8-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="c40b8-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="c40b8-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="c40b8-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="c40b8-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="c40b8-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="c40b8-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="c40b8-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="c40b8-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="c40b8-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="c40b8-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="c40b8-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="c40b8-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="c40b8-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="c40b8-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="c40b8-180">Archivos de código adicionales se agregaron tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="c40b8-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="c40b8-181">Se agregan dos archivos toosupport símbolo (token) de almacenamiento en caché: **Models\ADALTokenCache.cs** y **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="c40b8-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="c40b8-182">Un controlador adicional y la vista se agregaron tooillustrate acceso a la información de perfil de usuario mediante las API de Azure graph.</span><span class="sxs-lookup"><span data-stu-id="c40b8-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="c40b8-183">Estos archivos son **Controllers\UserProfileController.cs** y **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="c40b8-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="c40b8-184">El código de inicio adicional se agregó tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="c40b8-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="c40b8-185">Hola **startup.auth.cs** de archivos, un nuevo **OpenIdConnectAuthenticationNotifications** se agregó el objeto toohello **notificaciones** miembro de hello  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="c40b8-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="c40b8-186">Se trata de tooenable recibir hello OAuth código e intercambian para un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="c40b8-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="c40b8-187">Se realizaron cambios adicionales tooyour app.config o web.config</span><span class="sxs-lookup"><span data-stu-id="c40b8-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="c40b8-188">Hello entradas de configuración adicionales siguientes se han agregado.</span><span class="sxs-lookup"><span data-stu-id="c40b8-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="c40b8-189">Hello secciones de configuración siguientes y cadena de conexión se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="c40b8-189">hello following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="c40b8-190">Se ha actualizado la aplicación Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c40b8-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="c40b8-191">La aplicación de Azure Active Directory estaba actualizada tooinclude hello *leer datos de directorio* permiso y una clave adicional que se creó, a continuación, que se usó como hello *ida: ClientSecret* en hello  **Web.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="c40b8-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c40b8-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c40b8-192">Next steps</span></span>
- [<span data-ttu-id="c40b8-193">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c40b8-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

