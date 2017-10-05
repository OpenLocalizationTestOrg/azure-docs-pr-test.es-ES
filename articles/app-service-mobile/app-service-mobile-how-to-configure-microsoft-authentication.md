---
title: "Configuración de la autenticación mediante la cuenta Microsoft para la aplicación de Servicios de aplicaciones"
description: "Obtenga información acerca de cómo configurar la autenticación mediante la cuenta Microsoft para la aplicación de Servicios de aplicaciones."
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
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="e097a-103">Configuración de la aplicación Servicio de aplicaciones para usar el inicio de sesión de la cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="e097a-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e097a-104">En este tema se muestra cómo configurar Servicio de aplicaciones de Azure para usar la cuenta Microsoft como proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="e097a-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="e097a-105"><a name="register-microsoft-account"> </a>Registro de la aplicación con la cuenta de Microsoft</span><span class="sxs-lookup"><span data-stu-id="e097a-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="e097a-106">Inicie sesión en el [Azure Portal]y vaya a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e097a-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="e097a-107">Copie la **URL**, que posteriormente utilizará para configurar la aplicación con su cuenta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e097a-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="e097a-108">Vaya a la página [Mis aplicaciones] del Centro para desarrolladores de la cuenta Microsoft e inicie sesión con su cuenta Microsoft, si procede.</span><span class="sxs-lookup"><span data-stu-id="e097a-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="e097a-109">Haga clic en **Agregar una aplicación**, escriba el nombre de la aplicación y haga clic en **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="e097a-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="e097a-110">Tome nota del **Id. de aplicación**, ya que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="e097a-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="e097a-111">En "Plataformas", haga clic en **Agregar plataforma** y seleccione "Web".</span><span class="sxs-lookup"><span data-stu-id="e097a-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="e097a-112">En "URI de redirección" proporcione el punto de conexión de la aplicación y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e097a-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e097a-113">El URI de redirección es la dirección URL de la aplicación anexada con la ruta de acceso */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="e097a-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="e097a-114">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="e097a-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="e097a-115">Asegúrese de que está utilizando el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e097a-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="e097a-116">En "Secretos de aplicación", haga clic en **Generar nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e097a-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="e097a-117">Anote el valor que aparece.</span><span class="sxs-lookup"><span data-stu-id="e097a-117">Make note of the value that appears.</span></span> <span data-ttu-id="e097a-118">Una vez que salga de esta página, la contraseña no se volverá a mostrar.</span><span class="sxs-lookup"><span data-stu-id="e097a-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e097a-119">La contraseña es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="e097a-119">The password is an important security credential.</span></span> <span data-ttu-id="e097a-120">No la comparta con nadie ni la distribuya en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="e097a-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="e097a-121"><a name="secrets"> </a>Incorporación de información de la cuenta de Microsoft a la aplicación de Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e097a-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="e097a-122">En [Azure Portal], navegue hasta la aplicación y haga clic en **Configuración** >  **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="e097a-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="e097a-123">Si esta característica no está habilitada, **actívela**.</span><span class="sxs-lookup"><span data-stu-id="e097a-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="e097a-124">Haga clic en **Cuenta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e097a-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="e097a-125">Pegue los valores de identificador de la aplicación y de contraseña que obtuvo previamente y habilite opcionalmente los ámbitos que requiere la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e097a-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="e097a-126">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e097a-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="e097a-127">De forma predeterminada, el Servicio de aplicaciones ofrece autenticación pero no restringe el acceso autorizado al contenido del sitio y a las API.</span><span class="sxs-lookup"><span data-stu-id="e097a-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="e097a-128">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e097a-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="e097a-129">(Opcional) Para restringir el acceso al sitio solo a los usuarios autenticados mediante la cuenta Microsoft, en **Acción necesaria cuando la solicitud no está autenticada**, seleccione **Cuenta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e097a-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="e097a-130">Esto requiere que todas las solicitudes se autentiquen y que todas las solicitudes no autenticadas se redirijan a la cuenta Microsoft para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e097a-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="e097a-131">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e097a-131">Click **Save**.</span></span>

<span data-ttu-id="e097a-132">De este modo ya estará listo para usar la cuenta Microsoft para realizar la autenticación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e097a-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="e097a-133"><a name="related-content"> </a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="e097a-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Mis aplicaciones]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure Portal]: https://portal.azure.com/
