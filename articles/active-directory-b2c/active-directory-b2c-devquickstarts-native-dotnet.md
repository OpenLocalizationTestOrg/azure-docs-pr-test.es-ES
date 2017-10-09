---
title: aaaAzure B2C de Active Directory | Documentos de Microsoft
description: "¿Cómo toobuild una aplicación de escritorio de Windows que incluye el inicio de sesión, inicio de sesión y perfil de administración mediante el uso de Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C: creación de una aplicación de escritorio de Windows
Mediante el uso de Azure Active Directory (Azure AD) B2C, puede agregar la aplicación de escritorio de tooyour de características de administración de identidad de autoservicio eficaz en unos cuantos pasos. En este artículo le mostrará cómo toocreate una aplicación de "Lista de tareas pendientes" de Windows Presentation Foundation (WPF) de .NET que incluye el inicio de sesión, inicio de sesión de usuario y la administración de perfiles. aplicación Hello incluirá compatibilidad para registrarse e iniciar sesión mediante un nombre de usuario o el correo electrónico. También será posible registrarse e iniciar sesión con cuentas sociales, como Facebook y Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Obtener un directorio de Azure AD B2C
Para poder usar Azure AD B2C, debe crear un directorio o inquilino.  Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc. Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.

## <a name="create-an-application"></a>Creación de una aplicación
A continuación, debe toocreate una aplicación en el directorio B2C. Esto proporciona información de Azure AD que necesita toosecurely comunicarse con la aplicación. toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).  Asegúrese de:

* Incluir un **cliente nativo** en aplicación hello.
* Hola copia **URI de redireccionamiento** `urn:ietf:wg:oauth:2.0:oob`. Es dirección URL predeterminada de Hola para este ejemplo de código.
* Hola copia **Id. de aplicación** decir tooyour asignado aplicación. Lo necesitará más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Crear sus directivas
En Azure AD B2C, cada experiencia de usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Este ejemplo de código contiene tres experiencias de identidad: registro, inicio de sesión y edición de perfil. Deberá toocreate una directiva para cada tipo, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Cuando se crea tres directivas de hello, no olvide:

* Elija **ID. de inicio de sesión** o **inicio de sesión de correo electrónico** en la hoja de proveedores de identidad de Hola.
* Seleccionar **Nombre para mostrar** y otros atributos de registro en la directiva de registro.
* Elegir las notificaciones **Nombre para mostrar** e **Id. de objeto** como notificaciones de aplicación en todas las directivas. Puede elegir también otras notificaciones.
* Hola copia **nombre** de cada directiva después de haberlo creado. Deberían tener el prefijo de hello `b2c_1_`.  Necesitará estos nombres de directiva más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Una vez haya creado correctamente Hola tres directivas, está listo toobuild la aplicación.

## <a name="download-hello-code"></a>Descargar código de hello
Hola código para este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). ejemplo de Hola a toobuild que vaya, también puede [descargar un proyecto como un archivo .zip esqueleto](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). También puede clonar el esqueleto de hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

aplicación Hello completado también es [disponible como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) o en hello `complete` rama de hello mismo repositorio.

Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio. Hola `TaskClient` proyecto es Hola aplicación de escritorio de WPF que Hola usuario interactúa con. Para fines de Hola de este tutorial, llama a una tarea de back-end API web, hospedado en Azure, que almacena la lista de tareas pendientes de cada usuario.  No es necesario toobuild hello web API, tenemos ya se ejecuta automáticamente.

toolearn cómo una API web autentica las solicitudes de forma segura mediante el uso de Azure AD B2C, consulte el [API web Introducción artículo](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Ejecución de directivas
La aplicación se comunica con Azure AD B2C mediante el envío de mensajes de autenticación que especifican la directiva de hello desean tooexecute como parte de la solicitud de hello HTTP. .NET para aplicaciones de escritorio, puede usar hello obtener una vista previa de los mensajes de autenticación de biblioteca de autenticación de Microsoft (MSAL) toosend OAuth 2.0, ejecuta las directivas y obtener tokens que llamen a API web.

### <a name="install-msal"></a>Instalación de MSAL
Agregar MSAL toohello `TaskClient` proyecto usando Hola consola de administrador de paquetes de Visual Studio.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Escribir los detalles de B2C
Archivo abierto hello `Globals.cs` y cada uno de los valores de propiedad de hello reemplazar por los suyos propios. Esta clase se utiliza a lo largo de `TaskClient` valores tooreference de uso frecuente.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Crear hello PublicClientApplication
clase principal de Hola de MSAL es `PublicClientApplication`. Esta clase representa la aplicación de sistema de hello Azure AD B2C. Cuando hello inicializa de aplicación, crea una instancia de `PublicClientApplication` en `MainWindow.xaml.cs`. Esto puede usarse en toda la ventana hello.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Inicio de un flujo de registro
Cuando un usuario opts toosigns seguridad, desea tooinitiate un flujo de inicio de sesión que usa la directiva de inicio de sesión de Hola que creó. Con MSAL, simplemente llama a `pca.AcquireTokenAsync(...)`. Hola parámetros que se pasan demasiado`AcquireTokenAsync(...)` determinan qué token recibir, directiva de hello usada en la solicitud de autenticación de Hola y mucho más.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a>Inicio de un flujo de inicio de sesión
También puede iniciar un flujo de inicio de sesión en hello igual que iniciar un flujo de inicio de sesión. Cuando un usuario inicia sesión, asegúrese de Hola mismo llamar tooMSAL, esta vez utilizando la directiva de inicio de sesión:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Inicio de un flujo de edición de perfiles
Una vez más, puede ejecutar una directiva de perfil de edición en hello mismo modo:

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

En todos estos casos, MSAL devuelve un token en `AuthenticationResult` o genera una excepción. Cada vez que se obtendrá un token de MSAL, puede usar hello `AuthenticationResult.User` tooupdate Hola usuario datos de aplicación de hello, como Hola interfaz de usuario del objeto. AAL también cachés Hola token para su uso en otras partes de la aplicación hello.

### <a name="check-for-tokens-on-app-start"></a>Búsqueda de tokens en el inicio de la aplicación
También puede utilizar el seguimiento de tookeep MSAL Hola del inicio de sesión de estado del usuario.  En esta aplicación, es deseable Hola usuario tooremain iniciado sesión, incluso después de que cierre la aplicación hello y vuelva a abrirlo.  Dentro de hello `OnInitialized` reemplazar, utilice del MSAL `AcquireTokenSilent` toocheck de método para los tokens almacenados en caché:

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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
```

## <a name="call-hello-task-api"></a>Llamar a la API de la tarea de Hola
Ahora se ha usado las directivas de tooexecute MSAL y obtener tokens.  Cuando quiera toouse uno estas API de tarea de tokens toocall hello, puede volver a usar del MSAL `AcquireTokenSilent` toocheck de método para los tokens almacenados en caché:

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

Cuando Hola llamada demasiado`AcquireTokenSilentAsync(...)` se realiza correctamente y se encuentra un token en memoria caché de hello, puede agregar Hola token toohello `Authorization` encabezado de solicitud de hello HTTP. API de web de tarea de Hola usará la lista de tareas pendientes de este encabezado tooauthenticate Hola solicitud tooread Hola del usuario:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Usuario de inicio de sesión Hola out
Por último, puede usar MSAL tooend una sesión de usuario con la aplicación de hello cuando selecciona usuario hello **cerrar sesión**.  Al utilizar MSAL, esto se consigue mediante la desactivación de todos los tokens de Hola de caché de tokens de Hola de:

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Ejecutar la aplicación de ejemplo de Hola
Por último, compile y ejecute el ejemplo hello.  Registrarse para la aplicación hello usando un nombre de usuario o la dirección de correo electrónico. Cerrar sesión e iniciar sesión en como Hola mismo usuario. Edite el perfil de ese usuario. Cierre la sesión y regístrese con otro usuario diferente.

## <a name="add-social-idps"></a>Agregar IDP sociales
Actualmente, la aplicación hello admite solo inicio de sesión de usuario e inicio de sesión que usan **cuentas locales**. Se trata de cuentas almacenadas en el directorio B2C que utilizan un nombre de usuario y una contraseña. Con Azure AD B2C, puede agregar compatibilidad con otros proveedores de identidades (IDP) sin cambiar el código.

tooadd sociales IDPs tooyour aplicación, para comenzar, siga Hola detallada instrucciones que aparecen en estos artículos. Para cada IDP desea toosupport, necesita tooregister una aplicación en ese sistema y obtener un identificador de cliente.

* [Configurar Facebook como una IDP](active-directory-b2c-setup-fb-app.md)
* [Configurar Google como una IDP](active-directory-b2c-setup-goog-app.md)
* [Configurar Amazon como una IDP](active-directory-b2c-setup-amzn-app.md)
* [Configurar LinkedIn como una IDP](active-directory-b2c-setup-li-app.md)

Después de Agregar directorio de tooyour B2C de proveedores de identidad de hello, necesita tooedit cada una de las tres directivas tooinclude Hola IDPs nuevas, como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md). Después de guardar las directivas, vuelva a ejecutar la aplicación hello. Debería ver Hola que IDPS nueva se agregan como opciones de inicio de sesión y suscripción en cada una de sus experiencias de identidad.

Puede experimentar con las directivas y observar los efectos de hello en la aplicación de ejemplo. Agregue o quite proveedores de identidades, manipule notificaciones de aplicación o cambie atributos de registro. Experimente para ver cómo se combinan directivas, solicitudes de autenticación y MSAL.

Como referencia, Hola completado ejemplo [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). También puede clonarlo desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
