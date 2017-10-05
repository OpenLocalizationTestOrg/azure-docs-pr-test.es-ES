---
title: "Introducción al escritorio de Windows en Azure AD v2: prueba | Microsoft Docs"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="72048-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="72048-103">Test your code</span></span>

<span data-ttu-id="72048-104">Para probar la aplicación, presione `F5` para ejecutar el proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72048-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="72048-105">Aparecerá la ventana principal:</span><span class="sxs-lookup"><span data-stu-id="72048-105">Your Main Window should appear:</span></span>

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="72048-107">Cuando esté listo para realizar la prueba, haga clic en *Call Microsoft Graph API* (Llamar a la API Graph de Microsoft) y use una cuenta de Microsoft Azure Active Directory (cuenta profesional) o una cuenta Microsoft (live.com, outlook.com) para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="72048-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="72048-108">Si es la primera vez, verá una ventana que solicita al usuario que inicie sesión:</span><span class="sxs-lookup"><span data-stu-id="72048-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Inicio de sesión](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="72048-110">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="72048-110">Consent</span></span>
<span data-ttu-id="72048-111">La primera vez que inicie sesión en la aplicación, verá una pantalla de consentimiento similar a la siguiente, donde debe aceptar explícitamente:</span><span class="sxs-lookup"><span data-stu-id="72048-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Pantalla de consentimiento](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="72048-113">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="72048-113">Expected results</span></span>
<span data-ttu-id="72048-114">Debería ver la información de perfil de usuario devuelta por la llamada de API Graph de Microsoft en la pantalla de resultados de la llamada de API.</span><span class="sxs-lookup"><span data-stu-id="72048-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="72048-115">También debería aparecer información básica sobre el token obtenido a través de `AcquireTokenAsync` o `AcquireTokenSilentAsync` en el cuadro de información de token:</span><span class="sxs-lookup"><span data-stu-id="72048-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="72048-116">Propiedad</span><span class="sxs-lookup"><span data-stu-id="72048-116">Property</span></span>  |<span data-ttu-id="72048-117">Formato</span><span class="sxs-lookup"><span data-stu-id="72048-117">Format</span></span>  |<span data-ttu-id="72048-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="72048-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="72048-119">Nombre</span><span class="sxs-lookup"><span data-stu-id="72048-119">Name</span></span> | <span data-ttu-id="72048-120">{Nombre completo del usuario}</span><span class="sxs-lookup"><span data-stu-id="72048-120">{User Full name}</span></span> |<span data-ttu-id="72048-121">Nombre y apellido del usuario</span><span class="sxs-lookup"><span data-stu-id="72048-121">The user’s first and last name</span></span>|
|<span data-ttu-id="72048-122">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="72048-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="72048-123">El nombre de usuario utilizado para identificar al usuario</span><span class="sxs-lookup"><span data-stu-id="72048-123">The username used to identify the user</span></span>|
|<span data-ttu-id="72048-124">Token Expires</span><span class="sxs-lookup"><span data-stu-id="72048-124">Token Expires</span></span> |<span data-ttu-id="72048-125">{FechaHora}</span><span class="sxs-lookup"><span data-stu-id="72048-125">{DateTime}</span></span>         |<span data-ttu-id="72048-126">La hora en que expira el token.</span><span class="sxs-lookup"><span data-stu-id="72048-126">The time on which the token expires.</span></span> <span data-ttu-id="72048-127">MSAL ampliará la fecha de expiración para que renueve el token cuando sea necesario</span><span class="sxs-lookup"><span data-stu-id="72048-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="72048-128">Access token</span><span class="sxs-lookup"><span data-stu-id="72048-128">Access token</span></span> |<span data-ttu-id="72048-129">{Cadena}</span><span class="sxs-lookup"><span data-stu-id="72048-129">{String}</span></span>         |<span data-ttu-id="72048-130">La cadena de token enviada que se hará llegar a las solicitudes HTTP que requieran un encabezado de autorización</span><span class="sxs-lookup"><span data-stu-id="72048-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="72048-131">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="72048-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="72048-132">API Graph requiere el ámbito `user.read` para leer el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="72048-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="72048-133">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="72048-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="72048-134">Otras API Graph, así como las API personalizadas para el servidor back-end, requieren ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="72048-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="72048-135">Por ejemplo, para Graph, `Calendars.Read` es necesario para elaborar un listado de los calendarios del usuario.</span><span class="sxs-lookup"><span data-stu-id="72048-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="72048-136">Para tener acceso al calendario del usuario en un contexto de una aplicación, debe agregar la información de registro de la aplicación delegada de `Calendars.Read` y, a continuación, agregar `Calendars.Read` a la llamada `AcquireTokenAsync`.</span><span class="sxs-lookup"><span data-stu-id="72048-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="72048-137">Es posible que se pida al usuario algún consentimiento adicional a medida que aumente el número de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="72048-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



