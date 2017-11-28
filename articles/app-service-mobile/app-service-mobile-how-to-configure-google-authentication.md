---
title: "autenticación de Google aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure autenticación de Google para la aplicación de servicios de aplicaciones."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="53215-103">Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Google</span><span class="sxs-lookup"><span data-stu-id="53215-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="53215-104">Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Google como proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="53215-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="53215-105">procedimiento de hello toocomplete en este tema, debe tener una cuenta de Google que tiene una dirección de correo electrónico comprobada.</span><span class="sxs-lookup"><span data-stu-id="53215-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="53215-106">toocreate una nueva cuenta de Google, vaya demasiado[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="53215-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="53215-107"><a name="register"></a>Registro de la aplicación con Google</span><span class="sxs-lookup"><span data-stu-id="53215-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="53215-108">Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="53215-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="53215-109">Copia la **dirección URL**, que use tooconfigure posterior de la aplicación de Google.</span><span class="sxs-lookup"><span data-stu-id="53215-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="53215-110">Navegue toohello [API de Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) sitio Web, inicie sesión con sus credenciales de cuenta de Google, haga clic en **crear proyecto**, proporcionar un **nombre del proyecto**, a continuación, haga clic en  **Crear**.</span><span class="sxs-lookup"><span data-stu-id="53215-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="53215-111">En **Social APIs** (API sociales), haga clic en **Google+ API** (API de Google+") y, luego, en **Enable** (Habilitar).</span><span class="sxs-lookup"><span data-stu-id="53215-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="53215-112">Hola a la izquierda, **credenciales** > **pantalla de consentimiento de OAuth**, a continuación, seleccione la **dirección de correo electrónico**, escriba un **Product Name**y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="53215-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="53215-113">Hola **credenciales** , haga clic en **crear credenciales** > **identificador de cliente OAuth**, a continuación, seleccione **aplicación Web**.</span><span class="sxs-lookup"><span data-stu-id="53215-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="53215-114">Pegar Hola servicio de aplicaciones **URL** que copió anteriormente en **orígenes de JavaScript autorizados**, a continuación, pegue la redirección URI en **URI de redireccionamiento autorizados**.</span><span class="sxs-lookup"><span data-stu-id="53215-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="53215-115">Hola redirección URI es Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="53215-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="53215-116">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="53215-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="53215-117">Asegúrese de que está usando el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="53215-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="53215-118">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="53215-118">Then click **Create**.</span></span>
7. <span data-ttu-id="53215-119">En la siguiente pantalla de bienvenida, tome nota de los valores de hello de cliente de Hola secreto de cliente y el identificador.</span><span class="sxs-lookup"><span data-stu-id="53215-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="53215-120">secreto del cliente de Hello es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="53215-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="53215-121">No comparta este secreto con nadie ni lo distribuya en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="53215-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="53215-122"><a name="secrets"></a>Tooyour aplicación de Google agregar información</span><span class="sxs-lookup"><span data-stu-id="53215-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="53215-123">Nuevo en hello [portal de Azure], navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="53215-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="53215-124">Haga clic en **Configuración** y luego en **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="53215-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="53215-125">Si Hola autenticación / autorización característica no está habilitada, activar conmutador Hola demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="53215-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="53215-126">Haga clic en **Google**.</span><span class="sxs-lookup"><span data-stu-id="53215-126">Click **Google**.</span></span> <span data-ttu-id="53215-127">Pegue en valores de identificador de la aplicación y el secreto de aplicación Hola que obtenida anteriormente y, opcionalmente, habilite los ámbitos de que la aplicación requiere.</span><span class="sxs-lookup"><span data-stu-id="53215-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="53215-128">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="53215-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="53215-129">De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API.</span><span class="sxs-lookup"><span data-stu-id="53215-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="53215-130">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="53215-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="53215-131">(Opcional) toorestrict acceso tooyour sitio tooonly los usuarios autenticados por Google, establecer **tootake de acción cuando no se autentica la solicitud** demasiado**Google**.</span><span class="sxs-lookup"><span data-stu-id="53215-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="53215-132">Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están tooGoogle redirigida para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="53215-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="53215-133">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="53215-133">Click **Save**.</span></span>

<span data-ttu-id="53215-134">Ya estás listo toouse Google para la autenticación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="53215-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="53215-135"><a name="related-content"></a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="53215-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal de Azure]: https://portal.azure.com/

