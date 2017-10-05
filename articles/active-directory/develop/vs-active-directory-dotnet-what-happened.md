---
title: Cambios realizados en un proyecto de MVC al conectarse a Azure AD | Microsoft Docs
description: Describe lo que sucede a su proyecto de MVC cuando se conecta a Azure AD mediante los servicios conectados de Visual Studio.
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="60ded-103">¿Qué ha ocurrido a mi proyecto MVC (servicio conectado a Azure Active Directory de Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="60ded-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60ded-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="60ded-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="60ded-105">¿Qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="60ded-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="60ded-106">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="60ded-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="60ded-107">Referencias de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="60ded-107">NuGet package references</span></span>
* <span data-ttu-id="60ded-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="60ded-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="60ded-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="60ded-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="60ded-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="60ded-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="60ded-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="60ded-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="60ded-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="60ded-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="60ded-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="60ded-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="60ded-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="60ded-114">**Owin**</span></span>
* <span data-ttu-id="60ded-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="60ded-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="60ded-116">Referencias de .NET</span><span class="sxs-lookup"><span data-stu-id="60ded-116">.NET references</span></span>
* <span data-ttu-id="60ded-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="60ded-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="60ded-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="60ded-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="60ded-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="60ded-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="60ded-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="60ded-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="60ded-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="60ded-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="60ded-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="60ded-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="60ded-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="60ded-123">**Owin**</span></span>
* <span data-ttu-id="60ded-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="60ded-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="60ded-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="60ded-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="60ded-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="60ded-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="60ded-127">Se ha agregado el código</span><span class="sxs-lookup"><span data-stu-id="60ded-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="60ded-128">Se han agregado archivos de código a su proyecto</span><span class="sxs-lookup"><span data-stu-id="60ded-128">Code files were added to your project</span></span>
<span data-ttu-id="60ded-129">Se ha agregado una clase de inicio de autenticación, **App_Start/Startup.Auth.cs**, a su proyecto que contiene la lógica de inicio para la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60ded-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="60ded-130">Además, se ha agregado una clase de controlador (Controllers/AccountController.cs) que contiene los métodos **SignIn()** y **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="60ded-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="60ded-131">Por último, se ha agregado una vista parcial **Views/Shared/_LoginPartial.cshtml** que contiene un vínculo de acción para SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="60ded-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="60ded-132">Se ha agregado código de inicio a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="60ded-132">Startup code was added to your project</span></span>
<span data-ttu-id="60ded-133">Si ya tenía una clase de inicio en su proyecto, el método **Configuration** se ha actualizado para incluir una llamada a **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="60ded-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="60ded-134">Si no era así, se ha agregado una clase de inicio a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="60ded-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="60ded-135">Su archivo app.config o web.config tiene nuevos valores de configuración</span><span class="sxs-lookup"><span data-stu-id="60ded-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="60ded-136">Se han agregado las siguientes entradas de configuración.</span><span class="sxs-lookup"><span data-stu-id="60ded-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="60ded-137">Se ha creado una aplicación de Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="60ded-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="60ded-138">Se ha creado una aplicación de Azure AD en el directorio que seleccionó en el asistente.</span><span class="sxs-lookup"><span data-stu-id="60ded-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="60ded-139">Si he activado la *deshabilitación de la autenticación de cuentas de usuario individuales*, ¿qué otros cambios se realizaron en mi proyecto?</span><span class="sxs-lookup"><span data-stu-id="60ded-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="60ded-140">Se han quitado las referencias al paquete NuGet y se han quitado los archivos y se ha realizado una copia de seguridad de los mismos.</span><span class="sxs-lookup"><span data-stu-id="60ded-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="60ded-141">Según el estado del proyecto, tendrá que quitar referencias o archivos adicionales manualmente o modificar el código, según corresponda.</span><span class="sxs-lookup"><span data-stu-id="60ded-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="60ded-142">Referencias al paquete NuGet quitadas (si existen)</span><span class="sxs-lookup"><span data-stu-id="60ded-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="60ded-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="60ded-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="60ded-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="60ded-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="60ded-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="60ded-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="60ded-146">Se ha realizado una copia de seguridad de los archivos y se han eliminado (si existen)</span><span class="sxs-lookup"><span data-stu-id="60ded-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="60ded-147">Se ha realizado una copia de seguridad de cada uno de los siguientes archivos y se han eliminado del proyecto.</span><span class="sxs-lookup"><span data-stu-id="60ded-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="60ded-148">Los archivos de copia de seguridad se encuentran en una carpeta 'Backup' en la raíz del directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="60ded-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="60ded-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="60ded-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="60ded-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="60ded-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="60ded-153">Copia de seguridad de los archivos de código (si existen)</span><span class="sxs-lookup"><span data-stu-id="60ded-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="60ded-154">Se realizó una copia de seguridad de cada uno de los siguientes archivos antes de ser reemplazados.</span><span class="sxs-lookup"><span data-stu-id="60ded-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="60ded-155">Los archivos de copia de seguridad se encuentran en una carpeta 'Backup' en la raíz del directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="60ded-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="60ded-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-156">**Startup.cs**</span></span>
* <span data-ttu-id="60ded-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="60ded-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="60ded-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="60ded-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="60ded-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="60ded-160">Si activé *Leer datos de directorio*, ¿qué otros cambios se realizaron en mi proyecto?</span><span class="sxs-lookup"><span data-stu-id="60ded-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="60ded-161">Se han agregado referencias adicionales.</span><span class="sxs-lookup"><span data-stu-id="60ded-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="60ded-162">Referencias de paquetes de NuGet adicionales</span><span class="sxs-lookup"><span data-stu-id="60ded-162">Additional NuGet package references</span></span>
* <span data-ttu-id="60ded-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="60ded-163">**EntityFramework**</span></span>
* <span data-ttu-id="60ded-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="60ded-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="60ded-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="60ded-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="60ded-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="60ded-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="60ded-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="60ded-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="60ded-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="60ded-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="60ded-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="60ded-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="60ded-170">Referencias de .NET adicionales</span><span class="sxs-lookup"><span data-stu-id="60ded-170">Additional .NET references</span></span>
* <span data-ttu-id="60ded-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="60ded-171">**EntityFramework**</span></span>
* <span data-ttu-id="60ded-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="60ded-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="60ded-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="60ded-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="60ded-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="60ded-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="60ded-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="60ded-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="60ded-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="60ded-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="60ded-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="60ded-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="60ded-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="60ded-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="60ded-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="60ded-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="60ded-180">Se han agregado archivos de código adicionales a su proyecto</span><span class="sxs-lookup"><span data-stu-id="60ded-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="60ded-181">Se agregaron dos archivos para admitir el almacenamiento en caché de tokens: **Models\ADALTokenCache.cs** y **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="60ded-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="60ded-182">Se han agregado un controlador y una vista adicionales para ilustrar el acceso a la información de perfil de usuario mediante las API Graph de Azure.</span><span class="sxs-lookup"><span data-stu-id="60ded-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="60ded-183">Estos archivos son **Controllers\UserProfileController.cs** y **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="60ded-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="60ded-184">Se ha agregado código de inicio adicional al proyecto.</span><span class="sxs-lookup"><span data-stu-id="60ded-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="60ded-185">En el archivo **startup.auth.cs**, se agregó un nuevo objeto **OpenIdConnectAuthenticationNotifications** al miembro **Notifications** de **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="60ded-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="60ded-186">Esto permite recibir el código de OAuth y cambiarlo por un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="60ded-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="60ded-187">Se realizaron cambios adicionales en app.config o web.config</span><span class="sxs-lookup"><span data-stu-id="60ded-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="60ded-188">Se han agregado las siguientes entradas de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="60ded-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="60ded-189">Se han agregado las siguientes secciones de configuración y la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="60ded-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="60ded-190">Se ha actualizado la aplicación Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60ded-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="60ded-191">La aplicación Azure Active Directory se actualizó para incluir el permiso *Leer datos de directorio* y se creó una clave adicional que luego se usó como *ida:ClientSecret* en el archivo **web.config**.</span><span class="sxs-lookup"><span data-stu-id="60ded-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60ded-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60ded-192">Next steps</span></span>
- [<span data-ttu-id="60ded-193">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60ded-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

