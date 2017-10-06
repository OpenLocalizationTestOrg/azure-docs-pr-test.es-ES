---
title: "v2.0 de Active Directory aaaAzure aplicación nativa de .NET | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación nativa de .NET firma los usuarios con ambos Account personal de Microsoft y cuentas profesionales o educativas."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Agregar aplicación de escritorio de Windows de inicio de sesión tooa
Con el punto de conexión de Hola Hola v2.0, puede agregar rápidamente aplicaciones de escritorio de tooyour de autenticación con la compatibilidad para ambas cuentas de Microsoft personales y cuentas profesionales o educativas.  También habilita la toosecurely aplicación comunicarse con un back-end web api, así como [Hola Microsoft Graph](https://graph.microsoft.io) y algunos de hello [API unificada de Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory (AD) son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

Para [aplicaciones nativas de .NET que se ejecutan en un dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD proporciona Hola biblioteca de autenticación de identidad de Microsoft o MSAL.  Propósitos del MSAL en la vida es toomake más sencilla para su aplicación tooget tokens para llamar a servicios web.  toodemonstrate lo fácil es, a continuación, crearemos una aplicación de la lista de tareas de .NET WPF que:

* Signos de Hola usuario en & obtiene acceso a los tokens utilizando hello [protocolo de autenticación de OAuth 2.0](active-directory-v2-protocols.md).
* Llama a un servicio web de lista de tareas pendientes back-end, que también está protegido con OAuth 2.0.
* Usuario de hello signos out.

## <a name="download-sample-code"></a>Descarga de código de ejemplo
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

final de Hola de este tutorial también se incluye aplicación Hello completado.

## <a name="register-an-app"></a>Registrar una aplicación
Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).  Asegúrese de que:

* Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.
* Agregar hello **Mobile** plataforma para la aplicación.

## <a name="install--configure-msal"></a>Instalación y configuración de MSAL
Ahora que ya tiene una aplicación registrada en Microsoft, puede instalar MSAL y escribir código relacionado con identidades.  Para el punto de conexión MSAL toobe toocommunicate capaz de hello v2.0, deberá tooprovide con cierta información sobre el registro de aplicación.

* Comience por agregar MSAL toohello TodoListClient proyecto mediante la consola de administrador de paquetes de saludo.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* En hello TodoListClient proyecto, abra `app.config`.  Reemplace los valores de hello de elementos de Hola Hola `<appSettings>` Hola de sección tooreflect valores proporcionados en el portal de registro de aplicación Hola.  El código hará referencia a estos valores cada vez que use MSAL.
  
  * Hola `ida:ClientId` es hello **Id. de aplicación** de la aplicación copian desde el portal de Hola.
* En el proyecto de servicio TodoList hello, abra `web.config` en raíz de Hola de proyecto Hola.  
  
  * Reemplace hello `ida:Audience` valor con hello mismo **Id. de aplicación** desde el portal de Hola.

## <a name="use-msal-tooget-tokens"></a>Usar tokens de tooget MSAL
Hello principio básico detrás de MSAL es cada vez que la aplicación necesita un token de acceso, basta con llamar a `app.AcquireToken(...)`, y MSAL Hola rest.  

* Hola `TodoListClient` proyecto abierto `MainWindow.xaml.cs` y busque hello `OnInitialized(...)` método.  primer paso de Hello es la aplicación de tooinitialize `PublicClientApplication` -clase principal del MSAL que representa las aplicaciones nativas.  Esto es donde pasas MSAL Hola coordenadas debe toocommunicate con Azure AD y le indique cómo toocache símbolos (tokens).

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Cuando se inicia aplicación hello, se desea toocheck y vea si el usuario de hello ya ha iniciado en la aplicación hello.  Sin embargo, todavía no queremos tooinvoke una interfaz de usuario de inicio de sesión, nos aseguraremos de hacer el usuario de Hola por lo que haga clic en "Iniciar sesión" toodo.  También en hello `OnInitialized(...)` método:

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* Si usuario hello no ha iniciado sesión y haga clic en el botón "Iniciar sesión" Hola, se desea tooinvoke una interfaz de usuario de inicio de sesión y usuario Hola escriba sus credenciales.  Implementar el controlador del botón Hola inicio de sesión:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* Si Hola usuario correctamente inicia sesión, MSAL recibirá y almacenar en caché un token para usted y puede continuar hello toocall `GetTodoList()` método con confianza.  Todo lo que ha dejado tooget las tareas de un usuario es tooimplement hello `GetTodoList()` método.

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>Ejecute
¡Enhorabuena! Ahora tiene una aplicación .NET WPF que tiene Hola capacidad tooauthenticate usuarios en funcionamiento & seguro llamar a las API Web mediante OAuth 2.0.  Ejecute sus dos proyectos e inicie sesión con una cuenta de Microsoft personal o una cuenta profesional o educativa.  Agregue la lista de tareas del usuario de las tareas toothat.  Cierre la sesión y vuelva a iniciarla como tooview de otro usuario su lista de tareas pendientes.  Cierre la aplicación hello y volver a ejecutarlo.  Tenga en cuenta la sesión del usuario de hello permanece intacta, esto es así porque la aplicación hello almacena en memoria caché de símbolos (tokens) en un archivo local.

MSAL resulta fácil tooincorporate características de identidad comunes en la aplicación, con cuentas personales y profesionales.  Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentaciones usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.  Todo lo que realmente necesita tooknow es una sola llamada API, `app.AcquireTokenAsync(...)`.

Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), o se puede clonar desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Pasos siguientes
Ahora puede pasar a temas más avanzados.  Puede que desee tootry:

* [Proteger hello TodoListService Web API con el punto de conexión de hello v2.0](active-directory-v2-devquickstarts-dotnet-api.md)

Para obtener recursos adicionales, consulte:  

* [Guía del desarrollador de Hello v2.0 >>](active-directory-appmodel-v2-overview.md)
* [Etiqueta "msal" de StackOverflow &gt;&gt;](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.

