---
title: Cambios realizados en un proyecto de WebApi al conectarse a Azure AD | Microsoft Docs
description: Se describe lo que sucede al proyecto de WebApi al conectarse a Azure AD mediante Visual Studio.
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="71710-103">¿Qué ha ocurrido a mi proyecto de WebApi (servicio conectado de Visual Studio Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="71710-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71710-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="71710-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="71710-105">¿Qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="71710-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="71710-106">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="71710-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="71710-107">Referencias de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="71710-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="71710-108">Referencias de .NET</span><span class="sxs-lookup"><span data-stu-id="71710-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="71710-109">Cambios de código</span><span class="sxs-lookup"><span data-stu-id="71710-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="71710-110">Se han agregado archivos de código a su proyecto</span><span class="sxs-lookup"><span data-stu-id="71710-110">Code files were added to your project</span></span>
<span data-ttu-id="71710-111">Se ha agregado una clase de inicio de autenticación, **App_Start/Startup.Auth.cs**, a su proyecto que contiene la lógica de inicio para la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71710-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="71710-112">Se ha agregado código de inicio a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="71710-112">Startup code was added to your project</span></span>
<span data-ttu-id="71710-113">Si ya tenía una clase de inicio en su proyecto, el método **Configuration** se ha actualizado para incluir una llamada a `ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="71710-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="71710-114">Si no era así, se ha agregado una clase de inicio a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="71710-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="71710-115">Su archivo app.config o web.config tiene nuevos valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="71710-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="71710-116">Se han agregado las siguientes entradas de configuración.</span><span class="sxs-lookup"><span data-stu-id="71710-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="71710-117">Se ha creado una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71710-117">An Azure AD App was created</span></span>
<span data-ttu-id="71710-118">Se ha creado una aplicación de Azure AD en el directorio que seleccionó en el asistente.</span><span class="sxs-lookup"><span data-stu-id="71710-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="71710-119">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71710-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="71710-120">Si he activado la *deshabilitación de la autenticación de cuentas de usuario individuales*, ¿qué otros cambios se realizaron en mi proyecto?</span><span class="sxs-lookup"><span data-stu-id="71710-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="71710-121">Se han quitado las referencias al paquete NuGet y se han quitado los archivos y se ha realizado una copia de seguridad de los mismos.</span><span class="sxs-lookup"><span data-stu-id="71710-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="71710-122">Según el estado del proyecto, tendrá que quitar referencias o archivos adicionales manualmente o modificar el código, según corresponda.</span><span class="sxs-lookup"><span data-stu-id="71710-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="71710-123">Referencias al paquete NuGet quitadas (si existen)</span><span class="sxs-lookup"><span data-stu-id="71710-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="71710-124">Se ha realizado una copia de seguridad de los archivos y se han eliminado (si existen)</span><span class="sxs-lookup"><span data-stu-id="71710-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="71710-125">Se ha realizado una copia de seguridad de cada uno de los siguientes archivos y se han eliminado del proyecto.</span><span class="sxs-lookup"><span data-stu-id="71710-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="71710-126">Los archivos de copia de seguridad se encuentran en una carpeta 'Backup' en la raíz del directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="71710-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="71710-127">Copia de seguridad de los archivos de código (si existen)</span><span class="sxs-lookup"><span data-stu-id="71710-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="71710-128">Se realizó una copia de seguridad de cada uno de los siguientes archivos antes de ser reemplazados.</span><span class="sxs-lookup"><span data-stu-id="71710-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="71710-129">Los archivos de copia de seguridad se encuentran en una carpeta 'Backup' en la raíz del directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="71710-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="71710-130">Si activé *Leer datos de directorio*, ¿qué otros cambios se realizaron en mi proyecto?</span><span class="sxs-lookup"><span data-stu-id="71710-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="71710-131">Se realizaron cambios adicionales en app.config o web.config</span><span class="sxs-lookup"><span data-stu-id="71710-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="71710-132">Se han agregado las siguientes entradas de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="71710-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="71710-133">Se ha actualizado la aplicación Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71710-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="71710-134">La aplicación Azure Active Directory se actualizó para incluir el permiso *Leer datos de directorio* y se creó una clave adicional que luego se usó como *ida:Password* en el archivo `web.config`.</span><span class="sxs-lookup"><span data-stu-id="71710-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71710-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71710-135">Next steps</span></span>
- [<span data-ttu-id="71710-136">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71710-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

