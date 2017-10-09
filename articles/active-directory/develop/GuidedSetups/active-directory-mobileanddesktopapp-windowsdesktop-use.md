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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="2a321-103">Usar Hola biblioteca de autenticación de Microsoft (MSAL) tooget un token para hello API Graph de Microsoft</span><span class="sxs-lookup"><span data-stu-id="2a321-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="2a321-104">Esta sección muestra cómo toouse MSAL tooget un token de Hola API Graph de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2a321-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="2a321-105">En `MainWindow.xaml.cs`, agregar referencia de hello para la clase MSAL biblioteca toohello:</span><span class="sxs-lookup"><span data-stu-id="2a321-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2a321-106">Reemplace el código de clase <code>MainWindow</code> por:</span><span class="sxs-lookup"><span data-stu-id="2a321-106">Replace <code>MainWindow</code> class code with:</span></span>
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
### <a name="more-information"></a><span data-ttu-id="2a321-107">Más información</span><span class="sxs-lookup"><span data-stu-id="2a321-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="2a321-108">Obtención de un token de usuario interactivamente</span><span class="sxs-lookup"><span data-stu-id="2a321-108">Getting a user token interactive</span></span>
<span data-ttu-id="2a321-109">Llamar a hello `AcquireTokenAsync` resultados del método en una ventana preguntar Hola toosign de usuario en.</span><span class="sxs-lookup"><span data-stu-id="2a321-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="2a321-110">Las aplicaciones suelen requieran un toosign de usuario en forma interactiva Hola primera vez necesiten tooaccess un recurso protegido, o cuando una operación silenciosa tooacquire se produce un error en un token (por ejemplo, contraseña del usuario de hello expiró).</span><span class="sxs-lookup"><span data-stu-id="2a321-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="2a321-111">Obtención de un token de usuario en silencio</span><span class="sxs-lookup"><span data-stu-id="2a321-111">Getting a user token silently</span></span>
<span data-ttu-id="2a321-112">`AcquireTokenSilentAsync` controla las adquisiciones y la renovación de tokens sin interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="2a321-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="2a321-113">Después de `AcquireTokenAsync` se ejecuta para hello primera vez, `AcquireTokenSilentAsync` es tooaccess de hello método habitual usar tooobtain tokens que se usan los recursos para las llamadas subsiguientes - protegidos como llamadas toorequest o renovar los tokens se realizan en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="2a321-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="2a321-114">Finalmente, `AcquireTokenSilentAsync` se producirá un error: por ejemplo, usuario de hello ha cerrado la sesión, o ha cambiado su contraseña en otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2a321-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="2a321-115">Cuando MSAL detecta que se puede resolver el problema de hello exigiendo una acción interactiva, que se activa un `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="2a321-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="2a321-116">La aplicación puede abordar esta excepción de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="2a321-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="2a321-117">Realizar una llamada con `AcquireTokenAsync` inmediatamente, lo que ocasiona preguntar usuario hello en toosign.</span><span class="sxs-lookup"><span data-stu-id="2a321-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="2a321-118">Este patrón se utiliza normalmente en aplicaciones en línea que no hay ningún contenido sin conexión en la aplicación hello disponibles para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a321-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="2a321-119">ejemplo generada el programa de instalación interactiva Hello usa este patrón: puede verlo en Hola de acción a primera vez que ejecute el ejemplo hello: porque ningún usuario utilizado alguna vez la aplicación hello, `PublicClientApp.Users.FirstOrDefault()` contendrá un valor null y un `MsalUiRequiredException` excepción.</span><span class="sxs-lookup"><span data-stu-id="2a321-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="2a321-120">Hola código de ejemplo de Hola, a continuación, identificadores de Hola excepción mediante una llamada a `AcquireTokenAsync` resultante en Preguntar usuario hello en toosign.</span><span class="sxs-lookup"><span data-stu-id="2a321-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="2a321-121">Las aplicaciones también pueden realizar un usuario de toohello de indicación visual en un inicio de sesión interactivo se requiere para el usuario de hello puede seleccionar Hola momento toosign en, o puede volver a intentar la aplicación hello `AcquireTokenSilentAsync` en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="2a321-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="2a321-122">Se suele utilizar al usuario Hola puede usar otras funciones de aplicación hello sin que se va a interrumpir; por ejemplo, hay contenido sin conexión disponibles en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2a321-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="2a321-123">En este caso, puede decidir usuario hello cuando quieran toosign en recursos de hello protegido tooaccess, o toorefresh Hola información obsoleta o la aplicación puede decidir tooretry `AcquireTokenSilentAsync` cuando se restaure la red después de estar disponible temporalmente.</span><span class="sxs-lookup"><span data-stu-id="2a321-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="2a321-124">Llamar a la API de Microsoft Graph hello mediante el símbolo (token) de hello que acabara de obtener</span><span class="sxs-lookup"><span data-stu-id="2a321-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="2a321-125">Agregar nuevo método de hello debajo tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="2a321-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="2a321-126">método Hello es toomake usado un `GET` solicitud con API Graph con un encabezado de autorización:</span><span class="sxs-lookup"><span data-stu-id="2a321-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="2a321-127">Más información acerca de cómo realizar una llamada de REST a una API protegida</span><span class="sxs-lookup"><span data-stu-id="2a321-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="2a321-128">En esta aplicación de ejemplo Hola `GetHttpContentWithToken` método es toomake usa HTTP `GET` solicitud para un recurso protegido que requiera un llamador de contenido toohello Hola símbolo (token) y, a continuación, vuelva.</span><span class="sxs-lookup"><span data-stu-id="2a321-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="2a321-129">Este método agrega el token de hello adquirido en hello *encabezado de autorización HTTP*.</span><span class="sxs-lookup"><span data-stu-id="2a321-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="2a321-130">En este ejemplo, recurso de Hola es hello Microsoft Graph API *me* endpoint – que muestra información de perfil del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a321-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="2a321-131">Agregar un toosign método usuario Hola</span><span class="sxs-lookup"><span data-stu-id="2a321-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="2a321-132">Agregar Hola siguiendo el método tooyour `MainWindow.xaml.cs` toosign usuario hello:</span><span class="sxs-lookup"><span data-stu-id="2a321-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="2a321-133">Más información sobre el cierre de sesión</span><span class="sxs-lookup"><span data-stu-id="2a321-133">More info on Sign-Out</span></span>

<span data-ttu-id="2a321-134">`SignOutButton_Click`Quita Hola usuario de la caché de usuario MSAL: usuario actual de MSAL tooforget Hola eficazmente le indicará por lo que una solicitud futura tooacquire un token solo tendrá éxito si se realiza toobe interactivo.</span><span class="sxs-lookup"><span data-stu-id="2a321-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="2a321-135">Aunque la aplicación hello en este ejemplo es compatible con un solo usuario, MSAL es compatible con escenarios donde pueden ser varias cuentas con sesión iniciada en hello vez: un ejemplo es una aplicación de correo electrónico donde un usuario tiene varias cuentas.</span><span class="sxs-lookup"><span data-stu-id="2a321-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="2a321-136">Visualización de información de token básica</span><span class="sxs-lookup"><span data-stu-id="2a321-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="2a321-137">Agregar Hola siguiendo el método tootooyour `MainWindow.xaml.cs` toodisplay información básica sobre el token de hello:</span><span class="sxs-lookup"><span data-stu-id="2a321-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="2a321-138">Más información</span><span class="sxs-lookup"><span data-stu-id="2a321-138">More Information</span></span>

<span data-ttu-id="2a321-139">Tokens adquieren a través de *OpenID Connect* también contienen un pequeño subconjunto de usuario de toohello pertinente de información.</span><span class="sxs-lookup"><span data-stu-id="2a321-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="2a321-140">`DisplayBasicTokenInfo`Muestra información básica contenida en el token de hello: por ejemplo, del usuario de hello Mostrar nombre e Id., así como Hola cadena hello y fecha de caducidad del testigo que representa el token de acceso de hello propio.</span><span class="sxs-lookup"><span data-stu-id="2a321-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="2a321-141">Esta información se muestra para toosee.</span><span class="sxs-lookup"><span data-stu-id="2a321-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="2a321-142">Puede presionar hello *llamadas API de Microsoft Graph* botón varias veces y ver ese Hola mismo símbolo (token) se reutiliza para solicitudes posteriores.</span><span class="sxs-lookup"><span data-stu-id="2a321-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="2a321-143">También puede ver la fecha de expiración de Hola que se extiende al MSAL decide es tiempo toorenew Hola token.</span><span class="sxs-lookup"><span data-stu-id="2a321-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

