---
title: "aaaAzure AD v2 Windows Desktop Introducción - introducción | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones .NET de escritorio de Windows (XAML) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="28bf7-103">Hola llamada API de Microsoft Graph desde una aplicación de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="28bf7-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="28bf7-104">Esta guía muestra cómo una aplicación nativa de .NET de escritorio de Windows (XAML) puede obtener un token de acceso y llamar a la API Graph de Microsoft u otras API que requieran tokens de acceso desde un punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="28bf7-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="28bf7-105">Al final de Hola de esta guía, la aplicación se ser capaz de toocall API protegida mediante cuentas personales (incluidos outlook.com, live.com etc.) así como trabajar y cuentas de escuela de cualquier empresa u organización con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28bf7-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="28bf7-106">Esta guía requiere Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="28bf7-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="28bf7-107">¿No lo tiene?</span><span class="sxs-lookup"><span data-stu-id="28bf7-107">Don’t have it?</span></span> [<span data-ttu-id="28bf7-108">Descargue Visual Studio 2017 de manera gratuita</span><span class="sxs-lookup"><span data-stu-id="28bf7-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="28bf7-109">Funcionamiento de esta guía</span><span class="sxs-lookup"><span data-stu-id="28bf7-109">How this guide works</span></span>

![Funcionamiento de esta guía](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="28bf7-111">aplicación de ejemplo de Hola creada en esta guía habilita una API de Microsoft Graph tooquery de aplicación de escritorio de Windows o una API Web que acepta los tokens de punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="28bf7-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="28bf7-112">En este escenario, un símbolo (token) se agrega tooHTTP solicitudes a través del encabezado de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="28bf7-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="28bf7-113">Hola biblioteca de autenticación de Microsoft (MSAL) se administra la renovación y adquisición de tokens.</span><span class="sxs-lookup"><span data-stu-id="28bf7-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="28bf7-114">Tratamiento de la adquisición de tokens para tener acceso a API web protegidas</span><span class="sxs-lookup"><span data-stu-id="28bf7-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="28bf7-115">Cuando se autentica el usuario hello, aplicación de ejemplo de Hola recibe un token que puede ser utilizado tooquery API Graph de Microsoft o una API Web protegida por Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="28bf7-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="28bf7-116">Las API, como Microsoft Graph requieren un tooallow de token de acceso obtener acceso a recursos específicos, por ejemplo, tooread un perfil de usuario, obtener acceso a calendario del usuario o envían un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="28bf7-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="28bf7-117">La aplicación puede solicitar un token de acceso mediante MSAL tooaccess estos recursos mediante la especificación de ámbitos de API.</span><span class="sxs-lookup"><span data-stu-id="28bf7-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="28bf7-118">Este token de acceso es agregado toohello encabezado de autorización HTTP para todas las llamadas efectuadas contra Hola al recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="28bf7-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="28bf7-119">MSAL administra el almacenamiento en caché y la actualización de los tokens de acceso automáticamente, así que no tiene que preocuparse por ello.</span><span class="sxs-lookup"><span data-stu-id="28bf7-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="28bf7-120">Paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="28bf7-120">NuGet Packages</span></span>

<span data-ttu-id="28bf7-121">Esta guía usa Hola siguientes paquetes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="28bf7-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="28bf7-122">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="28bf7-122">Library</span></span>|<span data-ttu-id="28bf7-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="28bf7-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="28bf7-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="28bf7-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="28bf7-125">Biblioteca de autenticación de Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="28bf7-125">Microsoft Authentication Library (MSAL)</span></span>|

