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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Agregar aplicación de Xamarin Forms authentication tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Información general
Este tema muestra cómo tooauthenticate a los usuarios de una aplicación de servicio de Mobile aplicaciones desde la aplicación cliente. En este tutorial, agregará la autenticación al proyecto de inicio rápido de Xamarin Forms Hola utilizando un proveedor de identidad que es compatible con el servicio de aplicaciones. Después de que se va a correctamente autenticados y autorizados por la aplicación móvil, se muestra el valor de identificador de usuario de Hola y será capaz de tooaccess restringido datos de la tabla.

## <a name="prerequisites"></a>Requisitos previos
Para hello mejores resultados con este tutorial, se recomienda que complete primero hello [crear una aplicación de formularios de Xamarin] [ 1] tutorial. Después de completar este tutorial, tendrá un proyecto de Xamarin Forms que es una aplicación TodoList multiplataforma.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto de tooyour de paquete de extensión de autenticación de Hola. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Registro de la aplicación para la autenticación y configuración de App Services
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello

La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación. Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola. En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo. Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija. Debe ser único tooyour aplicaciones móviles. redirección de hello tooenable en servidor hello:

1. Hola [portal de Azure], seleccione su servicio en la aplicación.

2. Haga clic en hello **autenticación / autorización** opción de menú.

3. Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.  Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.  Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).  Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.

4. Haga clic en **Aceptar**.

5. Haga clic en **Guardar**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Restringir a los usuarios de tooauthenticated de permisos
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Agregar la biblioteca de clases portable de autenticación toohello
Aplicaciones móviles usa hello [LoginAsync] [ 3] método de extensión en hello [MobileServiceClient] [ 4] toosign en un usuario con el servicio de aplicaciones autenticación. Este ejemplo utiliza un flujo de autenticación de servidor administrado que muestra hello interfaz del proveedor de inicio de sesión en la aplicación hello. Para obtener más información, consulte [Autenticación administrada por el servidor][5]. Para proporcionar una mejor experiencia del usuario en la aplicación de producción, se recomienda usar la [autenticación administrada por el cliente][6].

tooauthenticate con un proyecto de Xamarin Forms, defina un **IAuthenticate** interfaz Hola biblioteca de clases Portable para aplicación hello. A continuación, agregue un **inicio de sesión** interfaz de usuario de botón toohello definida en hello biblioteca de clases Portable, que haga clic en autenticación toostart. Datos se cargan desde el back-end de hello aplicación móvil tras la autenticación correcta.

Hola implemente **IAuthenticate** interfaz para cada plataforma admitida por la aplicación.

1. En Visual Studio o Xamarin Studio, abra App.cs proyecto Hola con **Portable** en nombre de hello, que es el proyecto de biblioteca de clases Portable, a continuación, agregue siguientes de hello `using` instrucción:

        using System.Threading.Tasks;
2. En App.cs, agregue el siguiente de hello `IAuthenticate` definición inmediatamente antes de saludo de la interfaz `App` definición de clase.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. interfaz de hello tooinitialize con una implementación específica de la plataforma, agregar Hola siguiendo los miembros estáticos toohello **aplicación** clase.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Abra TodoList.xaml del proyecto de biblioteca de clases Portable de hello, agregue Hola siguiente **botón** elemento Hola *buttonsPanel* elemento de diseño, después de botón de hello existente:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Este botón desencadena una autenticación administrada por el servidor con el back-end de aplicación móvil.
5. Abra TodoList.xaml.cs del proyecto de biblioteca de clases Portable de hello, a continuación, agregue Hola siguiente campo toohello `TodoList` clase:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Reemplace hello **OnAppearing** método con el siguiente código de hello:

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

    Este código se asegura de que los datos solo se actualizan desde servicio Hola después de que se ha autenticado.
7. Agregar Hola después de controlador para hello **Clicked** eventos toohello **TodoList** clase:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Guardar los cambios y volver a generar el proyecto de biblioteca de clases Portable Hola no comprobar errores.

## <a name="add-authentication-toohello-android-app"></a>Agregar aplicación Android de autenticación toohello
Esta sección se muestra cómo hello tooimplement **IAuthenticate** interfaz en el proyecto de aplicación de Android Hola. Omita esta sección si no ofrece compatibilidad con dispositivos Android.

1. En Visual Studio o Xamarin Studio, haga clic en hello **droid** proyecto, a continuación, **establecer como proyecto de inicio**.
2. Hola de presionar F5 toostart del proyecto en el depurador de hello, a continuación, compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) después de la aplicación se inicia. código de Hello 401 se produce porque el acceso en hello back-end está restringido tooauthorized exclusivamente a los usuarios.
3. Abra MainActivity.cs en proyecto de Android hello y agregue el siguiente hello `using` instrucciones:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Hola de actualización **MainActivity** Hola de clase tooimplement **IAuthenticate** interfaz, como se indica a continuación:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Hola de actualización **MainActivity** clase agregando un **MobileServiceUser** campo y un **Authenticate** método, que es necesario por hello **IAuthenticate**  interfaz, como se indica a continuación:

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

    Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider][7].

6. Agregar Hola siguiente código dentro de <application> nodo de AndroidManifest.xml:

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

1. Agregar Hola después código toohello **OnCreate** método de hello **MainActivity** clase antes de la llamada de hello demasiado`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Este código garantiza autenticador Hola se inicializa antes de la carga de aplicación Hola.
2. Volver a generar la aplicación hello, ejecutarlo, a continuación, inicie sesión con el proveedor de autenticación de hello elegido y comprobar que pueda tooaccess datos como un usuario autenticado.

## <a name="add-authentication-toohello-ios-app"></a>Agregar aplicación de iOS de toohello de autenticación
Esta sección se muestra cómo hello tooimplement **IAuthenticate** interfaz en el proyecto de aplicación de iOS de Hola. Omita esta sección si no ofrece compatibilidad con dispositivos iOS.

1. En Visual Studio o Xamarin Studio, haga clic en hello **iOS** proyecto, a continuación, **establecer como proyecto de inicio**.
2. Hola de presionar F5 toostart del proyecto en el depurador de hello, a continuación, compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello. respuesta 401 Hola se produce porque el acceso en hello back-end está restringido tooauthorized exclusivamente a los usuarios.
3. Abra AppDelegate.cs en proyecto de iOS de Hola y agregue el siguiente hello `using` instrucciones:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Hola de actualización **AppDelegate** Hola de clase tooimplement **IAuthenticate** interfaz, como se indica a continuación:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Hola de actualización **AppDelegate** clase agregando un **MobileServiceUser** campo y un **Authenticate** método, que es necesario por hello **IAuthenticate**  interfaz, como se indica a continuación:

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

    Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider].

6. Actualizar clase de hello AppDelegate mediante la adición de sobrecarga del método OpenUrl (opciones de NSDictionary de aplicación, dirección url de NSUrl, UIApplication)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Agregar Hola después de la línea de código toohello **FinishedLaunching** llamada al método antes de hello demasiado`LoadApplication()`:

        App.Init(this);

    Este código garantiza autenticador Hola se inicializa antes de que se cargue la aplicación hello.

6. Agregar **{url_scheme_of_your_app}** esquemas tooURL Info.plist.

7. Volver a generar la aplicación hello, ejecutarlo, a continuación, inicie sesión con el proveedor de autenticación de hello elegido y comprobar que pueda tooaccess datos como un usuario autenticado.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Agregar autenticación tooWindows 10 (incluido Phone) proyectos de aplicaciones
Esta sección se muestra cómo hello tooimplement **IAuthenticate** interfaz en los proyectos de aplicación Hola Windows 10. Hola mismos pasos se aplican a proyectos de plataforma Universal de Windows (UWP), pero su uso hello **UWP** proyecto (con cambios anotados). Omita esta sección si no ofrece compatibilidad con dispositivos Windows.

1. "En Visual Studio, haga clic en cualquier hello **UWP** proyecto, a continuación, **establecer como proyecto de inicio**.
2. Hola de presionar F5 toostart del proyecto en el depurador de hello, a continuación, compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello. respuesta 401 Hola se produce porque el acceso en hello back-end está restringido tooauthorized exclusivamente a los usuarios.
3. Abra MainPage.xaml.cs para el proyecto de aplicación de Windows hello y agregue el siguiente hello `using` instrucciones:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Reemplace `<your_Portable_Class_Library_namespace>` con espacio de nombres de hello para la biblioteca de clases portable.
4. Hola de actualización **MainPage** Hola de clase tooimplement **IAuthenticate** interfaz, como se indica a continuación:

        public sealed partial class MainPage : IAuthenticate
5. Hola de actualización **MainPage** clase agregando un **MobileServiceUser** campo y un **Authenticate** método, que es necesario por hello **IAuthenticate** interfaz, como se indica a continuación:

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

    Si usa un proveedor de identidades que no sea Facebook, elija otro valor para [MobileServiceAuthenticationProvider].

1. Agregar Hola después de la línea de código en el constructor de Hola para hello **MainPage** clase antes de la llamada de hello demasiado`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Reemplace `<your_Portable_Class_Library_namespace>` con espacio de nombres de hello para la biblioteca de clases portable.

3. Si utilizas **UWP**, agregue Hola siguiente **OnActivated** reemplazo del método toohello **aplicación** clase:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Si ya existe una invalidación del método hello, agregar código condicional Hola de hello anterior fragmento de código.  Este código no es necesario para los proyectos de Windows universal.

3. Agregue **{esquema_URL_de_la_aplicación}** en Package.appxmanifest. 

4. Volver a generar la aplicación hello, ejecutarlo, a continuación, inicie sesión con el proveedor de autenticación de hello elegido y comprobar que pueda tooaccess datos como un usuario autenticado.

## <a name="next-steps"></a>Pasos siguientes
Completado este tutorial de la autenticación básica, considere la posibilidad de continuar en tooone de hello tutoriales:

* [Agregar aplicación de tooyour de notificaciones de inserción](app-service-mobile-xamarin-forms-get-started-push.md)

  Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de toosend de aplicación móvil back-end toouse centros de notificaciones de Azure.
* [Activación de la sincronización sin conexión para la aplicación de Windows](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end. Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil - ver, agregar o modificar datos, incluso cuando no hay ninguna conexión de red.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
