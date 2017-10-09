---
title: "aaaAzure AD v2 JS SPA guiada por el programa de instalación: Introducción | Documentos de Microsoft"
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
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="b8739-103">Hola llamada API de Graph de Microsoft desde una aplicación de página única (SPA) de JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8739-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="b8739-104">Esta guía muestra cómo una aplicación de página única (SPA) de JavaScript puede iniciar sesión en el trabajo personal y las cuentas de la escuela, obtener un token de acceso y llamar a Hola API Graph de Microsoft u Hola a otras API que requieren tokens de acceso de punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="b8739-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="b8739-105">Funcionamiento de esta guía</span><span class="sxs-lookup"><span data-stu-id="b8739-105">How this guide works</span></span>

![Cómo funciona la aplicación de ejemplo de Hola generado por esta guía](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="b8739-107">Más información</span><span class="sxs-lookup"><span data-stu-id="b8739-107">More Information</span></span>

<span data-ttu-id="b8739-108">aplicación de ejemplo de Hola creada por esta guía permite un Hola de tooquery SPA JavaScript API Graph de Microsoft o una API Web que acepta los tokens de punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="b8739-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="b8739-109">En este escenario, después de que un usuario inicia sesión, un token de acceso es que las solicitudes de tooHTTP solicitado y agregadas mediante el encabezado de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8739-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="b8739-110">Renovación y adquisición de tokens se controlan mediante Hola biblioteca de autenticación de Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="b8739-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="b8739-111">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="b8739-111">Libraries</span></span>

<span data-ttu-id="b8739-112">Esta guía usa Hola después de la biblioteca:</span><span class="sxs-lookup"><span data-stu-id="b8739-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="b8739-113">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="b8739-113">Library</span></span>|<span data-ttu-id="b8739-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="b8739-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="b8739-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="b8739-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="b8739-116">Biblioteca de autenticación de Microsoft para la vista preliminar de JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8739-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="b8739-117">*MSAL.js* Hola destinos *punto de conexión de Azure Active Directory v2* -que permite toosign cuentas personales, educativa y profesionales en y adquirir tokens.</span><span class="sxs-lookup"><span data-stu-id="b8739-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="b8739-118">Hola *punto de conexión de Azure Active Directory v2* tiene [algunas limitaciones](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b8739-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="b8739-119">Si está interesado en cuentas profesionales y educativas, use *adal.js* hello y *V1 extremo*.</span><span class="sxs-lookup"><span data-stu-id="b8739-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="b8739-120">toounderstand diferencias entre los extremos de v1 y v2 Hola leen hello [v1 y v2 comparación](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="b8739-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
