---
title: "Diagnóstico de errores con el Asistente para conexión de Azure Active Directory"
description: "El asistente para conexión de Active Directory detectó un tipo de autenticación no compatible"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="2542d-103">Diagnóstico de errores con el Asistente para conexión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2542d-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="2542d-104">Al detectar el código de autenticación anterior, el asistente detectó un tipo de autenticación incompatible.</span><span class="sxs-lookup"><span data-stu-id="2542d-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="2542d-105">¿Qué se está comprobando?</span><span class="sxs-lookup"><span data-stu-id="2542d-105">What is being checked?</span></span>
<span data-ttu-id="2542d-106">**Nota:** para detectar correctamente el código de autenticación anterior de un proyecto, este debe estar creado.</span><span class="sxs-lookup"><span data-stu-id="2542d-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="2542d-107">Si se produjo este error y no tiene un código de autenticación anterior en el proyecto, vuelva a compilarlo e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2542d-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="2542d-108">Tipos de proyecto</span><span class="sxs-lookup"><span data-stu-id="2542d-108">Project Types</span></span>
<span data-ttu-id="2542d-109">El asistente comprueba el tipo de proyecto que esté desarrollando, por lo que puede insertar la lógica de autenticación correcta en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2542d-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="2542d-110">Si no hay ningún controlador que derive de `ApiController` en el proyecto, el proyecto se considerará como un proyecto WebAPI.</span><span class="sxs-lookup"><span data-stu-id="2542d-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="2542d-111">Si solo hay controladores que derivan de `MVC.Controller` en el proyecto, el proyecto se considerará como proyecto MVC.</span><span class="sxs-lookup"><span data-stu-id="2542d-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="2542d-112">El asistente considera todo lo demás como no compatible.</span><span class="sxs-lookup"><span data-stu-id="2542d-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="2542d-113">Código de autenticación compatible</span><span class="sxs-lookup"><span data-stu-id="2542d-113">Compatible Authentication Code</span></span>
<span data-ttu-id="2542d-114">El asistente también comprueba la configuración de autenticación que se ha configurado previamente con el asistente o que es compatible con el asistente.</span><span class="sxs-lookup"><span data-stu-id="2542d-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="2542d-115">Si todos los valores de configuración están presentes, se considera un caso reentrante y el asistente abrirá y mostrará la configuración.</span><span class="sxs-lookup"><span data-stu-id="2542d-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="2542d-116">Si solo algunos valores de configuración están presentes, se considera un caso de error.</span><span class="sxs-lookup"><span data-stu-id="2542d-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="2542d-117">En un proyecto MVC, el asistente comprueba cualquiera de los siguientes valores de configuración, que se originan a partir de un uso anterior del asistente:</span><span class="sxs-lookup"><span data-stu-id="2542d-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="2542d-118">Además, el asistente comprueba los siguientes valores de configuración en el proyecto Web API, que se originan a partir del uso anterior del asistente:</span><span class="sxs-lookup"><span data-stu-id="2542d-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="2542d-119">Código de autenticación incompatible</span><span class="sxs-lookup"><span data-stu-id="2542d-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="2542d-120">Finalmente, el asistente trata de detectar versiones de código de autenticación que se hayan configurado con versiones anteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2542d-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="2542d-121">Si recibió este error, significa el proyecto contiene un tipo de autenticación incompatible.</span><span class="sxs-lookup"><span data-stu-id="2542d-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="2542d-122">El asistente detecta los siguientes tipos de autenticación de las versiones anteriores de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2542d-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="2542d-123">Autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="2542d-123">Windows Authentication</span></span> 
* <span data-ttu-id="2542d-124">Cuentas de usuario individuales</span><span class="sxs-lookup"><span data-stu-id="2542d-124">Individual User Accounts</span></span> 
* <span data-ttu-id="2542d-125">Cuentas organizativas</span><span class="sxs-lookup"><span data-stu-id="2542d-125">Organizational Accounts</span></span> 

<span data-ttu-id="2542d-126">Para detectar la autenticación de Windows en un proyecto MVC, el asistente busca el elemento `authentication` en el archivo **web.config** .</span><span class="sxs-lookup"><span data-stu-id="2542d-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="2542d-127">Para detectar la autenticación de Windows en un proyecto Web API, el asistente busca el elemento `IISExpressWindowsAuthentication` en el archivo **.csproj** del proyecto:</span><span class="sxs-lookup"><span data-stu-id="2542d-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="2542d-128">Para detectar la autenticación de cuentas de usuario individuales, el asistente busca el elemento de paquete en el archivo **Packages.config** .</span><span class="sxs-lookup"><span data-stu-id="2542d-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="2542d-129">Para detectar una forma anterior de autenticación con la cuenta de una organización, el asistente busca el siguiente elemento en **web.config**:</span><span class="sxs-lookup"><span data-stu-id="2542d-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="2542d-130">Para cambiar el tipo de autenticación, quite el tipo de autenticación incompatible y ejecute de nuevo el asistente.</span><span class="sxs-lookup"><span data-stu-id="2542d-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="2542d-131">Para obtener más información, consulte [Escenarios de autenticación en Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2542d-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="2542d-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2542d-132">Next steps</span></span>
- [<span data-ttu-id="2542d-133">Escenarios de autenticación para Azure AD</span><span class="sxs-lookup"><span data-stu-id="2542d-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)