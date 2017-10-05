---
title: "Introducción a iOS en Azure AD v2: prueba | Microsoft Docs"
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
ms.openlocfilehash: 4a88096d2b0a23708acdbc1798eac528599b4f71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
## <a name="test-querying-the-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="6460c-103">Prueba de consultas de la API de Microsoft Graph desde la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="6460c-103">Test querying the Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="6460c-104">Presione `Command` + `R` para ejecutar el código en el simulador.</span><span class="sxs-lookup"><span data-stu-id="6460c-104">Press `Command` + `R` to run the code in the simulator.</span></span>

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="6460c-106">Cuando esté listo para ejecutar la prueba, pulse *"Call Microsoft Graph API"* (Llamar a la API de Microsoft Graph) y se le pedirá que escriba su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="6460c-106">When you're ready to test, tap *‘Call Microsoft Graph API’* and you will be prompted to type your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="6460c-107">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="6460c-107">Consent</span></span>
<span data-ttu-id="6460c-108">La primera vez que inicie sesión en la aplicación, verá una pantalla de consentimiento similar a la siguiente, donde debe aceptar explícitamente:</span><span class="sxs-lookup"><span data-stu-id="6460c-108">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Pantalla de consentimiento](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="6460c-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="6460c-110">Expected results</span></span>
<span data-ttu-id="6460c-111">Debería ver la información del perfil de usuario devuelta por la llamada a la API de Microsoft Graph en la sección *Registro*.</span><span class="sxs-lookup"><span data-stu-id="6460c-111">You should see user profile information returned by the Microsoft Graph API call in the *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="6460c-112">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="6460c-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="6460c-113">La API de Microsoft Graph requiere el ámbito `user.read` para leer el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="6460c-113">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="6460c-114">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="6460c-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="6460c-115">Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="6460c-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="6460c-116">Por ejemplo, para Microsoft Graph, se requiere el ámbito `Calendars.Read` para enumerar los calendarios del usuario.</span><span class="sxs-lookup"><span data-stu-id="6460c-116">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="6460c-117">Para tener acceso al calendario del usuario en el contexto de una aplicación, debe agregar el permiso delegado `Calendars.Read` a la información del registro de la aplicación y, a continuación, agregar el ámbito `Calendars.Read` a la llamada a `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="6460c-117">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="6460c-118">Es posible que se pida al usuario algún consentimiento adicional a medida que aumente el número de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="6460c-118">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



