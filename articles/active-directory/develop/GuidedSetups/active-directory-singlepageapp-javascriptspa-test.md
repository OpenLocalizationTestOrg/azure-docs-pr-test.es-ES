---
title: aaaAzure AD v2 JS SPA interactiva Setup - prueba | Documentos de Microsoft
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="f7a71-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="f7a71-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="f7a71-104">Pruebas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7a71-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="f7a71-105">Si se utiliza Visual Studio, presione `F5` toorun el proyecto: explorador Hola se abre y le dirige demasiado*http://localhost: {port}* donde verá hello *llamadas API de Microsoft Graph* botón.</span><span class="sxs-lookup"><span data-stu-id="f7a71-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="f7a71-106">Pruebas con Python u otro servidor web</span><span class="sxs-lookup"><span data-stu-id="f7a71-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="f7a71-107">Si no se utiliza Visual Studio, asegúrese de que el servidor web se inicia y se configura el puerto TCP de toolisten tooa según Hola carpeta que contiene su *index.html* archivo.</span><span class="sxs-lookup"><span data-stu-id="f7a71-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="f7a71-108">Para Python, puede iniciar la escucha toohello puerto mediante la ejecución de Hola en comando hello prompt / terminal, desde la carpeta de la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="f7a71-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="f7a71-109">A continuación, abra el Explorador de Hola y escriba *http://localhost: 8080* o *http://localhost: {port}* : si hello *puerto* corresponde puerto toohello que es el servidor web escuchar.</span><span class="sxs-lookup"><span data-stu-id="f7a71-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="f7a71-110">Debería ver contenido de saludo de la página index.html con hello *llamadas API de Microsoft Graph* botón.</span><span class="sxs-lookup"><span data-stu-id="f7a71-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="f7a71-111">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f7a71-111">Test your application</span></span>

<span data-ttu-id="f7a71-112">Después de explorador Hola carga su *index.html*, haga clic en hello *llamadas API de Microsoft Graph* botón.</span><span class="sxs-lookup"><span data-stu-id="f7a71-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="f7a71-113">Si se trata de hello primera vez, Hola explorador redirecciones toohello v2 de Microsoft Azure Active Directory extremo, que te encuentres solicita toosign en.</span><span class="sxs-lookup"><span data-stu-id="f7a71-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Captura de pantalla de ejemplo](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="f7a71-115">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="f7a71-115">Consent</span></span>
<span data-ttu-id="f7a71-116">Hello primera vez que inicie sesión en la aplicación tooyour, se le presentará una consentimiento pantalla similar toohello a continuación, en las que necesite tooaccept:</span><span class="sxs-lookup"><span data-stu-id="f7a71-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Pantalla de consentimiento](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="f7a71-118">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="f7a71-118">Expected results</span></span>
<span data-ttu-id="f7a71-119">Debería ver la información de perfil de usuario devuelto por hello respuesta a llamadas de API Graph de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f7a71-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Results](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="f7a71-121">También verá información básica sobre el token de hello adquirido en hello *Token de acceso* y *notificaciones del Token de Id. de* cuadros.</span><span class="sxs-lookup"><span data-stu-id="f7a71-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="f7a71-122">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="f7a71-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="f7a71-123">Hola Microsoft Graph API requiere hello `user.read` definir el ámbito de perfil de usuario de tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="f7a71-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="f7a71-124">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="f7a71-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="f7a71-125">Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="f7a71-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="f7a71-126">Por ejemplo, para Microsoft Graph, Hola ámbito `Calendars.Read` es calendarios del usuario requiere toolist Hola.</span><span class="sxs-lookup"><span data-stu-id="f7a71-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="f7a71-127">En orden tooaccess Hola calendario del usuario en el contexto de Hola de una aplicación, deberá tooadd Hola `Calendars.Read` delegado información del registro de aplicación de permiso toohello y, a continuación, agregue hello `Calendars.Read` toohello ámbito `acquireTokenSilent` llamar.</span><span class="sxs-lookup"><span data-stu-id="f7a71-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="f7a71-128">usuario de Hola se solicitarán consentimientos adicionales a medida que aumente el número de Hola de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="f7a71-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="f7a71-129">Si un API de back-end no requiere un ámbito (no recomendado), puede usar hello `clientId` como ámbito de Hola Hola `acquireTokenSilent` o `acquireTokenRedirect` llamadas.</span><span class="sxs-lookup"><span data-stu-id="f7a71-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
