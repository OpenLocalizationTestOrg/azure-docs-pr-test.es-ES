---
title: "aaaAzure AD v2 Windows Desktop introducción: uso | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones .NET de escritorio de Windows (XAML) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Usar Hola biblioteca de autenticación de Microsoft (MSAL) tooget un token para hello API Graph de Microsoft

Esta sección muestra cómo toouse MSAL tooget un token de Hola API Graph de Microsoft.

1.  En `MainWindow.xaml.cs`, agregar referencia de hello para la clase MSAL biblioteca toohello:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Reemplace el código de clase <code>MainWindow</code> por:
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Más información
#### <a name="getting-a-user-token-interactive"></a>Obtención de un token de usuario interactivamente
Llamar a hello `AcquireTokenAsync` resultados del método en una ventana preguntar Hola toosign de usuario en. Las aplicaciones suelen requieran un toosign de usuario en forma interactiva Hola primera vez necesiten tooaccess un recurso protegido, o cuando una operación silenciosa tooacquire se produce un error en un token (por ejemplo, contraseña del usuario de hello expiró).

#### <a name="getting-a-user-token-silently"></a>Obtención de un token de usuario en silencio
`AcquireTokenSilentAsync` controla las adquisiciones y la renovación de tokens sin interacción del usuario. Después de `AcquireTokenAsync` se ejecuta para hello primera vez, `AcquireTokenSilentAsync` es tooaccess de hello método habitual usar tooobtain tokens que se usan los recursos para las llamadas subsiguientes - protegidos como llamadas toorequest o renovar los tokens se realizan en modo silencioso.
Finalmente, `AcquireTokenSilentAsync` se producirá un error: por ejemplo, usuario de hello ha cerrado la sesión, o ha cambiado su contraseña en otro dispositivo. Cuando MSAL detecta que se puede resolver el problema de hello exigiendo una acción interactiva, que se activa un `MsalUiRequiredException`. La aplicación puede abordar esta excepción de dos maneras:

1.  Realizar una llamada con `AcquireTokenAsync` inmediatamente, lo que ocasiona preguntar usuario hello en toosign. Este patrón se utiliza normalmente en aplicaciones en línea que no hay ningún contenido sin conexión en la aplicación hello disponibles para el usuario de Hola. ejemplo generada el programa de instalación interactiva Hello usa este patrón: puede verlo en Hola de acción a primera vez que ejecute el ejemplo hello: porque ningún usuario utilizado alguna vez la aplicación hello, `PublicClientApp.Users.FirstOrDefault()` contendrá un valor null y un `MsalUiRequiredException` excepción. Hola código de ejemplo de Hola, a continuación, identificadores de Hola excepción mediante una llamada a `AcquireTokenAsync` resultante en Preguntar usuario hello en toosign.

2.  Las aplicaciones también pueden realizar un usuario de toohello de indicación visual en un inicio de sesión interactivo se requiere para el usuario de hello puede seleccionar Hola momento toosign en, o puede volver a intentar la aplicación hello `AcquireTokenSilentAsync` en un momento posterior. Se suele utilizar al usuario Hola puede usar otras funciones de aplicación hello sin que se va a interrumpir; por ejemplo, hay contenido sin conexión disponibles en la aplicación hello. En este caso, puede decidir usuario hello cuando quieran toosign en recursos de hello protegido tooaccess, o toorefresh Hola información obsoleta o la aplicación puede decidir tooretry `AcquireTokenSilentAsync` cuando se restaure la red después de estar disponible temporalmente.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Llamar a la API de Microsoft Graph hello mediante el símbolo (token) de hello que acabara de obtener

1. Agregar nuevo método de hello debajo tooyour `MainWindow.xaml.cs`. método Hello es toomake usado un `GET` solicitud con API Graph con un encabezado de autorización:

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Más información acerca de cómo realizar una llamada de REST a una API protegida

En esta aplicación de ejemplo Hola `GetHttpContentWithToken` método es toomake usa HTTP `GET` solicitud para un recurso protegido que requiera un llamador de contenido toohello Hola símbolo (token) y, a continuación, vuelva. Este método agrega el token de hello adquirido en hello *encabezado de autorización HTTP*. En este ejemplo, recurso de Hola es hello Microsoft Graph API *me* endpoint – que muestra información de perfil del usuario de Hola.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Agregar un toosign método usuario Hola

1. Agregar Hola siguiendo el método tooyour `MainWindow.xaml.cs` toosign usuario hello:

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Más información sobre el cierre de sesión

`SignOutButton_Click`Quita Hola usuario de la caché de usuario MSAL: usuario actual de MSAL tooforget Hola eficazmente le indicará por lo que una solicitud futura tooacquire un token solo tendrá éxito si se realiza toobe interactivo.
Aunque la aplicación hello en este ejemplo es compatible con un solo usuario, MSAL es compatible con escenarios donde pueden ser varias cuentas con sesión iniciada en hello vez: un ejemplo es una aplicación de correo electrónico donde un usuario tiene varias cuentas.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Visualización de información de token básica

1. Agregar Hola siguiendo el método tootooyour `MainWindow.xaml.cs` toodisplay información básica sobre el token de hello:

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a>Más información

Tokens adquieren a través de *OpenID Connect* también contienen un pequeño subconjunto de usuario de toohello pertinente de información. `DisplayBasicTokenInfo`Muestra información básica contenida en el token de hello: por ejemplo, del usuario de hello Mostrar nombre e Id., así como Hola cadena hello y fecha de caducidad del testigo que representa el token de acceso de hello propio. Esta información se muestra para toosee. Puede presionar hello *llamadas API de Microsoft Graph* botón varias veces y ver ese Hola mismo símbolo (token) se reutiliza para solicitudes posteriores. También puede ver la fecha de expiración de Hola que se extiende al MSAL decide es tiempo toorenew Hola token.
<!--end-collapse-->

