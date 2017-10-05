---
title: "Configuración de la autenticación mediante Facebook para la aplicación de Servicios de aplicaciones"
description: "Obtenga información acerca de cómo configurar la autenticación mediante Facebook para la aplicación de Servicios de aplicaciones."
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
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="8b90e-103">Configuración de la aplicación Servicio de aplicaciones para usar el inicio de sesión de Facebook</span><span class="sxs-lookup"><span data-stu-id="8b90e-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="8b90e-104">En este tema se muestra cómo configurar Servicio de aplicaciones de Azure para usar Facebook como proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="8b90e-105">Para llevar a cabo el procedimiento descrito en este tema, debe tener una cuenta de Facebook asociada a una dirección de correo electrónico verificada y a un número de teléfono móvil.</span><span class="sxs-lookup"><span data-stu-id="8b90e-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="8b90e-106">Para crear una cuenta de Facebook, vaya a [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="8b90e-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="8b90e-107"><a name="register"> </a>Registro de la aplicación con Facebook</span><span class="sxs-lookup"><span data-stu-id="8b90e-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="8b90e-108">Inicie sesión en el [Portal de Azure]y vaya a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="8b90e-109">Copie la **Dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-109">Copy your **URL**.</span></span> <span data-ttu-id="8b90e-110">La usará para configurar la aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="8b90e-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="8b90e-111">En otra ventana del explorador, navegue hasta el sitio web de [Desarrolladores de Facebook] e inicie sesión con las credenciales de su cuenta de Facebook.</span><span class="sxs-lookup"><span data-stu-id="8b90e-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="8b90e-112">(Opcional) Si aún no se ha registrado, haga clic en **Apps** (Aplicaciones) > **Register as a Developer** (Registrarse como desarrollador), acepte la directiva y siga los pasos del registro.</span><span class="sxs-lookup"><span data-stu-id="8b90e-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="8b90e-113">Haga clic en **My Apps** (Mis aplicaciones) > **Add a New App** (Agregar una nueva aplicación) > **Website** (Sitio web) > **Skip and Create App ID** (Omitir y crear id. de aplicación).</span><span class="sxs-lookup"><span data-stu-id="8b90e-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="8b90e-114">En **Display Name** (Nombre para mostrar), escriba un nombre único para la aplicación, especifique el **correo electrónico de contacto**, elija una **categoría** para la aplicación, haga clic en **Create App ID** (Crear id. de aplicación) y complete la comprobación de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8b90e-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="8b90e-115">Esto le llevará al panel del desarrollador de la nueva aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="8b90e-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="8b90e-116">En "Inicio de sesión de Facebook", haga clic en **Comenzar**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="8b90e-117">Agregue el **URI de redirección** de la aplicación a **Valid OAuth redirect URIs** (URI de redirección de OAuth válidos) y haga clic en **Save Changes** (Guardar cambios).</span><span class="sxs-lookup"><span data-stu-id="8b90e-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8b90e-118">El URI de redirección es la dirección URL de la aplicación anexada con la ruta de acceso, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="8b90e-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="8b90e-119">Por ejemplo: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="8b90e-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="8b90e-120">Asegúrese de que está utilizando el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8b90e-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="8b90e-121">En el panel de navegación izquierdo, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="8b90e-122">En el campo **Secreto de la aplicación**, haga clic en **Mostrar**, escriba la contraseña si se le solicita y, a continuación, anote los valores de **Id. de aplicación** y **Secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="8b90e-123">Más adelante los usará para configurar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="8b90e-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8b90e-124">El secreto de aplicación es una credencial de seguridad importante,</span><span class="sxs-lookup"><span data-stu-id="8b90e-124">The app secret is an important security credential.</span></span> <span data-ttu-id="8b90e-125">No comparta este secreto con nadie ni lo distribuya en una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="8b90e-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="8b90e-126">La cuenta de Facebook que se utilizó para registrar la aplicación es un administrador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="8b90e-127">En este momento, solo los administradores pueden iniciar sesión en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="8b90e-128">Para autenticar otras cuentas de Facebook, haga clic en **App Review** (Revisión de aplicaciones) y habilite **Make <your-app-name> public** (Hacer pública <nombre-de-su-aplicación>) para habilitar el acceso público general mediante la autenticación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="8b90e-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="8b90e-129"><a name="secrets"> </a>Agregar información de Facebook a la aplicación</span><span class="sxs-lookup"><span data-stu-id="8b90e-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="8b90e-130">Vuelva al [Portal de Azure]y vaya a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="8b90e-131">Haga clic en **Configuración** > **Autenticación/autorización** y asegúrese de que **Autenticación de App Service** está **Activada**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="8b90e-132">Haga clic en **Facebook**, pegue los valores de Id. de aplicación y Secreto de la aplicación que obtuvo anteriormente, opcionalmente habilite los ámbitos que requiera la aplicación y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="8b90e-133">De forma predeterminada, el Servicio de aplicaciones ofrece autenticación pero no restringe el acceso autorizado al contenido del sitio y a las API.</span><span class="sxs-lookup"><span data-stu-id="8b90e-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="8b90e-134">Debe autorizar a los usuarios en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="8b90e-135">(Opcional) Para restringir el acceso al sitio solo a los usuarios autenticados mediante Facebook, en **Acción necesaria cuando la solicitud no está autenticada**, seleccione **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="8b90e-136">Esto requiere que todas las solicitudes se autentiquen y que todas las solicitudes no autenticadas se redirijan a Facebook para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="8b90e-137">Cuando termine de configurar la autenticación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="8b90e-138">De este modo ya estará listo para usar Facebook para realizar la autenticación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="8b90e-139"><a name="related-content"> </a>Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="8b90e-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="8b90e-140">[Desarrolladores de Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="8b90e-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="8b90e-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="8b90e-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="8b90e-142">[Portal de Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="8b90e-142">[Azure portal]: https://portal.azure.com/</span></span>
