---
title: "Configuración de la autenticación mediante Google para la aplicación de Servicios de aplicaciones"
description: "Obtenga información acerca de cómo configurar la autenticación mediante Google para la aplicación de Servicios de aplicaciones."
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="842da-103">Configuración de la aplicación Servicio de aplicaciones para usar el inicio de sesión de Google</span><span class="sxs-lookup"><span data-stu-id="842da-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="842da-104">En este tema se muestra cómo configurar Servicio de aplicaciones de Azure para usar Google como proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="842da-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="842da-105">Para llevar a cabo el procedimiento descrito en este tema, debe tener una cuenta de Google asociada a una dirección de correo electrónico verificada.</span><span class="sxs-lookup"><span data-stu-id="842da-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="842da-106">Para crear una cuenta de Google, vaya a [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="842da-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="842da-107"><a name="register"> </a>Registro de la aplicación con Google</span><span class="sxs-lookup"><span data-stu-id="842da-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="842da-108">Inicie sesión en el [Portal de Azure]y vaya a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="842da-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="842da-109">Copie la **URL**, que se utilizará más adelante para configurar la aplicación de Google.</span><span class="sxs-lookup"><span data-stu-id="842da-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="842da-110">Navegue al sitio web de [API de Google](http://go.microsoft.com/fwlink/p/?LinkId=268303), inicie sesión con las credenciales de su cuenta de Google, haga clic en **Create Project** (Crear proyecto), especifique un **nombre de proyecto** y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="842da-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="842da-111">En **Social APIs** (API sociales), haga clic en **Google+ API** (API de Google+") y, luego, en **Enable** (Habilitar).</span><span class="sxs-lookup"><span data-stu-id="842da-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="842da-112">En el panel de navegación izquierdo, haga clic en **Credentials** (Credenciales)  > **OAuth consent screen** (Pantalla de consentimiento de OAuth), seleccione su **dirección de correo electrónico**, escriba un **nombre de producto** y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="842da-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="842da-113">En la pestaña **Credentials** (Credenciales), haga clic en **Create credentials** (Crear credenciales) > **OAuth client ID** (Id. de cliente de OAuth) y seleccione **Web application** (Aplicación web).</span><span class="sxs-lookup"><span data-stu-id="842da-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="842da-114">Pegue la **URL** de App Service que copió anteriormente en **Authorized JavaScript Origins** (Orígenes de JavaScript autorizados) y luego pegue el identificador URI de redirección en **Authorized Redirect URI** (URI de redirección autorizado).</span><span class="sxs-lookup"><span data-stu-id="842da-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="842da-115">El URI de redirección es la dirección URL de la aplicación anexada a la ruta de acceso, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="842da-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="842da-116">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="842da-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="842da-117">Asegúrese de que está utilizando el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="842da-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="842da-118">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="842da-118">Then click **Create**.</span></span>
7. <span data-ttu-id="842da-119">En la siguiente pantalla, tome nota de los valores de id. de cliente y el secreto del cliente.</span><span class="sxs-lookup"><span data-stu-id="842da-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="842da-120">El secreto de cliente es una credencial de seguridad importante,</span><span class="sxs-lookup"><span data-stu-id="842da-120">The client secret is an important security credential.</span></span> <span data-ttu-id="842da-121">No comparta este secreto con nadie ni lo distribuya en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="842da-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="842da-122"><a name="secrets"> </a>Adición de información de Google a la aplicación</span><span class="sxs-lookup"><span data-stu-id="842da-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="842da-123">Vuelva al [Portal de Azure]y vaya a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="842da-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="842da-124">Haga clic en **Configuración** y luego en **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="842da-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="842da-125">Si esta característica no está habilitada, mueva el interruptor a la posición de **activada**.</span><span class="sxs-lookup"><span data-stu-id="842da-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="842da-126">Haga clic en **Google**.</span><span class="sxs-lookup"><span data-stu-id="842da-126">Click **Google**.</span></span> <span data-ttu-id="842da-127">Pegue los valores de identificador de la aplicación y de secreto de la aplicación que obtuvo previamente y habilite opcionalmente los ámbitos que requiere la aplicación.</span><span class="sxs-lookup"><span data-stu-id="842da-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="842da-128">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="842da-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="842da-129">De forma predeterminada, el Servicio de aplicaciones ofrece autenticación pero no restringe el acceso autorizado al contenido del sitio y a las API.</span><span class="sxs-lookup"><span data-stu-id="842da-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="842da-130">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="842da-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="842da-131">(Opcional) Para restringir el acceso al sitio solo a los usuarios autenticados mediante Google, en **Acción necesaria cuando la solicitud no está autenticada**, seleccione **Google**.</span><span class="sxs-lookup"><span data-stu-id="842da-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="842da-132">Esto requiere que todas las solicitudes se autentiquen y que todas las solicitudes no autenticadas se redirijan a Google para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="842da-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="842da-133">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="842da-133">Click **Save**.</span></span>

<span data-ttu-id="842da-134">De este modo ya estará listo para usar Google para realizar la autenticación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="842da-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="842da-135"><a name="related-content"> </a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="842da-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Portal de Azure]: https://portal.azure.com/

