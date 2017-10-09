---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción - introducción | Documentos de Microsoft"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="f129b-103">Agregar inicie sesión con la aplicación web ASP.NET Microsoft tooan</span><span class="sxs-lookup"><span data-stu-id="f129b-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="f129b-104">Esta guía demuestra cómo tooimplement inicie sesión con Microsoft mediante una solución de MVC de ASP.NET con una aplicación basada en Explorador de web tradicional con OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f129b-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="f129b-105">Al final de Hola de esta guía, la aplicación de ser capaz de tooaccept de inicio de sesión inicios de personal cuentas (incluidos outlook.com, live.com u otros datos) así como de trabajo y cuentas de cualquier empresa u organización que se integra con Azure Active Directory educativas.</span><span class="sxs-lookup"><span data-stu-id="f129b-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="f129b-106">Esta guía requiere Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f129b-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="f129b-107">¿No lo tiene?</span><span class="sxs-lookup"><span data-stu-id="f129b-107">Don’t have it?</span></span>  [<span data-ttu-id="f129b-108">Descargue Visual Studio 2017 de manera gratuita</span><span class="sxs-lookup"><span data-stu-id="f129b-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="f129b-109">Funcionamiento de esta guía</span><span class="sxs-lookup"><span data-stu-id="f129b-109">How this guide works</span></span>

![Funcionamiento de esta guía](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="f129b-111">Esta guía se basa en el escenario de Hola donde un explorador tiene acceso a un sitio web ASP.NET, que solicita un tooauthenticate de usuario a través de un botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f129b-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="f129b-112">En este escenario, la mayor parte de la página web de hello trabajo toorender Hola se produce en el lado del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f129b-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="f129b-113">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="f129b-113">Libraries</span></span>

<span data-ttu-id="f129b-114">Esta guía usa Hola después de bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="f129b-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="f129b-115">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="f129b-115">Library</span></span>|<span data-ttu-id="f129b-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="f129b-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="f129b-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="f129b-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="f129b-118">Software intermedio que permite que una aplicación toouse OpenIdConnect para la autenticación</span><span class="sxs-lookup"><span data-stu-id="f129b-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="f129b-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="f129b-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="f129b-120">Middleware que permite una sesión de usuario de aplicación toomaintain uso de cookies</span><span class="sxs-lookup"><span data-stu-id="f129b-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="f129b-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="f129b-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="f129b-122">Permite que las aplicaciones basadas en OWIN toorun en IIS mediante la canalización de solicitudes ASP.NET de Hola</span><span class="sxs-lookup"><span data-stu-id="f129b-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

