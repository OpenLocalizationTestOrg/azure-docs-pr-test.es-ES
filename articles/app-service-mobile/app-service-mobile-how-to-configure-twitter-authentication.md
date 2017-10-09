---
title: "autenticación de Twitter aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de cómo tooconfigure autenticación de Twitter para la aplicación de servicios de aplicaciones."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="2492d-103">Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Twitter</span><span class="sxs-lookup"><span data-stu-id="2492d-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="2492d-104">Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Twitter como proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2492d-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="2492d-105">procedimiento de hello toocomplete en este tema, debe tener una cuenta de Twitter que tiene un número de dirección y el teléfono de correo electrónico comprobada.</span><span class="sxs-lookup"><span data-stu-id="2492d-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="2492d-106">toocreate una nueva cuenta de Twitter, vaya demasiado<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="2492d-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="2492d-107"><a name="register"></a>Registro de la aplicación con Twitter</span><span class="sxs-lookup"><span data-stu-id="2492d-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="2492d-108">Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="2492d-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="2492d-109">Copie la **Dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="2492d-109">Copy your **URL**.</span></span> <span data-ttu-id="2492d-110">Utilizará este tooconfigure la aplicación de Twitter.</span><span class="sxs-lookup"><span data-stu-id="2492d-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="2492d-111">Navegue toohello [desarrolladores Twitter] de sitio Web, inicie sesión con sus credenciales de cuenta de Twitter y haga clic en **crear una aplicación nueva**.</span><span class="sxs-lookup"><span data-stu-id="2492d-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="2492d-112">Tipo de hello **nombre** y un **descripción** para la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="2492d-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="2492d-113">Pegar en la aplicación **URL** para hello **sitio Web** valor.</span><span class="sxs-lookup"><span data-stu-id="2492d-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="2492d-114">A continuación, en hello **dirección URL de devolución de llamada**, pegue hello **dirección URL de devolución de llamada** que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2492d-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="2492d-115">Se trata de la puerta de enlace de la aplicación móvil anexado con ruta de acceso de hello, */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="2492d-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="2492d-116">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="2492d-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="2492d-117">Asegúrese de que está usando el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2492d-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="2492d-118">En las páginas de hello en parte inferior de hello, lea y acepte los términos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2492d-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="2492d-119">A continuación, haga clic en **Crear aplicación de Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2492d-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="2492d-120">Esta aplicación de hello registros muestra detalles de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2492d-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="2492d-121">Haga clic en hello **configuración** ficha, comprobación de **permitir este toosign de toobe usa de la aplicación con Twitter**, a continuación, haga clic en **configuración de actualización de**.</span><span class="sxs-lookup"><span data-stu-id="2492d-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="2492d-122">Seleccione hello **claves y Tokens de acceso** ficha. Tome nota de los valores de hello de **consumidor clave (API)** y **secreto del consumidor (secreto de API)**.</span><span class="sxs-lookup"><span data-stu-id="2492d-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2492d-123">secreto del consumidor Hello es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="2492d-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="2492d-124">por lo que no debe compartirlo con nadie ni distribuirlo con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="2492d-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="2492d-125"><a name="secrets"></a>Agregar Twitter aplicación tooyour de información</span><span class="sxs-lookup"><span data-stu-id="2492d-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="2492d-126">Nuevo en hello [portal de Azure], navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="2492d-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="2492d-127">Haga clic en **Configuración** y luego en **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="2492d-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="2492d-128">Si Hola autenticación / autorización característica no está habilitada, activar conmutador Hola demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="2492d-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="2492d-129">Haga clic en **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2492d-129">Click **Twitter**.</span></span> <span data-ttu-id="2492d-130">Pegue en hello Id. de aplicación y el secreto de aplicación valores que obtenida anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2492d-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="2492d-131">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2492d-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="2492d-132">De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API.</span><span class="sxs-lookup"><span data-stu-id="2492d-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="2492d-133">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2492d-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="2492d-134">(Opcional) toorestrict acceso tooyour sitio tooonly los usuarios autenticados por Twitter, establecer **tootake de acción cuando no se autentica la solicitud** demasiado**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2492d-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="2492d-135">Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas están tooTwitter redirigida para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="2492d-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="2492d-136">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2492d-136">Click **Save**.</span></span>

<span data-ttu-id="2492d-137">Ya estás listo toouse Twitter para la autenticación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2492d-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="2492d-138"><a name="related-content"></a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="2492d-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[desarrolladores Twitter]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portal de Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
