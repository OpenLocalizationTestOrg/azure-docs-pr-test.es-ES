---
title: "aplicación de plataforma Universal de Windows (UWP) de aaaAdd authentication tooyour | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthenticate de toouse aplicaciones móviles de Azure aplicación servicio de la aplicación de plataforma Universal de Windows (UWP) mediante una variedad de proveedores de identidad, incluido: AAD, Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Agregar aplicación de Windows de autenticación tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tema muestra cómo tooyour de autenticación basada en la nube tooadd aplicación móvil. En este tutorial, agregará un proyecto de inicio rápido de autenticación toohello plataforma Universal de Windows (UWP) para las aplicaciones móviles utilizando un proveedor de identidad que es compatible con el servicio de aplicaciones de Azure. Después de que se va a correctamente autenticados y autorizados por el aplicación móvil de back-end, se muestra el valor de identificador de usuario de Hola.

Este tutorial se basa en Inicio rápido de aplicaciones móviles de Hola. Primero debe completar el tutorial de hello [empezar a trabajar con aplicaciones móviles](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Registrar la aplicación para la autenticación y configurar Hola servicio de aplicaciones
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

Ahora, puede comprobar que tooyour el acceso anónimo, back-end se ha deshabilitado. Con proyecto de aplicación UWP de hello establecer como proyecto de inicio de hello, implementar y ejecutar la aplicación hello; Compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello. Esto sucede porque la aplicación hello intenta tooaccess código de la aplicación móvil como un usuario no autenticado, pero Hola *TodoItem* tabla ahora requiere autenticación.

A continuación, se actualizará a los usuarios de hello aplicación tooauthenticate antes de solicitar recursos de su servicio de aplicación.

## <a name="add-authentication"></a>Agregar aplicación de autenticación toohello
1. En el proyecto de aplicación UWP Hola archivo MainPage.xaml.cs y agregue Hola siguiente fragmento de código:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Este código autentica el usuario Hola con un inicio de sesión de Facebook. Si está utilizando un proveedor de identidades distinto a Facebook, cambie el valor de Hola de **MobileServiceAuthenticationProvider** anteriormente toohello valor para el proveedor.
2. Reemplace hello **OnNavigatedTo()** método en MainPage.xaml.cs. A continuación, agregará un **iniciar sesión en** aplicación toohello de botón que desencadena la autenticación.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Agregue Hola siguiente fragmento de código toohello MainPage.xaml.cs:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Abrir archivo de proyecto de MainPage.xaml hello, busque el elemento Hola que define hello **guardar** botón y reemplazarlo con el siguiente código de hello:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Agregue Hola después toohello de fragmento de código App.xaml.cs:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Abra el archivo Package.appxmanifest, navegue demasiado**declaraciones**, en **declaraciones disponibles** lista desplegable, seleccione **protocolo** y haga clic en **agregar** botón. Configurar ahora hello **propiedades** de hello **protocolo** declaración. En **nombre para mostrar**, agregue nombre hello desea toodisplay toousers de la aplicación. En **Nombre**, agregue el {esquema_de_dirección_URL_de_la_aplicación}.
7. Presione aplicación Hola de hello F5 toorun clave, haga clic en hello **iniciar sesión en** botón e inicie sesión en la aplicación hello con su proveedor de identidades elegido. Una vez en el inicio de sesión correctamente, aplicación hello se ejecuta sin errores y es capaz de tooquery el back-end y realizar actualizaciones toodata.

## <a name="tokens"></a>Almacenar el token de autenticación de hello en cliente hello
ejemplo anterior de Hola mostrada un estándar inicio de sesión de, lo que requiere Hola cliente toocontact ambos proveedor de identidades de Hola y Hola servicio de aplicación cada vez que inicia la aplicación hello. No sólo es ineficaz, puede ejecutar este método en uso-está relacionada con problemas de muchos clientes pruebe toostart aplicación hello en el mismo tiempo. Un enfoque más adecuado es toocache Hola autorización token devuelto por el servicio de aplicaciones y try toouse esto antes de utilizar un inicio de sesión de basada en el proveedor.

> [!NOTE]
> Puede almacenar en caché símbolo (token) de hello emitido por servicios de aplicaciones independientemente de si está usando autenticación administrada por el cliente o servicio. Este tutorial utiliza la autenticación administrada por el servicio.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Pasos siguientes
Completado este tutorial de la autenticación básica, considere la posibilidad de continuar en tooone de hello tutoriales:

* [Agregar aplicación de tooyour de notificaciones de inserción](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de toosend de aplicación móvil back-end toouse centros de notificaciones de Azure.
* [Habilitación de la sincronización sin conexión para su aplicación](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end. Sincronización sin conexión permite a los usuarios finales toointeract con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
