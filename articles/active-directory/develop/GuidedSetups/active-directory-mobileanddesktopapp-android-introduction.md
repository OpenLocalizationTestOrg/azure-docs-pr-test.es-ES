---
title: "aaaAzure AD v2 Android Introducción - introducción | Documentos de Microsoft"
description: "Cómo puede una aplicación de Android obtener un token de acceso y llamar a las API Graph que requieren tokens de acceso desde el punto de conexión de Azure Active Directory v2"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="a7668-103">Hola llamada API de Microsoft Graph desde una aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="a7668-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="a7668-104">En esta guía se muestra cómo una aplicación nativa de Android puede obtener un token de acceso y llamar a la API Graph de Microsoft u otras API que requieran tokens de acceso desde un punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="a7668-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="a7668-105">Al final de Hola de esta guía, la aplicación se ser capaz de toocall API protegida mediante cuentas personales (incluidos outlook.com, live.com etc.) así como trabajar y cuentas de escuela de cualquier empresa u organización con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7668-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="a7668-106">Funcionamiento de este ejemplo</span><span class="sxs-lookup"><span data-stu-id="a7668-106">How this sample works</span></span>
![Funcionamiento de este ejemplo](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="a7668-108">ejemplo de Hola creado en esta guía se basa en un escenario donde una aplicación Android es tooquery usa una API Web que acepta los tokens de Azure Active Directory v2 endpoint – en este caso, Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="a7668-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="a7668-109">En este escenario, un símbolo (token) se agrega tooHTTP solicitudes a través del encabezado de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7668-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="a7668-110">Hola biblioteca de autenticación de Microsoft (MSAL) se administra la renovación y adquisición de tokens.</span><span class="sxs-lookup"><span data-stu-id="a7668-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="a7668-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a7668-111">Pre-requisites</span></span>
* <span data-ttu-id="a7668-112">Esta guía paso a paso se centra en Android Studio, pero cualquier otro entorno de desarrollo de aplicaciones de Android también es aceptable.</span><span class="sxs-lookup"><span data-stu-id="a7668-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="a7668-113">Se requiere Android SDK 21 o posterior (se recomienda SDK 25).</span><span class="sxs-lookup"><span data-stu-id="a7668-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="a7668-114">Se requiere Google Chrome o un explorador web que use pestañas personalizadas para esta versión de la biblioteca de autenticación de Microsoft (MSAL) para Android.</span><span class="sxs-lookup"><span data-stu-id="a7668-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="a7668-115">Nota: Google Chrome no se incluye en el Emulador de Visual Studio para Android.</span><span class="sxs-lookup"><span data-stu-id="a7668-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="a7668-116">Le recomendamos que tootest este código en un emulador con API de 25 o una imagen con API 21 o posterior que tenga con Google Chrome instalado.</span><span class="sxs-lookup"><span data-stu-id="a7668-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="a7668-117">¿Cómo toohandle token adquisición tooaccess API Web protegida</span><span class="sxs-lookup"><span data-stu-id="a7668-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="a7668-118">Cuando se autentica el usuario hello, aplicación de ejemplo de Hola recibe un token que puede ser utilizado tooquery API Graph de Microsoft o una API Web protegida por Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="a7668-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="a7668-119">Las API, como Microsoft Graph requieren un tooallow de token de acceso obtener acceso a recursos específicos, por ejemplo, tooread un perfil de usuario, obtener acceso a calendario del usuario o envían un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="a7668-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="a7668-120">La aplicación puede solicitar un token de acceso mediante MSAL tooaccess estos recursos mediante la especificación de ámbitos de API.</span><span class="sxs-lookup"><span data-stu-id="a7668-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="a7668-121">Este token de acceso es agregado toohello encabezado de autorización HTTP para todas las llamadas efectuadas contra Hola al recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="a7668-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="a7668-122">MSAL administra el almacenamiento en caché y la actualización de los tokens de acceso automáticamente, así que no tiene que preocuparse por ello.</span><span class="sxs-lookup"><span data-stu-id="a7668-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="a7668-123">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="a7668-123">Libraries</span></span>

<span data-ttu-id="a7668-124">Esta guía usa Hola después de bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="a7668-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="a7668-125">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="a7668-125">Library</span></span>|<span data-ttu-id="a7668-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="a7668-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="a7668-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="a7668-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="a7668-128">Biblioteca de autenticación de Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="a7668-128">Microsoft Authentication Library (MSAL)</span></span>|
