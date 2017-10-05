---
title: "Introducción a Android en Azure AD v2: prueba | Microsoft Docs"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="ea358-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="ea358-103">Test your code</span></span>

1. <span data-ttu-id="ea358-104">Implemente el código en el dispositivo/emulador.</span><span class="sxs-lookup"><span data-stu-id="ea358-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="ea358-105">Cuando esté listo para realizar la prueba, use una cuenta de Microsoft Azure Active Directory (cuenta profesional) o una cuenta Microsoft (live.com, outlook.com) para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ea358-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="ea358-106">![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="ea358-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="ea358-107">
![Inicio de sesión](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="ea358-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="ea358-108">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="ea358-108">Consent</span></span>
<span data-ttu-id="ea358-109">La primera vez que un usuario inicie sesión en la aplicación, verá una pantalla de consentimiento similar a la siguiente, donde debe aceptar explícitamente:</span><span class="sxs-lookup"><span data-stu-id="ea358-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Consentimiento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="ea358-111">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="ea358-111">Expected results</span></span>
<span data-ttu-id="ea358-112">Debería ver los resultados de una llamada al punto de conexión "me" de la API Graph de Microsoft utilizado para obtener el perfil de usuario: https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="ea358-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="ea358-113">Para ver una lista de los puntos de conexión comunes de Microsoft Graph, consulte este [artículo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="ea358-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="ea358-114">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="ea358-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="ea358-115">La API de Microsoft Graph requiere el ámbito `user.read` para leer el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="ea358-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="ea358-116">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="ea358-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="ea358-117">Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="ea358-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="ea358-118">Por ejemplo, para Microsoft Graph, se requiere el ámbito `Calendars.Read` para enumerar los calendarios del usuario.</span><span class="sxs-lookup"><span data-stu-id="ea358-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="ea358-119">Para tener acceso al calendario del usuario en el contexto de una aplicación, debe agregar el permiso delegado `Calendars.Read` a la información del registro de la aplicación y, a continuación, agregar el ámbito `Calendars.Read` a la llamada a `acquireTokenSilentAsync`.</span><span class="sxs-lookup"><span data-stu-id="ea358-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="ea358-120">Es posible que se pida al usuario algún consentimiento adicional a medida que aumente el número de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="ea358-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
