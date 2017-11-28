---
title: "Introducción a iOS en Azure AD v2 | Microsoft Docs"
description: "Cómo pueden llamar las aplicaciones de iOS (Swift) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 948693c8501ecc46a1508e5ea085846d0910783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="70eb7-103">Llamada a la API de Microsoft Graph desde una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="70eb7-103">Call the Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="70eb7-104">En esta guía se muestra cómo una aplicación nativa de iOS (Swift) puede obtener un token de acceso y llamar a la API de Microsoft Graph u otras API que requieran tokens de acceso desde un punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="70eb7-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call the Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="70eb7-105">Al final de esta guía, la aplicación podrá llamar a una API protegida utilizando cuentas personales (como outlook.com, live.com y otras), así como cuentas profesionales y educativas de cualquier empresa u organización que tenga Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70eb7-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="70eb7-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="70eb7-106">Pre-requisites</span></span>
> - <span data-ttu-id="70eb7-107">Para esta guía se requiere XCode 8.x.</span><span class="sxs-lookup"><span data-stu-id="70eb7-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="70eb7-108">Puede descargar XCode [aquí](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "Dirección URL de descarga de XCode").</span><span class="sxs-lookup"><span data-stu-id="70eb7-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="70eb7-109">[Carthage](https://github.com/Carthage/Carthage) para administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="70eb7-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="70eb7-110">Funcionamiento de esta guía</span><span class="sxs-lookup"><span data-stu-id="70eb7-110">How this guide works</span></span>

![Funcionamiento de esta guía](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="70eb7-112">La aplicación de ejemplo que se crea con esta guía permite que una aplicación iOS consulte a la API de Microsoft Graph o a una API web que acepte tokens desde un punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="70eb7-112">The sample application created by this guide enables an iOS application to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="70eb7-113">En este escenario, se agrega un token a las solicitudes HTTP a través del encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="70eb7-113">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="70eb7-114">La adquisición y la renovación de los tokens se realiza por medio de la biblioteca de autenticación de Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="70eb7-114">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="70eb7-115">Tratamiento de la adquisición de tokens para tener acceso a API web protegidas</span><span class="sxs-lookup"><span data-stu-id="70eb7-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="70eb7-116">Una vez que el usuario se autentica, la aplicación de ejemplo recibe un token que se puede utilizar para consultar a la API de Microsoft Graph o a una API web protegida mediante Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="70eb7-116">After the user authenticates, the sample application receives a token that can be used to query the Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="70eb7-117">Las API como Microsoft Graph requieren un token de acceso para permitir el acceso a recursos específicos; por ejemplo, para leer un perfil de usuario, tener acceso al calendario del usuario o enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="70eb7-117">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="70eb7-118">La aplicación puede solicitar un token de acceso mediante MSAL mediante la especificación de ámbitos de API.</span><span class="sxs-lookup"><span data-stu-id="70eb7-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="70eb7-119">Este token de acceso se agrega entonces al encabezado de autorización de HTTP para todas las llamadas efectuadas al recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="70eb7-119">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span>

<span data-ttu-id="70eb7-120">MSAL administra el almacenamiento en caché y la actualización de los tokens de acceso automáticamente, así que no tiene que preocuparse por ello.</span><span class="sxs-lookup"><span data-stu-id="70eb7-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="70eb7-121">Paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="70eb7-121">NuGet packages</span></span>

<span data-ttu-id="70eb7-122">Esta guía utiliza los siguientes paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="70eb7-122">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="70eb7-123">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="70eb7-123">Library</span></span>|<span data-ttu-id="70eb7-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="70eb7-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="70eb7-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="70eb7-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="70eb7-126">Versión preliminar de Biblioteca de autenticación de Microsoft para iOS</span><span class="sxs-lookup"><span data-stu-id="70eb7-126">Microsoft Authentication Library Preview for iOS</span></span>|

