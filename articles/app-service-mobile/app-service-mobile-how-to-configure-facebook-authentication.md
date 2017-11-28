---
title: "autenticación de Facebook aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure la autenticación de Facebook para la aplicación de servicios de aplicaciones."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="e5992-103">Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Facebook</span><span class="sxs-lookup"><span data-stu-id="e5992-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e5992-104">Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Facebook como proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="e5992-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="e5992-105">procedimiento de hello toocomplete en este tema, debe tener una cuenta de Facebook que tiene una dirección de correo electrónico comprobado y un número de teléfono móvil.</span><span class="sxs-lookup"><span data-stu-id="e5992-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="e5992-106">toocreate una nueva cuenta de Facebook, vaya demasiado[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="e5992-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="e5992-107"><a name="register"></a>Registro de la aplicación con Facebook</span><span class="sxs-lookup"><span data-stu-id="e5992-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="e5992-108">Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="e5992-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="e5992-109">Copie la **Dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="e5992-109">Copy your **URL**.</span></span> <span data-ttu-id="e5992-110">Utilizará este tooconfigure la aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="e5992-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="e5992-111">En otra ventana del explorador, navegue toohello [a los desarrolladores de Facebook] credenciales de cuenta de sitio Web e inicie sesión con su Facebook.</span><span class="sxs-lookup"><span data-stu-id="e5992-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="e5992-112">(Opcional) Si no ya ha registrado, haga clic en **aplicaciones** > **registrar como desarrollador**, a continuación, acepte la política de Hola y siga los pasos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e5992-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="e5992-113">Haga clic en **My Apps** (Mis aplicaciones) > **Add a New App** (Agregar una nueva aplicación) > **Website** (Sitio web) > **Skip and Create App ID** (Omitir y crear id. de aplicación).</span><span class="sxs-lookup"><span data-stu-id="e5992-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="e5992-114">En **nombre para mostrar**, escriba un nombre único para la aplicación, el tipo de su **correo electrónico de contacto**, elija un **categoría** para la aplicación, a continuación, haga clic en **crear Id. de aplicación**y completar la comprobación de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5992-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="e5992-115">Esto le llevará toohello panel del desarrollador para la nueva aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="e5992-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="e5992-116">En "Inicio de sesión de Facebook", haga clic en **Comenzar**.</span><span class="sxs-lookup"><span data-stu-id="e5992-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="e5992-117">Agregar la aplicación **URI de redireccionamiento** demasiado**URI de redireccionamiento válido OAuth**, a continuación, haga clic en **guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="e5992-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e5992-118">La redirección URI es Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="e5992-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="e5992-119">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="e5992-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="e5992-120">Asegúrese de que está usando el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e5992-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="e5992-121">En el panel de navegación izquierdo hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="e5992-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="e5992-122">En hello **secreto de la aplicación** , a continuación, haga clic en **mostrar**, proporcione la contraseña si solicitado, a continuación, tome nota de los valores de hello de **Id. de aplicación** y **secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="e5992-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="e5992-123">Use estos tooconfigure posterior de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="e5992-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e5992-124">secreto de la aplicación Hello es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="e5992-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="e5992-125">No comparta este secreto con nadie ni lo distribuya en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="e5992-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="e5992-126">cuenta de Facebook que era usado tooregister Hola aplicación Hello es un administrador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e5992-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="e5992-127">En este momento, solo los administradores pueden iniciar sesión en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5992-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="e5992-128">tooauthenticate otras cuentas de Facebook, haga clic en **revisión de aplicación** y habilitar **hagan < your--nombre de la aplicación > público** acceso público general tooenable mediante la autenticación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="e5992-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="e5992-129"><a name="secrets"></a>Tooyour aplicación de Facebook agregar información</span><span class="sxs-lookup"><span data-stu-id="e5992-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="e5992-130">Nuevo en hello [portal de Azure], navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="e5992-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="e5992-131">Haga clic en **Configuración** > **Autenticación/autorización** y asegúrese de que **Autenticación de App Service** está **Activada**.</span><span class="sxs-lookup"><span data-stu-id="e5992-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="e5992-132">Haga clic en **Facebook**, pegue en valores de identificador de la aplicación y el secreto de aplicación Hola que obtenida anteriormente, si lo desea habilitar los ámbitos necesarios para la aplicación y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e5992-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="e5992-133">De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API.</span><span class="sxs-lookup"><span data-stu-id="e5992-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="e5992-134">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5992-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="e5992-135">(Opcional) toorestrict acceso tooyour sitio tooonly los usuarios autenticados por Facebook, establecer **tootake de acción cuando no se autentica la solicitud** demasiado**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="e5992-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="e5992-136">Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están tooFacebook redirigida para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e5992-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="e5992-137">Cuando termine de configurar la autenticación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e5992-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="e5992-138">Ya estás listo toouse Facebook para la autenticación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5992-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="e5992-139"><a name="related-content"></a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="e5992-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[a los desarrolladores de Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portal de Azure]: https://portal.azure.com/
