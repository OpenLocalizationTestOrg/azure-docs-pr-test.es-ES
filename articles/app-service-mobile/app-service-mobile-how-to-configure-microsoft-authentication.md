---
title: "autenticación de Microsoft Account aaaHow tooconfigure para la aplicación de servicios de aplicaciones"
description: "Obtenga información acerca de la autenticación de Microsoft Account tooconfigure para la aplicación de servicios de aplicaciones."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="f4ac8-103">Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Account de Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4ac8-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="f4ac8-104">Este tema muestra cómo toouse de servicio de aplicaciones de Azure tooconfigure Account de Microsoft como un proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="f4ac8-105"><a name="register-microsoft-account"></a>Registro de la aplicación con la cuenta de Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4ac8-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="f4ac8-106">Inicie sesión en toohello [portal de Azure]y navegar por la aplicación tooyour.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="f4ac8-107">Copia la **dirección URL**, que posteriormente utiliza tooconfigure la aplicación con Microsoft Account.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="f4ac8-108">Navegue toohello [mis aplicaciones] página Hola Microsoft Account Developer Center e inicie sesión con su cuenta de Microsoft, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="f4ac8-109">Haga clic en **Agregar una aplicación**, escriba el nombre de la aplicación y haga clic en **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="f4ac8-110">Tome nota de hello **Id. de aplicación**, ya que la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="f4ac8-111">En "Plataformas", haga clic en **Agregar plataforma** y seleccione "Web".</span><span class="sxs-lookup"><span data-stu-id="f4ac8-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="f4ac8-112">En "URI de redireccionamiento" suministro Hola punto de conexión para la aplicación, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f4ac8-113">La redirección URI es Hola URL de la aplicación en la ruta de acceso de hello, le anexada */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="f4ac8-114">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="f4ac8-115">Asegúrese de que está usando el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="f4ac8-116">En "Secretos de aplicación", haga clic en **Generar nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="f4ac8-117">Tome nota del valor de Hola que aparece.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-117">Make note of hello value that appears.</span></span> <span data-ttu-id="f4ac8-118">Una vez que abandona la página de hello, no se vuelva a mostrar.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f4ac8-119">contraseña de Hello es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-119">hello password is an important security credential.</span></span> <span data-ttu-id="f4ac8-120">No comparta Hola contraseña con nadie ni distribuir dentro de una aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="f4ac8-121"><a name="secrets"></a>Agregar una cuenta Microsoft información tooyour aplicación de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f4ac8-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="f4ac8-122">Nuevo en hello [portal de Azure], navegue tooyour aplicación, haga clic en **configuración** > **autenticación / autorización**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="f4ac8-123">Si Hola autenticación / autorización característica no está habilitada, conéctelo **en**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="f4ac8-124">Haga clic en **Cuenta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="f4ac8-125">Pegue en valores de identificador de la aplicación y la contraseña de Hola que obtenida anteriormente y, opcionalmente, habilite los ámbitos de que la aplicación requiere.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="f4ac8-126">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="f4ac8-127">De forma predeterminada, servicio de aplicaciones proporciona autenticación pero no restringe el contenido de sitio de tooyour de acceso no autorizado y API.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="f4ac8-128">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="f4ac8-129">(Opcional) toorestrict acceso tooyour tooonly los usuarios del sitio autenticados la cuenta de Microsoft, establezca **tootake de acción cuando no se autentica la solicitud** demasiado**Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="f4ac8-130">Esto exige que todas las solicitudes de autenticación y todas las solicitudes no autenticadas se redirigen tooMicrosoft cuenta para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="f4ac8-131">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-131">Click **Save**.</span></span>

<span data-ttu-id="f4ac8-132">Ya estás listo toouse Account de Microsoft para la autenticación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4ac8-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="f4ac8-133"><a name="related-content"></a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="f4ac8-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[mis aplicaciones]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portal de Azure]: https://portal.azure.com/
