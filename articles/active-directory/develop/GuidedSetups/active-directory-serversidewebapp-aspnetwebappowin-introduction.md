---
title: "Introducción al servidor web de ASP.NET de Azure AD v2: primeros pasos | Microsoft Docs"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="f0fb2-103">Adición de inicio de sesión con Microsoft a una aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0fb2-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="f0fb2-104">Esta guía muestra cómo implementar el inicio de sesión con Microsoft mediante una solución MVC de ASP.NET con una aplicación basada en explorador web tradicional mediante OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f0fb2-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="f0fb2-105">Al final de esta guía, la aplicación podrá aceptar inicios de sesión de cuentas personales (como outlook.com, live.com y otras), así como cuentas profesionales y educativas de cualquier empresa u organización que se haya integrado con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0fb2-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="f0fb2-106">Esta guía requiere Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f0fb2-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="f0fb2-107">¿No lo tiene?</span><span class="sxs-lookup"><span data-stu-id="f0fb2-107">Don’t have it?</span></span>  [<span data-ttu-id="f0fb2-108">Descargue Visual Studio 2017 de manera gratuita</span><span class="sxs-lookup"><span data-stu-id="f0fb2-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="f0fb2-109">Funcionamiento de esta guía</span><span class="sxs-lookup"><span data-stu-id="f0fb2-109">How this guide works</span></span>

![Funcionamiento de esta guía](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="f0fb2-111">Esta guía se basa en un escenario en el que un explorador tiene acceso a un sitio web de ASP.NET y solicita a un usuario que se autentique a través de un botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f0fb2-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="f0fb2-112">En esa situación, la mayoría del trabajo para representar la página web se produce en el servidor.</span><span class="sxs-lookup"><span data-stu-id="f0fb2-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="f0fb2-113">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="f0fb2-113">Libraries</span></span>

<span data-ttu-id="f0fb2-114">Esta guía utiliza las siguientes bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="f0fb2-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="f0fb2-115">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="f0fb2-115">Library</span></span>|<span data-ttu-id="f0fb2-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="f0fb2-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="f0fb2-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="f0fb2-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="f0fb2-118">Middleware que permite a una aplicación que use OpenIDConnect para la autenticación</span><span class="sxs-lookup"><span data-stu-id="f0fb2-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="f0fb2-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="f0fb2-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="f0fb2-120">Middleware que permite a una aplicación que mantenga la sesión del usuario mediante cookies</span><span class="sxs-lookup"><span data-stu-id="f0fb2-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="f0fb2-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="f0fb2-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="f0fb2-122">Permite que aplicaciones basadas en OWIN se ejecuten en IIS mediante la canalización de solicitudes ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0fb2-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

