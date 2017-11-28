---
title: "Introducción a la autenticación de Mobile Apps en la aplicación de Xamarin Forms | Microsoft Docs"
description: "Obtenga información acerca de cómo utilizar Mobile Apps para autenticar usuarios de la aplicación de Xamarin Forms a través de una variedad de proveedores de identidad, incluidos AAD, Google, Facebook, Twitter y Microsoft."
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="df565-103">Agregue autenticación a su aplicación de Xamarin Forms</span><span class="sxs-lookup"><span data-stu-id="df565-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="df565-104">Información general</span><span class="sxs-lookup"><span data-stu-id="df565-104">Overview</span></span>
<span data-ttu-id="df565-105">En este tema se muestra cómo autenticar usuarios de una aplicación móvil de App Service desde la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="df565-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="df565-106">En este tutorial se agrega autenticación al proyecto de inicio rápido de Xamarin Forms mediante un proveedor de identidades compatible con App Service.</span><span class="sxs-lookup"><span data-stu-id="df565-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="df565-107">Una vez que la aplicación móvil haya realizado la autenticación y la autorización correctamente, se mostrará el valor de identificador de usuario y podrá acceder a datos de tabla restringida.</span><span class="sxs-lookup"><span data-stu-id="df565-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df565-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="df565-108">Prerequisites</span></span>
<span data-ttu-id="df565-109">Para obtener el mejor resultado con este tutorial, se recomienda completar primero el tutorial [Creación de una aplicación Xamarin.Forms][1].</span><span class="sxs-lookup"><span data-stu-id="df565-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="df565-110">Después de completar este tutorial, tendrá un proyecto de Xamarin Forms que es una aplicación TodoList multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="df565-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="df565-111">Si no usa el proyecto de servidor de inicio rápido descargado, debe agregar el paquete de extensión de autenticación al proyecto.</span><span class="sxs-lookup"><span data-stu-id="df565-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="df565-112">Para obtener más información acerca de los paquetes de extensión de servidor, consulte el artículo sobre cómo [trabajar con el SDK del servidor back-end de .NET para Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="df565-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="df565-113">Registro de la aplicación para la autenticación y configuración de App Services</span><span class="sxs-lookup"><span data-stu-id="df565-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="df565-114"><a name="redirecturl"></a>Adición de la aplicación a las direcciones URL de redirección externa permitidas</span><span class="sxs-lookup"><span data-stu-id="df565-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="df565-115">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df565-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="df565-116">Esto permite que el sistema de autenticación se redirija a la aplicación una vez completado el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="df565-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="df565-117">En este tutorial, se usará el esquema de dirección URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="df565-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="df565-118">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="df565-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="df565-119">Debe ser único para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="df565-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="df565-120">Para habilitar la redirección en el lado de servidor:</span><span class="sxs-lookup"><span data-stu-id="df565-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="df565-121">En [Azure Portal], seleccione App Service.</span><span class="sxs-lookup"><span data-stu-id="df565-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="df565-122">Haga clic en la opción de menú **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="df565-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="df565-123">En **URL de redirección externas permitidas**, introduzca `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="df565-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="df565-124">El valor de **esquema_de_dirección_URL_de_la_aplicación** de esta cadena es el esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="df565-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="df565-125">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="df565-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="df565-126">Debe tomar nota de la cadena que elija ya que necesitará ajustar el código de la aplicación móvil con el esquema de direcciones URL en varios sitios.</span><span class="sxs-lookup"><span data-stu-id="df565-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="df565-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="df565-127">Click **OK**.</span></span>

5. <span data-ttu-id="df565-128">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="df565-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="df565-129">Restricción de los permisos para los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="df565-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="df565-130">Agregar autenticación a la biblioteca de clases portables</span><span class="sxs-lookup"><span data-stu-id="df565-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="df565-131">Mobile Apps usa el método de extensión [LoginAsync][3] en [MobileServiceClient][4] para iniciar una sesión de usuario con autenticación de App Service.</span><span class="sxs-lookup"><span data-stu-id="df565-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="df565-132">Este ejemplo usa un flujo de autenticación administrado por servidor que muestra la interfaz de inicio de sesión del proveedor en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df565-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="df565-133">Para obtener más información, consulte [Autenticación administrada por el servidor][5].</span><span class="sxs-lookup"><span data-stu-id="df565-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="df565-134">Para proporcionar una mejor experiencia del usuario en la aplicación de producción, se recomienda usar la [autenticación administrada por el cliente][6].</span><span class="sxs-lookup"><span data-stu-id="df565-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="df565-135">Para realizar la autenticación con un proyecto de Xamarin Forms, defina en la biblioteca de clases portable una interfaz **IAuthenticate** para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df565-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="df565-136">Luego, agregue un botón **Inicio de sesión** a la interfaz de usuario definida en la biblioteca de clases portable, en el que se haga clic para iniciar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="df565-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="df565-137">Tras una autenticación correcta, los datos se cargan desde el back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="df565-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="df565-138">Implemente la interfaz **IAuthenticate** en cada plataforma que admitida la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df565-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="df565-139">En Visual Studio o Xamarin Studio, abra App.cs desde el proyecto con **Portable** en el nombre, que es el proyecto de la biblioteca de clases portable, y agregue las siguientes instrucción `using`:</span><span class="sxs-lookup"><span data-stu-id="df565-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="df565-140">En el archivo App.cs, agregue la siguiente definición de interfaz `IAuthenticate` inmediatamente antes de la definición de la clase `App`.</span><span class="sxs-lookup"><span data-stu-id="df565-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="df565-141">Para inicializar la interfaz con una implementación específica de la plataforma, agregue los siguientes miembros estáticos a la clase **App**.</span><span class="sxs-lookup"><span data-stu-id="df565-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="df565-142">Abra TodoList.xaml desde el proyecto de biblioteca de clases portable y agregue el siguiente elemento **Button** en el elemento de diseño *buttonsPanel* , después del botón existente:</span><span class="sxs-lookup"><span data-stu-id="df565-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="df565-143">Este botón desencadena una autenticación administrada por el servidor con el back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="df565-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="df565-144">Abra TodoList.xaml.cs desde el proyecto de biblioteca de clases portable y agregue el siguiente campo a la clase `TodoList` :</span><span class="sxs-lookup"><span data-stu-id="df565-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="df565-145">Reemplace el método **OnAppearing** por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="df565-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="df565-146">Este código garantiza que los datos solo se actualizan desde el servicio una vez que se haya realizado la autenticación.</span><span class="sxs-lookup"><span data-stu-id="df565-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="df565-147">Agregue el siguiente controlador para el evento **Clicked** a la clase **TodoList**:</span><span class="sxs-lookup"><span data-stu-id="df565-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="df565-148">Guarde los cambios, vuelva a compilar el proyecto de biblioteca de clases portable y compruebe que no haya errores.</span><span class="sxs-lookup"><span data-stu-id="df565-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="df565-149">Agregar autenticación a la aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="df565-149">Add authentication to the Android app</span></span>
<span data-ttu-id="df565-150">En esta sección se muestra cómo implementar la interfaz **IAuthenticate** en el proyecto de aplicación de Android.</span><span class="sxs-lookup"><span data-stu-id="df565-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="df565-151">Omita esta sección si no ofrece compatibilidad con dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="df565-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="df565-152">En Visual Studio o Xamarin Studio, haga clic con el botón derecho en el proyecto **droid** y luego en **Establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="df565-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="df565-153">Presione F5 para iniciar el proyecto en el depurador y después compruebe que, después de iniciarse la aplicación, se genera una excepción no controlada con el código de estado 401 (No autorizado).</span><span class="sxs-lookup"><span data-stu-id="df565-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="df565-154">El código 401 aparece porque el acceso en el back-end está restringido únicamente a usuarios autorizados.</span><span class="sxs-lookup"><span data-stu-id="df565-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="df565-155">Abra MainActivity.cs en el proyecto de Android y agregue las siguientes instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="df565-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="df565-156">Actualice la clase **MainActivity** para implementar la interfaz **IAuthenticate**, como sigue:</span><span class="sxs-lookup"><span data-stu-id="df565-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="df565-157">Actualice la clase **MainActivity**, para lo que debe agregar un campo **MobileServiceUser** y un método **Authenticate**, lo que necesita la interfaz **IAuthenticate**, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="df565-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="df565-158">Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="df565-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="df565-159">Agregue el código siguiente dentro del nodo <application> de AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="df565-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="df565-160">Agregue el siguiente código al método **onCreate** de la clase **MainActivity** antes de la llamada a `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="df565-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="df565-161">Este código garantiza que el autenticador se inicializa antes de que se cargue la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df565-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="df565-162">Vuelva a compilar la aplicación, ejecútela, inicie sesión con el proveedor de autenticación que elija y compruebe que pueda acceder a los datos como usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="df565-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="df565-163">Agregar autenticación a la aplicación de iOS</span><span class="sxs-lookup"><span data-stu-id="df565-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="df565-164">En esta sección se muestra cómo implementar la interfaz **IAuthenticate** en el proyecto de aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="df565-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="df565-165">Omita esta sección si no ofrece compatibilidad con dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="df565-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="df565-166">En Visual Studio o Xamarin Studio, haga clic con el botón derecho en el proyecto **iOS** y luego en **Establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="df565-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="df565-167">Presione F5 para iniciar el proyecto en el depurador y después compruebe que, después de iniciarse la aplicación, se genera una excepción no controlada con el código de estado 401 (No autorizado).</span><span class="sxs-lookup"><span data-stu-id="df565-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="df565-168">La respuesta 401 aparece porque el acceso en el back-end está restringido únicamente a usuarios autorizados.</span><span class="sxs-lookup"><span data-stu-id="df565-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="df565-169">Abra el archivo AppDelegate.cs en el proyecto de iOS y agregue las siguientes instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="df565-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="df565-170">Actualice la clase **AppDelegate** para implementar la interfaz **IAuthenticate** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="df565-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="df565-171">Actualice la clase **AppDelegate**, para lo que debe agregar un campo **MobileServiceUser** y un método **Authenticate**, lo que necesita la interfaz **IAuthenticate**, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="df565-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="df565-172">Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="df565-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="df565-173">Actualice la clase AppDelegate mediante la adición de la sobrecarga del método OpenUrl(UIApplication app, NSUrl url, NSDictionary options)</span><span class="sxs-lookup"><span data-stu-id="df565-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="df565-174">Agregue la siguiente línea de código al método **FinishedLaunching** antes de la llamada a `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="df565-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="df565-175">Este código garantiza que el autenticador se inicializa antes de que se cargue la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df565-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="df565-176">Agregue **{esquema_URL_de_la_aplicación}** a los esquemas de dirección URL de Info.plist.</span><span class="sxs-lookup"><span data-stu-id="df565-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="df565-177">Vuelva a compilar la aplicación, ejecútela, inicie sesión con el proveedor de autenticación que elija y compruebe que pueda acceder a los datos como usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="df565-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="df565-178">Adición de autenticación a proyectos de aplicaciones de Windows 10 (incluyendo Phone)</span><span class="sxs-lookup"><span data-stu-id="df565-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="df565-179">En esta sección se muestra cómo implementar la interfaz **IAuthenticate** en proyectos de aplicaciones de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="df565-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="df565-180">Los mismos pasos se aplican a los proyectos de plataforma universal de Windows (UWP), pero se usa el proyecto **UWP** (con cambios anotados).</span><span class="sxs-lookup"><span data-stu-id="df565-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="df565-181">Omita esta sección si no ofrece compatibilidad con dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="df565-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="df565-182">En Visual Studio, haga clic con el botón derecho en el proyecto **UWP**, y luego en **Establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="df565-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="df565-183">Presione F5 para iniciar el proyecto en el depurador y después compruebe que, después de iniciarse la aplicación, se genera una excepción no controlada con el código de estado 401 (No autorizado).</span><span class="sxs-lookup"><span data-stu-id="df565-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="df565-184">La respuesta 401 de produce porque el acceso en el back-end está restringido únicamente a usuarios autorizados.</span><span class="sxs-lookup"><span data-stu-id="df565-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="df565-185">Abra el archivo MainPage.xaml.cs en el proyecto de aplicación de Windows y agregue las siguientes instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="df565-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="df565-186">Reemplace `<your_Portable_Class_Library_namespace>` por el espacio de nombres de la biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="df565-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="df565-187">Actualice la clase **MainPage** para implementar la interfaz **IAuthenticate** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="df565-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="df565-188">Actualice la clase **MainPage**, para lo que debe agregar un campo **MobileServiceUser** y un método **Authenticate**, lo que necesita la interfaz **IAuthenticate**, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="df565-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="df565-189">Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="df565-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="df565-190">Agregue la siguiente línea de código en el constructor para la clase **MainPage** antes de la llamada a `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="df565-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="df565-191">Reemplace `<your_Portable_Class_Library_namespace>` por el espacio de nombres de la biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="df565-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="df565-192">Si utiliza **UWP**, agregue el siguiente reemplazo del método **OnActivated** a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="df565-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="df565-193">Si dicho reemplazo ya existe, agregue el código condicional del fragmento de código anterior.</span><span class="sxs-lookup"><span data-stu-id="df565-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="df565-194">Este código no es necesario para los proyectos de Windows universal.</span><span class="sxs-lookup"><span data-stu-id="df565-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="df565-195">Agregue **{esquema_URL_de_la_aplicación}** en Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="df565-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="df565-196">Vuelva a compilar la aplicación, ejecútela, inicie sesión con el proveedor de autenticación que elija y compruebe que pueda acceder a los datos como usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="df565-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df565-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df565-197">Next steps</span></span>
<span data-ttu-id="df565-198">Ahora que ha completado este tutorial de autenticación básica, considere la posibilidad de continuar con uno de los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="df565-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="df565-199">Incorporación de notificaciones push a su aplicación</span><span class="sxs-lookup"><span data-stu-id="df565-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="df565-200">: aprenda a agregar a la aplicación compatibilidad con notificaciones push y a configurar su back-end de aplicación móvil para usar Azure Notification Hubs para enviar notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="df565-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="df565-201">Activación de la sincronización sin conexión para la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="df565-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="df565-202">Aprenda a agregar compatibilidad sin conexión a una aplicación con un back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="df565-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="df565-203">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos), incluso cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="df565-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
