---
title: "aaaAzure AD v2 Windows Desktop introducción - prueba | Documentos de Microsoft"
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="d70f9-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="d70f9-103">Test your code</span></span>

<span data-ttu-id="d70f9-104">En orden tootest para la aplicación, presione `F5` toorun el proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d70f9-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="d70f9-105">Aparecerá la ventana principal:</span><span class="sxs-lookup"><span data-stu-id="d70f9-105">Your Main Window should appear:</span></span>

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="d70f9-107">Cuando esté listo tootest, haga clic en *llamadas API de Microsoft Graph* y usar Microsoft Azure Active Directory (cuenta profesional) o un toosign de cuenta de Microsoft Account (live.com, outlook.com) en.</span><span class="sxs-lookup"><span data-stu-id="d70f9-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="d70f9-108">Es Hola primera vez, verá una ventana solicitando al usuario toosign en:</span><span class="sxs-lookup"><span data-stu-id="d70f9-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Inicio de sesión](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="d70f9-110">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="d70f9-110">Consent</span></span>
<span data-ttu-id="d70f9-111">Hello primera vez que inicie sesión en la aplicación tooyour, le presentará una pantalla de consentimiento similar toohello a continuación, en los que necesite tooexplicitly acepte:</span><span class="sxs-lookup"><span data-stu-id="d70f9-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Pantalla de consentimiento](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="d70f9-113">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="d70f9-113">Expected results</span></span>
<span data-ttu-id="d70f9-114">Debería ver la información de perfil de usuario devuelto por llamada de API de Microsoft Graph hello en pantalla de resultados de llamar a la API de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="d70f9-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="d70f9-115">También debe ver información básica sobre el token de hello adquirido a través de `AcquireTokenAsync` o `AcquireTokenSilentAsync` en cuadro de información de símbolo (token) de hello:</span><span class="sxs-lookup"><span data-stu-id="d70f9-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="d70f9-116">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d70f9-116">Property</span></span>  |<span data-ttu-id="d70f9-117">Formato</span><span class="sxs-lookup"><span data-stu-id="d70f9-117">Format</span></span>  |<span data-ttu-id="d70f9-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="d70f9-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="d70f9-119">Nombre</span><span class="sxs-lookup"><span data-stu-id="d70f9-119">Name</span></span> | <span data-ttu-id="d70f9-120">{Nombre completo del usuario}</span><span class="sxs-lookup"><span data-stu-id="d70f9-120">{User Full name}</span></span> |<span data-ttu-id="d70f9-121">usuario de Hola y el apellido nombre</span><span class="sxs-lookup"><span data-stu-id="d70f9-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="d70f9-122">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="d70f9-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="d70f9-123">nombre de usuario de Hello usado usuario de hello tooidentify</span><span class="sxs-lookup"><span data-stu-id="d70f9-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="d70f9-124">Token Expires</span><span class="sxs-lookup"><span data-stu-id="d70f9-124">Token Expires</span></span> |<span data-ttu-id="d70f9-125">{FechaHora}</span><span class="sxs-lookup"><span data-stu-id="d70f9-125">{DateTime}</span></span>         |<span data-ttu-id="d70f9-126">hora de Hello en qué Hola expira el token.</span><span class="sxs-lookup"><span data-stu-id="d70f9-126">hello time on which hello token expires.</span></span> <span data-ttu-id="d70f9-127">MSAL extenderá la fecha de expiración de hello automáticamente al renovar el token de hello cuando sea necesario</span><span class="sxs-lookup"><span data-stu-id="d70f9-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="d70f9-128">Access token</span><span class="sxs-lookup"><span data-stu-id="d70f9-128">Access token</span></span> |<span data-ttu-id="d70f9-129">{Cadena}</span><span class="sxs-lookup"><span data-stu-id="d70f9-129">{String}</span></span>         |<span data-ttu-id="d70f9-130">cadena de token de Hello enviados que se enviarán las solicitudes de tooHTTP que requieren un encabezado de autorización</span><span class="sxs-lookup"><span data-stu-id="d70f9-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="d70f9-131">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="d70f9-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="d70f9-132">API Graph requiere hello `user.read` ámbito tooread perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="d70f9-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="d70f9-133">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="d70f9-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="d70f9-134">Otras API Graph, así como las API personalizadas para el servidor back-end, requieren ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="d70f9-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="d70f9-135">Por ejemplo, para el gráfico, `Calendars.Read` es calendarios del usuario toolist necesarios.</span><span class="sxs-lookup"><span data-stu-id="d70f9-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="d70f9-136">En orden tooaccess Hola calendario del usuario en un contexto de una aplicación, deberá tooadd `Calendars.Read` delegado información del registro de la aplicación y, a continuación, agregue `Calendars.Read` toohello `AcquireTokenAsync` llamar.</span><span class="sxs-lookup"><span data-stu-id="d70f9-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="d70f9-137">Se pedirá el nombre de usuario para consentimientos adicionales a medida que aumente el número de Hola de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="d70f9-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



