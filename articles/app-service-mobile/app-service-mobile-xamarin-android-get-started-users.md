---
title: "aaaGet iniciado con autenticación para aplicaciones móviles en Xamarin para Android"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de la aplicación de Xamarin para Android a través de una serie de proveedores de identidad, incluido AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Agregar aplicación de autenticación tooyour Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tema muestra cómo tooauthenticate a los usuarios de una aplicación móvil de la aplicación cliente. En este tutorial, agregará el proyecto de inicio rápido de toohello de autenticación utilizando un proveedor de identidad que es compatible con aplicaciones móviles de Azure. Después de que se va a correctamente autenticado y autorizado en hello aplicación móvil, se muestra el valor de identificador de usuario de Hola.

Este tutorial se basa en Inicio rápido de aplicación móvil de Hola. En primer lugar también debe completar el tutorial Hola [crear una aplicación de Xamarin.Android]. Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto de tooyour de paquete de extensión de autenticación de Hola. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Registro de la aplicación para la autenticación y configuración de Servicios de aplicaciones
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello

La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación. Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola. En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo. Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija. Debe ser único tooyour aplicaciones móviles. redirección de hello tooenable en servidor hello:

1. Hola [portal de Azure], seleccione su servicio en la aplicación.

2. Haga clic en hello **autenticación / autorización** opción de menú.

3. Hola **permite redirigir direcciones URL externas de**, escriba `url_scheme_of_your_app://easyauth.callback`.  Hola **url_scheme_of_your_app** de esta cadena es hello esquema de dirección URL para la aplicación móvil.  Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).  Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.

4. Haga clic en **Aceptar**.

5. Haga clic en **Guardar**.

## <a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente de hello en un dispositivo o emulador. Compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello. Esto sucede porque la aplicación hello intenta tooaccess su aplicación móvil de back-end como un usuario no autenticado. Hola *TodoItem* tabla ahora requiere autenticación.

A continuación, actualizará recursos de toorequest Hola la aplicación cliente de aplicación móvil de hello back-end a un usuario autenticado.

## <a name="add-authentication"></a>Agregar aplicación de autenticación toohello
aplicación Hello es Hola de toorequire actualizada a los usuarios tootap **iniciar sesión en** botón y autenticarse antes de que se muestran los datos.

1. Agregar Hola después código toohello **TodoActivity** clase:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    Esto crea un nuevo tooauthenticate método un usuario y un controlador de método para un nuevo **iniciar sesión en** botón. usuario de Hello en el código de ejemplo de Hola anterior se autentica mediante un inicio de sesión de Facebook. Un cuadro de diálogo es una vez autenticado, Id. de usuario de Hola de toodisplay usado.
   
   > [!NOTE]
   > Si está utilizando un proveedor de identidades distinto a Facebook, cambie el valor de Hola que se pasan demasiado**LoginAsync** anteriormente tooone de siguientes hello: *cuenta de Microsoft*, *Twitter*, *Google*, o *WindowsAzureActiveDirectory*.
   > 
   > 
2. Hola **OnCreate** (método), delete u Hola Comente después de la línea de código:
   
        OnRefreshItemsSelected ();
3. En el archivo de Activity_To_Do.axml hello, agregue siguientes de hello *LoginUser* botón definición antes de hello existente *AddItem* botón:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Agregue Hola elemento toohello Strings.xml recursos archivo siguiente:
   
        <string name="login_button_text">Sign in</string>
5. Abra el archivo AndroidManifest.xml Hola, agregue Hola siguiente código dentro de `<application>` elemento XML:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. En Visual Studio o Xamarin Studio, ejecute el proyecto de cliente de hello en un dispositivo o emulador e inicie sesión con su proveedor de identidades elegido. Una vez que ha iniciado sesión correctamente, aplicación hello mostrará el identificador de inicio de sesión y lista de Hola de elementos de lista de tareas y realizar toohello una actualización de datos.

<!-- URLs. -->
[crear una aplicación de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md