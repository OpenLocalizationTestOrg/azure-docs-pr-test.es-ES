---
title: "aaaGet iniciado con la autenticación para aplicaciones móviles en iOS de Xamarin"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de la aplicación de iOS de Xamarin a través de una serie de proveedores de identidad, incluido AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="94bdc-103">Agregar aplicación de autenticación tooyour Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="94bdc-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="94bdc-104">Este tema muestra cómo tooauthenticate a los usuarios de una aplicación de servicio de Mobile aplicaciones desde la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="94bdc-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="94bdc-105">En este tutorial, agregará el proyecto de inicio rápido de autenticación toohello Xamarin.iOS utilizando un proveedor de identidad que es compatible con el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="94bdc-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="94bdc-106">Después de que se va a correctamente autenticados y autorizados por la aplicación móvil, se muestra el valor de identificador de usuario de Hola y será capaz de tooaccess restringido datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="94bdc-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="94bdc-107">Primero debe completar el tutorial de hello [crear una aplicación de Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="94bdc-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="94bdc-108">Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto de tooyour de paquete de extensión de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="94bdc-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="94bdc-109">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="94bdc-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="94bdc-110">Registro de la aplicación para la autenticación y configuración de App Services</span><span class="sxs-lookup"><span data-stu-id="94bdc-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="94bdc-111">Agregue las direcciones URL de redirección externa permitido de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="94bdc-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="94bdc-112">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94bdc-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="94bdc-113">Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="94bdc-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="94bdc-114">En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo.</span><span class="sxs-lookup"><span data-stu-id="94bdc-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="94bdc-115">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="94bdc-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="94bdc-116">Debe ser único tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="94bdc-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="94bdc-117">redirección de hello tooenable en servidor hello:</span><span class="sxs-lookup"><span data-stu-id="94bdc-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="94bdc-118">Hola [portal de Azure], seleccione su servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94bdc-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="94bdc-119">Haga clic en hello **autenticación / autorización** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="94bdc-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="94bdc-120">Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="94bdc-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="94bdc-121">Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="94bdc-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="94bdc-122">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="94bdc-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="94bdc-123">Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="94bdc-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="94bdc-124">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="94bdc-124">Click **OK**.</span></span>

5. <span data-ttu-id="94bdc-125">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="94bdc-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="94bdc-126">Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="94bdc-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="94bdc-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="94bdc-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="94bdc-128">En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente de hello en un dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="94bdc-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="94bdc-129">Compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="94bdc-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="94bdc-130">Error de Hello es consola toohello registrados del depurador de Hola.</span><span class="sxs-lookup"><span data-stu-id="94bdc-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="94bdc-131">Por lo que en Visual Studio, debería ver error hello en la ventana de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="94bdc-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="94bdc-132">&nbsp;&nbsp;Este error no autorizado se produce porque la aplicación hello intenta tooaccess su aplicación móvil de back-end como un usuario no autenticado.</span><span class="sxs-lookup"><span data-stu-id="94bdc-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="94bdc-133">Hola *TodoItem* tabla ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="94bdc-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="94bdc-134">A continuación, actualizará recursos de toorequest Hola la aplicación cliente de aplicación móvil de hello back-end a un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="94bdc-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="94bdc-135">Agregar aplicación de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="94bdc-135">Add authentication toohello app</span></span>
<span data-ttu-id="94bdc-136">En esta sección, modificará Hola aplicación toodisplay una pantalla de inicio de sesión antes de mostrar los datos.</span><span class="sxs-lookup"><span data-stu-id="94bdc-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="94bdc-137">Cuando se inicia la aplicación hello, no se conectará no tooyour servicio de aplicaciones y no mostrará ningún dato.</span><span class="sxs-lookup"><span data-stu-id="94bdc-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="94bdc-138">Después de hello primera vez que el usuario Hola realiza gestos de actualización de hello, aparecerá la pantalla de inicio de sesión de bienvenida; Después de que se mostrará la lista de Hola de inicio de sesión correcto de los elementos de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="94bdc-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="94bdc-139">En el proyecto de cliente de hello, abra el archivo de hello **QSTodoService.cs** y agregue Hola siguiente mediante la instrucción y `MobileServiceUser` con toohello QSTodoService clase de descriptor de acceso:</span><span class="sxs-lookup"><span data-stu-id="94bdc-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="94bdc-140">Agregar nuevo método denominado **Authenticate** demasiado**QSTodoService** con hello siguiente definición:</span><span class="sxs-lookup"><span data-stu-id="94bdc-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="94bdc-141">Si está utilizando un proveedor de identidades que no sea un Facebook, cambie el valor de Hola que se pasan demasiado**LoginAsync** anteriormente tooone de siguientes hello: _cuenta de Microsoft_, _Twitter_, _Google_, o _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="94bdc-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="94bdc-142">Abra **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="94bdc-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="94bdc-143">Modificar la definición de método hello de **ViewDidLoad** quitar llamada Hola demasiado**RefreshAsync()** cuando se acerque el final de hello:</span><span class="sxs-lookup"><span data-stu-id="94bdc-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="94bdc-144">Modificar el método hello **RefreshAsync** tooauthenticate si hello **usuario** propiedad es null.</span><span class="sxs-lookup"><span data-stu-id="94bdc-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="94bdc-145">Agregue Hola siguiente código en parte superior de Hola de definición de método hello:</span><span class="sxs-lookup"><span data-stu-id="94bdc-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="94bdc-146">Abra **AppDelegate.cs**, agregar Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="94bdc-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="94bdc-147">Abra **Info.plist** de archivos, vaya demasiado**tipos de URL** en hello **avanzadas** sección.</span><span class="sxs-lookup"><span data-stu-id="94bdc-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="94bdc-148">Configurar ahora hello **identificador** hello y **esquemas de URL** de su tipo de dirección URL y haga clic en **Agregar tipo de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="94bdc-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="94bdc-149">**Esquemas de direcciones URL** debe ser Hola mismo como su {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="94bdc-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="94bdc-150">En Visual Studio o Xamarin Studio conectado tooyour Host de compilación de Xamarin en el equipo Mac, ejecutar el proyecto de cliente de hello destinado a un dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="94bdc-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="94bdc-151">Compruebe que la aplicación hello no muestra ningún dato.</span><span class="sxs-lookup"><span data-stu-id="94bdc-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="94bdc-152">Realizar gestos de actualización de hello desplazando hacia abajo de la lista de Hola de elementos, lo que hará que tooappear de pantalla de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="94bdc-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="94bdc-153">Una vez que ha escrito correctamente las credenciales válidas, aplicación hello mostrará la lista de Hola de elementos de lista de tareas y realizar toohello una actualización de datos.</span><span class="sxs-lookup"><span data-stu-id="94bdc-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[crear una aplicación de Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md