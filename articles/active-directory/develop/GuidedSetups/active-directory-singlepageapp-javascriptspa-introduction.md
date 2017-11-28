---
title: "Configuración de SPA de JS en Azure AD v2: introducción | Microsoft Docs"
description: "Cómo pueden llamar las aplicaciones SPA de JavaScript a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 3d195d0d67f8f82c9450ffd93767917698addee3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="c82e0-103">Llamar a la API de Microsoft Graph desde una aplicación de página única de JavaScript (SPA)</span><span class="sxs-lookup"><span data-stu-id="c82e0-103">Call the Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="c82e0-104">En esta guía se muestra cómo una aplicación de una sola página (SPA) de JavaScript puede iniciar sesión en cuentas personales, profesionales y educativas, obtener un token de acceso y llamar a la API de Microsoft Graph u otras API que requieran tokens de acceso desde el punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="c82e0-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="c82e0-105">Funcionamiento de esta guía</span><span class="sxs-lookup"><span data-stu-id="c82e0-105">How this guide works</span></span>

![Funcionamiento de la aplicación de ejemplo generada por esta guía](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="c82e0-107">Más información</span><span class="sxs-lookup"><span data-stu-id="c82e0-107">More Information</span></span>

<span data-ttu-id="c82e0-108">La aplicación de ejemplo que se crea con esta guía permite que una aplicación de página única de JavaScript consulte a la API de Microsoft Graph o a una API web que acepte tokens de un punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="c82e0-108">The sample application created by this guide enables a JavaScript SPA to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="c82e0-109">En este escenario, después de que un usuario inicia sesión, se solicita un token de acceso a las solicitudes HTTP a través del encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="c82e0-109">For this scenario, after a user signs-in, an access token is requested and added to HTTP requests via the authorization header.</span></span> <span data-ttu-id="c82e0-110">La adquisición y la renovación de los tokens se realizan por medio de la biblioteca de autenticación de Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c82e0-110">Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="c82e0-111">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="c82e0-111">Libraries</span></span>

<span data-ttu-id="c82e0-112">Esta guía utiliza la siguiente biblioteca:</span><span class="sxs-lookup"><span data-stu-id="c82e0-112">This guide uses the following library:</span></span>

|<span data-ttu-id="c82e0-113">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="c82e0-113">Library</span></span>|<span data-ttu-id="c82e0-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="c82e0-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="c82e0-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="c82e0-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="c82e0-116">Biblioteca de autenticación de Microsoft para la vista preliminar de JavaScript</span><span class="sxs-lookup"><span data-stu-id="c82e0-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="c82e0-117">*msal.js* apunta al *punto de conexión de Azure Active Directory v2*, lo que permite que las cuentas personales, profesionales y educativas inicien sesión y adquieran tokens.</span><span class="sxs-lookup"><span data-stu-id="c82e0-117">*msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens.</span></span> <span data-ttu-id="c82e0-118">El *punto de conexión de Azure Active Directory v2* tiene [algunas limitaciones](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="c82e0-118">The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="c82e0-119">Si solo le interesan las cuentas educativas y profesionales, use *adal.js* en el *punto de conexión V1*.</span><span class="sxs-lookup"><span data-stu-id="c82e0-119">If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*.</span></span> <span data-ttu-id="c82e0-120">Para comprender las diferencias entre los puntos de conexión v1 y v2, lea la [comparación entre v1 y v2](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="c82e0-120">To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
