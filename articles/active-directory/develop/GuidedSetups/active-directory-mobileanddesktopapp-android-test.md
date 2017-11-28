---
title: "aaaAzure AD v2 Android Introducción - prueba | Documentos de Microsoft"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="7ce6e-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="7ce6e-103">Test your code</span></span>

1. <span data-ttu-id="7ce6e-104">Implementar el código tooyour/emulador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="7ce6e-105">Cuando esté listo tootest, use Microsoft Azure Active Directory (cuenta profesional) o un toosign de cuenta de Microsoft Account (live.com, outlook.com) en.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="7ce6e-106">![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="7ce6e-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="7ce6e-107">
![Inicio de sesión](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="7ce6e-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="7ce6e-108">Consentimiento</span><span class="sxs-lookup"><span data-stu-id="7ce6e-108">Consent</span></span>
<span data-ttu-id="7ce6e-109">Hello primera vez que un usuario inicia sesión en la aplicación tooyour, le presentará una pantalla de consentimiento similar toohello siguiente, donde deben aceptar tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="7ce6e-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Consentimiento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="7ce6e-111">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="7ce6e-111">Expected results</span></span>
<span data-ttu-id="7ce6e-112">Debería ver resultados de Hola de un tooMicrosoft de llamada de API Graph 'me' punto de conexión usa el perfil de usuario de hello tootooobtain - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="7ce6e-113">Para ver una lista de los puntos de conexión comunes de Microsoft Graph, consulte este [artículo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="7ce6e-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="7ce6e-114">Más información sobre los ámbitos y permisos delegados</span><span class="sxs-lookup"><span data-stu-id="7ce6e-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="7ce6e-115">Hola Microsoft Graph API requiere hello `user.read` definir el ámbito de perfil de usuario de tooread Hola.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="7ce6e-116">Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="7ce6e-117">Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="7ce6e-118">Por ejemplo, para Microsoft Graph, Hola ámbito `Calendars.Read` es calendarios del usuario requiere toolist Hola.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="7ce6e-119">En orden tooaccess Hola calendario del usuario en un contexto de una aplicación, deberá tooadd Hola `Calendars.Read` delegado información del registro de aplicación de permiso toohello y, a continuación, agregue hello `Calendars.Read` toohello ámbito `acquireTokenSilentAsync` llamar.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="7ce6e-120">usuario de Hola se solicitarán consentimientos adicionales a medida que aumente el número de Hola de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="7ce6e-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
