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
# <a name="add-authentication-tooyour-xamarinios-app"></a>Agregar aplicación de autenticación tooyour Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tema muestra cómo tooauthenticate a los usuarios de una aplicación de servicio de Mobile aplicaciones desde la aplicación cliente. En este tutorial, agregará el proyecto de inicio rápido de autenticación toohello Xamarin.iOS utilizando un proveedor de identidad que es compatible con el servicio de aplicaciones. Después de que se va a correctamente autenticados y autorizados por la aplicación móvil, se muestra el valor de identificador de usuario de Hola y será capaz de tooaccess restringido datos de la tabla.

Primero debe completar el tutorial de hello [crear una aplicación de Xamarin.iOS]. Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto de tooyour de paquete de extensión de autenticación de Hola. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Registro de la aplicación para la autenticación y configuración de App Services
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello

La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación. Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola. En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo. Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija. Debe ser único tooyour aplicaciones móviles. redirección de hello tooenable en servidor hello:

1. Hola [portal de Azure], seleccione su servicio en la aplicación.

2. Haga clic en hello **autenticación / autorización** opción de menú.

3. Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.  Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.  Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).  Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.

4. Haga clic en **Aceptar**.

5. Haga clic en **Guardar**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Restringir a los usuarios de tooauthenticated de permisos
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente de hello en un dispositivo o emulador. Compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello. Error de Hello es consola toohello registrados del depurador de Hola. Por lo que en Visual Studio, debería ver error hello en la ventana de salida de hello.

&nbsp;&nbsp;Este error no autorizado se produce porque la aplicación hello intenta tooaccess su aplicación móvil de back-end como un usuario no autenticado. Hola *TodoItem* tabla ahora requiere autenticación.

A continuación, actualizará recursos de toorequest Hola la aplicación cliente de aplicación móvil de hello back-end a un usuario autenticado.

## <a name="add-authentication-toohello-app"></a>Agregar aplicación de autenticación toohello
En esta sección, modificará Hola aplicación toodisplay una pantalla de inicio de sesión antes de mostrar los datos. Cuando se inicia la aplicación hello, no se conectará no tooyour servicio de aplicaciones y no mostrará ningún dato. Después de hello primera vez que el usuario Hola realiza gestos de actualización de hello, aparecerá la pantalla de inicio de sesión de bienvenida; Después de que se mostrará la lista de Hola de inicio de sesión correcto de los elementos de lista de tareas.

1. En el proyecto de cliente de hello, abra el archivo de hello **QSTodoService.cs** y agregue Hola siguiente mediante la instrucción y `MobileServiceUser` con toohello QSTodoService clase de descriptor de acceso:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Agregar nuevo método denominado **Authenticate** demasiado**QSTodoService** con hello siguiente definición:

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

    >[AZURE.NOTE] Si está utilizando un proveedor de identidades que no sea un Facebook, cambie el valor de Hola que se pasan demasiado**LoginAsync** anteriormente tooone de siguientes hello: _cuenta de Microsoft_, _Twitter_, _Google_, o _WindowsAzureActiveDirectory_.

3. Abra **QSTodoListViewController.cs**. Modificar la definición de método hello de **ViewDidLoad** quitar llamada Hola demasiado**RefreshAsync()** cuando se acerque el final de hello:
   
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
4. Modificar el método hello **RefreshAsync** tooauthenticate si hello **usuario** propiedad es null. Agregue Hola siguiente código en parte superior de Hola de definición de método hello:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Abra **AppDelegate.cs**, agregar Hola siguiente método:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Abra **Info.plist** de archivos, vaya demasiado**tipos de URL** en hello **avanzadas** sección. Configurar ahora hello **identificador** hello y **esquemas de URL** de su tipo de dirección URL y haga clic en **Agregar tipo de dirección URL**. **Esquemas de direcciones URL** debe ser Hola mismo como su {url_scheme_of_your_app}.
7. En Visual Studio o Xamarin Studio conectado tooyour Host de compilación de Xamarin en el equipo Mac, ejecutar el proyecto de cliente de hello destinado a un dispositivo o emulador. Compruebe que la aplicación hello no muestra ningún dato.
   
    Realizar gestos de actualización de hello desplazando hacia abajo de la lista de Hola de elementos, lo que hará que tooappear de pantalla de inicio de sesión de Hola. Una vez que ha escrito correctamente las credenciales válidas, aplicación hello mostrará la lista de Hola de elementos de lista de tareas y realizar toohello una actualización de datos.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[crear una aplicación de Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md