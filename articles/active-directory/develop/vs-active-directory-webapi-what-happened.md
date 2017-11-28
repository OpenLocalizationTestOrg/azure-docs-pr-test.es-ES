---
title: aaaChanges realizado tooa WebApi proyecto cuando se conecta tooAzure AD | Documentos de Microsoft
description: Describe lo que sucede tooyour WebApi proyecto cuando se conecta tooAzure AD mediante Visual Studio
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
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="67826-103">¿Qué proyecto de WebApi toomy problema (servicio de Visual Studio Azure Active Directory conectado)</span><span class="sxs-lookup"><span data-stu-id="67826-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67826-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="67826-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="67826-105">¿Qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="67826-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="67826-106">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="67826-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="67826-107">Referencias de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="67826-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="67826-108">Referencias de .NET</span><span class="sxs-lookup"><span data-stu-id="67826-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="67826-109">Cambios de código</span><span class="sxs-lookup"><span data-stu-id="67826-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="67826-110">Archivos de código se agregaron tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="67826-110">Code files were added tooyour project</span></span>
<span data-ttu-id="67826-111">Una clase de inicio de autenticación, **App_Start/Startup.Auth.cs** agregó proyecto tooyour que contiene la lógica de inicio para la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67826-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="67826-112">El código de inicio se agregó tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="67826-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="67826-113">Si ya tenía una clase de inicio en el proyecto, Hola **configuración** método era tooinclude actualizado una llamada demasiado`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="67826-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="67826-114">En caso contrario, se agrega una clase de inicio tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="67826-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="67826-115">Su archivo app.config o web.config tiene nuevos valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="67826-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="67826-116">se han agregado Hola siguiendo las entradas de configuración.</span><span class="sxs-lookup"><span data-stu-id="67826-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="67826-117">Se ha creado una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67826-117">An Azure AD App was created</span></span>
<span data-ttu-id="67826-118">Una aplicación de Azure AD se creó en el directorio de Hola que seleccionó en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="67826-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="67826-119">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67826-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="67826-120">¿Si activa *deshabilitar la autenticación de cuentas de usuario individuales*, los cambios adicionales se aplicaron toomy proyecto?</span><span class="sxs-lookup"><span data-stu-id="67826-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="67826-121">Se han quitado las referencias al paquete NuGet y se han quitado los archivos y se ha realizado una copia de seguridad de los mismos.</span><span class="sxs-lookup"><span data-stu-id="67826-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="67826-122">Según el estado de saludo del proyecto, puede tener toomanually quitar referencias adicionales o archivos, o modificar el código según corresponda.</span><span class="sxs-lookup"><span data-stu-id="67826-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="67826-123">Referencias al paquete NuGet quitadas (si existen)</span><span class="sxs-lookup"><span data-stu-id="67826-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="67826-124">Se ha realizado una copia de seguridad de los archivos y se han eliminado (si existen)</span><span class="sxs-lookup"><span data-stu-id="67826-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="67826-125">Cada uno de los siguientes archivos se copia de seguridad y quitará Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="67826-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="67826-126">Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="67826-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="67826-127">Copia de seguridad de los archivos de código (si existen)</span><span class="sxs-lookup"><span data-stu-id="67826-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="67826-128">Se realizó una copia de seguridad de cada uno de los siguientes archivos antes de ser reemplazados.</span><span class="sxs-lookup"><span data-stu-id="67826-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="67826-129">Archivos de copia de seguridad se encuentran en una carpeta "Backup" hello raíz del directorio del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="67826-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="67826-130">¿Si activa *leer datos de directorio*, los cambios adicionales se aplicaron toomy proyecto?</span><span class="sxs-lookup"><span data-stu-id="67826-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="67826-131">Se realizaron cambios adicionales tooyour app.config o web.config</span><span class="sxs-lookup"><span data-stu-id="67826-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="67826-132">Hello entradas de configuración adicionales siguientes se han agregado.</span><span class="sxs-lookup"><span data-stu-id="67826-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="67826-133">Se ha actualizado la aplicación Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67826-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="67826-134">La aplicación de Azure Active Directory estaba actualizada tooinclude hello *leer datos de directorio* permiso y una clave adicional que se creó, a continuación, que se usó como hello *ida: contraseña* en hello `web.config` archivo.</span><span class="sxs-lookup"><span data-stu-id="67826-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67826-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67826-135">Next steps</span></span>
- [<span data-ttu-id="67826-136">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67826-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

