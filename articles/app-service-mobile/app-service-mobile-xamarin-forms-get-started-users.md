---
title: "aaaGet iniciado con la autenticación para aplicaciones móviles en aplicaciones de Xamarin Forms | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de la aplicación de formularios de Xamarin a través de una serie de proveedores de identidad, incluido AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="d0cdc-103">Agregar aplicación de Xamarin Forms authentication tooyour</span><span class="sxs-lookup"><span data-stu-id="d0cdc-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="d0cdc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d0cdc-104">Overview</span></span>
<span data-ttu-id="d0cdc-105">Este tema muestra cómo tooauthenticate a los usuarios de una aplicación de servicio de Mobile aplicaciones desde la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="d0cdc-106">En este tutorial, agregará la autenticación al proyecto de inicio rápido de Xamarin Forms Hola utilizando un proveedor de identidad que es compatible con el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="d0cdc-107">Después de que se va a correctamente autenticados y autorizados por la aplicación móvil, se muestra el valor de identificador de usuario de Hola y será capaz de tooaccess restringido datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0cdc-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d0cdc-108">Prerequisites</span></span>
<span data-ttu-id="d0cdc-109">Para hello mejores resultados con este tutorial, se recomienda que complete primero hello [crear una aplicación de formularios de Xamarin] [ 1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="d0cdc-110">Después de completar este tutorial, tendrá un proyecto de Xamarin Forms que es una aplicación TodoList multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="d0cdc-111">Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto de tooyour de paquete de extensión de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="d0cdc-112">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][2].</span><span class="sxs-lookup"><span data-stu-id="d0cdc-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="d0cdc-113">Registro de la aplicación para la autenticación y configuración de App Services</span><span class="sxs-lookup"><span data-stu-id="d0cdc-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="d0cdc-114"><a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="d0cdc-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="d0cdc-115">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="d0cdc-116">Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="d0cdc-117">En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="d0cdc-118">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="d0cdc-119">Debe ser único tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="d0cdc-120">redirección de hello tooenable en servidor hello:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="d0cdc-121">Hola [portal de Azure], seleccione su servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="d0cdc-122">Haga clic en hello **autenticación / autorización** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="d0cdc-123">Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="d0cdc-124">Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="d0cdc-125">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="d0cdc-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="d0cdc-126">Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="d0cdc-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-127">Click **OK**.</span></span>

5. <span data-ttu-id="d0cdc-128">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="d0cdc-129">Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="d0cdc-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="d0cdc-130">Agregar la biblioteca de clases portable de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="d0cdc-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="d0cdc-131">Aplicaciones móviles usa hello [LoginAsync] [ 3] método de extensión en hello [MobileServiceClient] [ 4] toosign en un usuario con el servicio de aplicaciones autenticación.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="d0cdc-132">Este ejemplo utiliza un flujo de autenticación de servidor administrado que muestra hello interfaz del proveedor de inicio de sesión en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="d0cdc-133">Para obtener más información, consulte [Autenticación administrada por el servidor][5].</span><span class="sxs-lookup"><span data-stu-id="d0cdc-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="d0cdc-134">Para proporcionar una mejor experiencia del usuario en la aplicación de producción, se recomienda usar la [autenticación administrada por el cliente][6].</span><span class="sxs-lookup"><span data-stu-id="d0cdc-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="d0cdc-135">tooauthenticate con un proyecto de Xamarin Forms, defina un **IAuthenticate** interfaz Hola biblioteca de clases Portable para aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="d0cdc-136">A continuación, agregue un **inicio de sesión** interfaz de usuario de botón toohello definida en hello biblioteca de clases Portable, que haga clic en autenticación toostart.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="d0cdc-137">Datos se cargan desde el back-end de hello aplicación móvil tras la autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="d0cdc-138">Hola implemente **IAuthenticate** interfaz para cada plataforma admitida por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="d0cdc-139">En Visual Studio o Xamarin Studio, abra App.cs proyecto Hola con **Portable** en nombre de hello, que es el proyecto de biblioteca de clases Portable, a continuación, agregue siguientes de hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="d0cdc-140">En App.cs, agregue el siguiente de hello `IAuthenticate` definición inmediatamente antes de saludo de la interfaz `App` definición de clase.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="d0cdc-141">interfaz de hello tooinitialize con una implementación específica de la plataforma, agregar Hola siguiendo los miembros estáticos toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="d0cdc-142">Abra TodoList.xaml del proyecto de biblioteca de clases Portable de hello, agregue Hola siguiente **botón** elemento Hola *buttonsPanel* elemento de diseño, después de botón de hello existente:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="d0cdc-143">Este botón desencadena una autenticación administrada por el servidor con el back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="d0cdc-144">Abra TodoList.xaml.cs del proyecto de biblioteca de clases Portable de hello, a continuación, agregue Hola siguiente campo toohello `TodoList` clase:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="d0cdc-145">Reemplace hello **OnAppearing** método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="d0cdc-146">Este código se asegura de que los datos solo se actualizan desde servicio Hola después de que se ha autenticado.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="d0cdc-147">Agregar Hola después de controlador para hello **Clicked** eventos toohello **TodoList** clase:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="d0cdc-148">Guardar los cambios y volver a generar el proyecto de biblioteca de clases Portable Hola no comprobar errores.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="d0cdc-149">Agregar aplicación Android de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="d0cdc-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="d0cdc-150">Esta sección se muestra cómo hello tooimplement **IAuthenticate** interfaz en el proyecto de aplicación de Android Hola.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="d0cdc-151">Omita esta sección si no ofrece compatibilidad con dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="d0cdc-152">En Visual Studio o Xamarin Studio, haga clic en hello **droid** proyecto, a continuación, **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="d0cdc-153">Hola de presionar F5 toostart del proyecto en el depurador de hello, a continuación, compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) después de la aplicación se inicia.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="d0cdc-154">código de Hello 401 se produce porque el acceso en hello back-end está restringido tooauthorized exclusivamente a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="d0cdc-155">Abra MainActivity.cs en proyecto de Android hello y agregue el siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="d0cdc-156">Hola de actualización **MainActivity** Hola de clase tooimplement **IAuthenticate** interfaz, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="d0cdc-157">Hola de actualización **MainActivity** clase agregando un **MobileServiceUser** campo y un **Authenticate** método, que es necesario por hello **IAuthenticate**  interfaz, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="d0cdc-158">Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="d0cdc-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="d0cdc-159">Agregar Hola siguiente código dentro de <application> nodo de AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="d0cdc-160">Agregar Hola después código toohello **OnCreate** método de hello **MainActivity** clase antes de la llamada de hello demasiado`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="d0cdc-161">Este código garantiza autenticador Hola se inicializa antes de la carga de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="d0cdc-162">Volver a generar la aplicación hello, ejecutarlo, a continuación, inicie sesión con el proveedor de autenticación de hello elegido y comprobar que pueda tooaccess datos como un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="d0cdc-163">Agregar aplicación de iOS de toohello de autenticación</span><span class="sxs-lookup"><span data-stu-id="d0cdc-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="d0cdc-164">Esta sección se muestra cómo hello tooimplement **IAuthenticate** interfaz en el proyecto de aplicación de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="d0cdc-165">Omita esta sección si no ofrece compatibilidad con dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="d0cdc-166">En Visual Studio o Xamarin Studio, haga clic en hello **iOS** proyecto, a continuación, **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="d0cdc-167">Hola de presionar F5 toostart del proyecto en el depurador de hello, a continuación, compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="d0cdc-168">respuesta 401 Hola se produce porque el acceso en hello back-end está restringido tooauthorized exclusivamente a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="d0cdc-169">Abra AppDelegate.cs en proyecto de iOS de Hola y agregue el siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="d0cdc-170">Hola de actualización **AppDelegate** Hola de clase tooimplement **IAuthenticate** interfaz, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="d0cdc-171">Hola de actualización **AppDelegate** clase agregando un **MobileServiceUser** campo y un **Authenticate** método, que es necesario por hello **IAuthenticate**  interfaz, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="d0cdc-172">Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="d0cdc-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="d0cdc-173">Actualizar clase de hello AppDelegate mediante la adición de sobrecarga del método OpenUrl (opciones de NSDictionary de aplicación, dirección url de NSUrl, UIApplication)</span><span class="sxs-lookup"><span data-stu-id="d0cdc-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="d0cdc-174">Agregar Hola después de la línea de código toohello **FinishedLaunching** llamada al método antes de hello demasiado`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="d0cdc-175">Este código garantiza autenticador Hola se inicializa antes de que se cargue la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="d0cdc-176">Agregar **{url_scheme_of_your_app}** esquemas tooURL Info.plist.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="d0cdc-177">Volver a generar la aplicación hello, ejecutarlo, a continuación, inicie sesión con el proveedor de autenticación de hello elegido y comprobar que pueda tooaccess datos como un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="d0cdc-178">Agregar autenticación tooWindows 10 (incluido Phone) proyectos de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d0cdc-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="d0cdc-179">Esta sección se muestra cómo hello tooimplement **IAuthenticate** interfaz en los proyectos de aplicación Hola Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="d0cdc-180">Hola mismos pasos se aplican a proyectos de plataforma Universal de Windows (UWP), pero su uso hello **UWP** proyecto (con cambios anotados).</span><span class="sxs-lookup"><span data-stu-id="d0cdc-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="d0cdc-181">Omita esta sección si no ofrece compatibilidad con dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="d0cdc-182">"En Visual Studio, haga clic en cualquier hello **UWP** proyecto, a continuación, **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="d0cdc-183">Hola de presionar F5 toostart del proyecto en el depurador de hello, a continuación, compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="d0cdc-184">respuesta 401 Hola se produce porque el acceso en hello back-end está restringido tooauthorized exclusivamente a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="d0cdc-185">Abra MainPage.xaml.cs para el proyecto de aplicación de Windows hello y agregue el siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="d0cdc-186">Reemplace `<your_Portable_Class_Library_namespace>` con espacio de nombres de hello para la biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="d0cdc-187">Hola de actualización **MainPage** Hola de clase tooimplement **IAuthenticate** interfaz, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="d0cdc-188">Hola de actualización **MainPage** clase agregando un **MobileServiceUser** campo y un **Authenticate** método, que es necesario por hello **IAuthenticate** interfaz, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="d0cdc-189">Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="d0cdc-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="d0cdc-190">Agregar Hola después de la línea de código en el constructor de Hola para hello **MainPage** clase antes de la llamada de hello demasiado`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="d0cdc-191">Reemplace `<your_Portable_Class_Library_namespace>` con espacio de nombres de hello para la biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="d0cdc-192">Si utilizas **UWP**, agregue Hola siguiente **OnActivated** reemplazo del método toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="d0cdc-193">Si ya existe una invalidación del método hello, agregar código condicional Hola de hello anterior fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="d0cdc-194">Este código no es necesario para los proyectos de Windows universal.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="d0cdc-195">Agregue **{esquema_URL_de_la_aplicación}** en Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="d0cdc-196">Volver a generar la aplicación hello, ejecutarlo, a continuación, inicie sesión con el proveedor de autenticación de hello elegido y comprobar que pueda tooaccess datos como un usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0cdc-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0cdc-197">Next steps</span></span>
<span data-ttu-id="d0cdc-198">Completado este tutorial de la autenticación básica, considere la posibilidad de continuar en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="d0cdc-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="d0cdc-199">Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="d0cdc-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="d0cdc-200">Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de toosend de aplicación móvil back-end toouse centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="d0cdc-201">Activación de la sincronización sin conexión para la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="d0cdc-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="d0cdc-202">Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="d0cdc-203">Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil - ver, agregar o modificar datos, incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="d0cdc-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
