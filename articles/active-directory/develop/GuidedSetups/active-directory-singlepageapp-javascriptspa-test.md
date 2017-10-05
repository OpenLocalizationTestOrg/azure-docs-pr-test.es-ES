---
title: "Configuración de SPA de JS en Azure AD v2: prueba | Microsoft Docs"
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
ms.openlocfilehash: c888760ab311e8ac08b1e625bb837f91047db645
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
## <a name="test-your-code"></a><span data-ttu-id="28260-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="28260-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="28260-104">Pruebas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="28260-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="28260-105">Si usa Visual Studio, presione `F5` para ejecutar el proyecto: el explorador se abre y le lleva a *http://localhost:{puerto}*, donde puede ver el botón *Llamar a API de Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="28260-105">If you are using Visual Studio, press `F5` to run your project: the browser opens and directs you to *http://localhost:{port}* where you see the *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="28260-106">Pruebas con Python u otro servidor web</span><span class="sxs-lookup"><span data-stu-id="28260-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="28260-107">Si no se utiliza Visual Studio, asegúrese de que se inicia el servidor web y de que está configurado para escuchar a un puerto TCP en función de la carpeta con el archivo *index.html*.</span><span class="sxs-lookup"><span data-stu-id="28260-107">If you are not using Visual Studio, make sure your web server is started and it is configured to listen to a TCP port based on the folder containing your *index.html* file.</span></span> <span data-ttu-id="28260-108">En el caso de Python, puede empezar a escuchar el puerto mediante su ejecución en el terminal o símbolo del sistema, en la carpeta de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="28260-108">For Python, you can start listening to the port by running the in the command prompt/ terminal, from the app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="28260-109">A continuación, abra el explorador y escriba *http://localhost:8080* o *http://localhost:{puerto}*: donde el *puerto* corresponde al puerto que está escuchando el servidor web.</span><span class="sxs-lookup"><span data-stu-id="28260-109">Then, open the browser and type *http://localhost:8080* or *http://localhost:{port}* - where the *port* corresponds to the port that your web server is listening to.</span></span> <span data-ttu-id="28260-110">Debería ver el contenido de su página index.html con el botón *Llamar a API de Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="28260-110">You should see the contents of your index.html page with the *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="28260-111">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="28260-111">Test your application</span></span>

<span data-ttu-id="28260-112">Una vez que el explorador cargue su página *index.html*, haga clic en el botón *Llamar a API de Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="28260-112">After the browser loads your *index.html*, click the *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="28260-113">Si se trata de la primera vez, el explorador le redirige al punto de conexión v2 de Microsoft Azure Active Directory, donde se le pide que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="28260-113">If this is the first time, the browser redirects you to the Microsoft Azure Active Directory v2 endpoint, where you are  prompted to sign in.</span></span>
 
![Captura de pantalla de ejemplo](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="28260-115">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="28260-115">Consent</span></span>
<span data-ttu-id="28260-116">La primera vez que inicie sesión en la aplicación, verá una pantalla de consentimiento similar a la siguiente, donde debe aceptar:</span><span class="sxs-lookup"><span data-stu-id="28260-116">The very first time you sign in to your application, you are presented with a consent screen similar to the following, where you need to accept:</span></span>

 ![Pantalla de consentimiento](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="28260-118">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="28260-118">Expected results</span></span>
<span data-ttu-id="28260-119">Debería ver la información del perfil de usuario devuelta por la respuesta a la llamada a la API de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="28260-119">You should see user profile information returned by the Microsoft Graph API call response.</span></span>
 
 ![Results](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="28260-121">También verá información básica sobre el token adquirido en los cuadros *Token de acceso* e *ID Token Claims* (Notificaciones de token de identificador).</span><span class="sxs-lookup"><span data-stu-id="28260-121">You also see basic information about the token acquired in the *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="28260-122">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="28260-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="28260-123">La API de Microsoft Graph requiere el ámbito `user.read` para leer el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="28260-123">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="28260-124">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="28260-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="28260-125">Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="28260-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="28260-126">Por ejemplo, para Microsoft Graph, se requiere el ámbito `Calendars.Read` para enumerar los calendarios del usuario.</span><span class="sxs-lookup"><span data-stu-id="28260-126">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="28260-127">Para tener acceso al calendario del usuario en el contexto de una aplicación, debe agregar el permiso delegado `Calendars.Read` a la información del registro de la aplicación y, a continuación, agregar el ámbito `Calendars.Read` a la llamada a `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="28260-127">In order to access the user’s calendar in the context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="28260-128">Es posible que se pida al usuario algún consentimiento adicional a medida que aumente el número de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="28260-128">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<span data-ttu-id="28260-129">Si una API de back-end no requiere un ámbito (no se recomienda), puede usar el valor de `clientId` como ámbito en las llamadas a `acquireTokenSilent` o `acquireTokenRedirect`.</span><span class="sxs-lookup"><span data-stu-id="28260-129">If a backend API does not require a scope (not recommended), you can use the `clientId` as the scope in the `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
