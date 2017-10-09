---
title: "aaaAzure AD v2 iOS Introducción - prueba | Documentos de Microsoft"
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="ba46d-103">Probar consultas Hola API Graph de Microsoft desde su aplicación de iOS</span><span class="sxs-lookup"><span data-stu-id="ba46d-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="ba46d-104">Presione `Command`  +  `R` toorun código de hello en el simulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba46d-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="ba46d-106">Cuando esté listo tootest, pulse *'Llamar a las API de Graph de Microsoft'* y será tootype solicitada su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="ba46d-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="ba46d-107">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="ba46d-107">Consent</span></span>
<span data-ttu-id="ba46d-108">Hello primera vez que inicie sesión en la aplicación tooyour, le presentará una pantalla de consentimiento similar toohello a continuación, en los que necesite tooexplicitly acepte:</span><span class="sxs-lookup"><span data-stu-id="ba46d-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Pantalla de consentimiento](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="ba46d-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="ba46d-110">Expected results</span></span>
<span data-ttu-id="ba46d-111">Debería ver la información de perfil de usuario devuelto por la llamada de API de Microsoft Graph Hola Hola *registro* sección.</span><span class="sxs-lookup"><span data-stu-id="ba46d-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="ba46d-112">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="ba46d-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="ba46d-113">Hola Microsoft Graph API requiere hello `user.read` definir el ámbito de perfil de usuario de tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="ba46d-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="ba46d-114">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="ba46d-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="ba46d-115">Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="ba46d-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="ba46d-116">Por ejemplo, para Microsoft Graph, Hola ámbito `Calendars.Read` es calendarios del usuario requiere toolist Hola.</span><span class="sxs-lookup"><span data-stu-id="ba46d-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="ba46d-117">En orden tooaccess Hola calendario del usuario en un contexto de una aplicación, deberá tooadd Hola `Calendars.Read` delegado información del registro de aplicación de permiso toohello y, a continuación, agregue hello `Calendars.Read` toohello ámbito `acquireTokenSilent` llamar.</span><span class="sxs-lookup"><span data-stu-id="ba46d-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="ba46d-118">usuario de Hola se solicitarán consentimientos adicionales a medida que aumente el número de Hola de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="ba46d-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



