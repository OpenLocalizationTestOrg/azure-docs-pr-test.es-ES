---
title: "errores de toodiagnose aaaHow con hello Asistente de conexión de Azure Active Directory"
description: "Asistente para la conexión de active directory de Hello detectó un tipo de autenticación incompatible"
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
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="c7bb1-103">Diagnóstico de errores con hello Asistente de conexión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7bb1-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="c7bb1-104">Al detectar el anterior código de autenticación, el Asistente de hello detectó un tipo de autenticación incompatible.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="c7bb1-105">¿Qué se está comprobando?</span><span class="sxs-lookup"><span data-stu-id="c7bb1-105">What is being checked?</span></span>
<span data-ttu-id="c7bb1-106">**Nota:** toocorrectly detecta el anterior código de autenticación en un proyecto, se debe compilar el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="c7bb1-107">Si se produjo este error y no tiene un código de autenticación anterior en el proyecto, vuelva a compilarlo e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="c7bb1-108">Tipos de proyecto</span><span class="sxs-lookup"><span data-stu-id="c7bb1-108">Project Types</span></span>
<span data-ttu-id="c7bb1-109">Asistente de Hello comprueba el tipo de Hola de proyecto que se va a desarrollar por lo que puede insertar lógica de autenticación adecuado de hello en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="c7bb1-110">Si no hay ningún controlador que se deriva de `ApiController` en el proyecto de hello, proyecto de Hola se considera un proyecto de WebAPI.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="c7bb1-111">Si hay solo los controladores que se derivan de `MVC.Controller` en el proyecto de hello, proyecto de Hola se considera un proyecto de MVC.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="c7bb1-112">Todo lo demás no es compatible con asistente Hola.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="c7bb1-113">Código de autenticación compatible</span><span class="sxs-lookup"><span data-stu-id="c7bb1-113">Compatible Authentication Code</span></span>
<span data-ttu-id="c7bb1-114">Asistente Hello también comprueba si la configuración de autenticación que se haya configurado anteriormente con el Asistente de Hola o es compatibles con el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="c7bb1-115">Si todos los valores están presentes, se considera un caso reentrante y abrirá el Asistente Hola Mostrar configuración Hola.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="c7bb1-116">Si solo algunos de los valores de hello están presentes, se considera un caso de error.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="c7bb1-117">En un proyecto MVC, Hola asistente comprueba cualquiera de hello después de la configuración, que genera frente al uso anterior del Asistente para hello:</span><span class="sxs-lookup"><span data-stu-id="c7bb1-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="c7bb1-118">Además, Hola asistente comprueba cualquiera de hello después de la configuración en un proyecto de API Web, que genera frente al uso anterior del Asistente para hello:</span><span class="sxs-lookup"><span data-stu-id="c7bb1-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="c7bb1-119">Código de autenticación incompatible</span><span class="sxs-lookup"><span data-stu-id="c7bb1-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="c7bb1-120">Por último, el Asistente de Hola intenta toodetect versiones de código de autenticación que se han configurado con versiones anteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="c7bb1-121">Si recibió este error, significa el proyecto contiene un tipo de autenticación incompatible.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="c7bb1-122">Asistente de Hello detecta Hola siguientes tipos de autenticación de las versiones anteriores de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c7bb1-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="c7bb1-123">Autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="c7bb1-123">Windows Authentication</span></span> 
* <span data-ttu-id="c7bb1-124">Cuentas de usuario individuales</span><span class="sxs-lookup"><span data-stu-id="c7bb1-124">Individual User Accounts</span></span> 
* <span data-ttu-id="c7bb1-125">Cuentas organizativas</span><span class="sxs-lookup"><span data-stu-id="c7bb1-125">Organizational Accounts</span></span> 

<span data-ttu-id="c7bb1-126">toodetect autenticación de Windows en un proyecto MVC, el Asistente de hello busca hello `authentication` elemento desde el **web.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="c7bb1-127">toodetect autenticación de Windows en un proyecto de API Web, el Asistente de hello busca hello `IISExpressWindowsAuthentication` elemento desde el proyecto **.csproj** archivo:</span><span class="sxs-lookup"><span data-stu-id="c7bb1-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="c7bb1-128">autenticación de cuentas de usuario individuales toodetect, Hola examina para elemento de paquete de Hola desde su **Packages.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="c7bb1-129">toodetect un formato antiguo de autenticación de cuenta profesional, Asistente Hola busca Hola siguiente elemento de **web.config**:</span><span class="sxs-lookup"><span data-stu-id="c7bb1-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="c7bb1-130">tipo de autenticación de toochange hello, quitar el tipo de autenticación incompatible de Hola y vuelva a ejecutar el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7bb1-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="c7bb1-131">Para obtener más información, consulte [Escenarios de autenticación en Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="c7bb1-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="c7bb1-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7bb1-132">Next steps</span></span>
- [<span data-ttu-id="c7bb1-133">Escenarios de autenticación para Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7bb1-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)